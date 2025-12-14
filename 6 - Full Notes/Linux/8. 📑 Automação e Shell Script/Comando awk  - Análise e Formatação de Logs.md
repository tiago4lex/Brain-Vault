2025-08-21 09:01

Status: #developed #Linux 

Tags: [[Linux]] | [[awk]] | [[logs]]

----
# Introdução

## O que é o `awk`?

O `awk` é uma **linguagem de processamento de texto** integrada ao Linux, usada para **varrer aarquivos linha por linha** e aplicar ações sobre cada linha com base em **padrões definidos**.

Ele é muito útil para:

- Extrair colunas específicas.
- Filtrar linhas com base em condições.
- Processar e formatar **logs do sistema**.
- Criar relatórios a partir de arquivos de texto.

---
# Sintaxe básica

```bash
awk 'padrão {ação}' arquivo
```

- `padrão`: condição a ser verificada em cada linha.
- `ação`: o que fazer quando a condição for verdadeira.
- `arquivo`: arquivo de entrada (pode ser um log).

Se nenhum padrão é especificado → o `awk` aplica a **ação** em todas as linhas.
Se nenhuma ação é especificada → o `awk` **imprime a linha inteira**.

---
# Variáveis internas mais usadas

- `$0` → linha inteira.
- `$1, $2, $3...` → colunas (separadas por espaço ou delimitador).
- `NR` → número da linha.
- `NF` → quantidade de campos (colunas) da linha.

---
# Exemplos práticos com logs

## 1. Extrair IPs de um log

```bash
awk '{print $1}' /var/log/auth.log
```

- Imprime a **primeira coluna** de cada linha do log (geralmente contém IP ou hostname).

## 2. Mostrar número da linha + conteúdo

```bash
awk '{print NR, $0}' /var/log/syslog
```

- Numera cada linha do log (`NR` = número da linha)

## 3. Filtrar falhas de login

```bash
awk '/Failed password/ {print $0}' /var/log/auth.log
```

- Procura linhas contendo `"Failed password"` e imprime a linha inteira.

## 4. Contar tentativas de login por usuário

```bash
awk '/Failed password/ {print $(NF-5)}' /var/log/auth.log | sort | uniq -c
```

- Nesse caso:
	- `$(NF-5)` → pega a coluna referente ao usuário (em logs do sshd, o usuário está nessa posição).
	- `sort | uniq -c` → conta quantas vezes cada usuário aparece.

## 5. Exibir data e mensagem do log formatado

```bash
awk '{print $1, $2, $3, "->", substr($0, index($0,$5))}' /var/log/syslog
```

- Esse comando:
	- `$1, $2, $3` → mostra **data e hora**.
	- `"->"` → adiciona um separador.
	- `substr($0, index($0,$5))` → imprime a mensagem do log a partir da quinta coluna.

**Exemplo de saída:**

```les
Aug 20 11:05:01 -> CRON[1234]: pam_unix(cron:session): session opened
```

---
# Formatação de saída

É possível usar `printf` dentro do `awk` para formatar colunas, alinhamentos e textos:

```bash
awk '{printf "Linha %d | Usuário: %-10s | IP: %s\n", NR, $9, $11}' /var/log/auth.log
```

- Esse comando imrpime:

```
Linha 23 | Usuário: tiago      | IP: 192.168.0.15
Linha 57 | Usuário: admin      | IP: 203.0.113.55
```

---
# Criando Scripts para Monitoramento de Logs

O `awk` pode ser facilmente integrado em **scripts Bash** para automatizar a análise de logs do sistema.

Isso é especialmente útil em **cibersegurança**, onde é necessário monitorar tentativas de login, erros e eventos suspeitos.

## Exemplo prático de script de monitoramento

```bash
#!/bin/bash

# Diretório onde os relatórios serão salvos
LOG_DIR="monitoramento_sistema"
mkdir -p $LOG_DIR

# Arquivo de saída
OUTPUT = "$LOG_DIR/monitoramento_logs_sistema.txt"

# Procurar mensagens críticas nop syslog e formatar com awk
grep -E "fail(ed)?|error|denied|unauthorized" /var/log/syslog \
| awk '{print $1, $2, $3, $5, $6, $7}' > $OUTPUT

echo "Relatório de monitoramento gerado em: $OUTPUT"
```

## Como o script funciona?

1. `mkdir -p $LOG_DIR` → Cria o diretório onde os relatórios serão armazenados (não dá erro se já existir).
2. `grep -E "fail(ed)?|error|denied|unauthorized"` → Filtra do `/var/log/syslog` apenas linhas que contenham **palavras relacionadas a falhas** (como "failed", "error", "denied").
3. `awk '{print $1, $2, $3, $5, $6, $7}'` → Extrai apenas as colunas de interesse:
	- `$1 $2 $3` → Data e hora da ocorrência.
	- `$5 $6 $7` → Serviço e mensagem resumida.

4. `> $OUTPUT` → Salva o resultado no arquivo `monitoramento_logs_sistema.txt`.

## Exemplo de saída do relatório

```
Aug 20 14:55:10 sshd[2345] pam_unix(sshd:auth): authentication failure
Aug 20 14:55:12 sshd[2345] Failed password for invalid user admin
Aug 20 14:55:15 sshd[2345] error: maximum authentication attempts exceeded
```

## Automatizando com `crontab`

Você pode configurar o script para rodar automaticamente em intervalos de tempo com o `crontab`:

```bash
crontab -e
```

E adicionar, por exemplo, para rodar a cada 10 minutos:

```
*/10 * * * * /home/tiago/monitorar_logs.sh
```

---
# Resumo

- `awk` é essencial para **analisar logs**.
- Usa colunas ($1, $2, etc.) e condições para extrair informações.
- Pode ser combinado com `sort`, `uniq`, `grep` para relatórios ainda mais completos.
- Muito usado em **segurança (SSH, auth.log)** e em automação de análise de logs.

---
# Referências

[Documentação Oficial do Comando awk pela GNU](https://www.gnu.org/software/gawk/manual/gawk.html)

