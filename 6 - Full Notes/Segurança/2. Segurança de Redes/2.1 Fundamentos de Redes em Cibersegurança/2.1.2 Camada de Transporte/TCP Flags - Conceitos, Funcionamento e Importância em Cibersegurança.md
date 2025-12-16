2025-12-16 06:08

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

As **TCP Flags** são campos de controle presentes no cabeçalho do protocolo TCP *(Transmission Control Protocol)*. Elas indicam o **estado da conexão**, controlam o fluxo de dados e permitem gerenciar eventos como abertura, manutenção e encerramento de conexões.

Em cibersegurança, o estudo das flags TCP é essencial para:

- análise de tráfego de rede;
- detecção de ataques e comportamentos anômatos;
- configuração de firewalls e IDS/IPS;
- realização de pentests e varreduras avançadas.

---
# O que são TCP Flags?

TCP Flags são **bits de controle** (0 ou 1) no cabeçalho TCP. Quando uma flag está marcada como 1, ela indica que determinada ação ou estado está ativo naquele pacote.

O cabeçalho TCP possui **9 flgas principais:**

- NS
- CWR
- ECE
- URG
- ACK
- PSH
- RST
- SYN
- FIN

Cada uma possui uma função específica dentro da comunicação TCP.

---
# Visão Geral das TCP Flags


| **Flag** | **Nome**                  | **Função Principal**                  |
| -------- | ------------------------- | ------------------------------------- |
| NS       | Nonce Sum                 | Proteção experimental contra spoofing |
| CWR      | Congestion Window Reduced | Controle de congestionamento          |
| ECE      | ECN Echo                  | Notificação de congestionamento       |
| URG      | Urgent                    | Dados urgentes presentes              |
| ACK      | Acknowledgment            | Confima recebimento                   |
| PSH      | Push                      | Entrega imediata de dados             |
| RST      | Reset                     | Reinicia/encerra conexão abruptamente |
| SYN      | Synchronize               | Inicia conexão TCP                    |
| FIN      | Finish                    | Finaliza conexão TCP                  |

---
# Explicação Detalhada de Cada TCP Flag

## 1. SYN (Synchronize)

**Função:** iniciar uma nova conexão TCP.

- Usada no **Three-Way Handshake**.
- Sincroniza os números de sequência iniciais (ISN).

**Exemplo:**

- Cliente envia pacote com `SYN=1`.

**Relação com ataques:**

- Base para **SYN Flood**.
- Usada em **SYN Scan** (`nmap -sS`).

## 2. ACK (Acknowledgment)

**Função:** confirmar o recebimento de pacotes.

- Presente na maioria dos pacotes após o handshake.
- Garante confiabilidade.

**Exemplo:**

- `ACK=1` confirma recepção de dados.

**Uso em segurança:**

- Identificar conexões válidas.
- Utilizado em **ACK Scan** para testar firewalls.

## 3. FIN (Finish)

**Função:** encerrar uma conexão TCP de forma graciosa.

- Indica que o host não tem mais dados para enviar.
- Conexão entra em estado de finalização.

**Exemplo:**

- Usado ao fechar uma sessão HTTP.

**Ataques relacionados**:

- **FIN Scan** (`nmap -sF`) para bypass de firewalls simples.

## 4. RST (Reset)

**Função:** encerrar uma conexão imediatamente.

- Usado quando ocorre erro ou conexão inválida.
- Não segue encerramento normal.

**Exemplo:**

- Porta fechada responde com RST.

**Riscos de segurança:**

- **TCP Reset Attack** (interrupção de sessões).
- Ataques MITM podem injetar RST falsos.

## 5. PSH (Push)

**Função:** forçar a entrega imediata dos dados ao aplicativo.

- Evita buffering excessivo.
- Muito usado em aplicações interativas (SSH).

**Uso prático:**

- Transmissão de comandos em tempo real.

## 6. URG (Urgent)

**Função:** indica presença de dados urgentes.

- Utiliza o campo **Urgent Pointer**.
- Pouco usado atualmente.

**Riscos:**

- Implementações antigas apresentavam falhas.
- Pode ser explorado em evasão de IDS.

## 7. ECE (ECN Echo)

**Função:** indica que o host detectou congestionamento na rede.

- Parte do mecanismo ECN *(Explicit Congestion Notification)*.
- Ajuda a evitar perda de pacotes.

**Uso:**

- Controle de congestionamento sem descartar pacotes.

## 8. CWR (Congestion Window Reduced)

**Função:** indica que o host reduziu sua janela de congestionamento.

- Resposta ao sinal ECE.
- Mantém estabilidade da rede.

## 9. NS (Nonce Sum)

**Função:** proteção experimental contra ataques de spoofing.

- Pouco implementada.
- Usada em conjunto com ECN.

---
# Combinações comuns de TCP Flags

| **Flags** | **Situação**            |
| --------- | ----------------------- |
| SYN       | Solicitação de conexão  |
| SYN + ACK | Aceitação de conexão    |
| ACK       | Confirmação de dados    |
| FIN + ACK | Encerramento normal     |
| RST       | Encerramento abrupto    |
| PSH + ACK | Envio imediato de dados |

---
# TCP Flags e Varreduras (Scanning)

Ferramentas de pentest exploram flags para mapear portas:

- **SYN Scan (-sS)** – rápido e discreto
- **FIN Scan (-sF)** – evasão de firewall
- **NULL Scan (-sN)** – sem flags
- **XMAS Scan (-sX)** – múltiplas flags ativas
- **ACK Scan (-sA)** – identifica filtros

---
# TCP Flags na Detecção de Ataques

IDS/IPS monitoram padrões suspeitos, como:

- grande volume de SYN sem ACK;
- RST inesperados;
- combinações inválidas de flags;
- pacotes malformados.

Esses sinais indicam possíveis ataques de:

- DoS/DDoS;
- port scanning;
- evasão de segurança.

---
# Ferramentas para Analisar TCP Flags

### Análise de Tráfego

- Wireshark
- Tcpdump

### Pentest

- Nmap
- Hping3
- Scapy

### Filtros Úteis (Wireshark)

- `tcp.flags.syn == 1`
- `tcp.flags.reset == 1`
- `tcp.flags.fin == 1`    
- `tcp.flags == 0x002` (SYN)

---
# Importância das TCP Flags em Cibersegurança

O domínio das TCP Flags permite:

- interpretar corretamente pacotes capturados;
- identificar ataques rapidamente;
- entender como firewalls tomam decisões;
- realizar pentests mais precisos;
- fortalecer políticas de segurança de rede.

---
# Conclusão

As TCP Flags são fundamentais para o funcionamento do protocolo TCP e para a segurança das redes modernas. Elas controlam conexões, permitem confiabilidade e, ao mesmo tempo, podem ser exploradas por atacantes.

Para profissionais de cibersegurança, entender profundamente cada flag, suas combinações e implicações práticas é um passo essencial para atuar em SOC, pentest, redes e resposta a incidentes.