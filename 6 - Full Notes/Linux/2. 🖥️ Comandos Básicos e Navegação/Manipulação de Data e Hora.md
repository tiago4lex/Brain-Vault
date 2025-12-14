
2025-07-29 17:34

Status: #developed #Linux 

Tags: [[Linux]] | [[date]]

----
# Introdução

O comando `date` é utilizado para:

- **Exibir** a data e hora atual do sistema.
- **Formatar** a data/hora em estilos personalizados.
- **Modificar** a data/hora (com permissões de superuser)
- **Converter** formato de datas
- **Usar em scripts** para gerar logs, nomes de arquivos, backups, etc.

---
# 📌 Sintaxe

```bash
date [opções] [+formato]
```

---
# 🕘 Exemplos Básicos

## 1. Exibir data e hora atuais

```bash
date
```

**Saída típica:**

```java
Mon Jul 29 17:42:10 -03 2025
```

## 2. Exibir apenas o ano, mês e dia

```bash
data +"%Y-%m-%d"
```

**Saída:**

```java
2025-07-29
```

## 3. Exibir hora no formato 24 horas

```bash
date +"%H:%M:%S"
```

**Saída:**

```java
17:40:54
```

## 4. Exibir dia da semana, data completa e hora

```bash
date +"%A, %d de %B de %Y - %H:%M"
```

**Exemplo de saída (em inglês):**

```java
Tuesday, 29 de July de 2025 - 17:42
```

---
# 📆 Principais Códigos de Formatação

| **Código** | **Significado**                            | **Exemplo**  |
| ---------- | ------------------------------------------ | ------------ |
| `%Y`       | Ano com 4 dígitos                          | `2025`       |
| `%y`       | Ano com 2 dígitos                          | `25`         |
| `%m`       | Mês (01-12)                                | `07`         |
| `%d`       | Dia do mês (01-31)                         | `29`         |
| `%H`       | Hora (00-23)                               | `17`         |
| `%I`       | Hora (01-12)                               | `05`         |
| `%M`       | Minuto (00-59)                             | `42`         |
| `%S`       | Segundo (00-59)                            | `10`         |
| `%A`       | Nome do dia da semana                      | `Tuesday`    |
| `%B`       | Nome do mês                                | `July`       |
| `%Z`       | Fuso horário                               | `-03`        |
| `%s`       | Timestamp UNIX (segundos desde 01/01/1970) | `1753821730` |

---
# 🔧 Alterar a Data e Hora do Sistema (como root)

```bash
sudo date --set="2025-07-29 17:45:00"
```

>[!warning] Atenção!
>Requer permissões administrativas. Evite em sistemas de produção - preferencialmente use `timedatectl`.

---
# 🛠️ Exemplos Práticos

## Nomear um backup com data

```bash
cp arquivo.txt backup_$(date +%Y%m%d_%H%M%S).txt
```

> Gera algo como `backup_20250729_174510.txt`

## Exibir a data de ontem

```bash
date -d "yesterday" +"%Y-%m-%d"
```

## Exibir a data daqui a 7 dias

```bash
date -d "+7 days" +"%A, %d/%m/%Y"
```
## Ver o timestamp atual

```bash
date +%s
```

→ Exemplo: `1753821730`

---
# ⏳ Relógio e Fuso Horário

```bash
timedatectl
```

> Mostra o horário local, UTC, RTC, e se o sistema está sincronizado com NTP.

