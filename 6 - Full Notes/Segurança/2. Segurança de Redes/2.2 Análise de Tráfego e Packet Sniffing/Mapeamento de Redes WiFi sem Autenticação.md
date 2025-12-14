  2025-09-28 12:42

Status: #developed #redes 

Tags: [[CyberSecurity]] | [[Redes de Computadores]]

----
# Limitações Fundamentais

É importante entender que sem a senha da rede WiFi, suas capacidades são severamente limitadas:

- ✗ **Não é possível conectar-se à rede**
- ✗ **Não é possível escanear hosts internos diretamente**
- ✗ **O mapeamento de portas interno é impossível**
- ✓ **Apenas reconhecimento externo e passivo é viável**

---
# Conceitos Técnicos

## 1. Reconhecimento Passivo vs Ativo

#### Reconhecimento Passivo:

- Monitoramento sem enviar pacotes para rede alvo.
- Coleta de informações através da escuta wireless.
- Detectável mas não atribuível diretamente.

#### Reconhecimento Ativo

- Envio direto de pacotes para a rede.
- Requer autenticação na rede WiFi.
- Mais detectável mas mais eficaz.

## 2. Estrutura de Redes WiFi

```text
SSID: Nome da rede visível
BSSID: Endereço MAC do access point
Channel: Canal de operação
Security: WPA2, WPA3, etc.
Clients: Dispositivos conectados
```

---
# Técnicas de Reconhecimento

## 1. Informações capturadas sem senha:

- SSID (nome da rede).
- BSSID (MAC do roteador).
- Força do sinal (RSSI).
- Tipo de criptografia (WPA2, WPA3).
- Canal de operação.
- Fabricante do equipamento (via OUI)

## 2. Identificação de Clientes Conectados

**Técnica:** Monitorar pacotes de broadcast/multicast.

- Dispositivos conectados frequentemente enviam pacotes.
- Endereços MAC dos clientes podem ser identificados.

## 3. Fingerprinting de Dispositivos

**Técnica:** Análise de padrões de tráfego.

- Identificação de tipos de dispositivos (IoT, mobile, etc.).
- Padrões temporais de atividade.

---
# Ferramentas Especializadas

## 1. Aircrack-ng Suite

```bash
# Instalação no Kali Linux
sudo apt update && sudo apt install aircrack-ng

# Componentes principais:
	# - airmon-ng: Interface monitoring
	# - airodump-ng: Captura de pacotes
	# - aireplay-ng: Injeção de pacotes
	# - aircrack-ng: Quebra de senhas
```

## 2. Kismet

```bash
# Instalação
sudo apt install kismet

# Scanner wireless passivo avançado
# Detecção de redes ocultas
# Geolocalização de dispositivos
```

## 3. Wireshark

```bash
# Instalação
sudo apt install wireshark

# Análise detalhada de pacotes
# Filtros avançados para tráfgo wireless.
```

## 4. Wash (para WPS)

```bash
# Instalação
sudo apt install reaver wash

# Detecção de WPS habilitado
# Identificação de vulnerabilidades WPS
```

---
# Exemplo Práticos e Comandos

## 1. Identificação Básica da Rede

**Comando:**

```bash
# Escanear redes WiFi disponíveis
sudo iwlist wlan0 scan | grep -E "ESSID|Address|Channel|Quality"
```

**Exemplo de saída:**

```text
ESSID:"Rede-Alvo"
Address: AA:BB:CC:DD:EE:FF
Channel:11
Frequency:2.462 GHz (Channel 11)
Quality=70/100 Signal level=-40 dBm
Encryption key:on
IE: IEEE 802.11i/WPA2 Version 1
```

## 2. Modo Monitor e Captura Detalhada

**Comandos:**

