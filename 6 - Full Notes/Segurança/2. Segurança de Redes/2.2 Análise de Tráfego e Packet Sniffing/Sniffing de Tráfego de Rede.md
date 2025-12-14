2025-09-05 09:22

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

O *sniffing* de tráfego consiste na captura e análise passiva de pacotes de dados que trafegam em uma rede. Esta técnica é essencial para administradores de rede diagnosticarem problemas, mas também pode ser utilizada maliciosamente para capturar informações sensíveis. Este documento detalha métodos, ferramentas e técnicas de análise de tráfego de rede.

---
# Fundamentos do *Sniffing* de Rede

## O que é *Sniffing* de Tráfego?

**Definição:** Captura passiva de pacotes de dados que trafegam através de uma rede de computadores.

**Modalidades:**

- ***Sniffing* Ativo:** Interfere na rede para redirecionar tráfego.
- ***Sniffing* Passivo:** Apenas escuta o tráfego existente.

## É necessário estar conectado à Rede?

Não necessariamente. Existem diferentes cenários:

### 1. *Sniffing* sem estar conectado

- **Modo Monitor Wireless:** Captura todos os pacotes no ar sem associar-se a nenhuma rede.
- **Port Mirroring/SPAN:** Em switches configurados, o tráfego é espelhado para uma porta.
- **ARP Spoofing:** Engana hosts para redirecionar tráfego através do atacante.

### 2. *Sniffing estando conectado*

- **Modo Promíscuo:** Interface captura todo tráfego da rede local.
- **Hubs (obsoletos):** Todo tráfego é broadcastado para todas as portas.

### 3. *Sniffing* Remoto/Passivo

- **Captura em Gateway:** *Sniffing* no ponto de saída da rede.
- **Tap Network:** Dispositivos físicos que copiam tráfego.

## Modos de Operação da Placa de Rede

```bash
# Modo maneged (normal)
sudo ip link set wlan0down
sudo iwconfig wlan0 mode managed
sudo ip link set wlan0up

# Modo monitor (para sniffing wireless)
sudo ip link set wlan0 down
sudo iwconfig wlan0 mode monitor
sudo ip link set wlan0 up
```

## Tipos de *Sniffing*

- **Local:** Na mesma sub-rede *(ARP spoofing)*.
- **Wireless:** Captura tráfego wireless (modo monitor).
- **Switchado:** Em redes com switch *(ARP poisoning)*

---
# Ferramentas de *Sniffing*

## 1. Wireshark (interface gráfica)

**Instalação:**

```bash
sudo apt update
sudo apt install wireshark
sudo usermod -aG wireshark $USER
```

**Uso Básico:**

```bash
# Iniciar wireshar (selecionar interface)
wireshark

# Ou via linha de comando
wireshark -i wlan0 -k
```

## 2. Tshark (versão CLI do Wireshark)

**Comando Essenciais:**

```bash
# Capturar pacotes na interface wlan0
tshark -i wlan0

# Capturar e Salvar em um arquivo
tshark -i wlan0 -w captura.pcap

# Ler arquivo capturado
tshark -r captura.pcap

# Filtrar por protocolo HTTP
tshark -i wlan0 -Y "http"

# Filtrar por IP de destino
tshark -i wlan0 -Y "ip.dst==192.168.1.1"
```

## 3. Tcpdump

**Instalação:**

```bash
sudo apt install tcpdump
```

**Exemplos de uso:**

```bash
# Capturar pacotes na interface eth0
sudo tcpdump -i eth0

# Capturar pacotes com verbose
sudo tcpdump -i eth0 -v

# Capturar e salvar em um arquivo
sudo tcpdump -i eth0 -w captura.pcap

# Ler arquivo capturado
sudo tcpdump -r captura.pcap

# Filtrar por porta 80 (HTTP)
sudo tcpdump -i eht0 port 80

# Filtrar por host específico
sudo tcpdump -i eht0 host 192.168.1.100
```

## 4. Outras Ferramentas

```bash
# Airodump-ng (para wireless)
sudo airodump-ng wlan0mon

# Driftnet (captura imagens)
sudo apt install driftnet
driftnet -i wlan0

# Urlsnarf (captura URLs)
sudo apt install dsniff
urlsnarf -i wlan0
```

---
# Técnicas de Captura

## *Sniffing* em Redes Wireless

