2025-12-16 07:13

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[UDP]]

----
# Introdução

O **UDP (User Datagram Protocol)** é um protocolo da **camada de transporte** do modelo TCP/IP. Diferente do TCP, o UDP é **não orientado à conexão**, ou seja, não estabelece sessões formais antes de enviar dados.

Ele prioriza **velocidade e baixo overhead**, abrindo mão de confiabilidade, controle de fluxo e retransmissão. Por isso, é amplamente utilizado em aplicações que exigem rapidez e toleram perda de pacotes.

Em cibersegurança, o UDP é extremamente relevante porque:

- é muito usado em **ataques DDoS**;
- é mais difícil de monitorar por não manter estado;
- é base de protocolos críticos da internet.

![[Pasted image 20251216071506.png]]

---
# Em qual camada o UDP atua?

- **Modelo OSI:** Camada 4 – Transporte
- **Modelo TCP/IP:** Camada de Transporte

O UDP atua diretamente acima do IP e abaixo dos protocolos de aplicação.

---
# Para que serve o Protocolo UDP?

O UDP é usado quando:

- a velocidade é mais importante que a confiabilidade;
- pequenas perdas de dados são aceitáveis;
- o controle de erro é feito pela aplicação.

### Exemplos de uso:

- streaming de vídeo e áudio;
- chamadas VoIP;
- jogos online;
- DNS;
- DHCP;
- NTP;
- SNMP.

---
# Características do UDP

### Principais características:

- não orientado à conexão;
- não realiza three-way handshake;
- não garante entrega;
- não garante ordem dos pacotes;
- não possui retransmissão;
- baixo overhead;
- comunicação rápida.

Essas características tornam o UDP eficiente, porém mais vulnerável.

---
# Como o UDP funciona?

No UDP, o envio de dados ocorre da seguinte forma:

1. A aplicação cria um datagrama UDP;
2. Define a porta de origem e destino;
3. O pacote é enviado diretamente via IP;
4. O receptor aceita ou descarta o pacote.

Não há confirmação de recebimento (ACK) nem controle de estado.

---
# Cabeçalho UDP

O cabeçalho UDP é simples e possui apenas **8 bytes**.

## Campos do Cabeçalho UDP

| **Campo**        | **Tamanho** | **Função**                   |
| ---------------- | ----------- | ---------------------------- |
| Porta de Origem  | 16 bits     | Identifica aplicação origem  |
| Porta de Destino | 16 bits     | Identifica aplicação destino |
| Comprimento      | 16 bits     | Tamanho do datagrama         |
| Checksum         | 16 bits     | Verificação básica de erro   |

Essa simplicidade contribui para a performance e para riscos de segurança.

---
# UDP vs TCP

| **Características** | **TCP**     | **UDP**        |
| ------------------- | ----------- | -------------- |
| Orientado à conexão | Sim         | Não            |
| Confiabilidade      | Alta        | Baixa          |
| Controle de fluxo   | Sim         | Não            |
| Ordem de pacotes    | Garantida   | Não garantida  |
| Velocidade          | Menor       | Maior          |
| Uso comum           | Web, e-mail | Streaming, DNS |

---
# Vulnerabilidades do Protocolo UDP

Por não manter estado e não validar conexões, o UDP é amplamente explorado em ataques.

## 1. IP Spoofing

O UDP permite facilmente a falsificação do IP de origem.

Impactos:

- dificulta rastreamento;
- facilita ataques de amplificação;
- contamina logs.

![[Pasted image 20251216072002.png]]

## 2. UDP Flood

Ataque de negação de serviço (DoS/DDoS).

O atacante envia grandes volumes de pacotes UDP para portas aleatórias.

Consequências:

- consumo de largura de banda;
- sobrecarga de CPU;
- indisponibilidade de serviços.

![[Pasted image 20251216071856.png]]

## 3. Amplification Attacks

Exploram servidores UDP mal configurados.

Exemplos:

- DNS Amplification;
- NTP Amplification;
- SSDP Amplification;
- Memcached (UDP).

Um pequeno request gera uma resposta muito maior à vítima.

![[Pasted image 20251216072109.png]]

## 4. Port Scanning UDP

Varreduras UDP são mais lentas, mas eficazes.

- portas abertas podem não responder;
- portas fechadas respondem com ICMP unreachable.

![[Pasted image 20251216072216.png]]

## 5. Falta de Autenticação

Protocolos UDP geralmente não possuem autenticação nativa.

Exemplo:

- SNMP v1/v2;
- TFTP;
- serviços internos expostos.

---
# Ataques reais baseados em UDP

- Ataques massivos de DNS Amplification na internet;
- DDoS contra servidores de jogos;
- Abuso de NTP em botnets;
- Ataques reflexivos usando spoofing.

---
# Mitigações de Ataques UDP

### 1. Firewalls e Rate Limiting

- limitar tráfego UDP;
- bloquear portas não utilizadas.

### 2. Filtragem Anti-Spoofing

- BCP 38;
- filtros de entrada em roteadores.

### 3. Hardening de Serviços UDP

- desativar serviços desnecessários;
- restringir acesso por IP;
- usar versões seguras de protocolos.

### 4. Monitoramento de Tráfego

- IDS/IPS;
- NetFlow;
- análise de picos anormais.

### 5. Uso de TCP ou TLS quando possível

- substituir UDP por TCP quando viável;
- usar DTLS para segurança sobre UDP.

---
## UDP e DTLS (Datagram TLS)

Como o UDP não possui criptografia, surgiu o **DTLS**.

Características:

- fornece criptografia e autenticação;
- mantém baixo overhead;
- usado em VoIP, WebRTC e IoT.

![[Pasted image 20251216072438.png]]

---
# Ferramentas para testes e análise UDP

### Análise de Tráfego

- Wireshark
- Tcpdump

### Pentest

- Nmap (`-sU` – UDP Scan)
- Hping3
- Scapy
- Metasploit

### Testes de DDoS (laboratórios controlados)

- LOIC / HOIC

----
# UDP em Ambientes Corporativos

Em empresas, o UDP deve ser tratado com cautela:

- muitos serviços críticos dependem dele;
- portas abertas aumentam a superfície de ataque;
- monitoramento é essencial.

Boas práticas:

- documentar serviços UDP;
- segmentar redes;
- usar firewalls stateful.

---
# Importância do UDP para Cibersegurança

Compreender o UDP permite:

- detectar ataques DDoS rapidamente;
- proteger serviços críticos;
- configurar firewalls corretamente;
- realizar pentests realistas;
- entender o funcionamento de protocolos essenciais da internet.

---
# Conclusão

O protocolo UDP é simples, rápido e extremamente poderoso. Essa simplicidade, no entanto, o torna um dos principais vetores de ataque da internet moderna.

Para profissionais de cibersegurança, dominar o UDP é essencial para atuar em defesa de redes, resposta a incidentes e testes de intrusão, garantindo disponibilidade e resiliência dos sistemas.