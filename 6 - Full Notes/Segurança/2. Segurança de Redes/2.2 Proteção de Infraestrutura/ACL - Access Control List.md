2026-01-01 21:13

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[ACLs]]

----
# Introdução

A **ACL *(Access Control List)*** é um mecanismo de segurança utilizado para **controlar quem pode acessar quais recursos**, definindo permissões explícitas de **permitir ou negar** ações com base em critérios como IP, protocolo, porta, usuário ou tipo de tráfego.

AS ACLs são amplamente utilizadas em **redes, sistemas operacionais, firewalls, roteadores, switches e aplicações**, sendo um dos conceitos mais fundamentais da segurança da informação.

![[Pasted image 20260101211736.png]]

---
# Para que serve uma ACL?

Uma ACL é usada para:

- controlar acesso a recursos de rede;
- restringir comunicação entre hosts;
- aplicar políticas de segurança;
- segmentar redes;
- reduzir superfície de ataque;
- apoia compliance e auditoria.

---
# Em qual camada a ACL atua?

Dependendo do contexto, a ACL pode atuar em diferentes camadas:

- **Camada 3 (Rede):** endereços IP
- **Camada 4 (Transporte):** TCP/UDP e portas
- **Camada 7 (Aplicação):** usuários, métodos, URLs

---
# Como funciona uma ACL?

Funcionamento básico:

1. Um pacote ou requisição chaga ao dispositivo
2. As regras da ACL são avaliadas **em ordem**
3. A primeira regra correspondente é aplicada
4. O tráfego é permitido ou negado
5. Se nenhuma regra casar, aplica-se a regra implícita (deny all)

---
# Conceitos fundamentais de ACL

## 1. Ordem das Regras

- regras são lidas de cima para baixo;
- a primeira correspondência é aplicada;
- ordem incorreta gera falhas de segurança.

## Regra Implícita (Deny All)

- todo tráfego não permitido explicitamente é bloqueado;
- princípio do menor privilégio.

---
# Tipos de ACL

## 1. ACL Padrão *(Standard ACL)*

- filtra apneas endereço IP de origem;
- controle básico;
- pouco granular.

## 2. ACL Estendida *(Extended ACL)*

- filtra IP de origem e destino;
- portas e protocolos;
- muito mais granular.

## 3. ACL Baseada em Tempo

- regras válidas apenas em horários específicos;
- útil para controle administrativo.

## 4. ACL Baseada em Aplicação

- URLs, métodos HTTP;
- comum em firewalls L7 e WAF.

---
# Exemplos de ACL em Diferentes Ambientes

## 1. ACL em Roteadores e Switches

Usada para:

- filtrar tráfego entre redes;
- bloquear protocolos;
- proteger dispositivos.

## 2. ACL em Firewalls

- define política de segurança;
- controla entrada e saída;
- base para regras de firewall.

## 3. ACL em Sistemas Operacionais

- permissões de arquivos e diretórios;
- controle de usuários e grupos.

## 4. ACL em Cloud

- AWS Security Groups e NACLs;
- Azure NSG;
- Google VPC Firewall Rules.

---
# Exemplos Práticos de Configuração de ACL

## 1. Exemplo Conceitual de ACL de Rede

- permitir HTTP da rede interna;
- negar acesso externo ao servidor.

## 2. ACL no Linux (iptables)

```bash
iptables -A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

## 3. ACL no Windows Firewall

```bash
New-NetFirewallRule -DisplayName "Permitir HTTP Interno" -Direction Inbound -Protocol TCP -LocalPort 80 -RemoteAddress 192.168.1.0/24 -Action Allow
```

---
# ACL e Princípio do Menor Previlégio

- conceder apenas o acesso necessário;
- reduzir impacto de comprometimentos;
- facilitar auditorias.

---
# Vulnerabilidades e Problemas Comuns em ACL

## 1. Regras muito permissivas

- uso excessivo de ANY;
- portas abertas desnecessariamente.

## 2. Ordem incorreta das regras

- regras específicas após regras genéricas;
- falhas de bloqueio.

## 3. Falta de revisão periódica

- regras obsoletas;
- acessos não justificados.

## 4. ACL excessivamente complexa

- difícil manutenção;
- erros humanos.

---
# Ferramentas para Auditoria e Teste de ACL

- Nmap
- Firewalk
- Hping3
- Wireshark
- Tufin
- AlgoSec

---
# ACL em Arquiteturas de Segurança

Usada em conjunto com:

- Firewall
- IDS/IPS
- WAF
- SIEM
- Segmentação de rede

---
# Boas Práticas de uso de ACL

- documentar regras;
- revisar periodicamente;
- aplicar menor privilégio;
- usar nomenclatura clara;
- testar antes de produção.    

---

# Importância da ACL na Cibersegurança

ACLs são a **base do controle de acesso** em redes e sistemas.

Uma ACL bem definida reduz drasticamente riscos de acesso indevido, movimentação lateral e vazamento de dados.

---
# Conclusão

A Access Control List é um conceito simples, porém extremamente poderoso.

Quando bem projetada, implementada e mantida, a ACL fortalece toda a arquitetura de segurança, sendo essencial para profissionais de **redes, SOC, Blue Team e arquitetura de segurança**.