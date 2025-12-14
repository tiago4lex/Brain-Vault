2025-08-21 10:04

Status: #developed #Linux 

Tags: [[Linux]] | [[Ping]] | [[curl]] | [[wget]] | [[Traceroute]] | [[nslookup]] | [[dig]]

----
# Verificação de Conectividade

No Linux, existem vários comandos para verificar se a máquina tem conectividade com a rede local e a internet.

## Comandos mais usados

### 1. `ping` - Verifica se um host responde:

```bash
ping -c 4 google.com
```

- `-c 4` → envia apenas 4 pacotes ICMP.
- Retorno indica tempo de resposta e perda de pacotes.

### 2. `curl` - Testa conexão HTTP/HTTPS

```bash
curl -I https://www.google.com
```

- `-I` → retorna apenas os headers da resposta.

### 3. `wget` - Similar ao `curl`, mas baixa arquivos/testa HTTP

```bash
wget -q --spider https://google.com && echo | "Online" || echo "Offline"
```

### 4. `traceroute` - Mostra o caminho dos pacotes até o destino

```bash
traceroute google.com
```

### 5. `nslookup` ou `dig` - Verifica se o DNS está funcionando

```bash
nslookup google.com
dig google.com
```

---
# Script de Monitoramento de Rede

Podemos automatizar a checagem de conectividade e registrar os resultados em logs.

## Script básico: Teste de conectividade com `ping`

```bash
#!/bin/bash

# Destino de teste
HOST="8.8.8.8" # Servidor DNS público do Google
LOG_DIR="monitoramento_rede"
LOG_FILE="$LOG_DIR/rede_status.log"

# Criar diretporio de logs caso não exista
mkdir -p $LOG_DIR

# Data e hora atuais
DATA=$(date +"%Y-%m-%d %H:%M:%S")

# Testar conectividade
ping -c 2 $HOST > /dev/null 2>&1

if [ $? -eq 0 ]; then
	echo "$DATA - Conectividade OK com $HOST" >> $LOG_FILE
else
	echo "$DATA - Falha de Conectividade com $HOST" >> $LOG_FILE
fi
```

## Script avançado: Monitoramento contínuo

Esse script verifica múltiplos serviços: **ping, DNS e HTTP**.

```bash
#!/bin/bash

# Destino de teste
LOG_DIR="monitoramento_rede"
LOG_FILE="$LOG_DIR/rede_detalhado.log"

# Criar diretporio de logs caso não exista
mkdir -p $LOG_DIR

# Data e hora atuais
DATA=$(date +"%Y-%m-%d %H:%M:%S")

# Teste de ping
if ping -c 2 8.8.8.8 > /dev/null 2>&1; then
	PING_STATUS="OK"
else
	PING_STATUS="FALHA"
fi

# Teste de DNS
if nslookup google.com > /dev/null 2>&1; then
	DNS_STATUS="OK"
else
	DNS_STATUS="FALHA"
fi

# Teste de HTTP
if curl -s --head https://www.google.com | grep "200 ok" > /dev/null; then
	HTTP_STATUS="OK"
else
	HTTP_STATUS="FALHA"
fi

# Registrar no log
echo "$DATA - Ping: $PING_STATUS | DNS: $DNS_STATUS | HTTP: $HTTP_STATUS" >> $LOG_FILE
```

## Automatizando com `crontab`

Para executar automaticamente a cada 5 minutos

```bash
crontab -e
```

Adicionar a linha

```
*/5 * * * * /home/tiago/monitorar_rede.sh
```

## Exemplo de Saída no Log

```yaml
2025-08-20 11:30:00 - Ping: OK | DNS: OK | HTTP: OK
2025-08-20 11:35:00 - Ping: OK | DNS: FALHA | HTTP: FALHA
2025-08-20 11:40:00 - Ping: FALHA | DNS: FALHA | HTTP: FALHA
```

---
# Saídas em Linux

Quando se executa um comando no terminal, ele pode gerar **dois tipos de saída:**

1. `stdout` ***(Standard Output)*** - Saída normal (ex: resultados de um comando).
	- Representado pelo número `1`.

2. `stderr` ***(Standard Error)*** - Mensagens de erro (ex: arquivo não encontrado).
	- Representado pelo número `2`.

## O que significa `2>&1`?

- `2` → representa o `stderr`.
- `1` → representa o `stdout`.
- `2>&1` → significa **redirecionar o `stderr` para o mesmo lugar onde o `stdout` está indo**.

**Exemplo simples:**

```bash
ls /etc /nao_exite > saida.txt 2>&1
```

- `ls /etc` gera saída normal → vai para `saida.txt`.
- `ls /nao_existe` gera erro → também vai para `saida.txt`.

Assim, tanto o resultado quanto os erros ficam juntos no mesmo arquivo.

## No contexto do script

```bash
ping -c 2 8.8.8.8 > /dev/null 2>&1
```

- `> /dev/null` → joga fora a saída normal (`stdout`).
- `2>&1` → redireciona os erros para o mesmo lugar (`stdout`), que já está indo para `/dev/null`.

Isso significa que **tanto o resultado do ping quanto mensagens de erro são descartados**.  

O comando fica “silencioso”, e só o código de retorno (`$?`) é usado para verificar se deu certo ou não.