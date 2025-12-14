2025-07-24 20:32

Status: #developed #Linux 

Tags: [[Linux]] | [[sudo]] | [[pwd]] | [[ls]] | [[cd]] | [[cat]]

----
# Introdução

O **Linux** é um sistema operacional de código aberto baseado em Unix, amplamente utilizado em servidores, dispositivos embarcados e computadores pessoais. Sua interface mais poderosa e flexível é a linha de comando, também conhecida como **terminal** ou **shell**.

---
# 🔍 Navegação no Sistema de Arquivos

## `pwd` - *Print Working Directory*

- **Descrição:** Exibe o caminho completo do diretório em que o usuário está atualmente no terminal.
- **Uso:**

```bash
pwd
/home/usuário/Documentos/projeto
```

## `ls` - *List*

- **Descrição:** Lista arquivos e pastas dentro do diretório atual.
- **Uso básico:**

```bash
ls
```

- **Com a opção `-a`:** Mostra arquivos ocultos (aqueles que começam com `.`).

```bash
ls -a
```

- **Outras opções úteis:**
	- `-l`: Exibe em formato de lista detalhada.
	- `-h`: Exibe tamanhos legíveis por humanos (usado com `-l`).
	- `-R`: Lista diretórios recursivamente.

## `cd` - *Change Directory*

- **Descrição:** Altera o diretório atual.
- **Uso:**

```bash
cd /caminho/do/diretorio
```

**Exemplos:**

- Mudar para o diretório chamado `projeto`:

	```bash
cd projeto
```

- Voltar ao diretório anterior:

```bash
cd -
```

- Ir para o diretório pessoal do usuário:

```bash
cd ~
```

---
# 🔐 Acesso com Privilégios de *Superuser*

## `sudo` - *SuperUser Do*

- **Descrição:** Executa comandos com privilégios de administrador (root).
- **Uso:**

```bash
sudo comando
```

- **Exemplo:**

```bash
sudo ls /root
```

### `sudo -i`

- **Descrição:** Inicia uma sessão interativa como root. Você permanece logado como root até sair.
- **Uso:**

```bash
sudo -i
```

- **Observação:** Equivalente a logar como root, com todas as permissões e o ambiente root.

### `sudo su`

- **Descrição:** Abre um shell root, mas mantendo o ambiente do usuário atual.
- **Uso:**

```bash
sudo su
```

- **Diferença do `sudo -i`:**
	- `sudo su`: ambiente do usuário
	- `sudo -i`: ambiente root

---
# 📄 Manipulação de Arquivos

## `cat` - *Concatenate*

- **Descrição:** Exibe o conteúdo de um ou mais arquivos. Também pode ser usado para criar ou concatenar arquivos.
- **Uso básico:**

```bash
cat arquivo.txt
```

- **Criar um arquivo:**

```bash
cat > novo.txt
```

(Depois digite o conteúdo e pressione `Ctrl + D` para salva)


- **Concatenar arquivos:**

```bash
cat arq1.txt arq2.txt > combinado.txt
```

## `exit`

- **Descrição:** Encerra a sessão atual do terminal
- **Uso:**

```bash
exit
```

- **Exemplo de uso:**
	- Sair da conta root.
	- Fechar o terminal.

