2026-01-18 20:20

Status: #developed #Linux 

Tags: [[Linux]] | [[chmod]] | [[umask]] | [[setfacl]]

----
# Introdução

O Linux é um sistema **multiusuários**, o que significa que o controle de acesso é essencial para garantir:

- Confidencialidade
- Integridade
- Disponibilidade (CIA Triad)

O controle de acesso define:

- **Quem** pode acessar um recurso
- **O que** pode fazer (ler, escrever, executar)

Os principais mecanismos nativos são:

- Permissões tradicionais (`chmod`)
- Máscara de criação (`umask`)
- Listas de controle de acesso (ACLs - `setfacl`)

---
# Modelo Clássico de Permissões no Linux

Todo arquivo/diretório possui permissões associadas a:

| **Entidade** | **Descrição**            |
| ------------ | ------------------------ |
| Owner (u)    | Dono do arquivo          |
| Group (g)    | Grupo do arquivo         |
| Others (o)   | Todos os demais usuários |

E três tipos de permissão:

| **Permissão** | **Arquivo**      | **Diretório**          |
| ------------- | ---------------- | ---------------------- |
| r (read)      | Ler conteúdo     | Listar arquivos        |
| w (write)     | Alterar conteúdo | Criar/remover arquivos |
| x (execute)   | Executar arquivo | Acessar diretório      |

---
# Controle de Permissões com `chmod`

## O que é `chmod`

O comando `chmod` *(change mode)* altera permissões de arquivos e diretórios.

## Visualizando permissões

```bash
ls -l arquivo.txt
```

Exemplo:

```bash
-rwxr-x--- 1 usuário dev 1234 arquivo.sh
```

Interpretação:

- `rwx` → dono
- `r-x` → grupo
- `---` → outros

## Modo simbólico

```bash
chmod u+x arquivo.sh
chmod g-w arquivo.txt
chmod o+r arquivo.txt
```

Combinações:

- `u` (user), `g` (group), `o` (others), `a` (all)
- `+` adiciona, `-` remove, ` = ` define exatamente

**Exemplo:**

```bash
chmod ug+rx arquivo.sh
```

## Modo numérico (octal)

| Valor | Permissão |
| ----- | --------- |
| 4     | read      |
| 2     | write     |
| 1     | execute   |

Exemplo:

```bash
chmod 750 script.sh
```

| **Dono** | **Grupo** | Outros  |
| -------- | --------- | ------- |
| 7 (rwx)  | 5 (r-x)   | 0 (---) |

## Permissões especiais

### SUID (Set User ID)

```bash
chmod u+s arquivo
```

- Executa o arquivo com permissões do dono
- Muito usado em binários como `passwd`

### SGID (Set Group ID)

```bash
chmod g+s diretório
```

- Arquivos criados herdam o grupo do diretório

### Sticky Bit

```bash
chmod +t diretório
```

- Apenas o dono pode apagar arquivos
- Exemplo clássico: `/tmp`

---
# Máscara de Criação `umask`

## O que é `umask`?

O `umask` define quais **permissões NÃO serão concedidas** na criação de novos arquivos e diretórios.

## Permissões padrão

| Tipo       | Base |
| ---------- | ---- |
| Arquivos   | 666  |
| Diretórios | 777  |

## Exemplo prático

```bash
umask
```

**Saída:**

```yaml
0022
```

Cálculo:

- Diretório: `777 - 022 = 755`
- Arquivo: `666 - 022 = 644`

## Definir `umask`

```bash
umask 027
```

Resultado:

- Diretórios: 750
- Arquivos: 640

> Muito usado para **ambientes corporativos e servidores**.

## Configurações persistentes

Adicionar em:

- `~/.bashrc`
- `/etc/profile`
- `/etc/login.defs`

---
# ACL - Listas de Controle de Acesso (`setfacl`)

## Por que ACLs existem?

O modelo tradicional é limitado:

> “Apenas um dono e um grupo”

ACLs permitem:

- Permissões **para usuários específicos**
- Permissões **para múltiplos grupos**

## Verificar suporte a ACL

```bash
mount | grep acl
```

## Ver ACL de um arquivo

```bash
getacl arquivo.txt
```

## Definir permissão para usuário específico

```bash
setfacl -m u:joao:r arquivo.txt
```

João pode ler o arquivo, mesmo não sendo dono.

## Definir permissão para grupo

```bash
setfacl -m g:devs:rw arquivo.txt
```

## ACL padrão diretórios

```bash
setfacl -d -m u:joao:rw diretorio/
```

Arquivos criados herdarão essa permissão.

## Remover ACLs

```bash
setfacl -b arquivo.txt
```


---
# Comparação: `chmod` vs `umask` vs `setfacl`

|Recurso|chmod|umask|setfacl|
|---|---|---|---|
|Altera permissões existentes|✅|❌|✅|
|Define permissões padrão|❌|✅|✅|
|Usuários específicos|❌|❌|✅|
|Múltiplos grupos|❌|❌|✅|
|Uso corporativo/avançado|⚠️|⚠️|✅|

---
# Boas Práticas de Segurança

✔ Evitar permissões `777`  
✔ Usar `umask` restritivo em servidores  
✔ Aplicar ACLs com moderação  
✔ Monitorar permissões de arquivos sensíveis  
✔ Revisar permissões de scripts executáveis  
✔ Proteger diretórios críticos (`/etc`, `/var/log`)

---
# Relação com Cibersegurança

Permissões mal configuradas podem levar a:

- Escalonamento de privilégios
- Vazamento de dados
- Execução arbitrária de código

Ferramentas como `chmod`, `umask` e `setfacl` são **controles de segurança fundamentais** para:

- Hardening de sistemas
- Defesa em profundidade
- Conformidade (ISO 27001, CIS Benchmarks)

---
# Conclusão

- `chmod` controla permissões básicas e especiaisq
- `umask` define políticas de criação seguras
- `setfacl` oferece controle granular avançado
- Juntos, formam a **base do controle de acesso no Linux**