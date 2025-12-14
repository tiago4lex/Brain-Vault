2025-12-01 20:42

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[TCP IP]]

----
# Introdução

O **Modelo TCP/IP (Transmission Control Protocol / Internet Protocol)** é o conjunto de protocolos que sustenta toda a comunicação da internet. Ele é amplamente utilizado na prática, ao contrário do modelo OSI, que é mais conceitual.

Criado pelo Departamento de Defesa dos EUA, o modelo TCP/IP foi projetado com foco em **interoperabilidade**, **robustez** e **resiliência**, permitindo que dispositivos em redes diferentes se comuniquem de forma eficiente.

Na cibersegurança, entender o modelo TCP/IP é fundamental para:

- identificar vetores de ataque;
    
- configurar firewalls, roteadores e IDS/IPS;
    
- analisar tráfego de rede (packet analysis);
    
- planejar defesa em múltiplas camadas.

![[image-304-1024x711.png]]

---
# As 4 Camadas do Modelo TCP/IP

O modelo TCP/IP é composto por **4 camadas principais**, cada uma corresponde a um conjunto de funções da rede.

## Visão Geral

| **Camada TCP/IP** | **Função Principal**            | **Protocolos Importantes** |
| ----------------- | ------------------------------- | -------------------------- |
| 4. Aplicação      | Interação do usuário e serviços | HTTP, DNS, SMTP, FTP, SSH  |
| 3. Transporte     | Comunicação fim a fim           | TCP, UDP                   |
| 2. Internet       | Roteamento IP e endereçamento   | IP, ICMP, ARP, OSPF, BGP   |
| 1. Acesso à Rede  | Enlace + Física                 | Ethernet, Wi-Fi, PPP       |

---
# Camadas de Acesso à Rede *(Network Access Layer)*

**Equivalente às camadas Física e Enlace do OSI.**

### Função
- Transmite quadros pela rede física
- Define como dispositivos acessam o meio
- Realiza detecção básica de erros

### Protocolos
- **Ethernet (802.3)**
- **Wi-Fi (802.11)**
- **PPP, Frame Relay, MPLS**
- **ARP** (Address Resolution Protocol)

### Vulnerabilidades Comuns
- **ARP Spoofing / Poisoning**
- **MAC Flooding**
- **VLAN Hopping**
- **Jamming (Wi-Fi)**
- **Sniffing de tráfego sem criptografia**
- **Ataques físicos ao cabeamento**

### Mitigações
- Habilitar **Port Security** em switches
- Usar **WPA3** em redes Wi-Fi
- Monitorar ARP (DHCP Snooping, Dynamic ARP Inspection)
- Segmentar redes com VLANs
- Controle de acesso físico

---
# Camada da Internet *(Internet Layer)*

**Equivalente à camada de Rede do OSI.**

### Função
- Roteamento de pacotes entre redes
- Endereçamento IP
- Fragmentação e reassembly

### Protocolos
- **IP (IPv4/IPv6)**
- **ICMP** — diagnóstico de rede
- **ARP** — resolução de endereços
- **Roteamento:** OSPF, BGP, EIGRP

### Vulnerabilidades Comuns
- **IP Spoofing**
- **ICMP Attacks** (Smurf Attack, Ping Flood)
- **DoS / DDoS volumétrico**
- **BGP Hijacking** (manipulação de rotas globais)
- **Roteamento inseguro em redes internas**

### Mitigações
- Filtros em firewalls e roteadores (ACLs)
- Anti-DDoS
- Monitoramento de rotas (RPKI no BGP)
- Bloqueio de ICMP desnecessário

---
# Camada de Transporte (Transport Layer)

**Equivalente à camada 4 do OSI.**

### Função
- Comunicação fim a fim entre processos
- Controle de fluxo e confiabilidade
- Multiplexação de portas

### Protocolos
- **TCP (Transmission Control Protocol)**
- **UDP (User Datagram Protocol)**
- **TLS/SSL** (embora também seja visto na camada de aplicação)

### Vulnerabilidades Comuns

- **Port Scanning** (Nmap)
- **TCP SYN Flood**
- **UDP Flood**
- **Session Hijacking**
- **Ataques de força bruta a portas de serviços**

### Mitigações

- Configuração de firewalls stateful
- Rate Limiting
- Utilização de IDS/IPS
- TLS para proteger sessões
- Fechar portas desnecessárias

---
# Camada de Aplicação (Application Layer)

**Equivalente às camadas 5, 6 e 7 do OSI.**

### Função
- Interface para serviços de rede
- Processamento de dados do usuário
- Protocolos de comunicação de alto nível

### Principais Protocolos
- **HTTP/HTTPS** — web
- **DNS** — resolução de nomes
- **FTP / SFTP** — transferência de arquivos
- **SMTP / IMAP** — e-mail
- **SSH** — acesso seguro
- **DHCP** — configuração automática

### Vulnerabilidades Comuns
- **SQL Injection**
- **Cross-Site Scripting (XSS)**
- **Command Injection**
- **CSRF**
- **DNS Spoofing / Cache Poisoning**
- **Brute Force**
- **Quebra de autenticação**
- **Erros de configuração de APIs**

### Mitigações
- Seguir recomendações OWASP
- WAF (Web Application Firewall)
- Autenticação multifator (MFA)
- Validação de entrada
- DNSSEC
- Hardening de servidores

---
# Ataques Classificados pelo Modelo TCP/IP

### Camada de Acesso

- Sniffing
- ARP Poisoning
- Evil Twin (Wi-Fi)

### Camada de Internet

- IP Spoofing
- ICMP Flood
- BGP Hijacking

### Camada de Transporte

- SYN Flood
- UDP Flood
- Port Scanning

### Camada de Aplicação

- SQL Injection
- XSS
- CSRF
- DNS Spoofing

---
# Ferramentas Relacionadas ao Modelo TCP/IP

### Análise de tráfego

- Wireshark    
- Tcpdump

### Testes de intrusão

- Nmap
- Nessus
- Burp Suite

### Defesas

- Firewalls (pfSense, iptables)
- IDS/IPS (Snort, Suricata)

---
# Conclusão

O **modelo TCP/IP é o alicerce da comunicação moderna** e dominá-lo é crucial para atuar em cibersegurança. Entender como cada camada funciona, quais protocolos utiliza e quais vulnerabilidades podem aparecer permite criar defesas robustas e identificar ataques rapidamente.

Combinado ao modelo OSI, o TCP/IP forma a base teórica e prática para análise, defesa e investigação digital.