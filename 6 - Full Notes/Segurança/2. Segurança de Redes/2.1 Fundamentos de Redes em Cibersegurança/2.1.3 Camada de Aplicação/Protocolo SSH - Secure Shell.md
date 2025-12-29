2025-12-28 22:30

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[SSH]]

----
# Introdução

O **SSH *(Secure Shell)*** é um protocolo de rede utilizado para **acesso remoto seguro**, administração de sistemas e transferências de arquivos de forma criptografada. Ele substitui protocolos inseguros com **Telnet**, **rlogin** e **FTP**, que transmitiam dados em texto puro.

Na cibersegurança, o SSH é um dos protocolos mais críticos, pois fornece **acesso direto a servidores**, equipamentos de rede e ambientes em nuvem. Uma configuração incorreta pode levar ao comprometimento total do sistema.

![[Pasted image 20251228223432.png]]

---
# Em qual camada o SSH atua?

- **Modelo OSI:** Camada 7 - Aplicação
- **Modelo TCP/IP:** Camada de Aplicação

O SSH utiliza:

- **TCP Porta 22** (padrão)

---
# Para que serve o SSH

O SSH é utilizado para:

- acesso remoto a servidores Linux/Unix;
- administração de sistemas;
- execução de comandos remotos;
- transferência segura de arquivos (SCP, SFTP);
- tunelamento de tráfego (SSH Tunneling);
- automação e DevOps.

---
# Como o SSH funciona?

O SSH estabelece uma conexão segura baseada em **criptografia assimétrica e simétrica**.

## Etapas da Conexão SSH

1. Cliente inicia a conexão TCP
2. Negociação de versões e algoritmos
3. Autenticação do servidor
4. Autenticação do cliente
5. Canal criptografado estabelecido

---
# Criptografia no SSH

## Criptografia Assimétrica

Usada para autenticação e troca de chaves.

## Criptografia Simétrica

Usada para comunicação após o handshake.

## Hashing

Usado para integridade dos dados.

---
# Autenticação no SSH

## 1. Autenticação por Senha

- simples;
- menos segura;
- vulnerável a brute force.

## 2. Autenticação por Chave Pública

- mais segura;
- baseada em par de chaves;
- amplamente recomendada.

## Autenticação Multifator (MFA)

- camada extra de segurança;
- integração com PAM, OTP.

---
# Componentes Importantes do SSH

- **sshd:** serviço servidor
- **ssh:** cliente
- **authorized_keys:** chaves permitidas
- **known_hosts:** chaves dos servidores conhecidos

---
# Vulnerabilidades Relacionadas ao SSH

## 1. Brute Force

Tentativas repetidas de senha.

Impacto:

- acesso não autorizado;
- comprometimento do sistema.

## 2. Credenciais Fracas

- senha simples;
- chaves vazadas.

## 3. SSH Mal Configurado

- login root habilitado;
- versões antigas;
- algoritmos fracos.

## 4. MITM (Man-in-the-Middle)

- Ocorre quando a chave do servidor não é válida.

## 5. Exploração de Versões Vulneráveis

- falhas no OpenSSH;
- CVEs conhecidos.

---
# Ataques Comuns Envolvendo SSH

- Brute force distribuído;
- Credential stuffing;
- Pivoting em redes internas;
- Backdoors via chaves SSH.

---
# Ferramentas para testes de Segurança SSH

### Pentest e Ataques

- Hydra
- Medusa
- Ncrack
- Metasploit

### Enumeração e Auditoria

- Nmap (`ssh-auth-methods`, `ssh-hostkey`)    
- ssh-audit

### Monitoramento

- Fail2ban    
- Logs do sistema

---
# Mitigação e Boas Práticas de Segurança SSH

## 1. Usar Autenticação por Chave

Desabilitar autenticação por senha.

## 2. Desabilitar Login Root

Usar sudo para administração.

## 3. Alterar Porta Padrão

Reduz ataques automatizados.

