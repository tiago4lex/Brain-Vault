2025-07-25 09:36

Status: #developed #Linux 

Tags: [[Linux]] | [[top]] | [[htop]] | [[kill]] | [[pkill]] | [[nice]] | [[renice]] | [[jobs]] | [[fg]] | [[bg]]

----
# Introdução

No Linux, **processos** são programes em execução. O sistema fornece diversos comandos para **monitorar, controlar e manipular** esses processos via terminal.

Aqui será apresentado os principais comandos de gerenciamento de processo: `ps`, `top`, `htop`, `kill`, `pkill`, `nice`, `renice`, `jobs`, `fg`, `bg`.

---
# 📋 `ps` — _Process Status_

- **Descrição**: Lista os processos em execução.
- **Uso comum**:

```bash
ps aux
```

- **Explicação das opções:**
	- `a`: Mostra processos de todos os usuários.
	- `u`: Mostra o nome do usuário.
	- `x`: Mostra processos que não estão associados a um terminal.

**Exemplo de uso:**

```bash
ps aux | grep firefox
```

→ Mostra processos relacionados ao Firefox.

---
# 📈 `top` — _Monitoramento em tempo real_

- **Descrição**: Exibe os processos em execução em tempo real, ordenados por uso de CPU/memória.
- **Uso**:

```bash
top
```

- **Atalhos úteis dentro do `top`**:
    - `q`: Sair
    - `k`: Matar um processo (insira o PID)
    - `P`: Ordenar por uso de CPU
    - `M`: Ordenar por uso de memória

---
# 🧰 `htop` — _Top melhorado (interface interativa)_

- **Descrição**: Ferramenta similar ao `top`, mas com interface mais amigável e colorida.
- **Uso**:

```bash
htop
```

- **Necessário instalar** (se ainda não tiver):

```bash
sudo apt install htop
```

---
# 🔫 `kill` — _Encerra processos pelo PID_

- **Descrição:** Envia sinais a processos (geralmente para encerrá-los).
- **Uso:**

```bash
kill -s sinal PID
```

ou

```bash
kill -9 PID
```

- **Sinais comuns:**
	- `-15`: (SIGTERM): Solicita término gracioso (padrão)
	- `-9`: (SIGKILL): Mata o processo forçadamente

**Exemplo:**

```bash
kill -9 1234
```

---
# ## 🎯 `pkill` — _Encerra processos pelo nome_

- **Descrição**: Mata processos com base no nome em vez do PID.
- **Uso**:

```bash
pkill nome_processo
```

**Exemplo:**

```bash
pkill firefox
```

---
# ## 📊 `nice` — _Inicia processos com prioridade definida_

- **Descrição**: Define a prioridade de um processo ao iniciá-lo.
- **Níveis de prioridade (`nice value`)**: vão de `-20` (maior prioridade) a `19` (menor prioridade).
- **Uso**:

```bash
nice -n 10 comando
```

**Exemplo:**

```bash
nice -n 5 ./script.sh
```

---
# ## 🔄 `renice` — _Altera a prioridade de um processo em execução_

- **Uso**:

```bash
renice -n novo_valor -p PID
```

**Exemplo:**

```bash
renice -n 0 -p 1234
```

---
# ⚙️ Processos em segundo plano

## `jobs`

- **Descrição**: Lista os processos em segundo plano da sessão atual.
- **Uso**:

```bash
jobs
```

## `bg`

- **Descrição**: Coloca um processo suspenso em segundo plano.
- **Uso**:

```bash
bg %1
```

## `fg`

- **Descrição**: Traz um processo em segundo plano para o primeiro plano.
- **Uso**:

```bash
fg %1
```

> `%1`, `%2`, etc., se referem aos IDs dos processos listados com `jobs`.

