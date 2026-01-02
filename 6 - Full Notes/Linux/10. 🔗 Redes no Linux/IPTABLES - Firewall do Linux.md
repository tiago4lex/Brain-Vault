2026-01-01 21:33

Status: #developed #Linux 

Tags: [[Linux]] | [[Redes de Computadores]] | [[Firewall]] | [[CyberSecurity]]

----
# Introdução

**IPTABLES** é o firewall padrão do kernel do Linux, um utilitário de espaço do usuário que permite configurar as tabelas de filtragem de pacotes fornecidas pelo framework Netfilter do kernel Linux. Ele funciona como um firewall com estado (stateful), permitindo controle granular sobre o tráfego de rede.

![[Pasted image 20260101213543.png]]
## Histórico e Contexto

- Desenvolvido como parte do projeto Netfilter
- Presente na maioria das distribuições Linux
- Interface principal para manipular regras de firewall
- Suporta IPv4 (iptables) e IPv6 (ip6tables)

---
# Arquitetura e Conceitos Fundamentais

## Fluxo de Pacotes no Netfilter

```text
PREROUTING -> ROUTING DECISION -> FORWARD -> POSTROUTING
      ↓                              ↓
    INPUT                          OUTPUT
      ↓                              ↓
	[Local]                        [Local]
	Process                        Process
```

## Componentes Principais

1. **Tabelas:** Conjuntos de regras para propósitos específicos
2. **Cadeias *(Chains)*:** Pontos de decisão no fluxo de pacotes
3. **Regras:** Instruções individuais de filtragem
4. **Alvos *(Targets)*:** Ações a serem tomadas quando uma regra corresponde

---
# Tabelas e Cadeias *(Chains)*

## Tabelas Disponíveis

- **filter (padrão):**
	- Filtragem básica de pacotes
	- Cadeias: INPUT, FORWARD, OUTPUT

- **NAT *(Network Address Translation)*:**
	- Modificação de endereços de origem/destino
	- Cadeias: PREROUTING, OUTPUT, POSTROUTING

- **mangle:**
	- Modificação especial de pacotes (TTL, TOS, etc.)
	- Cadeias: PREROUTING, INPUT, FORWARD, OUTPUT, POSTROUTING

- **raw:**
	- Configuração de isenção de conexões do rastreamento de conexão
	- Cadeias: PREROUTING, OUTPUT

- **security (SELinux):**
	- Marcadores de segurança para SELinux
	- Cadeias: INPUT, OUTPUT, FORWARD

## Cadeias e seus pontos no fluxo

| **Cadeia**  | **Ponto no Fluxo**               | **Função Principal**           |
| ----------- | -------------------------------- | ------------------------------ |
| PREROUTING  | Imediatamente após chegada       | NAT de destino, raw, mangle    |
| INPUT       | Após roteamento para host local  | Filtragem para serviços locais |
| FORWARD     | Para pacotes atravessando o host | Filtragem de roteamento        |
| OUTPUT      | Para pacotes gerados localmente  | Filtragem de saída local       |
| POSTROUTING | Imediamente antes de sair        | NAT de origem, mangle          |

---
# Sintaxe Básica do Comando

## Estrutura Geral

```bash
iptables [-t tabela] COMANDO [cadeia] [critérios] -j ALVO [opções]
```

## Elementos da Sintaxe

- `tablea`: Especifica qual tabela usar (padrão: filter)
- `COMANDO`: Ação a realizar (ex: `-A`, `-D`, `-I`)
- `cadeia`: Cadeia da tabela (ex: `INPUT`, `OUTPUT`, `FORWARD`)
- `critérios`: Condições para correspondência (ex.: `-p`, `-s`, `-d`)
- `-j ALVO`: Ação a tomar se corresponder (ex.: `ACCEPT`, `DROP`, `REJECT`)
- `opções`: Opções adicionais específicas do alvo

---
# Comandos e Opções Detalhadas

## 1. Comandos de Manipulação de Regras

### `-A`, `--append`

Adiciona regra ao final da cadeia

```bash
iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT
```

### `-I`, `--insert`

Insere regras em posição específica (padrão: início)

```bash
iptables -I INPUT 3 -s 10.0.0.5 -j DROP # Insere na posição 3
```

### `-D`, `--delete`

Remove regra específica

```bash
iptables -D INPUT -s 192.168.1.100 -j DROP
iptables -D INPUT 2 # Remove a 2ª regra da cadeia INPUT
```

### `-R`, `--replace`

Substitui regra existente

```bash
iptables -R INPUT 2 -s 192.168.1.0/24 -j ACCEPT
```

### `-L`, `--list`

