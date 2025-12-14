2025-07-28 16:48

Status: #developed #Linux 

Tags: [[Linux]] | [[sed]] | [[sort]]

----
# 🧩 `sed` — Stream Editor

## ▶️ Finalidade

O `sed` é um editor de fluxo de texto que permite **filtrar e transformar** conteúdo de arquivos ou do input de um comando.

## 📌 Sintaxe básica

```bash
sed [opções] 'comando' arquivo
```

## 🔧 Exemplos comuns

- **Substituir texto**

```bash
sed 's/antigo/novo' arquivo.txt
```

→ Substitui **a primeira ocorrência** de "antigo" por "novo" em cada linha.

```bash
sed 's/antigo/novo/g' arquivo.txt
```

→ Substitui **todas as ocorrências** de "antigo" por "novo" em cada linha

- **Deletar uma linha específica**

```bash
sed '5d' arquivo.txt
```

→ Remova a **linha 5** do arquivo

- **Excluir linhas que contenham uma palavra**

```bash
sed '/erro/d' arquivo.txt
```

→ Remove todas as linhas que contêm "erro"

- **Alterar diretamente o arquivo original** (com backup)

```bash
sed -i.bkp 's/test/produto/g' arquivo.txt
```

→ Substitui "teste" por "produto" no arquivo e salva o backup como `arquivo.txt.bkp`

## 🛠️ Principais opções do `sed`

| **Opção** | **Descrição**                                 |
| --------- | --------------------------------------------- |
| `s`       | Substitui texto                               |
| `d`       | Deleta linha                                  |
| `-i`      | Altera o arquivo diretamente                  |
| `/regex/` | Usa expressões regulares como padrão de busca |
| `g`       | Global (todas as ocorrências na linha)        |

---
# 🔠 `sort` — Ordenação de Linhas

## ▶️ Finalidade

O comando `sort` ordena linhas de texto **alfabeticamente, numericamente ou por colunas**.

## 📌 Sintaxe básica

```bash
sort [opções] arquivo
```

## 🔧 Exemplos comuns

- **Ordenar em ordem alfabética**

```bash
sort nomes.txt
```

- **Ordem inversa**

```bash
sort -r nomes.txt
```

- **Ordenar por número**

```bash
sort -n notas.txt
```

→ Organiza numericamente (útil para valores como notas ou IDs).

- **Remover duplicatas**

```bash
sort -u lista.txt
```

- **Ordenar pela segunda coluna**

```bash
sort -k 2 arquivo.csv
```

- **Ordenar com separador personalizado**

```bash
sort -t ':' -k 2 arquivo.txt
```

→ Usa `:` como separador de colunas e ordena pela 2ª coluna.

## 🛠️ Principais opções do `sort`

| **Opção** | **Descrição**                           |
| --------- | --------------------------------------- |
| `-n`      | Ordenação numérica                      |
| `-r`      | Ordem reversa                           |
| `-u`      | Remove duplicatas                       |
| `-k N`    | Ordenar pela coluna N                   |
| `-t C`    | Define o caractere separador de colunas |

---
# 💡 Uso combinado de `sed`, `sort`, `grep`, etc.

Esses comandos são muito usados juntos em *pipelines*.

**Exemplo:**

```bash
cat log.txt | grep "ERROR" | sort | uniq | sed 's/ERROR/ERRO:/g'
```

→ Extrai mensagens de erro, ordena, remove duplicatas e substitui "ERROR" por "ERRO:".

---
# 🔍 Exemplo real com substituição sensível (mascarando senhas)

```bash
sed -i 's/User password is .*/User password is -=REDACTED=-/g' "${arquivo}.filtrado"
```

## 💡 O que esse comando faz:

- `sed -i`: Edita o arquivo **diretamente** *(in-place)*.
- `'s/.../.../g'`: É uma **substituição global** (em todas as ocorrências da linha).
- `User password is .*`: O padrão procura por qualquer linha que comece com `User password is` **seguido de qualquer coisa** (o `.*` significa "qualquer coisa até o final da linha").
- `User password is -=REDACTED=-`: Substitui o conteúdo da linha por uma versão sanitizada, **ocultando a senha real.**
- `"${arquivo}.filtrado"`: Aponta para o nome do arquivo sendo modificado, armazenado numa variável chamada `arquivo`, com a extensão `.filtrado`.

#### ✅ Uso típico:

Esse comando é muito utilizado em **logs ou arquivos de configuração** para **remover dados sensíveis**, como senhas, antes de compartilhar ou armazenar.