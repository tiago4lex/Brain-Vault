
]2025-09-02 16:42

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes]] | [[Redes de Computadores]] | [[Wi-Fi]]

----
# Introdução

O reconhecimento e enumeração constituem a fase inicial do teste de penetração em redes wireless, envolvendo a descoberta, identificação e mapeamento de redes Wi-Fi, pontos de acesso e dispositivos clientes.

---
# Objetivos do Reconhecimento Wireless

## 1. Coleta de Informações

- Identificação de redes Wi-Fi disponíveis
- Coleta de SSIDs (visíveis e ocultos)
- Detecção de pontos de acesso e seus fabricantes
- Enumeração de clientes conectados

## 2. Análise de Metadados

- Canais utilizados
- Tipos de criptografia (WEP, WPA, WPA2, WPA3)
- Potência do sinal
- Taxas de transmissão suportadas

---
# Ferramentas de Reconhecimento

## 1. Aircrack-ng Suite

**Função:** Suite completa para auditoria wireless

```bash
# Colocar a interface em modo monitor
sudo airmon-ng check kill
sudo airmon-ng start wlan0

# Verificar modo monitor ativo
sudo airmon-ng

# Scanner de redes com airodum-ng
sudo airodump-ng -wlan0mon
```

**Exemplo de Saída:**

```txt
BSSID              PWR  Beacons  #Data  CH MB  ENC  CIPHER AUTH EESID
AA:BB:CC:DD:EE:FF  -42  100      45     6  54e WPA2 CCMP   PSK  Home-Network
11:22:33:44:55:66  -85  85       12     11 54e WEP  WEP    OPN  Public-WiFi
```

## 2. Kismet

**Função:** Detector de redes, sniffer e IDS wireless

```bash
# Instalação
sudo apt install kismet

# Execução
sudo kismet -c wlan0mon
```

**Características:**

- Detecção de redes ocultas (SSIDs não broadcastados)
- Identificação de clientes e tráfego
- Geolocalização de pontos de acesso
- Detecção de intrusos

## 3. Wifite

**Função:** Automação de ataques wireless

```bash
# Scanner básico
sudo wifite --showb

# Scanner com detalhes
sudo wifite --info
```

---
# Técnicas de Reconhecimento

## 1. Scanner Passivo

**Objetivo:** Coletar informações sem transmitir pacotes

```bash
# Scanner passivo com airodump-ng
sudo airodump-ng wlan0mon --write scan_results --output-format csv
```

**Vantagens:**

- Indetectável pela rede
- Coleta informações de redes ocultas
- Não altera o funcionamento da rede

## 2. Scanner Ativo

**Objetivo:** Forçar a rede a revelar informações

```bash
# Envio de probes para revelar SSIDs
sudo aireplay-ng wlan0mon --fakeauth 1 -a AA:BB:CC:DD:EE:FF
```

**Técnicas:**

- Deautenticação de clientes
- Injection de pacotes de *probe request*
- Forçar reassociação

---
# Análise de Dados Coletados

## 1. Interpretação de Resultados do `airodump-ng`

**Campos Importantes:**

- `BSSID`: Endereço MAC do ponto de acesso.
- `PWR`: Potência do sinal (quanto mais próximo de 0, melhor).
- `Beacons`: Número de pacotes de anúncio.
- `#Data`: Quantidade de dados transmitidos.
- `CH`: Canal de operação.
- `MB`: Velocidade máxima suportada.
- `ENC`: Tipo de criptografia
- `CIPHER`: Cipher suite utilizada.
- `AUTH`: Tipo de autenticação.
- `ESSID`: Nome da rede Wi-Fi

## 2. Identificação de Vulnerabilidades

**Identificadores de Vulnerabilidade**:

- Redes WEP (extremamente vulneráveis)
- WPS ativado (possibilidade de ataque Reaver)
- Redes abertas (sem autenticação)
- Client isolation desativado
- Power levels muito altos (possível interferência)

---
# Técnicas Avançadas

## 1. Detecção de SSIDs Ocultos

```bash
# Monitorar reassociações para revelar SSIDs Ocultos
sudo airodump-ng wlan0mon --essid-regex '.*' --showack
```

## 2. Fingerprinting de Dispositivos

```bash
# Identificar fabricante pelo OUI do MAC
curl -s "http://api.macvendors.com/AA:BB:CC"

# Usando macchanger para análise
macchanger -l | grep "AA:BB:CC"
```

## 3. Análise de Canais e Interferência

```bash
# Analisar espectro com wash
sudo wash -i wlan0mon

# Verificar congestionamento de canais
sudo airodump-ng wlan0mon --band abg
```

---
# Relatório de Reconhecimento

## 1. Estrutura do Relatório

```markdown
# Relatório de Reconhecimento Wireless

## 1. Resumo Executivo
- Total de redes detectadas: 15
- Redes vulneráveis identificadas: 3
  
## 2. Redes por Tipo de Criptografia
- WPA2: 10 redes
- WPA3: 2 redes
- WEP: 1 rede
- Open: 2 redes
  
## 3. Pontos de Acessos Críticos
- [BSSID]: AA:BB:CC:DD:EE:FF
	- SSID: Corporate-Net
	- Vulnerabilidade: WPS ativado
	- Recomendações: Desativar WPS
	  

## 4. Análise de Canais
- Canal 6: 4 redes (congestionado)
- Canal 11: 3 redes
- Canal 1: 2 redes
```

---
# Considerações Legais e Éticas

>[!warning] Conformidade Legal
>- Obter autorização por escrito antes do teste.
>- Limitar escopo às redes autorizadas.
>- Documentar todas as atividades.
>- Não alterar configurações de rede.

>[!info] Boas Práticas
>- Usar ferramentas apenas em ambiente controlado.
>- Não coletar dados pessoais.
>- Relatar vulnerabilidade de forma responsável.
>- Manter sigilo sobre informações sensíveis.

