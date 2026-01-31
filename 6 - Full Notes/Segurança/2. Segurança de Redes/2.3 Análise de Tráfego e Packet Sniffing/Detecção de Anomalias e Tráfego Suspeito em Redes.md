2026-01-14 18:30

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wireshark]]

----
# Introdução

**Detecção de anomalias** é o processo de identificar padrões de tráfego que **fogem do comportamento normal esperado** de uma rede, sistema ou aplicação. Diferente da detecção por assinatura (que busca algo conhecido), a detecção de anomalias foca no **inesperado**.

Em cibersegurança, isso é essencial para detectar:

- ataques novos ou desconhecidos (zero-day);
- movimentação lateral;
- comprometimentos silenciosos;
- uso indevido de recursos.

---
# O que é Tráfego Normal vs Tráfego Anômalo

## Tráfego Normal

- Padrões previsíveis
- Horários regulares
- Protocolos esperados
- Volume concistente

## Tráfego Anômalo

- Comportamento fora do padrão
- Volume incomum
- Protocolos inesperados
- Frequência irregular

A base da detecção de anomalias é o **baseline** da rede.

---
# Baseline de Rede

Um **baseline** é um perfil de comportamento normal da rede.

Inclui:

- horários de pico;
- protocolos mais usados;
- portas comuns;
- IPs frequentes;
- volume médio de tráfego.

Sem baseline, não existe detecção de anomalias confiável.

---
# Tipos de Anomalias de Tráfego.

## 1. Anomalias de Volume

- Pico repentino de tráfego
- Consume excessivo de banda

Exemplos:

- DDoS
- Exfiltração de dados

## 2. Anomalias de Frequência

- Muitas conexões em curto período

Exemplos:

- Port scan
- Brute force

## 3. Anomalias de Protocolo

- Uso de protocolos inesperados
- Protoccolos fora de contexto

Exemplos:

- ICMP excessivo
- DNS usado para tunelamento

## 4. Anomalias de Porta

- Portas incomuns
- Serviços não autorizados

Exemplos:

- Backdoors
- Malware

## 5. Anomalias Comportamentais

- Comunicação periódica
- Padrões automatizados

Exemplos:

- C2 *(Command and Control)*

---
# Indicadores Comuns de Tráfego Suspeito

- Muitas conexões SYN sem ACK
- Repetição de falhas de autenticação
- Sessões muito longas
- DNS com nomes aleatórios
- Tráfego fora do horário comercial

---
# Detecção de Anomalias no Wireshark

O Wireshark é uma ferramenta poderosa para análise manual de anomalias

## Filtros de Wireshark para Identificação de Anomalias

### 1. Detectar Port Scan (SYN Scan)

```bash
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Indicadores:

- Muitos SYN
- Poucos ACK

### 2. Detectar Possível DDoS

```bash
ip.dst == X.X.X.X
```

Observe:

- Muitas origens diferentes
- Mesmo destino

### 3. Identificar Brute Force SSH

```bash
tcp.port == 22
```

Combine com:

- Alta frequência
- Repetição de conexões

### 4. DNS Suspeito (Possível Tunelamento)

```bash
dns && strlen(dns.qry.name) > 50
```

Indicadores:

- Nomes longos
- Caracteres aleatórios

### 5. Tráfego ICMP Excessivo

```bash
icmp
```

Analise:

- Volume
- Frequência

### 6. Conexões TCP Incompletas

```bash
tcp.analysis.flags
```

Indicadores:

- Retransmissões
- Resets

---
# Análise de Anomalias em Tráfego Criptografado

Mesmo sem ver o payload, é possível detectar anomalias analisando:

- tamanho de pacotes;
- frequência
- destinos;
- tempo entre conexões.

---
# Ferramentas Automatizadas de Detecção de Anomalias

- Zeek (logs comportamentais)
- Suricata (IDS/IPS híbrido)
- SIEMs (correlação)
- Machine Learning

---
# Detecção de Anomalias em SOC

Fluxo típico:

1. Coleta de tráfego
2. Criação de baseline
3. Detecção de desvios
4. Alerta
5. Investigação
6. Resposta

---
# Erros Comuns

- Falta de baseline
- Muitos falsos positivos
- Análise sem contexto
- Ignorar horário e função do ativo

---
# Boas Práticas

- Conhecer o ambiente
- Combinar análise manual e automatizada
- Usar múltiplas fontes de dados
- Documentar padrões normais

---
# Conclusão

A detecção de anomalias e tráfego suspeito é uma das **habilidades mais importantes em cibersegurança moderna**, permitindo identificar ameaças avançadas que passam despercebidas por mecanismos tradicionais baseados apenas em assinaturas.