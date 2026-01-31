2026-01-13 10:05

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# O que é Análise de Tráfego de Rede

**Análise de tráfego de rede** é o processo de **capturar, inspecionar e interpretar pacotes de dados** que trafegam em uma rede. O objetivo é entender **como a rede se comporta**, identificar **problemas, falhas de segurança, ataques e atividades suspeitas**.

Em cibersegurança, analisar tráfego significa **enxergar o que realmente está acontecendo na rede**, e não apenas confiar em logs ou alertas.

![[Pasted image 20260113101744.png]]

---
# Por que a Análise de Tráfego é Importante

A análise de tráfego é essencial para:

- Detectar ataques em tempo real
- Investigar incidentes de segurança
- Identificar malware e comunicação C2
- Diagnosticar problemas de rede
- Validar regras de firewall, IDS/IPS e ACL
- Compreender o comportamento normal da rede

Sem análise de tráfego, muitos ataques passam **completamente invisíveis**.

---
# O que é Analisado no Tráfego de Rede

Durante a análise, pode ser observados:

- Endereços IP de origem e destino
- Portas e protocolos
- Flags TCP
- Payload (quando não criptografado)
- Volume e padrão de tráfego
- Frequência de conexões

---
# Tipos de Análise de Tráfego

## 1. Análise em Tempo Real

- Monitoramento contínuo
- Uso em SOC e NOC
- Detecção imediata de ameaças

## 2. Análise Pós-Incidente (Forense)

- Análise de arquivos PCAP
- Investigação de ataques
- Reconstrução de eventos

## 3. Análise Baseada em Assinatura

- Detecta padrões conhecidos
- Muito usada em IDS/IPS

## 4. Análise Comportamental

- Detecta anomalias
- Baseada em comportamento normal

---
# Ferramentas de Análise de Tráfego

## 1. Wireshark

- Análise profunda de pacotes
- Interface gráfica
- Ideal para aprendizado e forense

Exemplo de uso:

- Analisar handshake TCP
- Identificar DNS suspeito

![[Pasted image 20260113101808.png]]

## 2. `tcpdump`

- Captura em linha de comando
- Muito usado em servidores

Exemplo:

```bash
tcpdump -i etho0 port 80
```

![[Pasted image 20260113101928.png]]

## `tshark`

- Versão CLI do Wireshark
- Ideal para automação

![[Pasted image 20260113102034.png]]

## 4. Zeek (Bro)

- Análise comportamental
- Gera logs detalhados
- Muito usado em SOC

![[Pasted image 20260113102120.png]]

## 5. Suricata / Snort

- IDS/IPS
- Análise baseada em assinaturas

## 6. Netflow / IPFIX

- Análise de fluxo
- Não inspeciona payload
- Escalável

---
# Exemplos Práticos de Análise de Tráfego

## 1. Identificar Port Scan

Indicadores:

- Muitas portas acessadas em curto período
- Mesmo IP de origem

Ferramentas:

- Wireshark
- Zeek

## 2. Detectar Comunicação com C2

Indicadores:

- Conexões periódicas
- Domínios suspeitos
- DNS anômalo

## 3. Analisar Ataque de Brute Force

Indicadores:

- Muitas tentativas de login
- Mesma origem

Protocolos comuns:

- SSH
- FTP

## 4. Diagnóstico de Problemas de Rede

Exemplos:

- Alta latência
- Retransmissões TCP
- Perda de pacotes

---
# Análise de Tráfego Criptografado

Desafios:

- HTTPS e TLS
- VPN

Soluções:

- Análise de metadados
- TLS fingerprinting
- Proxy com inspeção SSL

---
# Análise de Tráfego em Ambientes Corporativos

## Blue Team

- Detecção de ataques
- Resposta a incidentes

## Red Team

- Evasão de detecção
- Análise de defesas

---
# Erros Comuns na Análise de Tráfego

- Falta de baseline    
- Analisar sem contexto    
- Ignorar tráfego criptografado

---
# Boas Práticas

- Criar baseline da rede    
- Coletar tráfego em pontos estratégicos
- Usar múltiplas ferramentas
- Documentar análises    

---
# Conclusão

A análise de tráfego de rede é uma **habilidade fundamental em cibersegurança**, permitindo visibilidade total da rede, detecção precoce de ataques e suporte a decisões defensivas e ofensivas. Quem domina análise de tráfego entende de verdade como a rede se comporta.