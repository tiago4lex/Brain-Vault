2025-12-01 20:14

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

O **Modelo OSI *(Open Systems Interconnection)*** é uma estrutura conceitual criada pelo ISO para padronizar a comunicação entre sistemas computacionais. Ele divide o processo de comunicação em **7 camadas**, cada uma com funções específicas e independentes.

Compreender o modelo OSI é essencial para cibersegurança, pois permite **identificar, classificar e mitigar vulnerabilidades** deforma estruturada.

![[osi_model_7_layers.png]]

---
# As 7 Camadas do Modelo OSI e Suas Vulnerabilidades

## Camada 1 — Física

**Função:** responsável pela transmissão de sinais elétricos, ópticos ou radiofrequência através de cabos, fibras, ondas etc.

**Dispositivos:** Cabos de rede, hubs, repetidores, placas NIC, antenas.

**Protocolos/padrões:** Ethernet físico, IEEE 802.11 físico, DSL, SONET.

**Vulnerabilidades típicas:**
- **Interferência eletromagnética** (EMI);
- **Ataques de interrupção física** *(cut-wire attacks)* — corte ou sabotagem de cabos;
- **Jamming Wireless** — interferência proposital em redes Wi-Fi;
- **Instalação de hardware malicioso**, como taps de rede.

**Mitigações:** blindagem física, controle de acesso, monitoramento ambiental.

## Camada 2 — Enlace de Dados

**Função:** garante entrega de quadros (frames) dentro de uma mesma rede local; controla erros e acesso ao meio.

**Protocolos:** Ethernet, ARP, VLAN (802.1Q, STP.

**Vulnerabilidades típicas:**
- **ARP Spoofing/Poisoning** — manipulação do ARP para interceptação ou redirecionamento;
- **MAC Flooding** — saturação de tabelas CAM de switches, causando comportamento de hub;
- **VLAN Hopping** — invasão de VLANs isoladas;
- **BPDU Attacks** — exploração de protocolos de spanning tree.

**Mitigação:** inspeção dinâmica ARP, port security, segmentação, 802.1X.

## Camada 3 — Rede

**Função:** responsável pelo roteamento e endereçamento IP.

**Protocolos:** IPv4, IPv6, ICMP, OSPF, BGP.

**Vulnerabilidades típicas:**
- **IP Spoofing** — falsificação de endereço IP;
- **ICMP Attacks** — ping flood, ICMP redirect;
- **DoS/DDoS baseados em rede** — SYN Flood, Smurf Attack;
- **BGP Hijacking** — desvio de tráfego em escala global.

**Mitigações:** filtros ACL, firewalls, sistemas anti-DDoS, RPKI para BGP.

## Camada 4 — Transporte

**Função:** garante comunicação fim a fim, controle de fluxo, segmentação e confiabilidade.

**Protocolos:** TCP, UDP.

**Vulnerabilidades típicas:**
- **TCP SYN Flood** — esgotamento de tabela de conexões;
- **UDP Flood** — tráfego UDP massivo;
- **Manipulação de portas e conexões** — port scanning, session hijacking.

**Mitigações:** rate limiting, firewalls stateful, IDS/IPS.

## Camada 5 — Sessão

**Função:** estabelece, mantém e encerra sessões de comunicação.

**Protocolos:** RPC, NetBIOS, PPTP, SIP.

**Vulnerabilidades típicas:*
- **Session Hijacking** — sequestro de sessão via roubo de token;
- **Ataques a gerenciamento de sessão** em aplicações que fazem controle inadequado.

**Mitigações:** tokens seguros, autenticação forte, gerenciamento criptografado de sessão.

## Camada 6 — Apresentação

**Função:** tradução de dados, compressão e criptografia.

**Protocolos / tecnologias:** TLS/SSL, ASCII, JPEG, MP3.

**Vulnerabilidades típicas:**
- **Quebra de criptografia fraca** (SSL antigo, DES, RC4);
- **Ataques de downgrade** (forçar uso de protocolos inseguros);
- **Exploração de formatos de arquivo** — parsing de PDFs, imagens, mídia.

**Mitigações:** cifragem moderna, certificados atualizados, validação de entrada.

## Camada 7 — Aplicação

**Função:** é onde o usuário interage e onde serviços de rede operam.

**Protocolos:** HTTP/S, DNS, FTP, SMTP, APIs REST.

**Vulnerabilidades típicas:**

- **SQL Injection**;
- **XSS**;
- **Command Injection**;
- **LFI/RFI**;
- **CSRF**;
- **Quebra de autenticação**;
- **Configurações inseguras em servidores web**.

**Mitigações:** WAF, validação de entrada, autenticação forte, práticas OWASP.

---
# Relação OSI x Segurança: Por que estudar por camadas?

Entender onde cada vulnerabilidade se encaixa ajuda a:

- Criar defesas mais eficientes;
- Identificar pontos fracos rapidamente;
- Realizar pentests estruturados;
- Implementar defesa em profundidade *(Defense in Depth)*;
- Dividir responsabilidades entre equipes de segurança.

---
# Comparação OSI x TCP/IP para Cibersegurança

Embora o modelo TCP/IP seja o mais usado na prática, o OSI ajuda a visualizar melhor vulnerabilidades por divisão conceitual.


| **OSI** | **TCP/IP**    | **Segurança**                 | **Exemplos**        |
| ------- | ------------- | ----------------------------- | ------------------- |
| 7, 6, 5 | Aplicação     | Proteção de protocolos e APIs | OSWAP, TLS          |
| 4       | Transporte    | Hardening de conexões         | firewalls stateful  |
| 3       | Internet      | Proteção IP e roteamento      | ACL, anti-DDoS      |
| 2, 1    | Acesso à rede | Segurança física e lógica     | MAC Filtering, VLAN |

---
# Ataques Comuns e Suas Camadas

- **MITM (Man-in-the-Middle):** camadas 2, 3 e 7
- **DoS e DDoS:** camadas 3 e 4
- **Brute force:** camada 7
- **DNS Spoofing:** camada 7
- **Eavesdropping:** camadas 1 e 2
- **Packet Injection:** camada 3

---
# Boas Práticas de Segurança em Todas as Camadas

- **Camadas 1–2:** segurança física, segmentação, VLANs, Wi-Fi seguro
- **Camada 3:** firewalls, filtragem, roteadores configurados corretamente
- **Camada 4:** proteção de portas e conexões
- **Camada 5:** gerenciamento seguro de sessões
- **Camada 6:** criptografia forte e atualizada
- **Camada 7:** hardening de aplicações, OWASP Top 10

---
# Conclusão

O modelo OSI é uma ferramenta poderosa na cibersegurança. Ele permite analisar redes e aplicações de forma sistemática, identificando vulnerabilidades em todas as etapas do fluxo de comunicação. Dominar esse modelo significa entender melhor onde ataques surgem e como mitigá-los com precisão.