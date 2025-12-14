2025-07-29 19:04

Status: #developed #Linux 

Tags: [[Linux]] | [[crontab]]

----
# 🎯 O que é o `crontab`?

O `crontab` *(CRON Table)* é usado para **agendar comandos ou scripts** para serem executados automaticamente em horários, datas ou intervalos definidos. Ele faz parte do serviço `cron`, o agendados de tarefas padrão no Linux.

---
# 📌 Sintaxe Básica

Um arquivo `crontab` tem a seguinte estrutura de 5 campos obrigatórios de tempo + o comando a ser executado:

```nginx
MIN HORA MÊS DIA-SEMANA comando
```

| **Campo**    | **Significado** | **Valores possíveis** |
| ------------ | --------------- | --------------------- |
| `MIN`        | Minuto          | 0-59                  |
| `HORA`       | Hora            | 0-23                  |
| `DIA`        | Dia do mês      | 1-31                  |
| `MÊS`        | Mês             | 1-12                  |
| `DIA-SEMANA` | Dia da semana   | 0-7 (0 e 7 = Domingo) |

---
# 🔧 Comandos úteis com `crontab`

| **Comando**                  | **Função**                                        |
| ---------------------------- | ------------------------------------------------- |
| `crontab -e`                 | Edita o agendador de tarefas do usuário atual     |
| `crontab -l`                 | Lista as tarefas agendadas                        |
| `crontab -r`                 | Remove todas as tarefas do usuário                |
| `sudo crontab -e`            | Edita tarefas do `root` (tarefas administrativas) |
| `crontab -u nome_usuario -e` | Edita o `crontab` de outro usuário (requer sudo)  |

---
# 🧪 Exemplos de Agendamentos

## Rodar um script todos os dias às 3h da manhã

```bash
0 3 * * * /home/usuario/backup.sh
```

## Rodar toda a segunda-feira às 8h

```bash
0 8 * * 1 /home/usuario/limpeza_temp.sh
```

## Rodar a cada 15 minutos

```bash
*/15 * * * * home/usuario/verificar_servico.sh
```

## Rodar a cada dia 1º de cada mês às 6h

```bash
0 6 * * /home/usuario/relatorio_mensal.sh
```

---
# 📝 Como salvar logs de comandos agendados

Para registrar a saída padrão (``stdout``) e erros (``stderr``), adicione ao final do comando:

```bash
0 3 * * * /home/usuario/script.sh >> /var/log/script.log 2>&1
```

---
# 🧠 Dicas importantes

- Sempre **teste seu script manualmente** antes de agendar.
- Use **caminhos absolutos** para comandos e arquivos no `crontab`.
- O ambiente do `cron` é mais restrito (sem as variáveis usuais como `$PATH`), então prefira escrever caminhos completos.

---
# 📂 Localização dos arquivos do cron

- `crontab -e` salva em: `/var/spool/cron/crontabs/usuario`
- Arquivos do sistema: `/etc/crontab` e `/etc/cron.*` (cron.hourly, cron.daily etc.)

---
# ⏱️ Ferramentas gráficas e alternativas

- `gnome-schedule`: Interface gráfica para agendamento (em desktops).    
- `at`: Agendamento **único** (não recorrente).
- `systemd timers`: Alternativa moderna ao cron (para sistemas com systemd).