```bash
# Colocar interface em modo monitor
sudo airmon-ng check kill
sudo airmon-ng start wlan0

# Capturar tráfego com airodump-ng
sudo airodump-ng wlan0mon --write captura_wifi

# Capturar handshakes WPA
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w handshake wlan0mon
```

## *ARP Spoofing* (*Sniffing* em Redes Switchadas)

```bash
# Habilitar IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward
```

- Permite que o tráfego continue fluindo após *spoofing*.

```bash
# Executar ARP spoofing com arpspoof
sudo arpspoof -i eth0 -t 192.168.1.10 192.168.1.1
```

```bash
# Ou com ettercap
sudo ettercap -T -M arp:remote /192.168.1.1// /192.168.1.100//
```

- `-T`: modo texto
- `-M arp:remote`: método ARP para *spoofing* remoto
- `/192.168.1.1//`: Gateway (alvo 1).
- `/192.168.1.100//`: Cliente (alvo 2)

**Saída Esperada:**

```text
ettercap 0.8.3 copyright 2001-2019 Ettercap Development Team

Listening on:
  eth0 -> AC:DE:48:00:11:22
	  192.168.1.50/255.255.255.0
	  fe80::aede:48ff:fe00:1122/64

SSL dissection needs a valid 'redir_command_on' script in the etter.conf file
Privileges dropped to EUID 65534 EGID 65534...

  33 plugins
  42 protocol dissectors
  57 ports monitored
24609 mac vendor fingerprint
1766 tcp OS fingerprint
2183 known services
Randomizing 255 hosts for scanning...
Scanning the whole netmask for 255 hosts...
* |==================================================>| 100.00 %

2 hosts added to the hosts list...

ARP poisoning victims:

 GROUP 1 : 192.168.1.1 AC:DE:48:11:22:33

 GROUP 2 : 192.168.1.100 AC:DE:48:AA:BB:CC

Starting Unified sniffing...

Text only Interface activated...
Hit 'h' for inline help
```

## Captura com Redirecionamento de Porta

```bash
# Redirecionar tráfego HTTP para porta 8080
sudo iptables -t nat -A PREROUTING -p tcp --dpot 80 -j REDIRECT --to-port 8080

# Capturar tráfego redirecionado
sudo tcpdump -i lo port 8080 -w http_caputre.pcap
```

---
# Análise de Tráfego

## Análise com Wireshark

**Filtros Comuns:**

```text
http.request           # Requisiçõe HTTP
tcp.port == 443        # Tráfego HTTPS
ip.src == 192.168.1.1  # Pacotes de orgiem es
dns                    # Consulta DNS
arp                    # Pacotes ARP
```

**Estatísticas Úteis:**

- **Conversations:** Visualizar conversações entre hosts.
- **Protocol Hierarchy:** Hierarquia de protocolos utilizados.
- **IO Graphs:** Gráficos de throughput.

## Análise com Tshark

### 1. Análise Básica

```bash
# Estatísticas de protocolos
tshark -r captura.pcap -q -z proto,colinfo
```

- `-r`: Lê arquivo de captura.
- `-q`: modo quieto (sem output contínuo).
- `-z proto,colinfo`: Estatísticas de protocolos com informações de coluna.

**Saída esperada:**

```text
===================================================================
Protocol | % Packets | % Bytes | Packets | Bytes | Mbit/s | End Packets | End Bytes | End Mbit/s
===================================================================
ETH      |    100.00 |   100.00 |   15000 | 15MB  |   1.23 |       15000 | 15MB      |      1.23
IP       |     95.00 |    95.50 |   14250 | 14MB  |   1.17 |       14250 | 14MB      |      1.17
TCP      |     80.00 |    85.00 |   12000 | 12MB  |   1.00 |       12000 | 12MB      |      1.00
HTTP     |     15.00 |    20.00 |    2250 |  3MB  |   0.25 |        2250 |  3MB      |      0.25
DNS      |      5.00 |     0.50 |     750 | 75KB  |   0.06 |         750 | 75KB      |      0.06
```

### 2. Análise de Conversações

```bash
# Top talkers (hosts que mais comunicam)
thsark -r captura.pcap -q -z conv,tcp
```

- `-z conv,tcp:` Estatísticas de conversações TCP

**Saída esperada:**

