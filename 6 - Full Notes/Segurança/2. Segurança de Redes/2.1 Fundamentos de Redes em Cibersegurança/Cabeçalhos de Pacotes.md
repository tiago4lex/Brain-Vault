2025-12-03 19:24

Status: #segurança #developed 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

Os cabeçalhos de pacotes são componentes fundamentais na comunicação de redes, funcionando como "etiquetas" que contêm informações essenciais para o roteamento, entrega e processamento de dados. Em cibersegurança, a análise e manipulação desses cabeçalhos são cruciais para detecção de ataques, investigação forense e implementação de defesas.

---
# Fundamentos de Pacotes de Rede

## 1. Modelo OSI e TCP/IP

- **Modelo OSI (7 camadas)**: Cada camada adiciona seu próprio cabeçalho.
- **Modelo TCP/IP (4 camadas):** Abstração prática do modelo OSI.
- **Encapsulamento:** Processo de adicionar cabeçalhos em cada camada.

## 2. Estrutura Básica de um Pacote

```
[Cabeçalho Camada 2] + [Cabeçalho Camada 3] + [Cabeçalho Camada 4] + [Dados] + [Trailer]
```

---
# Tipos de Cabeçalhos por Camada

## 1. Camada de Enlace (L2) - Cabeçalho Ethernet

**Estrutura (14 bytes):**

```
| Destino MAC (6B) | Origem MAC (6B) | Tipo (2B) |
```

![[unnamed.gif]]

- **Função:** Comunicação entre dispositivos na mesma rede física.
- **Vulnerabilidades:**
	- ARP Spoofing/Poisoning
	- MAC Flooding
	- VLAN Hopping

## 2. Camada de Rede (L3) - Cabeçalho IP

**IPv4 (20-60 bytes):**

![[cabeçalho ipv4.png]]

**Campos críticos:**

- **TTL *(Time to Live)*:** Prevenção de loops.
- **Protocolo:** Identifica próximo protocolo (TCP=6, UDP=17, ICMP=1).
- **Flags:** Controle de fragmentação.

**IPv6 (40 bytes fixos):**

- **Remoção de checksum** (delegado a camadas superiores).
- Endereços de 128 bits.
- Fluxo simplificado.

**Vulnerabilidades L3:**

- IP Spoofing.
- Teardrop Attack (fragmentação maliciosa).
- Ping of Death.
- Smurf Attack.

## 3. Camada de Transporte (L4)

**Cabeçalho TCP (20-60 bytes):**

![[red_compt_a13_f04_a.jpg]]

