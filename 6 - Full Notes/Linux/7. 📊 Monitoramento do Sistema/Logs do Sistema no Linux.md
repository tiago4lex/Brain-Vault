2025-08-20 11:37

Status: #developed #Linux 

Tags: [[Linux]] | [[logs]]

----
# Introdução

No Linux, **logs do sistema** são arquivos de texto que registram eventos importantes, como inicialização, autenticação, erros, tentativas de login, falhas de hardware, entre outros.

Esses registros são fundamentais para **administradores de sistemas** e **profissionais de segurança** já que permitem monitorar o sistema, auditar atividades e diagnosticar problemas.

---
# Onde os logs ficam armazenados?

Normalmente, os logs ficam em:

```bash
/var/log
```

Dentro dessa pasta, existem vários arquivos, cada um com uma função específica.

![[Pasted image 20250820114150.png]]

---
# Principais Arquivos de Log

## 1. `syslog`

- Contém **mensagens gerais do sistema** e de serviços em execução.
- Inclui eventos do kernel, serviços de rede, inicialização e muito mais.
- É um dos logs mais consultados para diagnosticar problemas.

**Exemplo:**

```bash
tail -f /var/log/syslog
```

## 2. `auth.log`

- Registra tudo relacionado a **autenticação e segurança:**
	- Logins bem-sucedidos e falhos.
	- Uso do comando `sudo`.
	- Tentativas de acesso SSH.
- Muito usado em auditoria e investigação de **tentativas de invasão**.

**Exemplo:**

```bash
grep "Failed password" /var/log/auth.log
```

## 3. `kern.log`

- Registra mensagens do **kernel do Linux**.
- Útil para identificar problemas de hardware, drivers ou módulos.

**Exemplo:**

```bash
dmesg | less
```

## 4. `dmesg`

- Arquivo relacionado ao **buffer de mensagens do kernel**.
- Mostra eventos desde a inicialização do sistema, como detecção de hardware.
- Muitas vezes é usado para **debug de hardware**.

## 5. `boot.log`

- Registra mensagens exibidas durante o processo de **boot**.
- Útil para analisar problemas de inicialização.

## 6. `failog`

- Contém registros de **tentativas de login falhas**.
- Acessível com o comando:

```bash
faillog
```

## 7. `lastlog`

- Mostra o **último login** de cada usuário.
- Acessível com o comando:

```bash
lastlog
```

## 8. `wtmp`

- Armazena histórico de **logins** e **logouts** de usuários.
- Consultado com o comando:

```bash
last
```

## 9. `btmp`

- Guarda registros de **tentativas de login inválidas**.
- Consultado com:

```bash
lastb
```

## 10. `apt`

- Diretório com logs relacionados ao **gerenciamento de pacotes APT:**
	- `/var/log/apt/history.log` → histórico de pacotes instalados/removidos.
	- `/var/log/apt/term.log` → saída detalhada dos comandos `apt`.

---
# Ferramentas para visualizar logs

- `tail -f arquivo.log` → acompanha o log em tempo real.
- `less arquivo.log` → navega dentro do log.
- `grep "palavra" arquivo.log` → filtra por palavra chave.
- `journalctl` → exibe logs do `systemd` (sistemas mais recentes).

**Exemplo:**

```bash
journalctl -xe
```

Mostra logs recentes com detalhes de erros.

---
