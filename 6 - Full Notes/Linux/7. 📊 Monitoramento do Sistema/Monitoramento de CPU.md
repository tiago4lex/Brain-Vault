2025-08-24 10:20

Status: #developed #Linux 

Tags: [[Linux]] | [[uptime]] | [[top]] | [[htop]] | [[mpstat]] | [[sar]]

----
# Introdução

A CPU é o “cérebro” do computador. Monitorar sua utilização ajuda a identificar gargalos, sobrecarga de processos, falhas de configuração e até ataques (como loops infinitos ou mineração de criptomoedas maliciosa).

No Linux, existem diversos comandos que permitem acompanhar o uso da CPU em tempo real e de forma histórica.

---
# `uptime`

Exibe há quanto tempo o sistema está ligado, número de usuários logados e a carga média da CPU.

### Sintaxe

```bash
uptime
```

### Exemplo de saída

```bash
11:55:32 up 2:10,  2 users,  load average: 0.45, 0.30, 0.25
```

📌 **load average** → representa a média de processos em execução ou esperando CPU nos últimos **1, 5 e 15 minutos**.

- Valor próximo ou maior que o número de núcleos do processador → indica sobrecarga.

---
# `top`

O `top` é o monitor de processos padrão do Linux, mostrando o consumo de CPU em tempo real.

### Sintaxe

```bash
top
```

📌 **Colunas importantes**:

- `%CPU` → uso percentual da CPU por processo.
- `us` → tempo em modo usuário.
- `sy` → tempo em modo kernel.
- `id` → tempo ocioso (idle).
- `wa` → tempo esperando I/O.

### Navegação:

- Pressione `P` → ordena por uso de CPU.
- Pressione `q` → sai do monitor.

---
# `htop`

## 3. **htop**

Versão mais amigável do `top`, com interface colorida e interativa.

### Instalação

```bash
sudo apt install htop -y
```

### Execução

```bash
htop
```

📌 Vantagens:

- Barras gráficas de consumo por núcleo.
- Ordenação dinâmica por CPU, RAM ou tempo de execução.
- Permite encerrar processos diretamente.

---
# `mpstat`

Parte do pacote `sysstat`, mostra estatísticas detalhadas da CPU.

### Instalação

```bash
sudo apt install sysstat -y
```

### Exemplo

```bash
mpstat 2 5
```

- `2` → intervalo de atualização em segundos.
- `5` → número de medições.

📌 Saída mostra uso da CPU por núcleo:

- `%usr` → tempo gasto em processos de usuário.
- `%sys` → tempo gasto em processos do kernel.
- `%idle` → tempo ocioso.

---
# `sar`

Ferramenta para monitoramento histórico da CPU (também no `sysstat`).

### Exemplo

```bash
sar -u 1 3
```

📌 Mostra estatísticas de uso da CPU a cada **1 segundo**, por **3 vezes**.

---
# `/proc/stat`

Arquivo de estatísticas da CPU

### Sintaxe

```bash
cat /proc/stat | grep "cpu"
```

📌 Contém dados de tempo da CPU em diferentes estados: usuário, sistema, idle, I/O, etc.

---
# Script de Monitoramento da CPU

Agora um exemplo de script simples que monitora a CPU, gera alertas quando ultrapassa **70% de uso** e salva em um arquivo de log.

```bash
#!/bin/bash

# Diretório e arquivo de log
LOG_DIR="monitoramento_sistema"
mkdir -p "$LOG_DIR"
CPU_LOG="$LOG_DIR/monitoramento_cpu_$(date +%F).txt"

# Função para monitorar CPU
monitorar_cpu() {
    USO_CPU=$(mpstat 1 1 | awk '/Average:/ && $12 ~ /[0-9.]+/ {print 100 - $12}') 
    # $12 corresponde ao %idle → uso = 100 - idle

    echo "$(date): Uso da CPU: $USO_CPU%" >> "$CPU_LOG"

    # Alerta se uso passar de 70%
    if (( $(echo "$USO_CPU > 70" | bc -l) )); then
        echo "$(date): ALERTA! CPU acima de 70% de uso." >> "$CPU_LOG"
    fi
}

# Execução contínua a cada 5 segundos
while true; do
    monitorar_cpu
    sleep 5
done
```

## Como funciona o Script

1. Usa o `mpstat` para medir o uso da CPU.
2. Calcula o percentual (`100 - %idle`).
3. Salva os resultados em um log separado por dia.
4. Se o valor for maior que **70%**, grava uma mensagem de alerta.
5. Roda em loop infinito com intervalo de **5 segundos**.

---
# Conclusão

- Para **ver rapidamente o estado da CPU** → `uptime`, `top`, `htop`.
- Para **estatísticas detalhadas** → `mpstat`, `sar`.
- Para **processos específicos** → `ps`.
- Para **monitoramento contínuo e logs** → scripts personalizados.