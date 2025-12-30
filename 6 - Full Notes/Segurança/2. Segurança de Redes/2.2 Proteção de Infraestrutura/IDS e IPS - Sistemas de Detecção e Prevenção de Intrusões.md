2025-12-30 08:14

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[IDS/IPS]]

----
# Introdução

**IDS *(Intrusion Detection System)*** e **IPS *(Intrusion Prevention System)*** são mecanismos de segurança projetados para **detectar, analisar e responder a atividades maliciosas** em redes e sistemas.

Enquanto o IDS tem foco em **detecção e alerta**, o IPS atua de forma **ativa**, bloqueando ataques em tempo real. Ambos são componentes essenciais em arquiteturas modernas de segurança.

![[Pasted image 20251230081823.png]]

---
# Diferença entre IDS e IPS

| **Característica** | **IDS**       | **IPS**             |
| ------------------ | ------------- | ------------------- |
| Função principal   | Detectar      | Detectar e bloquear |
| Ação automática    | Não           | Sim                 |
| Risco de impacto   | Baixo         | Médio/Alto          |
| Posicionamento     | Fora do fluxo | Em linha *(inline)* |

---
# Em qual camada IDS e IPS atuam?

- **Camada 3 (Rede):** análise de IP
- **Camada 4 (Transporte):** TCP/UDP
- **Camada 7 (Aplicação):** HTTP, DNS, SMB

Soluções modernas realizam **inspeção profunda de pacotes (DPI)**.

---
# Tipos de IDS e IPS

## 1. NIDS / NIPS (Network-based)

- monitora tráfego de rede;
- detecta ataques como scans, DoS exploits;
- comum em perímetros e data centers.

## 2. HIDS / HIPS (Host-based)

- instalado em servidores ou endpoints;
- monitora logs, arquivos e processos;
- detecta alterações suspeitas.

## 3. IDS/IPS Baseado em Wireless

- monitora redes Wi-Fi;
- detecta roque APs;
- ataques de deauth e spoofing.

---
# Como o IDS e IPS funcionam?

Fluxo básico:

1. Captura de tráfego ou eventos
2. Análise (assinatura, comportamento ou heurística)
3. Correlação de dados
4. Geração de alerta (IDS) ou bloqueio (IPS)
5. Registro em logs

---
# Métodos de Detecção

## 1. Detecção por Assinatura

- compara padrões conhecidos;
- rápido e preciso;
- não detecta zero-day.

## 2. Detecção por Anomalia

- identifica desvios de comportamentos normal;
- detecta ataques desconhecidos;
- pode gerar falsos positivos.

## 3. Detecção Heurística / Comportamental

- analisa comportamento e contexto;
- usado em soluções avançadas;
- exige tuning.

---
# Exemplos de Ataques Detectados por IDS/IPS

- Port Scan
- Brute Force
- SQL Injection
- Cross-Site Scripting (XSS)
- Buffer Overflow
- Malware
- DoS / DDoS

---
# Ferramentas IDS/IPS

## Open Source

- Snort
- Suricata
- Zeek (Bro)
- OSSEC
- Wazuh

## Comerciais

- Cisco Firepower
- Palo Alto NGFW
- FortiGate IPS
- Check Point IPS
- Trend Micro

---
# Posicionamento em Arquiteturas de Rede

Locais comuns:

- perímetro de rede;
- DMZ;
- entre VLANs;
- ambientes cloud;
- servidores críticos.

---
# IDS/IPS em Firewalls NGFW

Firewalls de próxima geração integram:

- firewall tradicional;
- IDS/IPS;
- antivírus;
- controle por aplicação;
- inspeção SSL.

---
# Principais vulnerabilidades e limitações

## 1. Falsos Positivos

- bloqueio de tráfego legítimo;
- impacto em produção.

## 2. Evasão de IDS/IPS

- fragmentação de pacotes;
- ofuscação;
- criptografia SSL.

## 3. Assinaturas Desatualizadas

- falha na detecção de ameaças recentes.

## 4. Performance

- alto consumo de recursos;
- latência em ambientes inline.

---
# Ferramentas para Testar IDS/IPS (Pentest)

- Nmap
- Metasploit
- Hping3
- Scapy
- Slowloris
- LOIC / HOIC (ambiente controlado)

---
# IDS/IPS em Ambientes Cloud

- AWS GuardDuty
- Azure Defender
- Google Cloud IDS

Integração com SIEM e SOAR.

---
# Boas Práticas de Uso

- tuning de regras;
- atualização constante;
- monitoramento contínuo;
- integração com SIEM;
- segmentação de rede;
- testes regulares.

---
# Importância de IDS e IPS na Cibersegurança

IDS e IPS aumentam significativamente a **visibilidade e capacidade de resposta** a ataques.

Eles não substituem firewalls, mas **complementam a defesa em profundidade**.

---
# Conclusão

IDS e IPS são componentes críticos de qualquer arquitetura de segurança madura.

Para profissionais de cibersegurança, dominar sua configuração, limitações e técnicas de evasão é essencial para atuar em **SOC, Blue Team, Red Team e Engenharia de Segurança**.