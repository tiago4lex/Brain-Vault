2025-08-25 11:47

Status: #developed #Linux 

Tags: [[Linux]] | [[systemd]]

----
# Introdução

## O que são Serviços no Linux?

Um serviço no Linux é um processo (ou conjunto de processos) que roda em segundo plano ***(background)*** para fornecer uma funcionalidade contínua ao sistema ou aos usuários.

### Exemplos de serviços comuns

- Servidores de rede (ex: **Apache, Nginx, SSH**).
- Banco de dados (ex: **MySQL, PostgreSQL**).
- Monitoramento (ex: **cron, syslog**).
- Gerenciamento de rede (ex: **NetworkManager, dhcpd**).

Um serviço:

- Pode iniciar automaticamente junto com o sistema (boot).
- Pode ser iniciado manualmente quando necessário.
- Normalmente não precisa de interação direta do usuário (roda “silenciosamente” em background).

---
# Características dos Serviços

1. **Execução em segundo plano:** diferentemente de processos interativos (como abrir o terminal).
2. **Longa duração:** serviços ficam ativos até serem parados ou até o sistema ser desligado.
3. **Automação:** podem ser configurados para iniciar automaticamente no boot.
4. **Gerenciamento centralizado:** no Linux moderno, via `systemd`.
5. **Isolamento:** muitos serviços rodam com permissões restritas (ex.: `www-data` para Apache).
6. **Dependências:** podem depender de outros serviços (ex.: **um servidor web pode depender do serviço de rede**).

---
# Tipos de Serviços no Linux

## 1. Serviços de Sistema

- Essenciais para o funcionamento do sistema.
- Exemplo: `systemd-udevd` (gerencia dispositivos), `cron` (agendamento de tarefas).

## 2. Serviços de Rede

- Fornece recursos pela rede.
- Exemplo: `sshd` (acesso remoto), `nginx` (servidor web), `smbd` (compartilhamento de arquivos).

## 3. Serviços de Aplicação

- Ligados a software instalados.
- Exemplo: `mysql` (banco de dados), `docker` (containers).

## 4. Serviços Temporários *(on-demand)*

- Ativados quando são necessários.
- Exemplos: `cups` (impressão) pode iniciar só quando alguém solicita impressão.

## 5. Serviços do Usuário

- Executados no contexto de um usuário específico.
- Exemplo: `pipewire` (áudio), `gnome-session` (sessão gráfica).

---
# Exemplos de Serviços

- **`sshd`** → serviço de acesso remoto via SSH.
- **`nginx` / `apache2`** → servidores web.
- **`cron`** → agendamento de tarefas automáticas.
- **`mysql` / `postgresql`** → bancos de dados.
- **`docker`** → gerenciamento de containers.
- **`systemd-logind`** → gerencia sessões de usuários.

---
# O papel do `systemd`

O **`systemd`** é hoje o **gerenciador de serviços e inicialização** mais usado no Linux. Ele organiza como os serviços são iniciados, gerenciados e monitorados.

### 📌 Características do `systemd`:

1. **Gerenciamento de serviços** → via comando `systemctl`.
2. **Inicialização paralela** → acelera o boot executando múltiplos serviços ao mesmo tempo.
3. **Monitoramento e reinício automático** → reinicia serviços em caso de falha.
4. **Integração com logs (`journalctl`)** → coleta e organiza logs de todos os serviços.
5. **Unidades (units)** → cada serviço é definido em um arquivo `.service`, mas o `systemd` também gerencia unidades de **dispositivos**, **sockets**, **timers** e **mounts**.
6. **Dependências e targets** → permite definir a ordem de inicialização dos serviços.

### 📌 Comandos comuns do `systemd`:

- **Iniciar serviço**:

```bash
sudo systemctl start ssh
```

- **Parar serviço**:

```bash
sudo systemctl stop ssh
```

- **Ver status do serviço**:

```bash
sudo systemctl status ssh
```

- **Habilitar no boot**:

```bash
sudo systemctl enable ssh
```

- **Ver logs de um serviço**:

```bash
sudo journalctl -u ssh 
```

---
# Conclusão

- **Serviços** são processos essenciais que garantem funcionalidades contínuas no Linux.
- Eles podem ser de sistema, rede, aplicação, temporários ou do usuário.
- Exemplos incluem **SSH, Apache, MySQL, Docker**.
- O **`systemd`** é a ferramenta moderna que centraliza o gerenciamento de serviços.
- Com ele, administradores podem **iniciar, parar, monitorar, reiniciar, e configurar a inicialização automática de serviços** de forma simples e padronizada.