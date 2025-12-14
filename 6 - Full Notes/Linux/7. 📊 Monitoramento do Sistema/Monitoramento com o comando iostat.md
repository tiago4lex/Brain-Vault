2025-08-24 10:39

Status: #developed #Linux 

Tags: [[Linux]] | [[iostat]]

----
# Introdução

## O que é o `iostat`?

O `iostat` *(Input/Output Statistics)* faz parte do pacote `sysstat` e é utilizado para coletar e exibir estatísticas sobre o uso da CPU e dos dispositivos de disco.

Ele ajuda a identificar gargalos de **I/O** (como disco lento ou sobrecarregado) e monitorar a performance geral do sistema.

---
# Instalação

No Ubuntu/Debian:

```bash
sudo apt update
sudo apt install sysstat -y
```

No CentOS/RHEL:

```bash
sudo yum install sysstat -y
```

---
# Sintaxe básica

```bash
iostat [opções] [intervalo] [contagem]
```

- `intervalo` → tempo em segundos entre cada atualização.
- `intervalo` → número de repetições.

**Exemplo:**

```bash
iostat 2 5
```

Mostra estatísticas a cada **2 segundos**, repetindo **5 vezes**.

---
# Principais colunas do `iostat`

### Na seção de CPU

- `%user` → tempo gasto em processos de usuário.
- `%system` → tempo gasto no kernel.
- `%iowait` → tempo esperando I/O (importante para detectar gargalos de disco).
- `%idle` → tempo ocioso.

### Na seção de dispositivos

- `Device` → nome do dispositivo (ex: `sda`, `sdb1`).
- `tps` → transações por segundo (leituras/escritas).
- `kB_read/s` → taxa de leitura em KB/s.
- `kB_wrtn/s` → taxa de escrita em KB/s.
- `kB_read` e `kB_wrtn` → total de dados lidos/escritos.

---
# Exemplos de Uso

## 1. Monitorar CPU e discos em tempo real

```bash
iostat -x 1
```

O parâmetro `-x` ativa o **modo detalhado**, mostrando estatísticas extras como `%util` (quanto tempo o dispositivo ficou ocupado).

## 2. Mostrar estatísticas em MB

```bash
iostat -m 2 3
```

Exibe em **MB/s**, atualizando a cada 2 segundos, por 3 vezes.

## 3. Monitorar somente CPU

```bash
iostat -c 5 2
```

Mostra apenas informações da CPU a cada 5 segundos, por 2 vezes.

## 4. Monitorar apenas disco

```bash
iostat -d 3
```

Mostra estatísticas apenas dos dispositivos de disco a cada 3 segundo.

---
# Exemplo de Script para Monitoramento com `iostat`

Aqui está um **script prático** que monitora I/O do disco e gera alertas caso o uso ultrapasse **70% de ocupação (`%util`)**.

```bash
#!/bin/bash

# Diretório e arquivo de log
LOG_DIR="monitoramento_sistema"
mkdir -p "$LOG_DIR"
IOSTAT_LOG="$LOG_DIR/monitoramento_iostat_$(date +%F).txt"

# Função para monitorar I/O com iostat
monitorar_iostat() {
    # Pega a utilização dos discos no modo detalhado (-x)
    iostat -x 1 2 | awk '
    BEGIN {alerta=0}
    /^Device/ {next}  # Ignora cabeçalho
    /^[a-z]/ {
        dispositivo=$1
        util=$NF   # %util é a última coluna
        printf "%s - %s: %s%% de uso\n", strftime("%Y-%m-%d %H:%M:%S"), dispositivo, util >> "'"$IOSTAT_LOG"'"
        if (util+0 > 70) {
            printf "%s - ALERTA! %s acima de 70%% de uso!\n", strftime("%Y-%m-%d %H:%M:%S"), dispositivo >> "'"$IOSTAT_LOG"'"
        }
    }'
}

# Loop infinito para monitorar continuamente
while true; do
    monitorar_iostat
    sleep 10
done
```

## Como funciona o Script?

1. Cria um arquivo de log separado por data.
2. Executa o `iostat -x 1 2` → coleta estatísticas detalhadas.
    - `1 2` → faz uma coleta a cada **1s**, repetindo **2 vezes** (a primeira geralmente é descartada por conter valores acumulados).

3. Filtra a coluna `%util`, que mostra quanto tempo o disco está ocupado.
4. Registra no log o uso de cada dispositivo.
5. Gera um alerta se o valor ultrapassar **70%**.
6. Repete o monitoramento a cada **10 segundos**.

---
# Conclusão

- O `iostat` é essencial para analisar gargalos de **disco** e **CPU vs I/O**.
- Ajuda a diferenciar se um problema de lentidão é por **processamento** ou por **acesso ao disco**.
- O script apresentado permite manter logs e alertas de uso crítico.