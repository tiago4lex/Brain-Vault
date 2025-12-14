2025-09-23 05:16

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[IoT]] | [[Man in The Middle]] | [[Wireshark]]

----
## **Introdução**

**Objetivo:** Capturar e analisar o tráfego de rede entre o app Android do smartwatch e seus servidores remotos.

**Arquitetura:**

```text
Smartwatch → App → Android → Router (Kali MITM) → Internet
```

---
## **Ferramentas Necessárias**

### Software Principal:

- **Kali Linux** (sistema principal)
- **Android Studio** (para emulador Android)
- **Wireshark** (análise de pacotes)
- **mitmproxy** (proxy MITM)
- **Burp Suit** (opcional para análise adicional)

### Hardware:

- Computador com Kali Linux
- Smartwatch físico
- Rede Wi-Fi para conectividade

---
## **Fase 1: Configuração do Ambiente Kali Linux**

### 1. Atualização do Sistema

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wireshark mitmproxy android-tools-adb
```

### 2. Configurar Wireshark para Captura

```bash
# Adicioanr usuário ao grupo wireshark
sudo usermod -aG wireshark $USER
newgrp wireshark

# Verificar permissões
wireshark --version
```

---
## **Fase 2: Configuração do Emulador Android**

### 1. Instalar Android Studio

```bash
# Download do Android Studio
wget https://redirector.gvt1.com/edgedl/android/studio/ide-zips/2023.3.1.19/android-studio-2023.3.1.19-linux.tar.gz
tar -xzf android-studio-*.tar.gz
cd android-studio/bin
./studio.sh
```

### 2. Criar AVD *(Android Virtual Device)*

1. Abra o Android Studio
2. Vá em **More Actions → Virtual Device Manager**

![[Imagem do WhatsApp de 2025-09-23 à(s) 05.42.51_39cde3eb.jpg]]

3. Clique em **Create Device**

![[Imagem do WhatsApp de 2025-09-23 à(s) 05.43.52_b446ce18.jpg]]

4. Escolha um dispositivo com **Play Store**

![[Imagem do WhatsApp de 2025-09-23 à(s) 05.45.46_2218ecb0.jpg]]

5. Selecione imagem com API nível 30+ (Android 11+)

![[Imagem do WhatsApp de 2025-09-23 à(s) 05.48.03_b551066b.jpg]]

6. Configure 4GB RAM e armazenamento suficiente

![[Imagem do WhatsApp de 2025-09-23 à(s) 05.50.56_0bb9e551.jpg]]

### 3. Configurar Emulador para Proxy

```bash
# Listar dispositivos Android
emulator -list-avds

# Iniciar emulador com proxy
emulator -avd NOME_DO_SEU_AVD -writable-system -http-proxy http://127.0.0.1:8080
```

>[!note] Nota:
>Talvez seja necessário instalar o pacote do `emulator` no sistema, caso não o tenha.

---
## **Fase 2: Configuração MITM**

### 1. Configurar MITMproxy

```bash
# Iniciar mimtmproxy em modo transparante
sudo mitmproxy --mode transparent --showhost

# Em outro terminal, configurar redirecionamento de porta
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 443 -j REDIRECT --to-port 8080
```

### 2. Configurar Proxy no Emulator

```bash
# Configurar proxy via ADB
adb shell settings put global http_proxy 192.168.1.100:8080

# Verificar configuração
adb shell settings get global http_proxy
```

---
## **Fase 4: Captura Wireshark**

