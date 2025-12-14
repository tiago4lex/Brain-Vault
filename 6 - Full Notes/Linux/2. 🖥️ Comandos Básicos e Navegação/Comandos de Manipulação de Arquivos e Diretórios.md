2025-07-24 21:53

Status: #developed #Linux 

Tags: [[Linux]] | [[cp]] | [[rm]] | [[nano]] | [[touch]] | [[mkdir]] | [[mv]]

----
# Introdução

Trabalhar com arquivos e diretórios é essencial no uso do terminal Linux. Nesta secção serão descritos comandos fundamentais como `mkdir`, `touch`, `cp`, `nano`, `rm` e `mv`. todos voltados para **criação, edição, movimentação, renomeação e exclusão** de arquivos e pastas.

---
# 📁 `mkdir` — *Make Directory*

- **Descrição:** Cria um ou mais diretórios (pastas).
- **Uso:**

```bash
mkdir nome_do_diretorio
```

**Exemplos:**

- Criar uma pasta chamada `meus_projetos`:

```bash
mkdir meus_projetos
```

- Criar vários diretórios de uma vez:

```bash
mkdir pasta1 pasta2 pasta3
```

- Criar subdiretórios com hierarquia:

```bash
mkdit -p projetos/frontend/react
```

A opção `-p` cria diretórios pais que ainda não existem.

---
# 📄 `touch` — *Criar Arquivos Vazios*

- **Descrição**: Cria arquivos vazios ou atualiza a data de modificação de arquivos existentes.
- **Uso**:

```bash
touch nome_do_arquivo
```

**Exemplos:**

- Criar um arquivo de texto:

```bash
touch notas.txt
```

- Criar vários arquivos ao mesmo tempo:

```bash
touch arquivo1.txt arquivo2.txt
```

---
# ✍️ `nano` — *Editor de Texto no Terminal*

- **Descrição**: Abre o editor de texto `nano`, que permite criar e editar arquivos diretamente pelo terminal.
- **Uso**:

```bash
nano nome_do_arquivo
```

**Exemplo:**

```bash
nano anotacoes.txt
```

- Atalhos úteis dentro do `nano`:
	- `Ctrl + O`: Salvar
	- `Enter`: Confirmar o nome do arquivo
	- `Ctrl + X`: Sair
	- `Ctrl + K`: Cortar linha
	- `Ctrl + U:` Colar linha

---
# 🔁 `mv` — *Move e Renomeia Arquivos ou Diretórios*

- **Descrição**: Move arquivos/diretórios ou altera seus nomes.
- **Uso**:

```bash
mv origem destino
```

**Exemplos:**

- **Renomear um arquivo:**

```bash
mv antigo.txt novo.txt
```

- **Mover arquivo para outra pasta:**

```bash
mv documento.txt /home/usuario/Documentos/
```

- **Mover e renomear ao mesmo tempo:**

```bash
mv texto.txt /home/usuario/Documentos/renomeado.txt
```

---
# ❌ `rm` — *Remove Arquivos e Diretórios*

- **Descrição**: Exclui arquivos e diretórios. Use com cautela — os arquivos são **removidos permanentemente**.
- **Uso**:

```bash
rm nome_do_arquivo
```

- **Opções comuns:**
	- `-r`: Remove diretórios recursivamente (necessário para pastas).
	- `-f`: Força a remoção, sem pedir confirmação.

**Exemplos:**

- Apagar um arquivo:

```bash
rm lixo.txt
```

- Apagar uma pasta e todo o seu conteúdo:

```bash
rm -r projetos_antigos
```

- Forçar a exclusão de uma pasta sem confirmação:

```bash
rm -rf backup/
```

>[!warning] **Atenção:**
>Não há lixeira. O comando `rm` **não** envia os arquivos para a lixeira!

---
# 📄➡️ `cp` — *Copy*

- **Descrição**: Copia arquivos e diretórios.
- **Uso**:

```bash
cp origem destino
```

- **Opções úteis:**
	- `-r`: Copia diretórios recursivamente.
	- `-v`: Modo "verbose", mostra o que está sendo copiado.

**Exemplos:**

- Copiar um arquivo para outra pasta:

```bash
cp texto.txt /home/usuario/Documentos
```

- Copiar e renomear o arquivo:

```bash
cp texto.txt copia_texto.txt
```

- Copiar uma pasta inteira:

```bash
cp -r projetos projetos_backup
```

---
# Resumo Rápido dos Comandos

| **Comando** | **Função**                         |
| ----------- | ---------------------------------- |
| `mkdir`     | Cria diretórios                    |
| `touch`     | Cria arquivos vazios               |
| `nano`      | Edita arquivos no terminal         |
| `mv`        | Move ou renomeia arquivos e pastas |
| `rm`        | Remove arquivos e diretórios       |
| `cp`        | Copia arquivos ou diretórios       |