**Flags TCP( (controle de conexão):**

- **SYN:** Sincronização (início conexão).
- **ACK:** Confirmação.
- **FIN:** Finalização.
- **RST:** Reset.
- **PHS**: Push (envio imediato).
- **URG:** Urgente.

**Vulnerabilidades TCP:**

- **SYN Flood** (ataque DDoS).
- **TCP Sequence Prediction**.
- **TCP Hijacking**.
- **Christmas Tree Attack** (flags todas ativas).

**Cabeçalho UDP (8 bytes):**

![[images.png]]

**Vulnerabilidades:**

- UDP Flood
- DNS Amplification

## 4. Outros Cabeçalhos Importantes

**ICMP (Internet Control Message Protocol)**:

- Usado para diagnóstico e erro.
- **Tipos comuns:** Echo Request/Replay (ping), Destination Unreachable
- **Ataques:** Ping Flood, ICMP Redirect Attack

**ARP (Address Resolution Protocol)**:

- Mapeamento IP → MAC.
- **Ataques:** ARP Poisoning, MITM.

---
# Análise Forense de Cabeçalhos

## 1. Detecção de Anomalias

**Indicadores de comprometimento:**

- TTL inconsistente.
- Portas não padrão em flags SYN.
- Padrões de fragmentação anormais.
- Flags TCP incomuns (SYN+FIN simultâneo).

## 2. Técnicas de Ofuscação

- **Fragmentação:** Evadir IDS/IPS
- **TTL Manipulation:** Mascarar origem.
- **Port Hopping:** Comunicação C2.

---
# Casos de Estudos Reais

## 1. Mirai Botnet (2026)

- **Técnica:** TCP SYN Flood com Spoofing.
- **Alvo:** DNS provider Dyn.
- **Impacto**: Queda de serviços como Twitter, Netflix.

![[01-searching-mirai.png]]

## 2. Stuxnet (2010)

![[origin.jpg]]

- **Características:** Uso de múltiplas vulnerabilidades L3/L4.
- **Propagação:** Fragmentação IP para evadir firewalls.

## 3. Equifax Breach (2017)

![[equifaxexploitedgaosept2018.jpg]]

- **Falha**: CVE-2017-5638 (Apache Struts)
- **Detecção**: Análise de padrões de cabeçalhos HTTP anormais

---
# Ferramentas de Análise

## 1. Captura e Inspeção

- **Wireshark/Tshark:** Análise detalhada.
- **tcpdump:** Linha de comando.
- **Nmap:** Varredura e fingerprinting.

## 2. Manipulação e Testes

- **Scapy (Python):** Criação/manipulação de pacotes.
- **hping3:** Testes de segurança.
- **Netcat:** Conexões brutas.

## 3. Exemplo com Scapy

```python
from scapy.all import *

# Criar pacote TCP SYN personalizado
ip = IP(src="192.168.1.100", dst="10.0.0.1")
tcp = TCP(sport=54321, dport=80, flags="S", seq=1000)
packet = ip/tcp
send(packet)
```

---
# Técnicas de Defesa

## 1 Hardening de Cabeçalhos

- **Filtragem RFC 2827**: Anti-spoofing
- **TCP Stack Hardening**: SYN cookies
- **Rate Limiting**: Proteção contra flooding

## 2 Monitoramento

- **IDS/IPS**: Snort, Suricata
- **SIEM**: Correlação de eventos
- **NetFlow**: Análise de tráfego

## 3. Regras de Firewall (Exemplo)

```bash
# Bloquear pacotes com flags inválidas
iptables -A INPUT -p tcp --tcp-flags ALL FIN,PSH,URG -j DROP

# Prevenir SMURF attack
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

---
# Tópicos Avançados

## Evasão de IDS/IPS

- **Fragmentação Overlap**: Pacotes sobrepostos
- **TCP Segmentation**: MSS manipulation
- **Encryption**: TLS/SSL ofusca conteúdo

## Protocolos Emergentes

- **QUIC**: UDP-based com segurança integrada
- **HTTP/3**: Impacto na análise de tráfego

## IPv6 Security Considerations

- **Extension Headers**: Novos vetores de ataque
- **Neighbor Discovery**: Substitui ARP

---
# Laboratório Prático Sugerido

## Topologia

```
[Atacante] --- [Switch] --- [Vítima]
                   |
               [IDS/IPS]
```

## Exercícios

1. Capturar handshake TCP completo
2. Identificar scan SYN em pcap
3. Implementar detector de ARP spoofing
4. Analisar ataques DDoS em arquivo de captura

## Recursos de Treinamento

- **PCAPs públicos:** Malware Traffic Analysis.
- **CTFs:** HackTheBox, TryHackMe.
- **Cursos:** SANS SEC503, Network+

---
# Conclusão

A compreensão profunda dos cabeçalhos de pacotes é fundamental para profissionais de cibersegurança. Eles representam tanto vetores de ataque quanto oportunidades de detecção. A evolução contínua dos protocolos exige aprendizado permanente, e a prática com ferramentas de análise é essencial para desenvolver habilidades efetivas.

---
# Referências

1. RFC 791 - Internet Protocol
2. RFC 793 - Transmission Control Protocol
3. Stevens, W. R. - TCP/IP Illustrated
4. Sanders, C. - Practical Packet Analysis
5. MITRE ATT&CK Framework