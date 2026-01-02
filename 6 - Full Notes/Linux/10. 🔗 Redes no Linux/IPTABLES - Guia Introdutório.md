2026-01-02 01:21

Status: #developed #Linux 

Tags: [[Linux]] | [[Redes de Computadores]] | [[IPTABLES]]

----
# O que o IPTABLES realmente faz?

O **iptables** é um firewall que **decide o destino de pacotes de rede**.

- Pense nele como um **porteiro:**
	- todo pacote que entra, sai ou passa pelo sistema
	- é avaliado por regras
	- e recebe uma decisão (permitir, bloquear, rejeitar, etc.)

Nada mais que isso.

---
# O que é um Pacote (o "objeto" que o IPTABLES manipula)?

Tudo no iptables gira em torno de **pacotes de rede**.

Um pacote contém informações como:

- IP de origem
- IP de destino
- protocolo (TCP, UDP, ICMP)
- porta de origem
- porta de destino
- flags TCP

![[Pasted image 20260102012459.png]]

>[!note] Nota:
>O **iptables NÃO manipula usuários, arquivos ou programas** — apenas pacotes.

---
# Tabelas, Cadeias e Regras

## 1. Estrutura Mental do IPTABLES

```text
Pacote → Tabela → Cadeia → Regras → Ação
```

- **Tabela:** tipo de decisão
- **Cadeia *(chain)*:** momento do caminho do pacote
- **Regra:** condição
- **Ação *(Target)*:** o que fazer

---
# As cadeias do IPTABLES

As cadeias representam **em que ponto da viagem o pacote está**.

Imagine o sistema como uma cidade:

## 1. PREROUTING — "Antes de decidir para onde vai"

📍 O pacote **acabou de chegar** no sistema.
- ainda não se sabe se ele será:
	- entregue localmente
	- encaminhado para outro host

Usado principalmente para:
- NAT (DNAT)
- redirecionamentos

> [!quote]
> 🧠 _"Antes de escolher o destino, quero mudar algo."_

## 2. INPUT — "Vai entrar neste sistema?"

📍 O pacote é **destinado ao próprio sistema**.
- Exemplos:
	- acesso SSH
	- acesso HTTP ao servidor

Pergunta que o iptables faz:

>[!quote]
>_"Esse pacote pode entrar no meu sistema?"_

## 3. FORWARD — "Vai passar por mim para outro lugar?"

📍 O sistema atua como **roteador/firewall**.
- O pacote:
	- entra por uma interface
	- sai por outra

Muito comum em:
- gateways
- firewalls de rede
- NAT

## 4. OUTPUT — "Estou enviando esse pacote"

📍 O pacote foi **gerado pelo próprio sistema**.
- Exemplos:
	- ping do servidor
	- atualizações via apt

Pergunta:

>[!quote]
>_"Posso enviar esse pacote para fora?"_

## 5. POSTROUTING — "Já decidi para onde vai, vou ajustar antes de sair"

📍 Última etapa antes de o pacote sair.
- Usado para:
	- SNAT/MASQUERADE

>[!quote]
>🧠 _"Antes de sair, vou alterar algo no pacote."_

---
# Fluxo visual completo de um pacote

```text
ENTRA
↓
PREROUTING
↓
┌───────────────┐
│ Destino local │──→ INPUT → Sistema
└───────────────┘
		│
		└──→ FORWARD → POSTROUTING → SAI

Sistema → OUTPUT → POSTROUTING → SAI
```

---
# O que significa "Manipulação" no IPTABLES?

Manipular significa **alterar informações do pacote**.

## Exemplos do que pode ser manipulado

- IP de origem
- IP de destino
- porta

Isso é feito principalmente pelo **NAT**.

## Por que manipular pacotes?

- compartilhar internet (NAT)
- esconder IPs internos
- redirecionar serviços

Sem manipulação, a internet moderna não funcionaria.

---
# Ações *(Targets)*: O que acontece com o pacote?

As ações dizem o **destino final do pacote**.

## 1. ACCEPT — "Pode passar"

- o pacote é permitido
- continua seu caminho

## 2. DROP — "Joga fora em silêncio"

- pacote descartado
- **nenhuma resposta enviada**

Usado para:

- ocultar serviços
- reduzir scans

## 3. REJECT — "Bloqueia, mas avisa"

- pacote descartado
- resposta enviada (ICMP ou TCP RST)

Usado quando:

- você quer deixar claro que o acesso é proibido

## 4. RETURN — "Volta para quem chamou"

- usado em cadeias personalizadas
- retorna para a cadeia anterior

## 5. LOG — "Registra e continua"

- registra o pacote em log
- **não bloqueia sozinho**

Normalmente usado antes do DROP.

---
# Regra simples explicada

## Exemplo 1 - Permitir SSH (porta 22)

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Explicação:

> "Permita que pacotes TCP destinados à porta 22 entrem neste sistema."

## Exemplo 2 - Bloquear acesso a uma porta específica

```bash
ip tables -A IPUT -p tcp --dport 23 -j DROP
```

Explicação:

> "Bloqueie silenciosamente qualquer pacote TCP que tente acessar a porta 23 (telnet)."

## Exemplo 3 - Permitir acesso HTTP apenas da rede interna

```bash
iptables -A INPUT -p tcp --dport 80 -s 192.168.1.0/24 -j ACCEPT
```

Explicação:

> "Permita acesso HTTP somente para pacotes vindos da rede 192.168.1.0/24."

## Exemplo 4 - Bloquear todo reste explicitamente

```bash
iptables -A INPUT -j DROP
```

Explicação:

> "Bloqueie qualquer pacote que não tenha sido permitido anteriormente."

## Exemplo 5 - Permitir conexões já estabelecidas

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Explicação:

> "Permita pacotes que façam parte de conexões já estabelecidas ou relacionadas."

## Exemplo 6 - Permitir ping (ICMP)

```bash
iptables -A INPUT -p icmp -j ACCEPT
```

Explicação:

> "Permita pacotes ICMP, como ping."

## Exemplo 7 - Bloquear um IP específico

```bash
iptables -A INPUT -s 10.10.10.50 -j DROP
```

Explicação:

> "Bloqueie qualquer pacote vindo do IP 10.10.10.50."

## Exemplo 8 - Permitir saída para a Internet (DNS e HTTP)

```bash
iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
```

Explicação:

> "Permita que este sistema faça consultas DNS e acesse sites HTTP".

---
# Erros comuns

- confundir INPUT com FORWARD
- esquecer da política padrão (DROP)
- criar regra e bloquear o próprio SSH
- não entender a ordem das regras

---
# Regra de ouro do iptables

> **iptables NÃO é difícil — ele só é rigoroso e literal.**

Se você:

- souber **onde o pacote está**    
- souber **o que quer fazer com ele**

Você saberá em qual cadeia atuar.

---
# Conclusão

Este documento serve como uma **base mental sólida** para entender o iptables.

Agora, ao olhar regras complexas, você conseguirá responder:

- onde o pacote está?
- o que está sendo analisado?
- qual ação está sendo tomada?