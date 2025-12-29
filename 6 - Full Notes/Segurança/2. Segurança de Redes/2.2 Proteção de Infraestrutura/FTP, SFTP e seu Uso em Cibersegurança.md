2025-07-27 07:08

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[FTP]] | [[SFTP]] | [[Protocolos]]

----
# Introdução

**FTP *(File Transfer Protocol)***  e **SFPT *(SSH File Transfer Protocol)*** são protocolos usados para transferências de arquivos entre sistemas. Enquanto o **FTP** é antigo e inseguro (sem criptografia), o **SFTP** é uma alternativa segura que opera sobre SSH. Ambos são alvos comuns em teste de penetração devido a configurações inadequadas e vulnerabilidades conhecidas.

---
# FTP *(File Transfer Protocol)*

## O que é FTP?

- Protocolo padrão para transferência de arquivos em rede TCP/IP.
- Opera nas **portas 20 (dados)** e **21 (controle)**.
- **Não é criptografado** (senhas e dados trafegam em texto claro).

## Como funciona?

1. **Conexão Inicial** (Porta 21): Autenticação do usuário.
2. **Transferência de Dados** (Porta 2 ou modo passivo): Envio/recebimento de arquivos.

## Comandos Básicos do FTP

| **Comando**     | **Descrição**               |
| --------------- | --------------------------- |
| `ftp <IP>`      | Conecta a um servidor FTP.  |
| `user <nome>`   | Define o usuário.           |
| `pass <senha>`  | Insere a senha.             |
| `ls`            | Lista arquivos no servidor. |
| `get <arquivo>` | Baixa um arquivo.           |
| `put <arquivo>` | Envia um arquivo.           |
| `bye`           | Encerra a sessão.           |

### Exemplo de conexão FTP

```bash
ftp 192.168.1.100
Connected to 192.168.1.100
Name (192.168.1.100:user): anonymous
Password: (deixe em branco ou use "anonymous")
ftp> ls
ftp> get arquivo.txt
ftp> bye
```

---
# SFTP *(SSH File Transfer Protocol)*

## O que é SFTP?

- Versão segura do FTP, rodando sobre **SSH (porta 22)**.
- **Criptografa** toda a comunicação (dados e autenticação).
- Usa chaves SSH para autenticação avançada.

## Comandos Básicos do SFTP


| **Comando**      | **Descrição**               |
| ---------------- | --------------------------- |
| `sftp user@host` | Conecta a um servidor SFTP. |
| `ls`             | Lista arquivos remotos.     |
| `lls`            | Lista arquivos locais.      |
| `get <arquivo>`  | Baixa um arquivo.           |
| `put <arquivo>`  | Envia um arquivo.           |
| `exit`           | Fecha a conexão.            |

### Exemplo de Conexão SFTP

```bash
sftp user@192.168.1.100
user@192.168.1.100 password: (insira a senha)
sftp> ls
sftp> get /remote/path/file.txt /local/path
sftp> exit
```

---
# Uso em Cibersegurança

## Testes de Penetração em FTP

### a) Enumeração de Serviços FTP

- Verifique se o FTP está ativo com `nmap`:

```bash
nmap -p 21,22 -sV 192.168.1.100
```

### b) Login Anônimo (Vulnerabilidade Comum)

- Muitos servidores FTP permitem login com `anonymous` (sem senha):

```bash
ftp 192.168.1.100
Name: anonymous
Password: (qualquer email ou vazio)
```

### c) Força Bruta em Credenciais FTP

```bash
hydra -L users.txt -P passwords.txt ftp://192.168.1.100
```

### d) Exploração de Vulnerabilidades

- **FTP Bounce Attack:** Abuso de proxy FTP para escanear redes internas.
- **Data Theft:** Arquivos sensíveis (ex.: `config.php`, `.env`) podem estar acessíveis.

## Testes de Penetração em SFTP

- **Força Bruta com `hydra`** (se permitir autenticação por senha):

```bash
hydra -L users.txt -P passwords.txt sftp://192.168.1.100 -s 22
```

- **Exploração de Chaves SSH Fracas:**
	- Se o SFTP permitir autenticação por chave pública, teste chaves conhecidas.

---
# Vulnerabilidades Comuns

## FTP

| **Vulnerabilidade**   | **Risco**                                                      |
| --------------------- | -------------------------------------------------------------- |
| Login Anônimo         | Acesso não autorizado a arquivos.                              |
| Senhas em Texto Claro | Sniffing de credenciais (use Wireshark para capturar tráfego). |
| FTP Bounce            | Ataques indiretos contra outras redes.                         |

## SFTP

| **Vulnerabilidades**     | **Risco**                                                 |
| ------------------------ | --------------------------------------------------------- |
| Senhas Fracas            | Ataques de força bruta.                                   |
| Chaves SSH Comprometidas | Uso de chaves vazadas (ex.: chaves padrão de appliances). |

---
# Ferramentas para Pentesting FTP/SFTP

| **Ferramentas** | **Uso**                                                          |
| --------------- | ---------------------------------------------------------------- |
| Nmap            | Varredura de portas e banners (`nmap -p 21 --script=ftp-*`)      |
| Hydra           | Força bruta em logins FTP/SFTP.                                  |
| Metasploit      | Módulos para exploração (ex.: `auxiliary/scanner/ftp/anonymous`) |
| Wireshark       | Captura de tráfego FTP não criptografado.                        |
| BruteSpray      | Automatiza ataques baseados em credenciais.                      |

---
# Mitigação de Riscos

## Para FTP:

- **Desative o FTP** (use SFTP ou FTPS).
- **Bloquei login anônimo** (configure `/etc/vsftpd.conf`):

```text
anonymous_enable=NO
```

- **Use firewalls** para restringir acesso (`iptables -A INPUT -p tcp --dport 21 -j DROP`)

## Para SFTP:

- **Desative autenticação por senha** (use apenas chaves SSH).
- **Limite usuários** com acesso SFTP:

```bash
Match Group sftpusers
	ChrootDirectory /home/%u
	ForceCommand internal-sftp	
```

---
# Exemplo de Exploração em um Pentest

## Cenário: Servidor FTP com Login Anônimo

1. **Descubra o serviço:**

```bash
nmap -p 21 192.168.1.100
```

2. **Conect-se como `anonymous`**

```bash
ftp 192.168.1.100
```

3. **Liste arquivos sensíveis:**

```bash
ls -la
get secret.txt
```

4. **Explore diretórios:**

```bash
cd /var/www/html
```

---
# Conclusão

- **FTP** é útil, mas **inseguro** (evite em ambientes críticos).
- **SFTP** é a alternativa recomendada (criptografia via SSH).
- **Pentesters** devem verificar:
    - Logins anônimos.
    - Credenciais padrão.
    - Arquivos expostos.

>[!warning] Atenção:
>**Use sempre SFTP/FTPS em produção e desative FTP não criptografado!**

---
# Referências:

- [RFC 959 - FTP](https://tools.ietf.org/html/rfc959)
- [OWASP FTP Security](https://owasp.org/www-community/vulnerabilities/FTP_Security)