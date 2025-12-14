2025-06-08 12:48

Status: #developed #Linux 

Tags: [[Linux]] | [[chmod]] | [[ls]]
 
----
# Introdução

O Linux organiza arquivos em uma estrutura hierárquica. Veja os principais diretórios:
  
| Diretório | Descrição                                                                                                                                                 |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/`       | Raiz do sistema                                                                                                                                           |
| `/home`   | Pastas dos usuários                                                                                                                                       |
| `/etc`    | Arquivos de configuração                                                                                                                                  |
| `/var`    | Arquivos variáveis (logs, bancos de dados)                                                                                                                |
| `/bin`    | Binários essenciais                                                                                                                                       |
| `/tmp`    | Arquivos temporários                                                                                                                                      |
| `/boot`   | armazenamento de arquivos necessários para a inicialização do sistema, incluindo o carregador de inicialização (boot loader) e o kernel do Linux.         |
| `/dev`    | armazenamento de arquivos de dispositivo (device files) que representam dispositivos de hardware, como discos rígidos, terminais e outros periféricos.    |
| `/lib`    | armazenamento de bibliotecas compartilhadas essenciais para binários localizados nos diretórios `/bin` e `\sbin`.                                         |
| `/media`  | ponto de montagem para mídias removíveis (drivers USB, por exemplo).                                                                                      |
| `/mnt`    | ponto de montagem temporária para sistemas de arquivos. Usado para montar temporariamente outros sistemas de arquivos durante a administração do sistema. |
| `/opt`    | armazenamento de aplicativos opcionais e pacotes de software adicionais que não fazem parte da instalação padrão do sistema.                              |
| `/proc`   | sistema de arquivos virtual que armazena informações sobre os processos em execução e o estado do kernel.                                                 |
| `/root`   | diretório pessoal do usuário root (superusuário).                                                                                                         |
| `/run`    | armazenamento de informações voláteis sobre o sistema desde a última inicialização, como PID files e sockets.                                             |
| `/sbin`   | armazenamento de binários essenciais para a administração do sistema, necessários para o boot e recuperação do sistema.                                   |
| `/srv`    | armazenamento de dados específicos de serviços fornecidos pelo sistema.                                                                                   |
| `/sys`    | sistema de arquivos virtual que fornece informações e interfaces para o kernel do Linux.                                                                  |
| `/usr`    | armazenamento de dados de usuário mais instalados pelo sistema, incluindo binários adicionais, bibliotecas e arquivos de cabeçalho.                       |

---
# Permissões de Arquivos

## Tipos de Permissões

Cada arquivo/pasta tem três categorias de permissões:

|Símbolo|Tipo|Descrição|
|---|---|---|
|`r`|**Leitura**|Permite visualizar o conteúdo.|
|`w`|**Escrita**|Permite modificar ou deletar.|
|`x`|**Execução**|Permite executar (arquivos) ou acessar (pastas).|

## Donos e Grupos

As permissões são aplicadas a três níveis:

| Nível          | Descrição                        |
| -------------- | -------------------------------- |
| **Dono (u)**   | Usuário proprietário do arquivo. |
| **Grupo (g)**  | Grupo associado ao arquivo.      |
| **Outros (o)** | Todos os demais usuários.        |

---
# Modificando Permissões

## Método 1: Modo Numérico *(Octal)*

Cada permissão tem um valo:

- `r` = 4
- `w` = 2
- `x` = 1

Some os valores para definir o nível de acesso:

| Permissão | Cálculo | Valor |
| --------- | ------- | ----- |
| `rwx`     | 4+2+1   | 7     |
| `rw-`     | 4+2     | 6     |
| `r-x`     | 4+1     | 5     |
| `r--`     | 4       | 4     |

```bash
chmod <dono><grupo><outros> arquivo
```

**Exemplos:**

```bash
chmod 755 script.sh    # Dono: rwx (7), Grupo/Outros: r-x (5)  
chmod 644 arquivo.txt  # Dono: rw- (6), Grupo/Outros: r-- (4)  
```

## Método 2: Modo Simbólico

Altera permissões específicas sem redefinir todas

| Símbolo | Ação                          |
| ------- | ----------------------------- |
| `+`     | Adiciona permissão.           |
| `-`     | Remove permissão.             |
| `=`     | Define permissões exatamente. |
**Comando:**

```bash
chmod <quem><operação><permissão> arquivo
```

**Exemplo:**

```bash
chmod u+x script.sh      # Adiciona execução ao dono.  
chmod g-w arquivo.txt    # Remove escrita do grupo.  
chmod o=rx pasta/        # Outros: apenas leitura + execução.  
```

---
# Alterando Dono e Grupo

Use `chown` para mudar o proprietário e `chgrp` para o grupo:

```bash
chown novo_usuario arquivo.txt      # Muda o dono.  
chown usuario:grupo arquivo.txt     # Muda dono e grupo.  
chgrp novo_grupo arquivo.txt        # Muda apenas o grupo.  
```

**Exemplo:**

```bash
sudo chown root:admin /backup/      # Define dono "root" e grupo "admin".  
sudo chmod 750 /backup/             # Dono: rwx, Grupo: r-x, Outros: nenhum.  
```


---
# Visualizando Permissões

Use `ls -l` para ver permissões:

```bash
ls -l arquivo.txt
```

**Saída:**

```text
-rw-r--r-- 1 usuario grupo 1024 Jun 8 10:00 arquivo.txt
```
#### Decifrando `-rw-r--r--`:

- O **primeiro caractere** (`-`) indica tipo (**`-`** = arquivo, **`d`** = pasta).

- Os **três grupos seguintes** representam:
    - **Dono (rw-)** → Leitura (`r`) + Escrita (`w`), sem execução (`-`).
    - **Grupo (r--)** → Apenas leitura (`r`).
    - **Outros (r--)** → Apenas leitura (`r`).

---
# Casos de Uso Comuns

| Situação                            | Comando Recomendado     |
| ----------------------------------- | ----------------------- |
| Script executável para o dono.      | `chmod u+x script.sh`   |
| Arquivo confidencial (apenas dono). | `chmod 600 secreto.txt` |
| Pasta compartilhada em grupo.       | `chmod 775 projetos/`   |
| Bloquear acesso público.            | `chmod o-rwx arquivo`   |

---
# Dicas Importantes

## ⚠️ **Cuidado com `chmod 777`!**

Libera acesso **total** a todos (inclusive execução). Use apenas em ambientes controlados

## **Pastas vs. Arquivos:**

- Para pastas, a permissão `x` significa **acesso** (sem ela, não é possível listar arquivos dentro). 

## **Superuser (root):**

- Se precisar alterar permissões de arquivos do sistema, use `sudo` antes do comando.

---
# Conclusão

- Permissões (`r`, `w`, `x`) controlam acesso a arquivos e pastas.
- Use `chmod` (modo numérico ou simbólico) para modificá-las.
- `chown` e `chgrp` alteram donos e grupos.