Lista regras na cadeia

```bash
iptables -L  # Lista todas as cadeias da tabela filter
iptables -t nat -L  # Lista tabela nat
iptables -L INPUT -v  # Lista com informações verbosas
iptables -L --line-numbers  # Mostra números de linha
```

### `-F`, `--flush`

Remove todas as regras da cadeia

```bash
iptables -F INPUT  # Limpa cadeia INPUT
iptables -F  # Limpa todas as cadeias da tabela atual
```

### `-Z`, `--zero`

Zera contadores de pacotes e bytes

```bash
iptables -Z  # Zera todos os contadores
iptables -Z INPUT 2  # Zera contador da regra 2 da cadeia INPUT
```

### `-N`, `--new-chain`

Cria nova cadeia definida pelo usuário

```bash
iptables -N LOG_DROP
```

### `-X`, `--delete-chain`

Remove cadeia definida pelo usuário

```bash
iptables -X LOG_DROP
```

### `-P`, `--policy`

Define política padrão para cadeia

```bash
iptables -P INPUT DROP
```

## 2. Opções de Correspondência *(Match Criteria)*

### Especificações de Endereços

```bash
-s, --source       # Endereço/IP de origem
-d, --destination  # Endereço/IP de destino
-i, --in-interface # Interface de entrada
-o, --out-interface # Interface de saída
```

### Protocolos

```bash
-p, --protocol     # Protocolo (tcp, udp, icmp, all)
```

### Portas (para TCP/UDP)

```bash
--sport, --source-port      # Porta de origem
--dport, --destination-port # Porta de destino
--port                      # Ambas as portas (origem e destino)
```

### Estado da Conexão

```bash
--sport, --source-port      # Porta de origem
--dport, --destination-port # Porta de destino
--port                      # Ambas as portas (origem e destino)
```

### Módulos de Correspondência Comuns

```bash
-m multiport                # Múltiplas portas
-m limit                    # Limitação de taxa
-m mac                      # Endereço MAC
-m time                     # Restrição por tempo
-m string                   # Correspondência de string
-m recent                   # Bloqueio baseado em atividade recente
-m connlimit                # Limite de conexões
```

## 3. Alvos *(Targets)*

### Ações Básicas

```bash
-j ACCEPT    # Aceita o pacote
-j DROP      # Descarta silenciosamente
-j REJECT    # Rejeita com mensagem de erro
-j RETURN    # Retorna à cadeia chamadora
```

### Ações Especiais

```bash
-j LOG       # Registra no log do kernel
-j DNAT      # Destination NAT
-j SNAT      # Source NAT
-j MASQUERADE # NAT dinâmico (para IPs dinâmicos)
-j REDIRECT  # Redirecionamento de porta
```

### Cadeias de Usuário

```bash
-j NOME_DA_CADEIA  # Salta para cadeia definida pelo usuário
```

---
# Políticas Padrão *(Default Policies)*

## Configuração Segura Inicial

```bash
# 1. Definir políticas padrão como DROP
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

# 2. Permitir tráfego de loopback
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# 3. Permitir tráfego estabelecido e relacionado
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 4. Permitir ICMP (ping)
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

---
# Exemplos Práticos de Configuração

## 1. Servidor Web Básico

```bash
# Limpar regras existentes
iptables -F
iptables -t nat -F
iptables -t mangle -F

# Definir políticas padrão
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Permitir localhost
iptables -A INPUT -i lo -j ACCEPT

# Permitir conexões estabelecidas
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Permitir SSH (porta 22) de uma rede específica
iptables -A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -m conntrack --ctstate NEW -j ACCEPT

# Permitir HTTP (porta 80) e HTTPS (porta 443)
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW -j ACCEPT

# Permitir ping (ICMP)
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

# Log de pacotes rejeitados (opcional)
iptables -A INPUT -j LOG --log-prefix "IPTABLES-DROPPED: "
```

## 2. Gateway/NAT para Rede Interna

```bash
# Habilitar forwarding no kernel
echo 1 > /proc/sys/net/ipv4/ip_forward

# NAT para rede interna (192.168.1.0/24)
iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE

# Permitir forwarding para rede interna
iptables -A FORWARD -i eth1 -o eth0 -s 192.168.1.0/24 -j ACCEPT
iptables -A FORWARD -i eth0 -o eth1 -d 192.168.1.0/24 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

## 3. Redirecionamento de Portas *(Port Forwarding)*

```bash
# Redirecionar porta externa 8080 para servidor interno na porta 80
iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.100:80
iptables -A FORWARD -p tcp -d 192.168.1.100 --dport 80 -j ACCEPT
```

