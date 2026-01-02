2026-01-02 12:45

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[VPN]]

----
# Introdução

Uma **VPN (Virtual Private Network)** é uma tecnologia que cria um **túnel criptografado** entre dois pontos de uma rede, normalmente entre um cliente e um servidor VPN. Esse túnel garante **confidencialidade, integridade e autenticidade** dos dados transmitidos, mesmo quando a comunicação ocorre por redes inseguras como a internet.

Fluxo simplificado:

```text
Cliente → Túnel VPN criptografado → Servidor VPN → Internet
```

![[Pasted image 20260102124807.png]]

---
# Para que uma VPN é utilizada

VPNs são usadas para:

- Proteger comunicações em redes públicas (Wi-Fi)
- Acesso remote seguro a redes corporativas
- Interligar filiais (site-to-site)
- Ocultar IP real do usuário
- Bypass de restrições geográficas
- Suporte a atividades de segurança ofensiva e defensiva

---
# Como uma VPN funciona?

1. O cliente inicia uma conexão com o servidor VPN.
2. Ocorre autenticação (usuário/senha, certificado ou chave).
3. É negociado um protocolo criptográfico.
4. Um túnel criptografado é estabelecido.
5. Todo o tráfego passa a ser encapsulado e protegido.

Tecnologias usadas:

- Criptorgrafia
- Encapsulamento
- Autenticação
- Integridade de dados

---
# Conceitos Importantes

## 1. Tunelamento

Encapsulamento de pacotes dentro de outros pacotes para atravessar redes públicas.

## 2. Criptografia

Protege os dados contra interceptação (AES, ChaCha20).

## 3. Autenticação

Garante que apenas usuários autorizados se conectem.

---
# Tipos de VPN

## 1. VPN Client-to-Site (Remote Access)

- Usuário remoto se conecta à rede corporativa
- Muito usada em home office

**Exemplos:**

- OpenVPN
- AnyConnect (Cisco)

![[Pasted image 20260102125326.png]]

## 2. VPN Site-to-Site

- Conecta duas redes distintas
- Muito usada entre filiais

![[Pasted image 20260102125413.png]]

## 3. VPN Pessoal / Comercial

- Focada em privacidade
- Oculta IP real

Exemplos:

- NordVPN
- ProtonVPN

![[Pasted image 20260102125448.png]]

---
# Protocolos de VPN

## 1. OpenVPN

- Open source
- Usa TLS/SSL
- Muito seguro e flexível

![[Pasted image 20260102125600.png]]

## 2. IPsec

- Muito usado em ambientes corporativos    
- Opera na camada de rede

Modos:

- Tunnel
- Transport

![[Pasted image 20260102125637.png]]

## 3. WireGuard

- Moderno e rápido
- Código enxuto
- Criptografia moderna

![[Pasted image 20260102125652.png]]

## 4. L2TP/IPsec

- Combinação de protocolos
- Mais antigo

## 5. PPTP (Obsoleto)

- Inseguro
- Não recomendado

![[Pasted image 20260102125856.png]]

---
# VPN e Camadas OSI

- IPsec → Camada 3
- OpenVPN → Camada 4/7
- WireGuard → Camada 3

---
# Exemplos Práticos de Uso

## 1. Conectar a uma VPN OpenVPN

```bash
openvpn --config cliente.ovpn
```

## 2. Verificar IP após VPN

```bash
curl ifconfig.me
```

## 3. WireGuard (Cliente)

```bash
wg-quick up wg0
```

---
# VPN em Cibersegurança

## 1. Uso Defensivo (Blue Team)

- Acesso remoto seguro
- Proteção contra sniffing
- Segmentação de rede

## 2. Uso Ofensivo (Red Team)

- Ocultar origem
- Pivoting
- Conexão segura a C2

---
# Vulnerabilidades e Riscos de VPN

- Credenciais fracas
- Certificados vazados
- Falhas de configuração
- Exploração de serviços expostos

Exemplos reais:

- CVEs em Pulse Secure
- Fortinet VPN exploits

---
# Ferramentas Relacionadas

- OpenVPN
- StrongSwan
- WireGuard
- SoftEther

---
# VPN vs Proxy vs Tor

| **Tecnologia** | **Função Principal**       |
| -------------- | -------------------------- |
| VPN            | Túnel criptografado        |
| Proxy          | Intermediário de aplicação |
| Tor            | Anonimato em múltiplos nós |

---
# Boas Práticas de Segurança

- MFA para VPN
- Certificados fortes
- Atualizações constantes
- Restringir acesso por ACL

---
# Conclusão

VPNs são fundamentais para segurança moderna, oferecendo proteção de dados, acesso remoto seguro e suporte tanto para **infraestrutura corporativa** quanto para **operações de cibersegurança ofensivas e defensivas**.