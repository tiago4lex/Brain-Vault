2025-08-23 10:20

Status: #developed #Linux 

Tags: [[Linux]] | [[df]] | [[du]] | [[sort]] | [[ls]] | [[find]] | [[ncdu]] | [[baobab]] | [[filelight]]

----
# Introdução

A verificação do uso de disco é uma das tarefas essenciais no **gerenciamento de sistemas Linux**. Administradores precisam acompanhar o espaço disponível para evitar falhas em serviços, perda de dados ou travamentos do sistema devido à falta de armazenamento.

O Linux oferece uma série de ferramentas de linha de comando que permitem monitorar espaço em disco, identificar pastas e arquivos que mais ocupam espaço e até gerar relatórios automatizados.

---
# Comando `df` *(Disk Free)*

O `df` exibe informações sobre o uso de disco em partições montadas.

## Sintaxe

```bash
df [opções]
```

## Exemplos

### 1. Mostrar uso de todas as partições

```bash
df
```

**Saída esperada:**

```
Filesystem     1K-blocks     Used   Available   Use%  Mounted on
/dev/sda1      30830592  12034564   17239420    42%   /
tmpfs          4023248          0   4023248     0%    /dev/shm
```

### 2. Mostrar valores em formato legível (MB/GB)

```bash
df -h
```

**Saída:**

```
Filesystem      Size  Used   Available    Use%   Mounted on
/dev/sda1        30G   12G         18G     42%   /
tmpfs           3.9G     0        3.9G      0%   /dev/shm
```

### 3. Mostrar apenas a partição raiz:

```bash
df -h /
```

---
# Comando `du` *(Disk Usage)*

O `du` exibe o tamanho de diretórios e arquivos.

## Sintaxe

```bash
du [opções] [caminho]
```

## Exemplos

### 1. Mostrar uso de uma pasta

```bash
du /var
```

### 2. Formato legível (MB/GB)

```bash
du -h /var
```

### 3. Mostrar apenas o total

```bash
du -sh /var
```

**Saída:**

```
1.5G   /var
```

### 4. Mostrar os 10 diretórios que mais ocupam espaço em `/home`

```bash
du -sh /home/* | sort -h | tail -10
```

### 5. Mostrar arquivos individuais na listagem

```bash
du -ah
```

- **`-a` (All files)**Inclui arquivos individuais na listagem, além de diretórios.

### 6. Grand Total

```bash
du -hc
```

- **`-c` (Grand total)**Adiciona uma linha final com o total geral do espaço listado.

### 7. Mostrar data e hora de modificação

```bash
du --time -h
```

---
# Localizando Arquivos Grandes

## Usando `find`

Procurar arquivos maiores que 500MB:

```bash
find / -type f -size +500M
```

## Usando `ls`

Listar arquivos maiores primeiro:

```bash
ls -lhs /var/log
```

## Usando `du` + `sort`

Listar pastas por ordem de tamanho

```bash
du -sh /var/* | sort -h
```

---
# Monitoramento em Tempo Real

## Comando `ncdu` *(NCurses Disk Usage)*

Ferramenta interativa para explorar uso de disco (precisa ser instalado)

```bash
sudo apt install ncdu -y
ncdu /
```

Permite navegar pelas pastas e visualizar graficamente os diretórios que ocupam mais espaço.

---
# Scripts de verificação automática

Um script simples para monitorar uso de disco:

```bash
#!/bin/bash
# Script para verificar uso de disco e gerar alerta

USO=$(df -h / awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$USO" -ge 80 ]; then
	echo "Atenção: Disco acima de 80% de uso! ($USO%)"
else
	echo "Disco em condições normais. Uso atual: $USO%"
fi
```

**Saída possível:**

```
Disco em condições normais. Uso atual: 42%
```

ou

```
Atenção: Disco acima de 80% de uso! (83%)
```

## Explicando o Script

### 1.

```bash
USO=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
```

Esse comando é responsável  por **pegar a porcentagem de uso do disco da partição raiz `/` e guardar esse número na variável `USO`.**

Vamos por partes:

- `df -h /`
	- `df` mostra o uso do disco.
	- `-h` deixa em formato legível (MB/GB).
	- `/` especifica que queremos apenas a partição raiz (o disco principal onde o Linux está instalado).

**Exemplo de Saída:**

```
Filesystem      Size  Used  Avail  Use%  Mounted on
/dev/sda1        30G   24G   6.0G   80%  /
```

- `awk 'NR==2 {print $5}'`
	- `NR==2` significa: **pegue apenas a segunda linha** (a primeira é o cabeçalho).
	- `{print $5}` imprime a **quinta coluna**, que no exemplo acima é `80%` (a coluna de uso de disco).

Resultado parcial:

```shell
80%
```

- `sed 's/%//'`
	- O `sed` está removendo o símbolo `%` do valor.
	- Assim, `80%` vira apenas `80`.

Agora a variável `USO` contém apenas o número `80`, pronto para ser usado em comparações numéricas.

### 2.

```bash
if [ "$USO" -ge 80 ]; then
```

Esse trecho faz a **comparação** do valor armazenado em `USO`.

- `[ "$USO" -ge 80 ]`
	- Os colchetes `[]` são a forma do shell para **testar condições**.
	- `"$USO"` é o valor da variável (ex.: `80`).
	- `-ge` significa ***greater than or equal*** (maior ou igual).
	- `80` é o limite definido.

Então, essa condição está perguntando:
- **"O uso do disco é maior ou igual a 80%?"**

Se **sim**, executa o bloco após o `then` (mostra o alerta).
Se **não**, vai para o `else` e mostra mensagem de uso normal.

---
# Análise Gráfica

Algumas ferramentas gráficas úteis:

- **Baobab *(Disk Usage Analyzer)*** - interface simples para analisar graficamente.

![[Pasted image 20250823104630.png]]

- **Filelight** - apresenta gráficos interativos.

Instalação (Debian/Ubuntu):

```bash
sudo apt install baobab filelight
```

---
# Boas Práticas

- Configure **aletas automáticos** via `cron` para rodar verificações periódica.
- Limpe regularmente arquivos de log antigos:

```bash
sudo journalctl --vacuum-time=7d
```

- Utilize ferramentas como `ncdu` para investigações rápidas.
- Monitore diretórios críticos (`/var/log`, `/tmp`, `/home`, `/var/lib/mysql`).

---
# Conclusão

Monitorar o uso de disco no Linux **é fundamental para a saúde do sistema**. Ferramentas como `df` e `du` fornecem a visão rápida, emnquando `ncdu` e scripts de automação oferecem análises mais avançadas.

Mantes boas práticas de limpeza e monitoramento garante que servidores e estações de trabalho não sofram interrupções por falta de espaço.