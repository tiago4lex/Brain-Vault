2025-07-28 17:21

Status: #developed #Linux 

Tags: [[Linux]] | [[diff]] | [[uniq]]

----
## 🔁 `uniq` — Remoção de Linhas Duplicadas

## ▶️ Finalidade

O comando `uniq` é usado para **filtrar linhas repetidas consecutivas** em arquivos ou na saída de comandos. Muito útil para limpeza de dados e resumos simples.

## 📌 Sintaxe

```bash
uniq [opções] [entrada] [saída]
```

>[!important] Importante:
>O `uniq` **só remove duplicatas consecutivas.** Use com `sort` se quiser garantir a remoção de todas as duplicatas.

## 🔧 Exemplos

- **Remover linhas duplicadas consecutivas**

```bash
uniq lista.txt
```

- **Garantir remoção de todas as duplicatas** (com `sort`)

```bash
sort list.txt | uniq
```

- **Mostrar apenas as linhas duplicadas**

```bash
uniq -d lista.txt
```

- **Mostrar apenas as linhas únicas**

```bash
uniq -u lista.txt
```

- **Contar o número de vezes que cada linha aparece**

```bash
uniq -c list.txt
```

→ Exibe quantas vezes cada linha aparece (útil para estatísticas)

## 🛠️ Principais opções de `uniq`

| **Opção**         | **Descrição**                                       |
| ----------------- | --------------------------------------------------- |
| `-c`              | Mostra a contagem de cada linha                     |
| `-d`              | Exibe apenas as linhas duplicadas                   |
| `-u`              | Exibe apenas as linhas únicas                       |
| `-i`              | Ignora diferenças entre a maiúsculas e minúsculas   |
| `--skip-fields=N` | Ignora os primeiros N campos (separados por espaço) |
| `--skip-chars=N`  | Ignora os primeiros N caracteres                    |

---
# 📂 `diff` — Comparar Arquivos Linha por Linha

## ▶️ Finalidade

O comando `diff` é usado para **comparar dois arquivos** e exibir suas **diferenças linha a linha**. Muito utilizado por desenvolvedores e administradores de sistemas para identificar alterações entre versões de arquivos.

## 📌 Sintaxe

```bash
diff [opções] arquivo1 arquivo2
```

## 🔧 Exemplos

- **Comparar dois arquivos**

```bash
diff arquivo1.txt arquivo2.txt
```

→ Mostra as linhas que diferem entre os dois arquivos, com marcações para indicar alterações, adições e remoções.

- **Exibir diferenças de forma lado a lado**

```bash
diff -y arquivo1.txt arquivo2.txt
```

→ Mostra os arquivos em colunas paralelas (lado a lado).

- **Ignorar espaços em branco**

```bash
diff -b arquivo1.txt arquivo2.txt
```

- **Gerar saída no formato patch** (para aplicar com `patch`)

```bash
diff -u antigo.txt novo.txt > alteracoes.patch
```

→ Muito usado em controle de versões. O arquivo `.patch` pode ser aplicado com o comando `patch`.

## 🛠️ Principais opções de `diff`

| **Opção** | **Descrição**                             |
| --------- | ----------------------------------------- |
| `-u`      | Formato unificado (usado em patches)      |
| `-c`      | Formato context (também usado em patches) |
| `-y`      | Comparação lado a lado                    |
| `-i`      | Ignora maiúsculas/minúsculas              |
| `-w`      | Ignora todos os espaços em branco         |
| `-r`      | Compara diretórios recursivamente         |

