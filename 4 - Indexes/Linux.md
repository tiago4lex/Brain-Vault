
#Linux 

---
## 1. 🌱 **Introdução ao Linux**

- História e Filosofia do Linux
- Distribuições Populares (Ubuntu, Fedora, Debian, Arch etc.)
- Instalação do Linux (Dual Boot / Máquina Virtual / WSL)
- Estrutura de Diretórios do Linux (`/bin`, `/home`, `/etc`, etc.)

---

## 2. 🖥️ **Comandos Básicos e Navegação**

- ✅ [[Comandos Básicos de Terminal]]
    - `pwd`, `ls`, `cd`, `cat`, `sudo`

-  Comandos de Privilégio    
    - `sudo`, `sudo -i`, `sudo su`

- ✅ [[Comandos de Manipulação de Arquivos e Diretórios]]    
    - `mkdir`, `touch`, `mv`, `rm`, `cp`, `nano`

- Controle de Versão e Repositórios
    - `git clone`

- ✅ [[Manipulação de Data e Hora]]    
    - `date`


---

## 3. 📁 **Sistema de Arquivos e Manipulação de Texto**

- Interagindo com o Sistema de Arquivos
	- ✅ [[Interagindo com o Sistema de Arquivos - Part 1]]
	- ✅ [[Interagindo com o Sistema de Arquivos - Part 2]]

- ✅ [[Editor de Texto Vim - Comandos e Atalhos]]
	- `vim`

- Localizando Arquivos
	- ✅ [[Procurando por arquivos]]
		- `grep`, `find`
	- ✅ [[Comandos de Busca e Localização]]
	    - `find`, `locate`, `grep`, `which`, `whereis`

- ✅ [[Manipulação de Texto]]    
    - `sed`, `sort`, `awk`

- ✅ [[Comparação e Filtragem de Dados]]    
    - `diff`, `uniq`

- ✅ [[Análise de Conteúdo (Word Count)]]
    - `wc`

- ✅ [[Expressões Regulares (Regex)]]    
- ✅ [[Compactação e Descompactação de Arquivos]]
    - `tar`, `gzip`, `gunzip`


---

## 4. 🔐 **Usuários, Grupos e Permissões**

- ✅ [[Gerenciamento de Usuários e Grupos]]
    - `adduser`, `userdel`, `usermod`, `chown`, `chmod`

- ✅ [[Login via SSH - Comandos Básicos]]    
    - `ssh`, `scp`, geração de chaves SSH, permissões
        

---

## 5. ⚙️ **Operadores e Redirecionamentos**

- ✅ [[Shell Operators]]
    - Operadores lógicos (`&&`, `||`, `!`)
    - Redirecionamento (`>`, `>>`, `<`, `2>`, `&>`, `2>&1`)
    - Pipes (`|`), substituições, `xargs`

---

## 6. 📦 **Gerenciamento de Pacotes**

- ✅ [[Comandos de Redirecionamento e Gerenciamento de Pacotes com APT]]
- Gerenciadores por distro: `apt`, `dnf`, `yum`, `pacman`, `snap`
- Instalação de softwares e atualização do sistema

---

## 7. 📊 **Monitoramento do Sistema**

- ✅ [[Conceitos de Serviços]]
- ✅ [[Gerenciamento de Processo no Linux]]
    - Monitoramento: `top`, `htop`
    - Controle de processos: `ps`, `kill`, `nice`, `renice`

- ✅ [[Logs do Sistema no Linux]]    
    - Arquivos importantes: `/var/log/syslog`, `auth.log`, `kern.log`, etc.

- ✅ [[Verificação de Uso de Disco]]
	- `df`, `du`

- ✅ [[Monitoramento de Memória RAM]]
	- `free`, `top`, `htop`

- ✅ [[Monitoramento de CPU]]
	-  `uptime`, `top`, `htop`  `mpstat`, `sar`

- ✅ [[Monitoramento com o comando iostat]]
	- `iostat`

- ✅ [[Monitoramento de Memória RAM]]
	- `free`, `vmstat`, `stop`

- ✅ [[Criação de Serviços no systemd]]
	- `systemd`, `systemctl`

---

## 8. 📑 **Automação e Shell Script**

- [[Introdução ao Shell Script]]
    - Variáveis, parâmetros, funções, laços (`for`, `while`, `until`)

- ✅ [[Agendamento de Tarefas]]    
    - Agendamentos com `crontab`

-  Scripts de Monitoramento    
    - [[Comando awk  - Análise e Formatação de Logs]] `awk`
    - Monitoramento de rede com `ping` e `curl`

---

## 9. 🔒 **Segurança e Permissões**

- [[Permissões Avançadas e Mecanismos de Segurança]]
	- Controle de acesso com `chmod`, `umask`, `setfacl`

- [[Sticky Bit - Controle de Exclusão em Diretórios Compartilhados]]
- Conceitos de root, sudoers
- Firewall básico (`ufw`, `iptables`)
- SSH seguro, fail2ban, autenticação por chave

---

## 10. 🔗 **Redes no Linux**

- Interfaces de Rede e Configurações de IP
    - `ip`, `ifconfig`, `nmcli`

- ✅ [[Verificação de Conectividade com a Internet e Monitoramento de Rede]] 
    - `ping`, `traceroute`, `curl`, `wget`, `nslookup`, `dig`
    - [[Comando Curl no Linux]]
    - [[Comandos Avançados com Curl]]

- [[IPTABLES - Firewall do Linux]]
	- [[IPTABLES - Guia Introdutório]]

- Hosts, DNS, roteamento    

---

## 11. 🐧 **Ambiente e Customização**

- Variáveis de ambiente (`PATH`, `HOME`, etc.)
- Personalização do bash (`.bashrc`, `.bash_profile`)
- Alias e funções personalizadas

---

## 12. 🧠 **Tópicos Avançados (futuros)**

- Montagem de sistemas de arquivos (`mount`, `umount`, `fstab`)
- Gerenciamento de serviços (`systemctl`, `service`)
- Contêineres com Docker no Linux
- Kernel, boot e init systems