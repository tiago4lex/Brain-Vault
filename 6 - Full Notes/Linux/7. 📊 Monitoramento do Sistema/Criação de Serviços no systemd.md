2025-08-25 11:14

Status: #developed #Linux 

Tags: [[Linux]] | [[systemd]]

----
# Introdução

## O que é o `systemd`?

O `systemd` é o sistema de inicialização e gerenciamento de serviços mais usado nas distribuições modernas de Linux (como Ubuntu, Debian, CentOS, Fedora).

Ele substituis os scripts tradicionais do **SysVinit**, oferecendo mais velocidade padronização e recursos avançados.

**O `systemd` é responsável por:**

- Inicializar o sistema.
- Gerenciar serviços (start, stop, restart, reload).
- Controlar dependências entre processos.
- Gerenciar via logs via `journalctl`.

---
# Importância do `systemd`

1. **Automatização:** permite que scripts/programas iniciam automaticamente no boot.
2. **Padronização:** serviços são controlados sempre pelos mesmos comandos (`systemctl`).
3. **Monitoramento:** integração com `journalctl` facilita análise de logs.
4. **Confiabilidade:** reinício automático de serviços em caso de falha.
5. **Escalabilidade:** fundamental em servidores que rodam múltiplos serviços.

---
# Estrutura de um arquivo de serviço (`.service`)

Um arquivo de unidade do `systemd` geralmente fica em:

```swift
/etc/systemd/system/nome_do_servico.service
```

E segue este formato:

```
[Unit]
Description=Descrição do serviço
After=network.target

[Service]
ExectStart=/caminho/para/o/programa ou script
Restart=always
User=usuario
WorkingDirectory=/caminho/diretorio
StandardOutput=append:/var/log/nome_do_servico.log
StandardError=append:/var/log/nome_do_servico.err

[Install]
WantedBy=multi-user.target
```

### Explicação das seções

- `[Unit]`
	- `Description=` → breve descrição.
	- `After=` → define dependências (ex.: só iniciar após a rede estar ativa).

- `[Service]`
	- `ExecStart=` → comando ou script que será executado.
	- `Restart=` → política de reinício (`no`, `on-failure`, `always`).
	- `User=` → usuário que vai rodar o serviço.
	- `WorkingDirectory=` → define diretório de trabalho.
	- `StandardOutput` e `StandardError` → redirecionam logs.

- `[Install]`
	- `WantedBy=` → define o nível de execução (geralmente `multi-user.target`).]

---
# Exemplos de Serviços

## 1. Serviço para rodar um script de monitoramento

Crie o arquivo:

```bash
sudo nano /etc/systemd/system/monitoramento.service
```

Conteúdo:

```ini
[Unit]
Description=Monitoramento de Sistema
After=network.target

[Service]
ExecStart=/home/usuario/monitoramento_logs_sistema.sh
Restart=always
User=usuario
WorkingDirectory=/home/usuario
StandardOutput=append:/home/usuario/monitoramento.log
StandardError=append:/home/usuario/monitoramento.err

[Install]
WantedBy=multi-user.target
```

## 2. Serviço para rodar um servidor web (Flask, por exemplo)

```ini
[Unit]
Description=Aplicação Flask
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/usuario/app.py
WorkingDirectory=/home/usuario
Restart=always
User=usuario

[Install]
WantedBy=multi-user.target
```

---
# Comandos principais (`systemctl`)

- **Iniciar o serviço:**

```bash
sudo systemctl start nome_do_servico
```

- **Parar o serviço:**

```bash
sudo systemctl stop nome_do_servico
```

- **Reiniciar o serviço:**

```bash
sudo systemctl restart nome_do_servico
```

- **Ver status do serviço:**

```bash
sudo systemctl status nome_do_servico
```

- **Habilitar no boot:**

```bash
sudo systemctl enable nome_do_servico
```

- **Desabilitar no boot:**

```bash
sudo systemctl disable nome_do_servico
```

- **Recarregar as unidades (necessário após criar/editar):**

```bash
sudo systemctl daemon-reload
```

---
# Logs do serviço

Todos os logs de serviços gerenciados pelo `systemd` vão para o `journalctl`

**Exemplo:**

```bash
journalctl -u nome_do_servico
```

**Opções úteis:**

- `-f` → acompanhar em tempo real (`tail -f` style).
- `--since "1 hour ago"` → logs da última hora.

---
# Diferentes usos do `systemd`

1. **Rodar scripts personalizados** (ex: backup, monitoramento, sync).
2. **Gerenciar aplicações web** (Flask, Node.js, Django).
3. **Serviços críticos de infraestrutura** (bancos de dados, proxies, VPNs).
4. **Automação de tarefas administrativas** (limpeza de logs, envio de alertas).
5. **Criar timers** → substitui cron jobs com unidades `.timer`.

---
# Conclusão

- O **`systemd`** é hoje o padrão no Linux para gerenciar **serviços, processos e inicialização**.
- Criar um serviço garante que scripts/programas rodem automaticamente no boot e sejam facilmente controlados.
- Ele substitui soluções improvisadas como adicionar scripts em `rc.local` ou `cron @reboot`.
- Com recursos de logs, reinício automático e controle de dependências, o `systemd` é indispensável para **servidores de produção**.

---
# Referências

- [Documentação do systemd](https://systemd.io)