2025-07-28 18:24

Status: #developed #Linux 

Tags: [[Linux]] | [[wc]]

----
# Introdução

O comando `wc` ***(Word Count)*** é usado para contar:

- **linhas**
- **palavras**
- **caracteres**
- **bytes**
- **tamanho máximo de linha** (em caracteres)

Ele é amplamente utilizado para estatísticas básicas em arquivos de texto e pode ser combinado com outros comandos por meio de **pipes** (`|`)

---
# 📌Sintaxe

```bash
wc [opções] [arquivo(s)]
```

## 📊 Exemplos Básicos

- **Contar linhas, palavras e caracteres de um arquivo**

```bash
wc arquivo.txt
```

**Saída exemplo:**

```bash
10 50 300 arquivo.txt
```

- `10` linhas
- `50` palavras
- `300` caracteres
- nome do arquivo final

---
### 🔸 Contar apenas o número de linhas

```bash
wc -w arquivo.txt
```

### 🔸 Contar apenas palavras

```bash
wc -l arquivo.txt
```

### 🔸 Contar apenas caracteres (antigo) ou bytes (atual)

```bash
wc -m arquivo.txt    # número de caracteres (com acentos, UTF-8)
wc -c arquivo.txt    # número de bytes
```

### 🔸 Contar caracteres da saída de um comando

```bash
ls | wc -l
```

> Conta **quantas linhas** (entradas) existem na listagem do diretório.

### 🔸 Contar palavras digitadas pelo usuário

```bash
echo "Linux é um sistema poderos" | wc -w
```

> Resultado: `5` (são 5 palavras).

---
# 🛠️ Principais opções do `wc`

| **Opção** | **Significado**                     |
| --------- | ----------------------------------- |
| `-l`      | Conta o número de **linhas**        |
| `-w`      | Conta o número de **palavras**      |
| `-c`      | Conta o número de **bytes**         |
| `-m`      | Conta o número de **caracteres**    |
| `-L`      | Mostra o tamanho da **maior linha** |

---
# 🧪 Exemplo Prático de Uso com Pipes

## 🔍 Contar o número de usuários no sistema:

```bash
cat /etc/passwd | wc -l
```

> Mostra quantos usuários (linhas) existem no arquivo `/etc/passwd`

## 🔍 Contar apenas os arquivos `.log` de um diretório:

```bash
ls *.log | wc -l
```

