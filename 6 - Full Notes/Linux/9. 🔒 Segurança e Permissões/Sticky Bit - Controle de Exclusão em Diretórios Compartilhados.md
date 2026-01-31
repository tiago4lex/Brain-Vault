2026-01-22 13:26

Status: #developed #Linux 

Tags: [[Linux]]

----
# Introdução

## O que é o Sticky Bit?

O **Sticky Bit** é uma **permissão especial** do Linux aplicada **principalmente a diretórios**, que **restringe a exclusão e renomeação** de arquivos.

Quando ativado em um diretório:

- Qualquer usuário pode **criar arquivos** (se tiver permissão escrita)
- **Apenas o dono do arquivo**, o **dono do diretório** ou o **root** podem **apagar ou renomear** esses arquivos.

> Isso impede que usuários apaguem arquivos de outros usuários em diretórios compartilhados.

---
# Por que o Sticky Bit existe?

Sem Sticky Bit:

- Usuários com permissão de escrita em um diretório poderiam apagar arquivos de qualquer outro usuário.

Com Sticky Bit:

- Escrita continua permitida
- Exclusão fica restrita ao proprietário

> É uma **medida essencial de segurança em ambientes multiusuário**.

---
# Exemplo clássico: `/tmp`

O diretório `/tmp` é o exemplo mais conhecido:

```bash
ls -ld /tmp
```

Saída típica:

```bash
drwxrwxrwt 10 root root 4096 Aug 23 10:00 /tmp
```

## Interpretação

- `rwx` → dono (root)
- `rwx` → grupo
- `rwt` → outros
- **`t` indica Sticky Bit ativo**

✔ Todos podem criar arquivos  
✔ Ninguém pode apagar arquivos de outros usuários

---
# Como funciona na prática

## Sem Sticky Bit

```bash
mkdir /tmp_test
chomod 777 /tmp_test
```

Agora:

- Qualquer usuário pode criar arquivos
- Qualquer usuário pode apagar arquivos dos outros

>[!warning] Atenção:
>**Risco de segurança elevado!**

## Ativando Sticky Bit

### Modo simbólico

```bash
chmod +t diretorio
```

### Modo numérico

```bash
chmod 1777 diretorio
```

> O 1 no início representa o Sticky Bit

| **Digítio** | Significado  |
| ----------- | ------------ |
| 1           | Sticky Bit   |
| 7           | rwx (owner)  |
| 7           | rwx (group)  |
| 7           | rwx (others) |

## Removendo o Sticky Bit

```bash
chmod -t diretorio
```

Ou:

```bash
chmod 0777 diretorio
```

---
# Identificando o Sticky Bit

## No `ls -l`

- `t` → Sticky Bit ativo e permissão de execução
- `T` → Sticky Bit ativo **sem** permissão de execução

Exemplos:

```text
drwxrwxrwt  → correto
drwxrwxrwT  → mal configurado
```

> Sticky Bit em diretórios **exige permissão de execução** (`x`) para funcionar corretamente.

---
# Onde o Sticky Bit deve ser usado?

✔ Diretórios temporários  
✔ Diretórios compartilhados entre usuários  
✔ Ambientes multiusuário (universidades, servidores)  
✔ Sistemas com múltiplos serviços escrevendo no mesmo diretório

Exemplos:

```bash
/tmp
/var/tmp
/diretorio_compartilhado
```

---
# Onde NÃO usar Sticky Bit?

❌ Arquivos regulares (obsoleto e sem efeito prático hoje)  
❌ Diretórios privados  
❌ Diretórios sensíveis do sistema (`/etc`, `/bin`, `/usr`)

---
# Sticky Bit vs SUID vs SGID

|Permissão|Uso principal|Risco|
|---|---|---|
|**Sticky Bit**|Proteção contra exclusão|Baixo|
|**SUID**|Executar como dono|Alto|
|**SGID**|Herança de grupo|Médio|

> Sticky Bit é o **mais seguro** entre as permissões especiais.

---
# Relação com Segurança e Hardening

O Sticky Bit:

- Previne **DoS local** (apagando arquivos alheios)
- Reduz riscos em diretórios públicos
- É recomendado em **CIS Benchmarks**
- Evita abuso em ambientes multiusuário

---
# Teste prático

```bash
mkdir /tmp_lab
chmod 1777 /tmp_lab
ls -ld /tmp_lab
```

Saída esperada:

```bash
drwxrwxrwt 2 usuario usuario 4096 Aug 23 10:30 /tmp_lab
```

---
# Conclusão

- Sticky Bit controla **quem pode apagar arquivos**
- Funciona principalmente em **diretórios**
- Essencial para diretórios compartilhados
- Simples, seguro e extremamente importante

