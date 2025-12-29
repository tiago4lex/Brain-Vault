2025-07-27 06:31

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Telnet]] | [[Protocolos]]

----
# Introdução

**Telnet** *(Telecommunication Network)* é um protocolo de rede antigo utilizado para comunicação bidirecional baseada em texto entre dispositivos em uma rede. Ele opera na **camada de aplicação** do modelo OSI e usa a porta **TCP 23** por padrão.

## Histórico

- Desenvolvido em **1969** como parte do projeto ARPANET.
- Foi amplamente substituído pelo **SSH** (Secure Shell) devido a questões de segurança.

---
# Para que Serve o Telnet?

O Telnet é usado para:

- **Acesso remoto** a servidores e dispositivos de rede (roteadores, switches).
- **Depuração de serviços** (ex.: verificar se uma porta está respondendo).
- **Automação de tarefas** em sistemas legados.
- **Testes básicos de conectividade** em rede.

>[!warning] Atenção:
>- Telnet **não é criptografado** (todas as comunicações são em texto claro).
>- **Não recomendado** para uso em ambientes de produção devido a riscos de segurança.

---
# Como o Telnet Funciona?

## Arquitetura Cliente-Servidor

1. **Cliente Telnet →** Inicia a conexão (ex.: `telnet 192.168.1.1`).
2. **Servidor Telnet →** Escuta na porta 23 e responde à conexão.
3. **Sessão Interativa →** Permite enviar comandos como se estivesse localmente.

## Formato das Mensagens

- Dados são transmitidos em **texto ASCII**.
- Comandos Telnet são precedidos por um **caractere de controlo (IAC - *Interpret as Command*)**.

---
# Como Estabelecer um Conexão Telnet?

## No Linux

```bash
telnet <IP> <porta>
```

Exemplo (conectar a um servidor na porta 23)

```bash
telnet 192.168.1.100.23
```

## No Windows

1. **Ative o cliente Telnet** (se não estiver instalado):

```powershell
dims /online /Enable-Feature /FeatureName:TelnetClient
```

2. Conecte-se:

```cmd
telnet 192.168.1.100 23
```

## Testando uma Porta Específica

Verificar se a porta 80 está aberta em um servidor web:

```bash
telnet example.com 80
```

Se a conexão for bem-sucedida, digite:

```http
GET / HTTP/1.1
Host: example.com
```

---
# Uso do Telnet em Cibersegurança

Apesar de inseguro, o Telnet ainda é relevante para:

## 1. Testes de Penetração (Pentesting)

- **Enumeração de serviços:** Verificar banners de servidores (ex.: FTP, SMTP).

```bash
telnet 192.168.1.100 25
```

Saída:

```text
220 mail.example.com ESMTP Postfix
```

- **Exploração de credenciais fracas:** Ataques de força bruta em logins Telnet.

## 2. Red Team / Simulação de Ataques

- **Sniffing de credenciais:** Como o Telnet não é criptografado, um invasor pode capturar logins com ferramentas como **Wireshark**
- **Ataques MITM *(Man-in-the-Middle)*:** Interceptação de sessões Telnet em redes não seguras.

## 3. Análise Forense

- Investigar logs de servidores legados que ainda usam Telnet.

---
# Riscos de Segurança do Telnet

| **Vulnerabilidades**   | **Impacto**                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| Dados em texto claro   | Credencias e comandos podem ser capturados com sniffers (ex.: Wireshark). |
| Sem autenticação forte | Vulnerável a ataques de força bruta.                                      |
| Banner disclosure      | Expõe versões de software, facilitando exploits.                          |

---
# Alternativas Seguras ao Telnet


| **Protocolo** | **Vantagens**                                                |
| ------------- | ------------------------------------------------------------ |
| SSH           | Criptografia AES, autenticação por chaves, tunneling seguro. |
| RDP           | Ideal para acesso gráfico remoto (Windows).                  |
| VPN           | Cria um túnel criptografado para acesso a redes internas.    |

---
# Exemplo de Ataque com Telnet (Simulado)

## Cenário: Capturando Credenciais Telnet

1. **Inicie um servidor Telnet vulnerável** (ex.: em uma VM):

```bash
sudo apt install telnetd
```

2. **Capture o tráfego com Wireshark:**
	- Filtre por `tcp.port == 23`.

3. **Conecte-se ao servidor:**

```bash
telnet 192.168.1.100
```

4. **Observe no Wireshark:**
	- As credenciais digitadas aparecem em texto claro.

---
# Mitigação de Riscos

- **Desative o Telnet** em sistemas modernos:

```bash
sudo systemctl disable telnet.scoket
```

- **Use SSH** para acesso remoto:

```bash
ssh usuario@192.168.1.100
```

- **Implemente firewalls** para bloquear a porta 23:

```bash
sudo ufw deny 23
```

---
# Conclusão

- **O que é?** Protocolo antigo para acesso remoto em texto claro.
- **Para que serve?** Acesso a dispositivos legados e testes básicos.
- **Riscos:** Inseguro (sem criptografia).
- **Recomendação:** Substitua por **SSH** ou **VPN**.

> 🔐 **Use Telnet apenas em ambientes controlados e nunca em redes públicas!**

---
# Referências:

- [RFC 854 - Especificação do Telnet](https://tools.ietf.org/html/rfc854)
- [OWASP - Riscos de Protocolos Inseguros](https://owasp.org/)