2025-07-26 09:56

Status: #developed #Linux 

Tags: [[Linux]] | [[vim]]

----
# 📌 O que é o `vim`?

O `vim` ***(Vi Improved)*** é um dos editores de texto mais poderosos e usados no mundo Linux e Unix. Ele é uma versão aprimorada do clássico edito `vi`, com muitos recursos adicionais como realce de sintaxe, múltiplos níveis de desfazer, busca, macros, entre outros.

>[!note] Nota
>O Vim é um editor **baseado em modos**, o que o torna muito diferente de editores como Nano, VS Code ou Notepadd++.

---
# 🧠 Principais Modos do Vim

O Vim funciona em **diferentes modos, e entender isso é essencial para usá-lo:**

| **Modo**         | **Função Principal**                        |
| ---------------- | ------------------------------------------- |
| Normal           | Navegar, deletar, copiar, colar, etc.       |
| Inserção         | Digitar texto normalmente                   |
| Comando          | Executar comandos (`:w`, `:q`, `:wq`)       |
| Visual           | Selecionar texto                            |
| Linha de Comando | Usado para salvar, sair, buscar, substituir |

---
# 🚀 Iniciando o Vim

```bash
vim nome_do_arquivo.txt
```

- Se o arquivo não existir, ele será criado.
- O Vim abre por padrão no **modo normal**.

---
# 🔄 Alternando entre Modos

| **Ação**                   | **Comando**                                        |
| -------------------------- | -------------------------------------------------- |
| Entrar no modo de inserção | `i` (antes do cursor), `I` (início da linha)       |
| Voltar para o modo normal  | `Esc`                                              |
| Entrar no modo de comando  | `:` (do modo normal)                               |
| Entrar no modo visual      | `v` (caracteres), `V` (linhas), `Ctrl + v` (bloco) |

---
# 💾 Comandos no Modo de Comando

| **Comando**   | **Ação**                                   |
| ------------- | ------------------------------------------ |
| `:w`          | Salva um arquivo                           |
| `:q`          | Sai do vim                                 |
| `:wq` ou `:x` | Salva e sai                                |
| `:q!`         | Sai **sem salvar**                         |
| `:e nome.txt` | Abre outro arquivo                         |
| `:set number` | Mostra números de linha                    |
| `:syntax on`  | Ativa realce de sintaxe (útil para código) |

---
# ⌨️ Navegação no Modo Normal

| **Tecla**  | **Ação**                                         |
| ---------- | ------------------------------------------------ |
| `h`        | Move o cursor para a esquerda                    |
| `l`        | Move o cursos para a direita                     |
| `j`        | Move para a linha de baixo                       |
| `k`        | Move para a linha de cima                        |
| `gg`       | Vai para o início do arquivo                     |
| `G`        | Vai para o fim do arquivo                        |
| `0`        | Vai para o início da linha atual                 |
| `^`        | Vai para o primeiro caractere não vazio da linha |
| `$`        | Vai para o fim da linha                          |
| `Ctrl + f` | Página para frente                               |
| `Ctrl + b` | Página para trás                                 |

---
# ✂️ Edição de Texto (Modo Normal)


| **Comando** | **Ação**                      |
| ----------- | ----------------------------- |
| `i`         | Insere antes do cursor        |
| `I`         | Insere no início da linha     |
| `a`         | Adiciona depois do cursor     |
| `A`         | Adiciona no fim da linha      |
| `o`         | Abre nova linha abaixo        |
| `O`         | Abre nova linha acima         |
| `x`         | Deleta caractere sob o cursor |
| `dd`        | Deleta a linha atual          |
| `yy`        | Copia a linha                 |
| `p`         | Cola após o cursor            |
| `u`         | Desfaz última ação            |
| `Ctrl + r`  | Refaz ação desfeita           |
| `r<char>`   | Substitui um caractere        |

---
# 🔍 Busca e Substituição

## 🔎 Buscar

- **Buscar palavra:**

```vim
/palavra
```

- Repetir busca para frente: `n`
- Repetir busca para trás: `N`

## ✏️ Substituir

- Substituir a palavra "velha" por "nova" em uma linha:

```vim
:s/velha/nova
```

- Em todo o arquivo (global):

```vim
:%s/velha/nova/g
```

- Confirmar cada substituição:

```vim
:%s/velha/nova/gc
```

---
# 🧠 Dicas Extras

- Use `:help` dentro do Vim para acessar a documentação
- Para iniciantes, uma boa prática é usa `vimtutor` no terminal:

```bash
vimtutor
```

- Você pode personalizar o Vim com um arquivo chamado `.vimrc`.



