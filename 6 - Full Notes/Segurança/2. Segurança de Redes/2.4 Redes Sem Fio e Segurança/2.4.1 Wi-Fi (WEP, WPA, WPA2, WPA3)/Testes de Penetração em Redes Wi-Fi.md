2025-09-03 16:07

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wi-Fi]]

----
# Introdução

Os testes de penetração em redes Wi-Fi envolver várias técnicas para avaliar a segurança de redes wireless. Aqui estão os principais tipos:

---
# 1. Reconhecimento e Enumeração

- **War Driving:** Mapeamento de redes Wi-Fi disponíveis em uma área.
- **Scanning de redes:** Identificação de SSIDs, pontos de acesso e clientes.
- **Fingerprinting:** Identificação de tipos de equipamentos e versões.

---
# 2. Quebra de Autenticação

- **Ataques a WEP:** Exploração de vulnerabilidades no protocolo WEP.
- **Ataques a WPA/WPA2:**
	- Ataques de dicionário.
	- Ataques de força bruta.
	- Ataques PMKID.
	- Ataques a WPS *(Wi-Fi Protected Setup)*
- **Ataques a WPA3:** Explorando vulnerabilidades no protocolo mais recente.

---
# 3. Ataques a Redes Enterprise

- **Ataques a EAP:** Exploração de métodos de autenticação 802.1x
- **Credential harvesting:** Captura de credenciais de usuários.
- **Ataques de certificados:** Manipulação de certificados digitais.

---
# 4. Ataques a Clientes

- **Evil Twin:** Pontos de Acesso falsos.
- **KARMA attacks:** Resposta a sondas de clientes.
- **Ataques de desautenticação:** Forçar clientes a se reconectarem.
- **Ataques a WPA3-Enterprise:** Explorando vulnerabilidades específicas.

---
# 5. Ataques de Pós-Exploração

- **Sniffing de tráfego:** Captura e análise de dados transmitidos.
- **Man-in-the-Middle:** Interceptação de comunicações.
- **Injeção de pacotes:** Manipulação do fluxo de dados.

---
# 6. Ferramentas Comuns no Kali Linux

- **Aircrack-ng suite:** Para quebra de chaves WEP/WPA
- **Wifite:** Automação de ataques a redes Wi-Fi
- **Reaver:** Ataques a WPS.
- **Hostapd-wpe:** para ataques a redes Enterprise.
- **Eaphammer:** Ataques a redes WPA2-Enterprise.
- **Kismet:** Detecção de redes e análise de tráfego.

---
# 7. Testes Avançados

- **Ataques a protocolos específicos:** 802.11r, 802.11w
- **Ataques a redes mesh**.
- **Exploração de vulnerabilidades em implementações específicas**.
- **Ataques a IoT devices via Wi-Fi**.