```text
================================================================================
TCP Conversations
Filter:<No Filter>
                                               |       <-      | |       ->      | |     Total     |
                                               | Frames  Bytes | | Frames  Bytes | | Frames  Bytes |
192.168.1.100:49672   <-> 142.250.184.206:443  |   1150   125KB| |    850    95KB| |   2000   220KB|
192.168.1.100:49670   <-> 34.120.182.96:443    |    600    65KB| |    400    45KB| |   1000   110KB|
192.168.1.101:5353    <-> 224.0.0.251:5353     |     50     5KB| |     50     5KB| |    100    10KB|
================================================================================
```

### 3. Extração de Objetos HTTP

```bash
# Extrari objetos HTTP
tshark -r captura.pcap --export-objects http,http_objects
```

- `--export-objects http,[diretorio]`: Extrai objetos http para diretório.

**Saída esperada:**

```text
Exporting 15 objects (exported 0 already)
HTTP object 1 (image/png): http://example.com/image.png -> http_objects/image.png
HTTP object 2 (text/html): http://example.com/page.html -> http_objects/page.html
...
Successfully exported 15 objects
```

### 4. Análise de Tráfego HTTP

```bash
# Filtrar e exportar credenciais HTTP
tshark -r captura.pcap -Y "http.request.methos == POST" -T fields -e http.host -e http.request.uri -e http.file_data
```

- `-Y`: Filtro de display (equivalente a wireshark filter).
- `-T fields`: Saída em campos específicos.
- `-e http.post`: Campo host HTTP.
- `-e http.request.uri`: Campo URI da requisição.
- `-e http.file_data:` Dados do POST.

**Saída Esperada:**

```text
example.com /login.php username=admin&password=secret123
api.service.com /auth/token grant_type=password&username=user&password=pass123
```

## Análise com Tcpdump

```bash
# Analisar arquivo capturado
sudo tcpdump -r captura.pcap -n

# Contar pacotes por protocolo
sudo tcpdump -r captura.pcap -n | awk '{print $5}' | cut -d. -f1-4 | sort | uniq -c | sort -n

# Extrair URLs HTTP
sudo tcpdump -r captura.pcap -n -A -s0 | grep -E "GET|POST|Host:"
```

---
# Técnicas de Análise Específicas

## Análise de Tráfego HTTP

```bash
# Filtrar métodos HTTP
tshark -r captura.pcap -Y "http.request.method == POST"

# Extrair cookies
tshark -r captura.pcap -Y "http.cookie" -T fields -e http.cookie

# Capturar user agents
tshark -r captura.pcap -Y "http.user_agent" -T fields -e http.user_agent
```

## Análise de Tráfego DNS

```bash
# Consultar DNS
tshark -r captura.pcap -Y "dns" -T fields -e frame.time -e ip.src -e dns.qry.name
```

- `-e frame.time`: Timestamp do pacote
- `-e ip.src`: IP de origem
- `-e dns.qry.name`: Nome consultado no DNS

**Saída esperada:**

```text
Jan 1, 2024 12:34:56.123456 192.168.1.100 google.com
Jan 1, 2024 12:34:56.234567 192.168.1.100 facebook.com
Jan 1, 2024 12:34:57.345678 192.168.1.101 update.microsoft.com
```


```bash
# Respostas DNS
tshark -r captura.pcap -Y "dns.flags.response == 1" -T fields -e dns.resp.name -e dns.a
```

## Análise de Tráfego SSL/TLS

```bash
# Client Hello packets
tshark -r captura.pcap -Y "ssl.handshake.type == 1" -T fields -e ip.src -e ssl.handshake.extensions_server_name
```

- `ssl.handshake.type == 1:` *Client Hello*
- `ssl.handshake.extension_server_name`: campo SNI

**Saída esperada:**

```text
192.168.1.100 github.com
192.168.1.100 api.stripe.com
192.168.1.101 cdn.amazon.com
```

```bash
# Extrair chaves SSL (se disponíveis)
tshark -r captura.pcap -o "tls.keylog_file:sslkeylog.log" -Y "http"
```

---
# Exemplos Práticos de *Sniffing*

## 1. Captura de Credenciais HTTP

```bash
# Capturar tráfego HTTP
sudo tcpdump -i wlan0 -w http-traffic.pcap port 80
``` 

