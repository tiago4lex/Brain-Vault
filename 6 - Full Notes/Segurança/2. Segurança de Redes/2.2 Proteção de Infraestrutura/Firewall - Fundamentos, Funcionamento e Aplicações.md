2025-12-29 15:48

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Firewall]]

----
# Introdução

## O que é um Firewall?

Um **firewall** é um mecanismo de segurança responsável por **monitorar, filtrar e controlar o tráfego de rede**, permitindo ou bloqueando conexões com base em **regras de segurança previamente definidas**.

Ele atua como uma **barreira entre redes confiáveis e não confiáveis**, como uma rede interna e a Internet, sendo um dos **principais pilares da segurança de redes**.

![[Pasted image 20251229155034.png]]

---
# Para que serve um Firewall?

O firewall é utilizado para:

- bloquear acessos não autorizados;
- permitir apenas tráfego legítimo;
- segmentar redes internas;
- proteger servidores e estações;
- reduzir a superfície de ataque;
- apoiar políticas de segurança da informação.

---
# Em qual camada o Firewall atua?

Dependendo do tipo, o firewall pode atuar em múltiplas camadas:

- **Camada 3 (Rede):** IP
- **Camada 4 (Transporte):** TCP / UDP
- **Camada 7 (Aplicação):** HTTP, HTTPS, DNS, etc.

Firewalls modernos podem atuam em **várias camadas simulltaneamente**.

---
# Como um Firewall funciona?

Funcionamento básico:

1. Um pacote chega ao firewall
2. O firewall analisa o pacote (IP, porta, protocolo, estado, conteúdo)
3. As regras são avaliadas
4. O tráfego é permitido ou bloqueado
5. O evento pode ser registrado em logs

---
# Tipos de Firewall

## 1. Firewall de Filtragem de Pacotes

- analisa IP, porta e protocolo;
- rápido, porém limitado;
- não entende o contexto da conexão.

![[Pasted image 20251229155525.png]]

## 2. Firewall Stateful (inspeção com estado)

- acompanha o estado da conexão;
- mais seguro que filtragem simples;
- amplamente utilizado.

![[Pasted image 20251229155600.png]]

## 3. Firewall de Aplicação (Layer 7)

- inspeciona o conteúdo do tráfego;
- entende protocolos como HTTP;
- pode bloquear ataques específicos.

![[Pasted image 20251229155702.png]]

## 4. Next-Generation Firewall (NGFW)

Inclui:

- inspeção profunda de pacotes (DPI);
- IDS/IPS integrado;
- controle por aplicação;
- filtragem por usuários;
- integração com threat intelligence.

![[Pasted image 20251229155809.png]]

---
# Exemplos de Firewalls Domésticos

- Firewall do roteador residencial
- Windows Defender Firewall
- UFW (Linux)
- iptables / nftables

---
# Exemplos de Firewalls Corporativos

### Dispositivos (Hardware / Appliance)

- FortiGate (Fortinet)

![[Pasted image 20251229155919.png]]

- Palo Alto Networks

![[Pasted image 20251229155938.png]]

- Cisco ASA / Firepower

![[Pasted image 20251229155958.png]]

- Sophos XG

![[Pasted image 20251229160014.png]]

- Check Point

![[Pasted image 20251229160035.png]]

### Firewalls em Software / Open Source

- pfSense

![[Pasted image 20251229160052.png]]

- OPNsense

![[Pasted image 20251229160110.png]]

- IPFire

![[Pasted image 20251229160129.png]]

---
# Ferramentas e Tecnologias Relacionadas a Firewall

- iptables / nftables
- UFW
- firewalld
- Windows Firewall
- pf

---
# Exemplos práticos de configuração de Firewall

## 1. UFW (Linux)

Permitir SSH:

```bash
sudo ufw allow ssh
```

**Bloquear porta específica:**

```bash
sudo ufw deny 23
```

**Ativar firewall:**

```bash
sudo ufw enable
```

## 2. iptables

Permitir SSH:

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

**Bloquear tudo o resto:**

```bash
iptables -P INPUT DROP
```

## 3. Windows Firewall (PowerShell)

```bash
New-NetFirewallRule -DisplayName "Bloquear FTP" -Direction Inbound -Protocol TCP -LocalPort 21 -Action Block
```

---
# Firewall em Ambientes Corporativos

Utilizações comuns:

- DMZ;
- segmentação de rede;
- controle de tráfego entre VLANs;
- proteção de servidores críticos;
- acesso remoto seguro.

---
# Principais vulnerabilidades relacionadas a Firewall

## 1. Regras mal configuradas

- portas desnecessárias abertas;
- regras muito permissivas.

## 2. Falta de Atualização

- exploração de falhas conhecidas;
- CVEs em appliances.

## 3. Bypass de Firewall

- tunelamento;
- tráfego criptografado não inspecionado;
- uso de portas permitidas.

## 4. Falta de Monitoramento

- logs não analisados;
- ataques passam despercebidos.

---
# Ferramentas para Pentest e Avaliação de Firewall

- Nmap
- Masscan
- Hping3
- Metasploit
- Firewalk
- Wireshark

---
# Firewall e IDS/IPS

Diferença:

- Firewall: controla tráfego
- IDS: detecta ataques
- IPS: detecta e bloqueia ataques

Muitos NGFW combinam essas funções.

---
# Boas Práticas de Segurança com Firewall

- princípio do menor privilégio;
- segmentação de rede;
- revisão periódica de regras;
- logs centralizados;
- firewall interno e externo;
- integração com SIEM.

---
# Importância do Firewall na Cibersegurança

O firewall não é apenas um bloqueador de portas, mas um **componente estratégico de defesa**.

Quando corretamente configurado e monitorado, ele reduz drasticamente riscos de invasão, movimentação lateral e vazamento de dados.

---
# Conclusão

Firewalls são indispensáveis em qualquer ambiente conectado à Internet, seja doméstico ou corporativo.

Para profissionais de cibersegurança, compreender **tipos, configurações, limitações e técnicas de evasão** é essencial para atuar em **Blue Team, Red Team, SOC e arquitetura de segurança**.