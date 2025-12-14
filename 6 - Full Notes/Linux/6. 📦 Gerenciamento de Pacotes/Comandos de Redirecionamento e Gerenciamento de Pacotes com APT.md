2025-07-25 08:35

Status: #developed #Linux 

Tags: [[Linux]] | [[apt]] | [[>]] | [[>>]]

----
# Introdução

- **Redirecionamento de saída** com os operadores `>` e `>>`
- **Gerenciamento de pacotes** com o gerenciador APT (`apt update`, `apt install`, etc.).

---
# 🔁 Redirecionamento de Saída no Terminal

O terminal Linux permite redirecionar a saída dos comandos para arquivos. Isso é útil para registrar logs, salvar resultados ou sobrescrever/criar arquivos automaticamente.

## `>` — Redirecionamento com sobrescrita

- **Descrição:** Redireciona a saída de um comando para um arquivo, **sobrescrevendo** o conteúdo existente (ou criando o arquivo se ele não existir).
- **Uso:**

```bash
comando > arquivo.txt
```

**Exemplo:**

```bash
echo "Olá, mundo!" > saudacao.txt
```

**Resultado:** cria (ou sobrescreve) o arquivo `saudacao.txt` com o conteúdo `"Olá, mundo!`.

##  `>>` — Redirecionamento com adição (append)

- **Descrição:** Redireciona a saída para o final do arquivo, **sem apagar** o que já estava lá.
- **Uso:**

```bash
comando >> arquivo.txt
```

**Exemplo:**

```bash
echo "Nova linha" >> saudacao.txt
```

**Resultado:** Adiciona `"Nova linha"` ao final do arquivo `saudacao.txt`

---
# 📦 Gerenciamento de Pacotes com APT

APT *(Advanced Package Tool)* é o sistema de gerenciamento de pacotes usado por distribuições Linux baseadas em Debian, como Ubuntu.

## `sudo apt update`

- **Descrição:** Atualiza a lista de pacotes disponíveis dos repositórios configurados.
- **Uso:**

```bash
sudo apt update
```

- **Função:** Não insta nem atualiza pacotes ainda - apenas atualiza as *informações* sobre o que está disponível para instalação/atualização.

## `sudo apt install`

- **Descrição:** Instala pacotes do repositório APT.
- **Uso:**

```bash
sudo apt install nome-do-pacote
```

**Exemplo:**

```bash
sudo apt install htop
```

Isso instalará o program `htop`, se ele estiver disponível.

## `sudo apt upgrade`

- **Descrição:** Atualiza todos os pacotes instalados para suas versões mais recentes disponíveis.
- **Uso:**

```bash
sudo apt upgrade
```

- **Recomendado após** o `sudo apt update`

## `sudo apt purge`

- **Descrição:** Remove completamente um pacote, **incluindo seus arquivos de configuração**.
- **Uso:**

```bash
sudo apt purge nome-do-pacote
```

**Exemplo:**

```bash
sudo apt purge htop
```

- **Diferença de** `apt remove`: `purge` remove os arquivos de configuração; `remove` não.

---