- `-i wlan0`: Interface de captura.
- `-w http_traffic.pcap`: Salva em arquivo.
- `port 80`: Filtra apenas porta HTTP

```bash
# Analisar em busca de credenciais
tshark -r http_traffic.pcap -Y "http.request == POST" -T fields -e http.post -e http.request.uri -e http.file_data | grep -i "user\|pass\|login"
```

- `grep -i`: *Case insensitive search* por usuário, senha e login.

**Saída esperada:**

```bash
webmail.company.com /login.php username=johndoe&password=Welcome123
api.service.com /oauth/token grant_type=password&username=admin&password=P@ssw0rd!
```

## 2. Monitoramento de Rede Local

```bash
# Capturar tráfego na rede local
sudo tcpdump -i eth0 -w local_network.pcap net 192.168.1.0/24
```

- `net 192.168.1.0/24`: Filtra por rede específica.

```bash
# Identificar hosts ativos
tshark -r local_network.pcap -T fields -e ip.src | sort | uniq
```

- `sort`: Ordena endereços IP.
- `uniq -c`: Conta ocorrências únicas.
- `sort -nr`: Ordena numericamente em ordem reversa.

**Saída esperada:**

```text
   1245 192.168.1.100
    893 192.168.1.1
    456 192.168.1.101
    234 192.168.1.102
     12 192.168.1.255
```

## 3. Detecção de Scanners de Rede

```bash
# Capturar tráfego de varredura
sudo tcpdump -i eth0 -w scan_detection.pcap "tcp[13] & 2 != 0"
```

- `"tcp[13] & 2 != 0"`: Filtro byte-level para flag SYN

```bash
# Analisar tentativas de conexão
tshark -r scan_detection.pcap -Y "tcp.flags.syn == 1 and tcp.flags.ack == 0" -T fields -e ip.src | sort | uniq -c | sort -n
```

- `tcp.flags.syn == 1 and tcp.flags.ack == 0`: Apenas SYN packets.

**Saída esperada:**

```text
   150 192.168.1.200
    45 192.168.1.201
     2 192.168.1.100
```

---
# Técnicas de Proteção Contra *Sniffing*

## 1. Prevenção em Redes Wireless

- Usar WPA3 em vez de WPA2
- Desativar WPS
- Implementar 802.1X com autenticação mútua
- Monitorar por APs falsos

## 2. Proteção em Redes Cabeadas

- Implementar port security em switches
- Configurar DHCP snooping
- Usar ARP inspection
- Segmentar rede com VLANs

## 3. Proteção de Dados

- Usar HTTPS sempre que possível
- Implementar VPN para tráfego sensível
- Usar SSH em vez de Telnet
- Criptografar tráfego com TLS/SSL

## 4. Detecção de *Sniffing*

```bash
# Monitorar modo promíscuo
ip link show | grep PROMISC

# Verificar ARP tables inconsistentes
arp -a

# Usar ferramentas de detecção
sudo apt install arpwatch
sudo arpwatch -i eth0
```

---
# Interpretação de Dados Capturados

## Estrutura de um Pacote TCP/IP

```text
[ Ethernet Header ] [ IP Header ] [ TCP Header ] [ Data ]
```

## Campos Importantes para Análise

**Cabeçalho Ethernet:**

- MAC Source/Destination

**Cabeçalho IP:**

- IP Source/Destination
- TTL
- Protocol

**Cabeçalho TCP:**

- Source/Destination Port
- Flags (SYN, ACK, FIN, RST)
- Sequence Number

## Exemplo de Análise de Pacote

```bash
# Pacote TCP completo
tshark -r captura.pcap -Y "tcp" -V -c 1

# Extrair payloade de pacote
tshark -r captura.pcap -Y "frame.number == 123" -T fields -e data
```

---
# Recursos e Referências

## Documentação Oficial

- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [Tcpdump Man Page](https://www.tcpdump.org/manpages/tcpdump.1.html)
- [Tshark Man Page](https://www.wireshark.org/docs/man-pages/tshark.html)

## Livros Recomendados

- "Wireshark Network Analysis" by Laura Chappell
- "Network Flow Analysis" by Michael W. Lucas
- "The Practice of Network Security Monitoring" by Richard Bejtlich

## Cursos e Treinamentos

- Wireshark Certified Network Analyst (WCNA)
- Cisco CyberOps Associate
- SANS SEC503: Intrusion Detection In-Depth