## 4. Proteção contra Ataques Comuns

```bash
# Proteção contra SYN Flood
iptables -A INPUT -p tcp --syn -m limit --limit 10/second --limit-burst 20 -j ACCEPT
iptables -A INPUT -p tcp --syn -j DROP

# Proteção contra port scanning
iptables -A INPUT -p tcp --tcp-flags ALL FIN,URG,PSH -j DROP
iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP
iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Bloquear endereços maliciosos
iptables -A INPUT -s 10.0.0.0/8 -j DROP
iptables -A INPUT -s 172.16.0.0/12 -j DROP
iptables -A INPUT -s 192.168.0.0/16 -j DROP

# Limitar conexões SSH
iptables -A INPUT -p tcp --dport 22 -m connlimit --connlimit-above 3 --connlimit-mask 32 -j REJECT
```

## 5. Regras com Logging

```bash
# Criar cadeia para logging
iptables -N LOGGING

# Configurar logging
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP

# Enviar tráfego suspeito para logging
iptables -A INPUT -p tcp --dport 23 -j LOGGING  # Telnet
iptables -A INPUT -p tcp --dport 1433 -j LOGGING  # SQL Server
iptables -A INPUT -p tcp --dport 3389 -j LOGGING  # RDP
```

---
# Casos de Uso Comuns

## 1. Configuração de Servidor

```bash
#!/bin/bash
# Script de firewall para servidor

IPT="/sbin/iptables"

# Resetar todas as regras
$IPT -F
$IPT -X
$IPT -t nat -F
$IPT -t nat -X
$IPT -t mangle -F
$IPT -t mangle -X

# Políticas padrão
$IPT -P INPUT DROP
$IPT -P FORWARD DROP
$IPT -P OUTPUT ACCEPT

# Loopback
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT

# Conexões estabelecidas
$IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# SSH
$IPT -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
$IPT -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 --name SSH -j DROP
$IPT -A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT

# Serviços web
$IPT -A INPUT -p tcp --dport 80 -m state --state NEW -j ACCEPT
$IPT -A INPUT -p tcp --dport 443 -m state --state NEW -j ACCEPT

# DNS
$IPT -A INPUT -p udp --dport 53 -j ACCEPT
$IPT -A INPUT -p tcp --dport 53 -j ACCEPT

# ICMP (ping)
$IPT -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/second -j ACCEPT

# Logging
$IPT -A INPUT -j LOG --log-prefix "DROP: " --log-level 7
$IPT -A INPUT -j DROP
```

## 2. Firewall Pessoal/Workstation

```bash
#!/bin/bash
# Firewall para estação de trabalho

IPT="/sbin/iptables"

# Limpar tudo
$IPT -F
$IPT -X

# Políticas padrão
$IPT -P INPUT DROP
$IPT -P FORWARD DROP
$IPT -P OUTPUT ACCEPT

# Localhost
$IPT -A INPUT -i lo -j ACCEPT

# Conexões estabelecidas
$IPT -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# DNS
$IPT -A OUTPUT -p udp --dport 53 -j ACCEPT
$IPT -A OUTPUT -p tcp --dport 53 -j ACCEPT

# HTTP/HTTPS
$IPT -A OUTPUT -p tcp --dport 80 -j ACCEPT
$IPT -A OUTPUT -p tcp --dport 443 -j ACCEPT

# SSH
$IPT -A OUTPUT -p tcp --dport 22 -j ACCEPT

# NTP
$IPT -A OUTPUT -p udp --dport 123 -j ACCEPT

# ICMP
$IPT -A OUTPUT -p icmp -j ACCEPT
$IPT -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

## 3. Proteção Avançada

```bash
# Proteção contra IP spoofing
iptables -A INPUT -i eth0 -s 10.0.0.0/8 -j DROP
iptables -A INPUT -i eth0 -s 172.16.0.0/12 -j DROP
iptables -A INPUT -i eth0 -s 192.168.0.0/16 -j DROP
iptables -A INPUT -i eth0 -s 127.0.0.0/8 -j DROP

# Proteção contra ataques de força bruta
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name ssh
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 3 --name ssh -j DROP

# Rate limiting para serviços
iptables -A INPUT -p tcp --dport 80 -m limit --limit 25/minute --limit-burst 100 -j ACCEPT
```

---
# Depuração e Monitoramento

## 1. Verificação de Regras

```bash
# Listar regras com números de linha
iptables -L -n --line-numbers

# Listar regras específicas com contadores
iptables -L INPUT -v -n

# Verificar regras NAT
iptables -t nat -L -v -n

