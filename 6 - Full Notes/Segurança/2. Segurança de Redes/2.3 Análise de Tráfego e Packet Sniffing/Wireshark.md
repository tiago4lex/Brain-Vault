2025-09-29 09:37

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] 

----
# Introdução

**Wireshark** é um analisador de protocolo de código aberto usado para análise de tráfego de rede em tempo real e arquivos de captura. É a ferramenta padrão da indústria para troubleshooting análise de segurança e desenvolvimento de protocolos.

![[Pasted image 20250929094031.png]]

### Características Principais

- Suporte a mais de 2.000 protocolos.
- Captura em tempo real e análise offline.
- Interface gráfica intuitiva e linha de comando (`tshark`).
- Filtros poderosos de exibição e captura.
- Análise estatística avançada.
- Exportação de dados em múltiplos formatos.

---
# Instalação e Configuração

## Instalação Linux

```bash
# Debian/Ubuntu
sudo apt update && sudo apt install wireshark

# Adicionar usuário ao grupo wireshark
sudo usermod -a -G wireshark $USER

# Reiniciar a sessão para aplicar as mudanças
```

## Instalação no Windows

1. Download do instalador em [wireshark.org](https://wireshark.org)
2. Instalar com WinPcap/Npcap para captura de pacotes
3. Recomendado: Instalar USBPcap para análise USB

## Configuração Inicial

```bash
# Verificar interfaces disponíveis
wireshark -D

# Ou via interface gráfica: Capture > Options
```

## Interface do Usuário

**Componentes Principais:**

![[Pasted image 20250929095458.png]]

1. **Barra de Menu:** Arquivo, Capture, Analyze, Statistics, etc.
2. **Barra de Ferramentas:** Iniciar/Parar captura, aplicar filtros.
3. **Lista de Pacotes:** Visão geral dos pacotes capturados.
4. **Detalhes do Pacote:** Análise hierárquica do protocolo.
5. **Bytes do Pacote:** Visualização hexadecimal/ASCII.
6. **Barra de Status:** Informações da captura atual.

## Atalhos importantes

- `CTRL + E`: Iniciar/Parar Captura.
- `CTRL + F`: Buscar pacotes.
- `CTRL + R`: Aplicar filtro.
- `CTRL + ALT + A`: Abrir arquivo de captura.
- `Tab:` Navegar entre painéis.

---
# Captura de Pacotes

## Captura Básica

```bash
# Via linha de comando com tshark
tshark -i eth0 -w captura.pcap

# Capturar número limitado de pacotes
tshark -i eth0 -c 100 -w primeiros_100.pcap

# Capturar apenas HTTP
tshark -i eth0 "tcp port 80" -w http_traffic.pcap
```

## Opções de Captura Avançada

```bash
# Capturar com buffer ring (sobrescreve quando cheio)
tshark -i eth0 -b filesize:1000000 -b files:10 -w rotativo.pcap

# Capturar com filtro de host
tshark -i eth0 -f "host 192.168.1.100" -w host_especifico.pcap

# Capturar com tamanho de snapshop reduzido
tshark -i eth0 -s 64 -w headears_apenas.pcap
```

## Interface Gráfica - Opções de Captura

- **Interface:** Selecionar interface de rede.
- ***Promiscuous Mode:*** Capturar todo tráfego na rede.
- ***Capture filter:*** Filtro durante a captura (BPF syntax)
- **File:** Salvar automaticamente em arquivo.
- **Options:** Configurações avançadas de buffe.

---
# Filtros Básicos

## Sintaxe de Filtros

Os filtros do Wireshark usam syntax **BPF *(Berkley Packet Filter)***

## Filtros por Protocolo

```text
http    - Tráfego HTTP
dns     - Consulta e respostas DNS
tcp     - Pacotes TCP
udp     - Pacotes UDP
icmp    - Pacotes ICMP (ping)
arp     - Pacotes ARP
```

**Exemplo de saída filtrada por HTTP:**

```text
No.     Time        Source          Destination     Protocol Length Info
    1 0.000000    192.168.1.100   93.184.216.34   HTTP     345 GET / HTTP/1.1
    2 0.150234    93.184.216.34   192.168.1.100   HTTP     1434 HTTP/1.1 200 OK
```

## Filtros por IP

```text
ip.addr == 192.168.1.1      - Tráfego de/para IP específico
ip.src == 192.168.1.100     - Tráfego da fonte
ip.dst == 8.8.8.8           - Tráfego para destino
ip.src == 192.168.1.0/24    - Tráfego de subrede
```

**Exemplo de saída:**

```text
No.     Time        Source          Destination     Protocol Length Info
    1 0.000000    192.168.1.100   8.8.8.8         DNS      78 Standard query
    2 0.025000    8.8.8.8         192.168.1.100   DNS      142 Standard query response
```

## Filtros por Porta

```text
tcp.port == 80              - Tráfego na porta 80
tcp.srcport == 443          - Tráfego da porta fonte 443
tcp.dstport == 22           - Tráfego para porta destino 22
udp.port == 53              - Tráfego DNS
```

## Filtro por Tamanho

```text
frame.len == 64             - Pacotes exatos de 64 bytes
frame.len > 1000            - Pacotes maiores que 1000 bytes
frame.len < 128             - Pacotes menores que 128 bytes
```

---
# Filtros Avançados

## Filtros de Protocolo Específicos

```text
http.request.method == "GET"     - Requisições HTTP GET
http.request.method == "POST"    - Requisições HTTP POST
http.response.code == 404        - Respostas 404
dns.qry.name contains "google"   - Consultas DNS para google
dns.flags.response == 1          - Apenas respostas DNS
tcp.flags.syn == 1               - Pacotes SYN (início conexão)
tcp.flags.fin == 1               - Pacotes FIN (fim conexão)
```

## Filtros com Operadores Lógicos

```text
ip.addr == 192.168.1.100 and tcp.port == 80
http and ip.src == 192.168.1.50
dns and !(ip.addr == 8.8.8.8)
tcp.port == 80 or tcp.port == 443
```

## Filtros de Performance e Erros

```text
tcp.analysis.retransmission      - Retransmissões TCP
tcp.analysis.duplicate_ack       - ACKs duplicados
tcp.analysis.zero_window         - Zero window (congestionamento)
tcp.analysis.lost_segment        - Segmentos perdidos
icmp.type == 3                   - ICMP Destination Unreachable
```

## Filtros de Aplicação

```text
http.request.uri contains "login"    - URLs com login
http.cookie contains "session"       - Cookies de sessão
http.user_agent contains "Android"   - User Agents Android
smtp.req.command == "MAIL"           - Comandos SMTP
```

## Filtros Avançados de TCP

```text
tcp.stream eq 5                      - Stream TCP específico
tcp.window_size < 1460               - Janelas TCP pequenas
tcp.analysis.ack_rtt > 0.1           - RTT alto
tcp.seq == 1                         - Número de sequência específico
```

---
# Análise de Protocolos

## Análise HTTP

```text
# Filtrar métodos específicos
http.request.method == "GET"
http.request.method == "POST"
http.request.method == "PUT"

# Filtrar por conteúdo
http.request.uri contains ".php"
http.request.uri contains "admin"
http.response.code == 200
http.response.code == 404

# Extrair arquivos
File > Export Objects > HTTP
```

**Exemplo de análise HTTP GET:**

```text
Hypertext Transfer Protocol
    GET /index.html HTTP/1.1\r\n
    Host: www.example.com\r\n
    User-Agent: Mozilla/5.0...\r\n
    Accept: text/html\r\n
    \r\n
```

## Análise DNS

```text
# Consultas e respostas
dns.qry.name == "google.com"
dns.resp.addr == 8.8.8.8

# Tipos de consulta
dns.qry.type == 1        # A record
dns.qry.type == 28       # AAAA record
dns.qry.type == 15       # MX record

# Analisar tempo de resposta
dns.time > 1.0
```

**Exemplo de resposta DNS:**

```text
Domain Name System (response)
    Transaction ID: 0x1234
    Flags: 0x8180 Standard query response, No error
    Questions: 1
    Answer RRs: 1
    Answers
        google.com: type A, class IN, addr 172.217.28.206
```

## Análise TCP

```text
# Handshake completo
tcp.flags.syn == 1 and tcp.flags.ack == 0    # SYN
tcp.flags.syn == 1 and tcp.flags.ack == 1    # SYN-ACK
tcp.flags.ack == 1 and tcp.flags.syn == 0    # ACK

# Problemas de conexão
tcp.analysis.retransmission    # Retransmissões
tcp.analysis.zero_window       # Janela zero
tcp.analysis.duplicate_ack     # ACKs duplicados
```

---
# Técnicas de Análise

## *Follow TCP Stream*

```text
1. Clicar direito em pacote TCP > Follow > TCP Stream
2. Analisar conversa completa entre cliente-servidor
3. Identificar dados transmitidos
4. Exportar conteúdo (texto, arquivos, etc.)
```

**Exemplo de saída:**

```text
GET /login.php HTTP/1.1
Host: exemplo.com
User-Agent: Mozilla/5.0...

HTTP/1.1 200 OK
Content-Type: text/html
...
<html><body>Login Page</body></html>
```

## Análise Estatística

```text
Statistics > Conversation > IPv4    - Top conversas
Statistics > Protocol Hierarchy     - Hierarquia de protocolos
Statistics > HTTP > Packet Counter  - Estatísticas HTTP
Statistics > IO Graphs              - Gráficos de tráfego
```

## Exportação de Dados

```text
File > Export Packet Dissections > As CSV    - Dados em CSV
File > Export Objects > HTTP                 - Arquivos HTTP
File > Export Specified Packets              - Pacotes específicos
```

## Color Rules Para Análise Visual

```text
# Regras comuns de coloração
tcp.analysis.retransmission    - [Amarelo] Retransmissões
http                           - [Verde] Tráfego HTTP
dns                            - [Azul] Consultas DNS
tcp.flags.syn == 1             - [Roxo] Conexões novas
```

---
# Casos Práticos

## Caso 1: Análise de Ataque de Força Bruta

```text
# Filtro para múltiplas tentativas de login
http.request.uri contains "login" and http.request.method == "POST"

# Análise:
1. Identificar IPs com múltiplas tentativas
2. Verificar user agents diferentes
3. Analisar padrão temporal
4. Exportar credenciais tentadas
```

**Comandos específicos:**

```bash
# Contar tentativas por IP
tshark -r ataque.pcap -Y 'http.request.method == "POST"' -T fields -e ip.src | sort | uniq -c | sort -nr

# Extrair usuários tentados
tshark -r ataque.pcap -Y 'http.request.method == "POST"' -T fields -e http.file_data
```

## Caso 2: Detecção de Port Scanning

```text
# Filtro para varredura de portas
tcp.flags.syn == 1 and tcp.flags.ack == 0 and tcp.window_size <= 1024

# Análise:
1. Identificar IP fonte suspeito
2. Verificar múltiplas portas destino
3. Analisar timing entre tentativas
4. Checar por padrões conhecidos
```

**Filtros avançados para scanning:**

```text
# SYN para múltiplas portas do mesmo IP
tcp.flags.syn == 1 and tcp.flags.ack == 0

# Com contagem estatística
Statistics > Conversations > TCP
```

## Caso 3: Troubleshooting de Performance

```text
# Filtros para problemas de rede
tcp.analysis.retransmission        # Retransmissões
tcp.analysis.duplicate_ack         # ACKs duplicados
tcp.analysis.zero_window           # Congestionamento
tcp.analysis.window_update         # Atualizações de janela
icmp.type == 3                     # Host inalcançável
```

**Análise de throughput:**

```text
Statistics > IO Graph
- Adicionar filtros específicos
- Configurar intervalo de tempo
- Comparar diferentes fluxos
```

## Caso 4: Análise de Malware

```text
# Comportamentos suspeitos
dns.qry.name contains ".tk" or dns.qry.name contains ".ml"
http.request.uri contains "exe" or http.request.uri contains "dll"
tcp.port == 4444 or tcp.port == 1337  # Portas comuns de backdoor

# Análise de C2 (Command and Control)
1. Identificar beaconing (consultas DNS periódicas)
2. Analisar user agents anormais
3. Verificar conexões para IPs suspeitos
```

---
# Ferramentas Avançadas

## `tshark` - Linha de Comando

```bash
# Análise básica
tshark -r captura.pcap -Y "http" -T fields -e frame.time -e ip.src -e ip.dst

# Estatísticas de conversação
tshark -r captura.pcap -q -z conv,tcp

# Exportar dados específicos
tshark -r captura.pcap -Y "dns" -T json > dns_data.json

# Análise em tempo real
tshark -i eth0 -Y "tcp.port == 80" -V
```

## `edicap` - Manipulação de Capturas

```bash
# Dividir arquivo grande
editcap -c 10000 grande.pcap dividido.pcap

# Filtrar por tempo
editcap -A "2023-01-01 00:00:00" -B "2023-01-02 00:00:00" entrada.pcap saida.pcap

# Remover duplicatas
editcap -d entrada.pcap saida_sem_duplicatas.pcap
```

## `mergecap` - Combinar Capturas

```bash
# Combinar múltiplos arquivos
mergecap -w combinado.pcap cap1.pcap cap2.pcap cap3.pcap

# Ordenar por timestamp
mergecap -w ordenado.pcap -s 2 cap1.pcap cap2.pcap
```

## `capinfos` - Informações do Arquivo

```bash
# Estatísticas do arquivo
capinfos captura.pcap

# Saída detalhada
capinfos -Tmux captura.pcap
```

---
# Exemplos de Saída e Interpretação

## Exemplo 1: Handshake TCP normal

```text
1 0.000000 192.168.1.100 → 93.184.216.34 TCP 74 49152 → 80 [SYN] Seq=0 Win=64240
2 0.025000 93.184.216.34 → 192.168.1.100 TCP 74 80 → 49152 [SYN, ACK] Seq=0 Ack=1
3 0.025100 192.168.1.100 → 93.184.216.34 TCP 66 49152 → 80 [ACK] Seq=1 Ack=1
```

**Interpretação**: Conexão estabelecida com sucesso em ~25ms.

## Exemplo 2: Retransmissão TCP

```text
1 0.000000 192.168.1.100 → 93.184.216.34 TCP 74 [SYN]
2 1.023000 192.168.1.100 → 93.184.216.34 TCP 74 [SYN]  # RETRANSMISSÃO
3 3.071000 192.168.1.100 → 93.184.216.34 TCP 74 [SYN]  # RETRANSMISSÃO
```

**Interpretação**: Problema de conectividade - SYN não está sendo respondido.

## Exemplo 3: HTTP 404 Not Found

```text
HTTP/1.1 404 Not Found\r\n
Content-Type: text/html\r\n
Content-Length: 1234\r\n
\r\n
<html><body><h1>404 Not Found</h1></body></html>
```

**Interpretação**: Recurso solicitado não existe no servidor.

## Exemplo 4: DNS Query com Resposta

```text
Query: google.com type A, class IN
Response: google.com type A, class IN, addr 172.217.28.206
```

**Interpretação**: Resolução DNS bem-sucedida para [google.com](https://google.com/).

---
# Dicas de Performance

## Otimização para Grandes Capturas

```text
1. Usar filtros de captura quando possível
2. Aumentar buffer size nas opções
3. Usar arquivos múltiplos com ring buffer
4. Considerar análise com tshark para datasets muito grandes
```

## Análise Eficiente

```text
1. Começar com estatísticas de conversação
2. Usar filtros para focar em tráfego relevante
3. Aplicar color rules para identificação visual
4. Exportar dados para análise externa quando necessário
```

---
# Conclusão

O Wireshark é uma ferramenta extremamente poderosa para análise de rede. O domínio completo requer:

1. **Entendimento de protocolos de rede**
2. **Prática com filtros e análise**
3. **Conhecimento de padrões de tráfego normais e anômalos**
4. **Habilidade para correlacionar eventos**