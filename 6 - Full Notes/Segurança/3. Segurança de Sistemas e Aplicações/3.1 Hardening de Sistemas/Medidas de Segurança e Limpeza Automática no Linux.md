2025-09-03 09:17

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Linux]]

----
# Medidas Gerais de Segurança no Linux

## 1. Proteção Básica do Sistema

- **Atualizações regulares:** Manter o sistema atualizado.

```bash
sudo apt update && sudo apt upgrade -y
```

- **Firewall configurado:** Uso do UFW *(Uncomplicated Firewall)*

```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

## 2. Controle de Permissões

- **Princípio do menor privilégio:** Usar contas de usuário sem privilégios root.
- **Configuração de `sudo`:** Limitar comandos privilegiados.

```bash
# Editar configurações do sudo
sudo visudo
```

## 3. Criptografia e Proteção de Dados

- **Criptografia de disco:** LUKS para partições sensíveis.
- **Home directory criptografada:** `encryptfs-utils`

```bash
sudo apt install encryptfs-utils
```

---
# Limpeza Automática de Arquivos Temporários

## 1. Diretórios que Requeres Limpeza Regular

**Diretórios Comuns:**

```text
/tmp/
/var/tmp/
~/.cache/
~/.thumbnails/
~/.local/share/Trash/
~/.bash_history/
~/.viminfo/
~/.mysql_history/
~/.ssh/known_hosts/ (cuidado: pode quebrar conexões)
~/.recently-used.xbel
```

## 2. Script de Limpeza Automática

**Criar script de limpeza:**

```bash
#!/bin/bash
# clean_tmp.sh - Script para limpeza de arquivos temporários

