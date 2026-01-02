2026-01-02 13:21

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

**Segmentação de redes** é a prática de dividir uma rede maior em **sub-redes menores e isoladas**, com o objetivo de melhorar **segurança, desempenho, controle de acesso e gerenciamento**. Cada segmento possui regras específicas de comunicação, reduzindo a superfície de ataque.

Ideia central:

> Nem todo dispositivo de falar com todo mundo.

---
# Por que segmentar redes é importante?

Principais benefícios:

- Redução do impacto de ataques
- Contenção de movimentação lateral
- Melhor controle de acesso
- Menor broadcast
- Conformidade com normas de segurança

Em cibersegurança, segmentação é uma das **medidas defensivas mais eficazes.**

---
# Segmentação vs Isolamento

- **Segmentação**: comunicação controlada entre redes
- **Isolamento**: comunicação totalmente bloqueada

Exemplo:

- Usuários ↔ Servidores (segmentado)
- Usuários ↔ Ambiente crítico (isolado)

---
# Tipos de Segmentação de Redes

## 1. Segmentação Física

- Uso de switches, roteadores e cabos diferentes
- Alta segurança
- Alto custo

Exemplo:

- Rede administrativa separada fisicamente da rede de visitantes

## 2. Segmentação Lógica

- Usa VLANs e sub-redes
- Mais comum em ambientes corporativos
- Flexível e escalável

Exemplo:

- VLAN 10 → Usuários
- VLAN 20 → Servidores

## 3. Segmentação por Sub-Rdes *(Subnetting)*

- Divisão do endereço IP
- Reduz broadcast
- Facilita controle

## 4. Microsegmentação

- Segmentação extremamente granular
- Baseada em identidade e aplicação
- Muito usada em ambientes cloud e Zero Trust

---
# Tecnologias Utilizadas na Segmentação

- VLAN (802.1Q)
- Subnetting
- Firewall
- ACL
- VPN
- SDN *(Software Defined Networking)*

---
# Segmentação e Camadas OSI

- Camada 2 → VLAN
- Camada 3 → Roteamento e Sub-redes
- Camada 4–7 → Firewall e políticas avançadas

---
# Exemplos de Segmentação na Prática

## 1. Segmentação Básica em uma Empresa

| **Segmento** | **Função** |
| ------------ | ---------- |
| VLAN 10      | Usuários   |
| VLAN 20      | Servidores |
| VLAN 30      | DMZ        |
| VLAN 40      | Visitantes |

## 2. Segmentação com Firewall

- Usuários → Internet (permitido)
- Usuários → Servidores (restrito)
- Visitantes → Internet (permitido)
- Visitantes → Rede interna (bloqueado)

---
# Segmentação e DMZ

A **DMZ (Zona Desmilitarizada)** é um segmento intermediário entre a rede interna e a internet.

Serviços comuns na DMZ:

- Web server
- Mail server
- DNS público

Objetivo:

> Proteger a rede interna caso o servidor exposto seja comprometido.

---
# Segmentação em Cibersegurança

## 1. Defesa (Blue Team)

- Conter ransomware
- Reduzir movimento lateral
- Limitar acesso privilegiado

## 2. Ataque (Red Team)

- Bypass de segmentação
- Pivoting entre redes
- Enumeração de rotas

---
# Erros comuns de segmentação

- Permitir comunicação irrestrita entre VLANs
- Firewall permissivo demais
- Falta de logs
- Excesso de regras genéricas

---
# Ferramentas Relacionadas

- Firewalls (pfSense, FortiGate)
- Switches gerenciáveis
- iptables / nftables
- Nmap
- Wireshark

---
# Segmentação em Cloud

- VPC (AWS)
- VNets (Azure)
- Security Groups
- Network ACLs

---
# Boas Práticas de Segmentação

- Princípio do menor privilégio
- Documentar a topologia
- Revisar regras periodicamente
- Monitorar tráfego entre segmentos    

---

# Conclusão

Segmentação de redes é um **pilar da segurança moderna**, essencial para reduzir riscos, conter ataques e estruturar redes resilientes tanto em ambientes **on-premise** quanto **cloud**.