# Verificar regras de mangle
iptables -t mangle -L -v -n
```

## 2. Monitoramento em Tempo Real

```bash
# Monitorar logs do iptables
tail -f /var/log/kern.log | grep iptables

# Verificar contadores de pacotes
watch -n 1 'iptables -L -v -n'

# Monitorar conexões ativas
conntrack -L
```

## 3. Testando Regras

```bash
# Testar com ping
ping -c 1 IP_DESTINO

# Testar com telnet/netcat
telnet IP_DESTINO PORTA
nc -zv IP_DESTINO PORTA

# Testar com traceroute
traceroute IP_DESTINO
```

## 4. Salvando e Restaurando Regras

### Salvar regras atuais

```bash
# Método tradicional
iptables-save > /etc/iptables/rules.v4

# Ou usando redirecionamento
iptables-save > iptables-backup.txt
```

### Restaurar regras

```bash
iptables-restore < /etc/iptables/rules.v4
```

### Configurar persistência (Ubuntu/Debian)

```bash
# Instalar pacote
apt-get install iptables-persistent

# Salvar regras atuais
netfilter-persistent save

# Recarregar regras
netfilter-persistent reload
```

### Configurar persistência (RHEL/CentOS)

```bash
# Salvar regras
service iptables save  # Ou: /sbin/service iptables save

# Configurar para iniciar com o sistema
chkconfig iptables on
```

---
# IPTABLES vs NFTABLES

## Comparação

| **Característica** | **IPTABLES**                            | **NFTABLES**                            |
| ------------------ | --------------------------------------- | --------------------------------------- |
| Sintaxe            | Complexa, múltiplos comandos            | Unificada, mais simples                 |
| Desempenho         | Bom                                     | Melhor (processamento em um passo)      |
| IPv4/IPv6          | Comandos separados (iptables/ip6tables) | Unificado (suporte nativo a dual stack) |
| Manutenção         | Em modo de legado                       | Ativamente desenvolvido                 |
| Complexidade       | Mais verboso                            | Mais conciso                            |

## Migração para NFTABLES

```bash
# Converter regras iptables para nftables
iptables-save > iptables-backup.txt
iptables-restore-translate -f iptables-backup.txt > nftables-rules.txt

# Carregar no nftables
nft -f nftables-rules.txt
```

---
# Boas Práticas <a name="boas-práticas"></a>

## 1.Segurança

1. **Princípio do menor privilégio**: Só permita o necessário
2. **Política padrão DROP**: Comece bloqueando tudo
3. **Regras específicas primeiro**: Ordene das mais específicas para as mais gerais
4. **Logging adequado**: Log apenas o necessário para evitar DoS no logging

## 2 Organização

1. Use scripts comentados
2. Mantenha backup das regras
3. Documente regras complexas
4. Use cadeias definidas pelo usuário para organização

## 3 Manutenção

1. Teste regras em ambiente controlado primeiro
2. Use ferramentas de análise de regras
3. Monitore logs regularmente
4. Atualize regras conforme necessidades mudam

## 4. Script de Boas Práticas

```bash
#!/bin/bash
# Template de firewall com boas práticas

# Caminho do iptables
IPT="/sbin/iptables"

# Limpeza completa
$IPT -F
$IPT -X
for table in filter nat mangle raw; do
    $IPT -t $table -F
    $IPT -t $table -X
done

# Políticas padrão seguras
$IPT -P INPUT DROP
$IPT -P FORWARD DROP
$IPT -P OUTPUT DROP

# Localhost ilimitado
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT

# Conexões estabelecidas e relacionadas
$IPT -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
$IPT -A OUTPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# ICMP controlado
$IPT -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/second -j ACCEPT

# [INSIRA SUAS REGRAS ESPECÍFICAS AQUI]

# Logging do que é rejeitado (limitar para evitar DoS)
$IPT -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# Rejeição final com mensagem
$IPT -A INPUT -j REJECT --reject-with icmp-host-prohibited
$IPT -A FORWARD -j REJECT --reject-with icmp-host-prohibited

# Salvar regras
iptables-save > /etc/iptables/rules.v4
```

---
# Recursos Adicionais

## Comandos úteis para aprendizado

```bash
# Ver ajuda completa
man iptables
man iptables-extensions

# Ver extensões disponíveis
iptables -m help

# Listar alvos disponíveis
iptables -j help

# Tutorial interativo
sudo iptables -L -v -n --line-numbers
```

## Ferramentas Complementares

- **fail2ban**: Bloqueio automático de IPs maliciosos
- **ufw**: Front-end simplificado para iptables
- **firewalld**: Firewall dinâmico com zonas
- **Shorewall**: Configuração de firewall de alto nível

---