# Função para limpar diretórios com verificação
clean_directory() {
	if [ -d "$1" ]; then
		echo "Limpando diretório: $1"
		rm -rf "${1}"/*
		rm -rf "${1}"/.* 2>/dev/null # Ignora erros para . e ..
	fi
}

# Limpar diretórios temporários do sistema
clean_directory "/tmp"
clean_directory "/var/tmp"

# Limpar cache e temporários do sistema
clean_directory "${HOME}/.cache"
clean_directory "${HOME}/.thumbnails"
clean_directory "${HOME}/.local/share/Trash"

# Limpar histório do npm
clean_directory "${HOME}/.npm"

# Limpar cache do navegador (exemplo para Firefox)
if [ -d "${HOME}/.mozilla/firefox" ]; then
	find "${HOME}/.mozilla/firefox" -name "*.default-release" -type d | while read profile; do
		clean_directory "${profile}/cache"
		clean_directory "${profile}/storage"
		rm -f "${profile}/cookies.sqlite" 2>/dev/null
		rm -f "${profile}/places.sqlite" 2>/dev/null
	done
fi

echo "Limpeza concluída: $(date)"  >> /var/log/cleanup.log
```

**Tornar o script executável:**

```bash
sudo chmod +x clean_tmp.sh
sudo mv clean_tmp.sh /usr/local/bin/
```

---
# Configuração de Limpeza no Desligamento

## Método 1: `systemd service` (recomendado)

**Criar serviço `systemd`**:

```bash
# /etc/systemd/system/cleanup.service
[Unit]
Description=Limpeza de arquivos temporários no desligamento
DefaultDependencies=no
Before=shutdown.target reboot.target halt.target

[Service]
Type=oneshot
ExectStart=/usr/local/bin/clean_tmp.sh
RemainAfterExit=yes
User=root

[Install]
WantedBy=halt.target reboot.target shutdown.target
```

**Habilitar o serviço:**

```bash
sudo systemctl deamon-reload
sudo systemctl enable cleanup.service
```

## Método 2: Script no `/etc/rc.local`

```bash
# Adicionar ao /etc/rc.local (antes do exit 0)
/usr/local/bin/clean_tmp.sh
```

## Método 3: Cron Job para Limpeza Regular

```bash
# Editar crontab do root
sudo crontab -e

# Adicionar linha para limpeza diária às 3h
0 3 * * * /use/local/bin/clean_tmp.sh
```

---
# Configurações Específicas por Aplicativo

## 1. Navegadores Web

**Firefox: Configuração para não manutenção de histórico**

- Digitar `about:config` na barra de endereços.
- Definir:
	- `browser.cache.disk.enable = false`
	- `browser.cache.memomy.enable = true`
	- `browser.history_expire_days = 0`
	- `browser.privatebrowsing.autostart = true`

**Chrome/Chromium:**

```bash
# Iniciar com modo incógnito por padrão
chromium-browser --inconito
```

## 2. Bash History Control

**Configurar para não salvar histórico:**

```bash
# Adicionar ao ~/.bashrc
export HISTZIE=0
export HISTFILESIZE=0
unset HISTFILE

# Ou limpar histórico a cada comando
export PROMTP_COMMAND="history -c; history -w"
```

## 3. Configurações do GNOME (se aplicável)

```bash
gsettings set org.gnome.desktop.privacy remember-recent-files false
gsettings set org.gnome.desktop.privacy remove-old-temp-files true
gsettings set org.gnome.desktop.privacy remove-old-trash-files true
```

---
# Ferramentas de Limpeza Automática

## 1. BleachBit

```bash
# Instalação
sudo apt install bleachbit

# Execução com limpeza padrão
bleachbit --clean system.cache system.tmp system.trash
```

## 2. Stacer (Interface Gráfica)

```bash
# Instalação
sudo apt install stacer

# Oferece limpeza de cache e monitoramento do sistema
```

## 3. Scripts personalizados por Aplicativo

```bash
#!/bin/bash
# clean_apps.sh - Limpeza específica por aplicativo

# Docker
docker system prune -af

# NPM
npm cache clean --force

# Pip
rm -rf ~/.cache/pip

# Docker
docker system prune -af --volumes
```

---
# Medidas de Segurança Avançadas

## 1. Filesystems Temporários em RAM

```bash
# Configurar /tmp em tmpfs (adicionar ao /etc/fstab)
tmpfs /tmp tmpfs defaults,noatime,mode=1777,size=1G 0 0
```

## 2. Contêineres de Segurança

**Usar `firejail` para aplicativos:**

```bash
sudo apt install firejail
firejail --private chromium-browser
```

## 3. Virtualização para Atividades Sensíveis

```bash
# Usar márquinas virtuais descartáveis
sudo apt install virtualbox virtualbox-ext-pack
```

---
# Considerações e Precauções

>[!warning] Risco de Limpeza Excessiva
>- Perda de dados sem backup.
>- Quebra de funcionalidades de aplicativos.
>- Problemas de desempenho por recriação constante de cache.

>[!warning] Diretórios que NÃO Devem Ser Limpos
>```text
>/var/log/ (logs do sistema)
>~/.ssh/ (chaves SSH)
>~/.gnupg/ (chave GPG)
>~/.password-store/ (gerenciado de senhas)
>/etc/ (configurações do sistema)
>```

## Backup de Configurações Importantes

```bash
# Script de backup de configurações essenciais
#!/bin/bash
BACKUP_DIR="${HOME}/.config_backup"
mkdir -p "${BACKUP_DIR}"
cp -r ~/.ssh "${BACKUP_DIR}"
cp -r ~/.gnupg "${BACKUP_DIR}"
cp -r ~/.config/important_app "${BACKUP_DIR}"
```

---
# Monitoramento e Verificação

## 1. Verificação de Eficácia

```bash
# Verificar se arquivos temporários estão sendo removidos
sudo find /tmo -type 0f 0mtime +1 | wc -l

# Monitorar uso de disco
df -h | grep -E '(tmpfs|/tmp|/var/tmp)'

# Verificar logs de limpeza
tail -f /var/log/cleanup.log
```

## 2. Teste de Configurações

```bash
# Testar script de limpeza manualmente
sudo /usr/local/bin/clean_tmp.sh

# Verificar serviços systemd
systemctl status cleanup.service
journalctl -u cleanup.service
```

---
# Checklist de Implementação

- Criar scrip de limpeza personalizado.
- Configurar serviço systemd para execução no desligamento.
- Testar script manualmente.
- Configurar limpeza regular via cron.
- Ajustar configurações de aplicativos específicos.
- Implementar backups de configurações importantes.
- Configurar filesystems temporários em RAM.
- Estabelecer monitoramento contínuo.
- Documentar procedimentos para restauração.

---
# Conclusão

A limpeza automática é uma medida eficaz para privacidade, mas deve ser implementada com cuidado para não comprometer a funcionalidade do sistema.

Recomenda-se testar extensivamente em ambiente controlado antes de implantar em produção.