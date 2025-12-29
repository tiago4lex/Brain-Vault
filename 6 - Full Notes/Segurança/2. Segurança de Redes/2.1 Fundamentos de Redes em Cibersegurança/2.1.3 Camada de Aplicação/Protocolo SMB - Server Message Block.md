2025-12-29 13:30

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[SMB]]

----
# Introdução

O **SMB (Server Message Block)** é um protocolo de rede utilizado para **compartilhamento de arquivos, pastas, impressoras e outros recursos** em redes locais. Ele é amplamente utilizado em ambientes **Windows**, sendo um dos pilares do funcionamento de **redes corporativas e domínios Active Directory**.

Do ponto de vista da cibersegurança, o SMB é um **alvo crítico**, pois fornece acesso direto a recursos internos e já foi explorado em **ataques de grande impacto global**, como o WannaCry.

![[Pasted image 20251229133212.png]]

---
# Em qual camada o SMB atua?

- **Modelo OSI:** Camada 7 – Aplicação
- **Modelo TCP/IP:** Camada de Aplicação

Portas padrão:

- **445/TCP** – SMB direto sobre TCP (principal)
- **139/TCP** – SMB sobre NetBIOS (legado)

---
# Para que serve o SMB?

O SMB é usado para:

- compartilhamento de arquivos e pastas;
- acesso remoto a recursos de rede;
- impressão em rede;
- autenticação e autorização em domínios Windows;
- suporte a serviços do Active Directory.

---
# Como SMB funcina?

O SMB segue o modelo **cliente-servidor**.

Fluxo simplificado:

1. Cliente se conecta ao servidor SMB
2. Autenticação do usuário
3. Negociação da versão do protocolo
4. Acesso aos recursos compartilhados
5. Transferência de dados

---
# Versões do protocolo SMB

## 1. SMBv1 (Obsoleto e Inseguro)

- sem criptografia;
- vulnerável a múltiplos ataques;
- explorado pelo WannaCry.

## 2. SMBv2

- melhorias de desempenho;
- redução de overhead;
- suporte a assinaturas.

## 3. SMBv3

- criptografia nativa;
- maior segurança;
- suporte a ambientes modernos.

---
# Autenticação no SMB

O SMB utiliza mecanismos de autenticação do Windows.

## 1. NTLM

- legado;
- vulnerável a relay e brute force.

## 2. Kerberos

- padrão em Active Directory;
- mais seguro;
- depende de sincronização de tempo.

---
# Recursos e Funcionalidades do SMB

- compartilhamento de arquivos;
- permissões NTFS;
- controle de acesso;
- locking de arquivos;
- SMB Signing;
- SMB Encryption.

---
# Principais vulnerabilidades do SMB

## 1. SMBv1 Habilitado

- exploração remota;
- propagação de worms.

## 2. Null Session

- enumeração sem autenticação;
- vazamento de informações.

## 3. NTLM Relay

- reutilização de hashes;
- acesso não autorizado.

## 4. EternalBlue (MS17-010)

Falha crítica explorada por ransomware.

Impacto:

- execução remota de código;
- comprometimento total do sistema.

## 5. Credenciais Fracas

- senhas simples;
- compartilhamentos abertas.

---
# Ataques reais envolvendo SMB

- WannaCry
- NotPetya
- Lateral Movement em redes corporativas
- Ransomware em ambientes Windows

----
# Ferramentas para testes de segurança SMB

### Enumeração

- Nmap (`smb-enum-shares`, `smb-enum-users`)
- enum4linux
- smbclient

### Ataques e Exploração

- Metasploit    
- CrackMapExec
- Impacket
- Responder

### Análise e Monitoramento

- Wireshark    
- Logs do Windows (Event Viewer)

---
# Mitigações e Boas Práticas de Segurança SMB

## 1. Desabilitar SMBv1

Essencial em qualquer ambiente moderno.

## 2. Usar SMBv3 com Criptografia

- proteção de dados em trânsito.

## 3. Forçar Kerberos

- evitar NTLM quando possível.

## 4. Habilitar SMB Signing

- previne ataques de relay.

## 5. Controle de Acesso Rigoroso

- permissões mínimas;
- revisar compartilhamentos.

## 6. Segmentação de Rede

- limitar acesso lateral.

---
# SMB em Active Directory

O SMB é fortemente integrado ao AD:

- compartilhamentos SYSVOL e NETLOGON;
- scripts de login;
- políticas de grupo.

Falhas no SMB podem comprometer todo o domínio.

---
# SMB vs NFS

| **Características** | **SMB**       | **NFS**          |
| ------------------- | ------------- | ---------------- |
| Sistema             | Windows       | Linux/Unix       |
| Autenticação        | NTLM/Kerberos | UID/GID/Kerberos |
| Criptografia        | SMBv3         | NFSv4            |

---
# Importância do SMB para Cibersegurança

Dominar o SMB permite:

- realizar pentests internos;
- detectar movimentação lateral;
- proteger ambientes Windows;
- responder a incidentes;
- auditar Active Directory.

---
# Conclusão

O protocolo SMB é essencial para redes corporativas, mas também representa um **dos maiores vetores de ataque interno** quando mal configurado.

Versões antigas, autenticação fraca e permissões excessivas tornam o SMB um alvo prioritário para ransomware e movimentação lateral.

Para profissionais de cibersegurança, compreender profundamente o SMB é fundamental para atuar em **Blue Team, Red Team e segurança de Active Directory**.