## 4. Configurar Fail2Ban

Bloqueio automático de IPs.

## 5. Hardening do SSH

- desativar protocolos antigos;
- usar algoritmos fortes;
- limitar usuários permitidos.

## 6. Monitoramento e Logs

Analisar tentativas suspeitas.

---
# SSH Tunneling (Port Forwarding)

O SSH permite criar túneis criptografados.

Tipos:

- Local Port Forwarding
- Remote Port Forwarding
- Dynamic Port Forwarding (SOCKS)

---
# SSH em ambientes corporativos e Cloud

Usado em:

- servidores Linux;
- containers;
- Kubernetes;
- AWS, Azure, GCP.

Boas práticas:

- uso de bastion host;
- rotação de chaves;
- controle de acesso baseado em função.

---
# Importância do SSH para Cibersegurança

Compreender o SSH permite:

- administrar sistemas com segurança;
- detectar ataques de força bruta;
- proteger acessos privilegiados;
- realizar pentests internos;
- responder a incidentes.

---
# Configuração Prática e Comandos Essenciais do SSH

## 1. Instalando e Habilitando o SSH

Em sistemas Linux (Debian/Ubuntu):

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

Verificar status:

```bash
sudo systemctl status ssh
```

## 2. Arquivo de configuração do SSH (`sshd_config`)

O principal arquivo de configuração do servidor SSH é:

```bash
/etc/ssh/sshd_config
```

Configurações importantes para segurança:

```bash
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowUsers usuario1 usuario2
```

Após alterações:

```bash
sudo systemctl restart ssh
```

## 3. Conectando-se a um servidor via SSH

Conexão básica:

```bash
ssh usuario@ip_do_servidor
```

Especificando porta:

```bash
ssh usuario@ip_do_servidor -p 2222
```

Conectando com chave específica:

```bash
ssh -i chave_privada.pem usuario@ip_do_servidor
```

## 4. Gerando um Par de Chaves SSH (acesso sem senha)

Gerar chave SSH (recomendado Ed25519):

```bash
ssh-keygen -t ed25519 -C "meu_email@exemplo.com"
```

Arquivos gerados:

- chave privada: `~/.ssh/id_ed25519`
- chave pública: `~/.ssh/id_ed25519.pub`

>[!warning] Atenção:
>Nunca compartilhe a chave privada.


## 5. Copiando a chave pública para o Servidor

Forma automática:

```bash
ssh-copy-id usuario@ip_do_servidor
```

Forma manual:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copiar o conteúdo para o arquivo:

```bash
~/.ssh/authorized_keys
```

no servido.

Permissões corretas:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## 6. Testando acesso SSH sem senha

Após configurar as chaves:

```bash
ssh usuario@ip_do_servidor
```

Se configurado corretamente, o aceso ocorrerá **sem solicitar senha**.

## 7. SSH Tunneling - Exemplos Práticos

**Port Forwarding Local:**

```bash
ssh -L 8080:localhost:80 usuario@servidor
```

**Port Forwarding Remote:**

```bash
ssh -R 9090:localhost:22 usuario@servidor
```

**Port Forwarding Dinâmico (SOCKS Proxy):**

```bash
ssh -D 1080 usuario@servidor
```

## 8. Boas Práticas de Segurança no uso diário do SSH

- usar chaves com passphrase;
- nunca compartilhar chaves privadas;
- remover chaves não utilizadas;
- monitorar logs (`/var/log/auth.log`);
- usar Fail2ban;
- manter o OpenSSH atualizado.

---
# Conclusão

O protocolo SSH é um dos pilares da administração segura de sistemas. Ele oferece confidencialidade, integridade e autenticação, mas apenas quando **corretamente configurado**.

Configurações fracas, chaves expostas ou versões desatualizadas podem transformar o SSH em um vetor crítico de ataque.

Para profissionais de cibersegurança, dominar o SSH é essencial para atuar em **Blue Team, Red Team, DevSecOps e Cloud Security**.