```bash
# Parar processos que interferem
sudo airmon-ng check kill

# Ativar modo monitor
sudo airmon-ng start wlan0

# Capturar informações detalhadas
sudo airodump-ng wlan0mon

# Forcar em uma rede específica
sudo airodump-ng --bssid AA:BB:CC:DD:EE:FF --channel 11 wlan0mon
```

**Saída:**

```text
BSSID              PWR  Beacons  #Data  CH  MB   ENC  CIPHER AUTH ESSID
AA:BB:CC:DD:EE:FF  -40      100    450  11  54e  WPA2 CCMP   PSK  Rede-Alvo

BSSID              STATION            PWR   Rate    Lost  Frames  Probe
AA:BB:CC:DD:EE:FF  11:22:33:44:55:66  -42   1e-24      0      123
AA:BB:CC:DD:EE:FF  AA:BB:CC:11:22:33  -48   2e-24      2       89
```

## 3. Identificação de IPs Públicos e Range

**Técnica Indireta:**

```bash
# Identificar tráfego DNS para descobrir IP público
# Capturar pacotes DNS da rede
sudo tcpdump -i wlan0mon -n port 53
```

**Saída:**

```text
15:30:25.123456 IP 192.168.1.15.54321 > 8.8.8.8.53: 34567+ A? google.com. (32)
```

Neste caso, 192.168.1.15 é cliente interno, mas não sabemos o IP público.

## 4. Tentativas de Discovery sem Autenticação

***Deauth Attack*** para Coleta de Handshake:

```bash
# Capturar handshake WPA
sudo airodump-ng --bssid AA:BB:CC:DD:EE:FF --channel 11 --write capture wlan0mon

# Enviar pacostes de deautenticação (em outro terminal)
sudo aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon
```

## 5. Análise com Kismet

**Configurações e Uso:**

```bash
# Editar configuração
sudo nano /etc/kismet/kismet.conf

# Execucar Kismet
sudo kismet -c wlan0mon

# Acessar interface web: https://localhost:2501
```

---
# Possibilidades Limitadas de Mapeamento

## 1. Identificação de Serviços Expostos Externamente

**Mesmo sem acesso à rede interna, é possível:**

```bash
# Escanear IP público do roteador (se descobir)
nmap -sS -p 80,443,22,21,25 [IP_PUBLICO]

# Verificar se há portas forwardadas
nmao -sS -p- --min-rate 5000 [IP_PUBLICO]
```

## 2. Exemplo de Descoberta de IP Público

**Técnica Indireta (quando possível)**

1. Monitorar tráfego de clientes para serviços externos.
2. Identificar padrões de conexão.
3. Usar Shodan ou Censys para buscar por SSID ou BSSID.
4. Às vezes redes têm informações expostas em busca.

---
# Exemplo Completo: Cenário Hipotético

## Fase 1: Reconhecimento Inicial

```bash
# Listar ingerfaces wireless
iwconfig

# Escaner redes
sudo iswlist wlan0 scan > scan_results.txt

# Filtrar rede alvo
grep -A 10 -B "Rede Alvo" scan_results.txt
```

## Fase 2: Análise Detalhada

```bash
# Modo monitor
sudo airmon-ng start wlan0

# Captura focada
sudo airodump-ng --bssid AA:BB:CC:DD:EE:FF --channel 11 --write rede_alvo wlan0mon
```

## Fase 3: Análise de Clientes

```bash
# Ver clientes conectados a partir do arquivo de captura
cat rede_alvo-01.csv | grep AA:BB:CC:DD:EE:FF

# Identificar fabricantes pelos MACs
echo "AA:BB:CC" | grep -i -f - /usr/share/iee-dataa/oui.txt
```

---
# Conclusão

Sem a senha da rede WiFi, o mapeamento interno é praticamente impossível. As técnicas apresentadas permitem apenas reconhecimento externo limitado. Para um pentest completo, é necessário:

1. Conseguir as credenciais de acesso legítimas.
2. Conectar-se à rede para realizar escaneamentos internos.
