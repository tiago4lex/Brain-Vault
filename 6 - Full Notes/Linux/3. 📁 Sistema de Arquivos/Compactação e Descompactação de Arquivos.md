2025-07-29 18:36

Status: #developed #Linux 

Tags: [[Linux]] | [[tar]] | [[gzip]] | [[gunzip]]

----
# 🎯 Objetivo

A compactação é usada para **reduzir o tamanho** de arquivos ou **agrupar vários arquivos/diretórios** em um único arquivo. É útil para:

- Backups
- Transferência de arquivos
- Organização

---
# 📌 Comando `tar` (Tape Archive)

## ✅ Função:

O `tar` serve para **agrupar** vários arquivos/diretórios em um único arquivo `.tar` (sem compressão por padrão). Pode ser usado junto com `gzip` ou `bzip2` para compressão real.

## 📚 Sintaxe:

```bash
tar [opções] nome-do-arquivo.tar [arquivos/diretórios]
```

## 🧪 Exemplos de uso

### Criar um arquivo `.tar` **(sem compressão)**

```bash
tar -cf arquivos.tar pasta1 arquivo2.txt
```

- `-c`: criar um novo arquivo
- `-f`: define o nome do arquivo

### Extrair um `.tar`

```bash
tar -xf arquivos.tar
```

- `-x`: extrai
- `-f`: usa arquivo como entrada

---
# 🗜️ Comando `gzip` (GNU zip)

## ✅ Função:

Compacta arquivos individuais usando o algoritmo **DEFLATE.** O resultado é um arquivo `.gz`.

## 📚 Sintaxe:

```bash
gzip [opções] arquivo
```

## 🧪 Exemplos

### Compactar um arquivo

```bash
gzip log.txt
```

> Cria `log.txt.gz` e **remove o original**

### Manter o original

```bash
gzip -k log.txt
```

### Descompactar

```bash
gunzip log.txt.gz
```

> Recupera `log.txt`

---
# 📦 Compactação com `tar + gzip`

A combinação mais comum é usar o `tar` com `gzip` para gerar arquivos `.tar.gz` ou `.tgz`.

## Criar um `.tar.gz`

```bash
tar -czf backup.tar.gz pasta1 arquivo.txt
```

- `-z`: usa `gzip` para compressão
- `-c`: cria
- `-f`: define o nome
- `-v` (opcional): mostra progresso

## Extrair um `.tar.gz`

```bash
tar -xzf backup.tar.gz
```

- `-x`: descompacta

## Listar conteúdo de um `.tar.gz` sem extrair

```bash
tar -tzf backup.tar.gz
```

- `-t`: lista todo o conteúdo dentro do arquivo compactado sem extrair o seu conteúdo

---
# 📦 Outras extensões comuns

| **Extensão**       | **Descrição**                           |
| ------------------ | --------------------------------------- |
| `.tar`             | Arquivo agrupado, sem compressão        |
| `.gz`              | Arquivo comprimido com gzip             |
| `.tar.gz` / `.tgz` | Agrupado e comprimido com gzip          |
| `.zip`             | Formato alternativo (ver `zip`/`unzip`) |

---
# 🛠️ Exemplo prático de backup

```bash
tar -czvf meus_dados_$(date +%Y-%m-%d).tar.gz ~/Documentos
```

> Criar um backup de pasta `Documentos` com timestamp da data.
