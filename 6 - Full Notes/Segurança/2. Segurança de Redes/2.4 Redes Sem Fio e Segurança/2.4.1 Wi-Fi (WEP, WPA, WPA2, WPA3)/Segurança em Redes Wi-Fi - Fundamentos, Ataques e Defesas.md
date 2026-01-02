2026-01-02 13:35

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wi-Fi]]

----
# Introdução

Redes **Wi-Fi** utilizam ondas de rádio para transmitir dados, o que significa que o tráfego **pode ser capturado por qualquer pessoa dentro do alcance do sinal**. Por isso, segurança em redes sem fio é um tema crítico em ambientes domésticos, corporativos e públicos.

A segurança Wi-Fi envolve:

- Autenticação
- Criptografia
- Controle de acesso
- Monitoramento

---
# Como funciona uma rede Wi-Fi?

Componentes básicos:

- **Access Point (AP):** ponto de acesso sem fio
- **Cliente:** notebook, celular, IoT
- **SSID:** nome da rede
- **Canal:** frequência usada (2.4 GHz / 5 GHz / 6 GHz)

Fluxo básico:

```text
cliente → autenticação → associação → troca de dados
```

---
# Padrões Wi-Fi (IEEE 802.11)

Principais padrões:

- 802.11b/g/n → 2.4 GHz
- 802.11a/ac → 5 GHz
- 802.11ax (Wi‑Fi 6 / 6E)

Cada evolução melhora desempenho e segurança.

---
# Tipos de Segurança Wi-Fi

## Rede Aberta (Open)

- Sem senha
- Sem criptografia
- **Altamente insegura**

## WEP (Obsoleto)

- Criptografia fraca
- Facilmente quebrável
- Não deve ser usado

## WPA

- Melhoria sobre WEP
- Ainda vulnerável

## WPA2

- Usa AES-CCMP
- Muito difundido
- Pode ser vulnerável a ataques de força bruta

## WPA3

- Mais seguro
- Proteção contra brute force offline
- Forward secrecy

---
# Métodos de Autenticação

## 1. WPA2/WPA3-PSK (Senha Compartilhada)

- Usada em casas e pequenas empresas
- Segurança depende da força da senha

## 2. WPA2/WPA3-Enterprise (802.1X)

- Usa servidor RADIUS
- Autenticação individual por usuário
- Muito mais seguro

---
# Principais Ataques em Redes Wi-Fi

## 1. Sniffing

- Captura de pacotes
- Comum em redes abertas

## 2. Ataque de Deauth

- Força desconexão de clientes
- Usada para capturar handshake

## 3. Brute Force / Dictionary Attack

- Tentativa de descobrir a senha
- Explora senhas fracas

## 4. Evil Twin

- AP falso imitando o legítimo
- Roubo de credenciais

## 5. KRACK

- Explora falhas no WPA2
- Afeta reuso de chaves

---
# Ferramentas usadas em ataques Wi-Fi (Pentest)

- aircrack‑ng
- airodump‑ng
- aireplay‑ng
- reaver (WPS)
- wifite
- hcxdumptool

---
# Ferramentas de defesa e monitoramento

- WIDS / WIPS
- IDS/IPS wireless
- Logs de AP
- Detecção de Rogue AP

---
# Segurança Wi-Fi em Ambientes Corporativos

Boas práticas:

- WPA3‑Enterprise
- 802.1X + RADIUS
- Segmentação de redes (VLAN)
- Rede separada para convidados
- Monitoramento contínuo

---
# Segurança Wi-Fi Doméstica

Recomendações:

- Usar WPA3 ou WPA2‑AES
- Senhas fortes
- Desativar WPS
- Atualizar firmware
- Ocultar gerenciamento remoto

---
# Wi-Fi e Segmentação de Redes

- Wi‑Fi corporativo ≠ Wi‑Fi convidados
- IoT em VLAN separada
- Integração com firewall e ACL

---
# Wi-Fi e IDS/IPS

- Detecção de ataques wireless
- Identificação de APs maliciosos
- Bloqueio automático (WIPS)

---
# Vulnerabilidades Comuns

- Senhas fracas
- Firmware desatualizado
- WPS habilitado
- Falta de monitoramento

---
# Boas Práticas

- Princípio do menor privilégio
- Auditorias periódicas
- Monitorar espectro RF
- Educação dos usuários

---
# Conclusão

Segurança em redes Wi‑Fi é um **ponto crítico da cibersegurança moderna**, exigindo boas configurações, monitoramento contínuo e entendimento dos ataques para garantir **confidencialidade, integridade e disponibilidade** das comunicações sem fio.