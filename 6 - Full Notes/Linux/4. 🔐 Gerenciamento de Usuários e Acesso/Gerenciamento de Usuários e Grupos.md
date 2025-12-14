2025-07-27 21:37

Status: #developed #Linux 

Tags: [[Linux]] | [[chown]] | [[adduser]] | [[addgroup]] | [[deluser]] | [[delgroup]] | [[usermod]]

----
# Introdução

No Linux, **usuários e grupos** são a base do sistema de permissões e segurança. Cada arquivo, processo e recurso é associado a um usuário *(user)* e a um grupo *(group)*.

---
# 📌 1. Conceitos Fundamentais

## 🧑 Usuário

- Representa uma identidade no sistema (real ou de sistema).
- Cada usuário possui:
	- Um nome (`username`)
	- Um ID (`UID`)
	- Um diretório pessoal (`home/nome`)
	- Um shell padrão (`bin/bash`, `bin/sh`, etc.)

## 👥 Grupo

- Um conjunto de usuários.
- Usado para atribuir permissões em conjunto.
- Cada usuário pertence a um grupo primário *(default)* e pode ser adicionado a grupos secundários.

---
# 🛠️ Criando e Removendo Usuários

## 🔧 Criar um usuário

```bash
sudo adduser nome_do_usuario
```

> Esse comando cria o usuário, diretório `home`, define shell e pede uma senha.

**Exemplo:**

```bash
sudo adduser julia
```

## ❌ Remover um usuário

```bash
sudo deluser nome_do_usuario
```

**Remover também o diretório home e arquivos associados:**

```bash
sudo deluser --remove-home nome-do-usuario
```

**Exemplo:**

```bash
sudo deluser --remove-home julia
```

---
# 👥 Criando e Removendo Grupos

## 🔧 Criar um grupo

```bash
sudo addgroup nome_do_grupo
```

**Exemplo:**

```bash
sudo addgroup desenvolvedores
```

## ❌ Remover um grupo

```bash
sudo delgroup nome_do_grupo
```

---
# 👤 Gerenciar associação de usuários a grupos

## ➕ Adicionar usuário a um grupo

```bash
sudo usermod -aG nome_do_grupo nome_do_usuario
```

> O `-aG` adiciona o grupo à lista de grupos secundários.

**Exemplo:**

```bash
sudo usermod -aG sudo julia
```

## 👁️ Ver grupos de um usuário

```bash
groups nome_do_usuario
```

**Exemplo:**

```bash
groups tiago
```

---
# 🔐 Permissões de Arquivos e Diretórios

**Cada arquivo ou pasta tem:**

- **Proprietário *(user)***
- **Grupo *(group)***
- **Permissões para:**
	- Usuário (u)
	- Grupo (g)
	- Outros (o)

## 🔍 Ver permissões

```bash
ls -l
```

**Exemplos de saída:**

```bash
-rw-r--r-- 1 julia desenvolvedores 2048 jul 24 20:00 relatorio.txt
```

- `julia`: usuário dono
- `desenvolvedores`: grupo
- `rw-`: permissões do usuário
- `r--`: permissões do grupo
- `r--`: permissões para outros

## ✏️ Alterar dono e grupo do arquivo

**Mudar usuário done:**

```bash
chown novo_usuario arquivo.txt
```

**Mudar dono e grupo:**

```bash
sudo chown usuario:grupo arquivo
```

**Exemplo:**

```bash
sudo chown julia:desenvolvedores relatorio.txt
```

## ✏️ Alterar permissões

Com `chmod`

```bash
chmod [permissões] arquivo
```

**Formatos possíveis:**

- **Simbólico:**

```bash
chmod u+x script.sh      # Adiciona permissão de execução para o usuário
chmod g-w arquivo.txt    # Remove permissão de escrita do grupo
chmod o+r arquivo.txt    # Adiciona leitura para outros
```

- **Numérico (modo octal):**
	- `r = 4`, `w = 2`, `x = 1`
	- Soma dos valores:
	    - `chmod 755 arquivo.sh` → `rwxr-xr-x`
	    - `chmod 644 arquivo.txt` → `rw-r--r--`

---
# 🔄 Alternar entre usuários no terminal

## Usar `su` *(switch user)*

```bash
su nome_do_usuario
```

**Exemplo:**

```bash
su julia
```

> Será solicitada a senha do usuário


## Usar `sudo -u`

```bash
sudo -u nome_do_usuario comando
```

**Exemplos:**

```bash
sudo -u julia whoami
```

> Executa o comando como se fosse o outro usuário.

---
# Dicas Extras

- Para editar **usuários manualmente** é usado:

```bash
sudo nano /etc/passwd
sudo nano /etc/group
```

> ⚠️ Só edite manualmente se souber o que está fazendo!

- Pra ver **UID** e **GID**:

```bash
id julia
```

- Pra **bloquear um usuário temporariamente:**

```bash
sudo usermod -L nome
```

- Para **desbloquear:**

```bash
sudo usermod -U nome
```

---
# Resumo dos Principais Comandos


| **Ação**                      | **Comando**                                |
| ----------------------------- | ------------------------------------------ |
| Criar usuário                 | `sudo adduser nome`                        |
| Deletar usuário               | `sudo deluser nome`                        |
| Criar group                   | `sudo addgroup nome`                       |
| Deletar grupo                 | `sudo delgroup nome`                       |
| Adicionar usuário a grupo     | `sudo usermod -aG usuario`                 |
| Ver grupos de um usuário      | `groups usuario`                           |
| Mudar dono e grupo de arquivo | `sudo chown usuario:grupo arquivo`         |
| Mudar permissões              | `chmod 755 arquivo` ou `chmod u+x arquivo` |
| Alternar usuário              | `su usuario` ou `sudo -u usuario comando`  |
| Ver UID/GID                   | `id usuario`                               |

