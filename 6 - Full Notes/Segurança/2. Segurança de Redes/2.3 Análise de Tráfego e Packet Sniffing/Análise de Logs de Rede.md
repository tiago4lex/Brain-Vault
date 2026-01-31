2026-01-14 18:49

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

**Análise de logs de rede** é o processo de coletar, correlacionar e interpretar registros gerados por dispositivos e serviços de rede para **indentificar eventos de segurança, falahs operacionais e comportamentos suspetiso**.

Logs são evidências. Eles mostram **o que aconteceu, quando, de onde, como e em muitos casos por quem**.

---
# Por que Logs de Rede são tão importantes?

A análise de logs é essencial para:

- Detecção de ataques
- Investigação de incidentes (DFIR)
- Auditoria e compliance
- Validação de controles de segurança
- Criação de alertas e correlações

Sem logs, **não existe visibilidade nem investigação confiável**.

---
# Principais Fontes de Logs de Rede

## 1. Firewalll

Registra:

- conexões permitidas/bloqueadas
- IP de origem e destino
- portas e protocolos

## 2. IDS / IPS

Registra:

- assinaturas detectadas
- tentativas de ataque
- severidade do evento

## 3. Roteadores e Switches

Registra:

- eventos de interface
- mudanças de rota
- erros de rede

## 4. Servidores DNS

Registra:

- consultas de domínio
- origem de requisição
- resposta DNS

## 5. Servidores Proxy

Registra:

- URLs acessadas
- usuários
- tempo de conexão

## 6. VPN

Registra:

- login/logout
- IP atribuído
- falhas de autenticação

---
# Estruturas Comuns de um Log de Rede

Campos frequentes:

- timestamp (data e hora)
- origem (IP/host)
- destino (IP/host)
- ação (permitir/bloquear)
- protocolo
- mensagem

Exemplo:

```text
2026-01-10 10:15:22 ALLOW TCP 192.168.1.10:52344 -> 10.0.0.5:22
```

---
# Tipos de Eventos Observados em Logs

- Conexões permitidas
- Conexões bloqueadas
- Falhas de autenticação
- Mudanças de configuração
- Alertas de segurança

---
# Análise Manual de Logs

Etapas básicas:

1. Coletar logs
2. Filtrar eventos relevantes
3. Correlacionar horários e IPs
4. Identificar padrões
5. Tirar conclusões

---
# Exemplos Práticos de Análise de Logs

## 1. Detecção de Brute Force SSH

Indicadores:

- muitas falhas de login
- mesmo IP de origem

Logs comuns:

- firewall
- servidor SSH

## 2. Detecção de Port Scan

Indicadores:

- várias portas acessadas    
- curto intervalo de tempo

Logs comuns:

- firewall
- IDS

## 3. Comunicação Suspeita DNS

Indicadores:

- domínios aleatórios
- muitas consultas

## 4. Uso Indevido de VPN

Indicadores:

- login fora do horário
- múltiplos IPs

---
# Correlação de Logs

A correlação consiste em **ligar eventos de diferentes fontes**.

Exemplo:

- firewall bloqueia IP
- IDS gera alerta
- servidor registra falha

Isso aumenta a confiança da detecção.

---
# Ferramentas para Análise de Logs

## 1. Ferramentas Locais

- grep / awk
- journalctl
- ELK Stack (Elasticsearch, Logstash, Kibana)

## 2. SIEM

- Splunk
- Wazuh
- QRadar

Funções:

- centralização
- correlação

---
# Logs e Detecção de Anomalias

Logs permitem identificar:

- padrões normais
- desvios
- comportamentos anormais

Logs complementam a análise de tráfego.

---
# Desafios na Análise de Logs

- grande volume de dados
- falsos positivos
- falta de padronização
- sincronização de tempo

---
# Boas Práticas

- centralizar logs 
- sincronizar NTP
- definir retenção
- proteger integridade dos logs
- revisar periodicamente

---
# Logs em Ambientes Corporativos e SOC

Fluxo típico:

1. coleta
2. normalização
3. correlação
4. alerta
5. resposta

---
# Logs, Tráfego e Segurança

- tráfego mostra _como_
- logs mostram _o que_

Os dois juntos dão visibilidade completa.

---
# Conclusão

A análise de logs de rede é uma **habilidade essencial em cibersegurança**, permitindo detecção, investigação e resposta a incidentes. Quem domina logs consegue reconstruir ataques e fortalecer defesas com precisão.