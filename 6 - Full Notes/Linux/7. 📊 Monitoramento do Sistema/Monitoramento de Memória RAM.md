2025-08-24 09:54

Status: #developed #Linux 

Tags: [[Linux]] | [[free ]] | [[vmstat]] | [[top]]

----
# Introdução

A memória RAM é um dos recursos mais críticos em qualquer sistema operacional. Monitorar sua utilização permite identificar gargalos, prever falhas de desempenho e entender melhor como os processos consomem recursos.

---
# `free`

O comando `free` é o mais básico e direto para verificar o consumo de memória.

## Sintaxe

```bash
free -h
```

### Opções principais:

- `-h`: exibe valores em formato legível (KB, MB, GB).
- `-m`: mostra valores em megabytes.
- `-g`: mostra valores em gigabytes.
- `-s <segundos>`: atualiza os dados continuamente no intervalo definido.

## Exemplo

```bash
free -h
```

### Saída

```vnet
              total        used        free      shared  buff/cache   available
Mem:           15Gi       5.8Gi       2.1Gi       512Mi       7.2Gi       8.9Gi
Swap:          2.0Gi       256Mi       1.7Gi
```

**Interpretação:**

- **total** → total de memória física instalada.
- **used** → memória usada.
- **free** → memória livre sem uso algum.
- **buff/cache** → memória usada para cache do sistema (que pode ser liberada).
- **available** → memória efetivamente disponível para novos processos.

---
# `vmstat`

O `vmstat` *(Virtual Memory Statistics)* fornece estatísticas detalhadas sobre processos, memória, swap, I/O, e CPU.

## Sintaxe

```bash
vmstat 2 5
```

## Explicação

- `2` → intervalo de atualização em segundos.
- `5` → número de vezes que o comando será executado.

**Saída relevante para RAM**:

- `free` → memória livre.
- `buff` → buffers utilizados.
- `cache` → memória usada em cache.
- `si/so` → swap in/swap out (memória indo para swap).

---
# `top`

O comando `top` é um monitor em tempo real de processos, CPU e memória.

## Sintaxe

```bash
top
```

**Colunas relacionadas à RAM**:

- `RES` → memória física usada pelo processo.
- `VIRT` → memória virtual usada.
- `SHR` → memória compartilhada.
- `%MEM` → percentual de uso da RAM pelo processo.
### Navegação:

- Pressione `M` dentro do `top` → ordena processos pelo uso de memória.
- Pressione `q` → sai do monitor.

---
# `htop`

Uma versão mais amigável e colorida do `top`.

## Instalação

```bash
sudo apt install htop -y
```

## Execução

```bash
htop
```

**Vantagens:**

- Interface interativa e colorida.
- Gráficos de uso de CPU, memória e swap.
- Filtros para organizar processos por consumo.

![[Pasted image 20250824100218.png]]

---
# `/proc/meminfo`

O arquivo `/proc/meminfo` contém informações detalhadas sobre o uso de memória.

## Sintaxe

```bash
cat /proc/meminfo
```

Informações úteis:

- `MemTotal` → total de memória.
- `MemFree` → memória livre.
- `MemAvailable` → memória disponível.
- `Buffers`, `Cached` → memória usada para cache/buffer.
- `SwapTotal`, `SwapFree` → informações da swap.

Se quiser ver apenas o essencial:

```bash
grep -E "MemTotal|MemFree|MemAvailable|SwapTotal|SwapFree" /proc/meminfo
```

---
# `sar` (opcional, ferramenta mais avançada)

Parte do pacote `sysstat` coleta estatísticas históricas de memória.

## Instalação

```bash
sudo apt install sysstat -y
```

## Exemplo

```bash
sar -r 2 5
```

> Mostra estatísticas de uso de memória a cada 2 segundos, 5 vezes.

---
# Exemplos práticos de monitoramento automático

## Monitorar continuamente o uso de memória

```bash
watch -n 2 free -h
```

## Monitorar processos que mais consomem RAM

```bash
ps aux --sort=-%mem | head -n 10
```

---
# Conclusão

- Para **ver rapidamente** → use `free -h`.
- Para **estatísticas detalhadas** → use `vmstat`.
- Para **monitoramento em tempo real** → use `top` ou `htop`.    
- Para **análise profunda** → consulte `/proc/meminfo` ou use `sar`.

Esses comandos são fundamentais para diagnosticar problemas de desempenho e entender como a RAM está sendo utilizada no Linux.