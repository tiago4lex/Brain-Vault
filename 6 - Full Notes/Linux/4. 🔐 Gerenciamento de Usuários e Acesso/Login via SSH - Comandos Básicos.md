2025-06-08 12:27

Status: #developed #Linux 

Tags: [[Linux]] | [[SSH]]

----
# Introdução

Este documento fornece um guia prático para iniciantes em Linux, cobrindo:

1. **Como fazer login em uma máquina Linux via SSH**
2. **Comandos básicos para navegação e execução de tarefas**
3. **Interação com o sistema de arquivos**

---
# Login em uma Máquina Linux via SSH

O **SSH *(Secure Shell)*** é um protocolo que permite acessar remotamente um servidor Linux de forma segura.

## Pré-requisitos

- Ter um cliente SSH instalado (no Windows, use **PuTTy** ou **Git Bash**; no Linux/macOS, use o terminal).
- Conhecer o **endereço IP** ou **domínio** da máquina remota.
- Ter um **usuário** e **senha** válidos (ou chave SSH configurada).

## Comando para conectar

No terminal (Linux/macOS) ou Git Bash (Windows):

```bash
ssh usuario@ip_do_servidor
```

**Exemplo:**

```bash
ssh joao@192.168.1.100
```

### Primeiro acesso?

- Se for a primeira vez que o servidor é acessado, uma mensagem sobre a autenticidade do host será exibida. Digite `yes` para continuar.
- Em seguida, insira sua senha quando solicitado.

### Usando uma Porta Diferente (Padrão 22)

Se o servidor usar uma porta diferente (ex: 2222), use:

```bash
ssh -p 2222 usuario@ip_do_servidor
```

---
# Comando Básicos par Navegação

Depois de logado, é possível interagir com o sistema usando os seguintes comando.

## Comandos Essenciais

| Comando | Descrição                    | Exemplo                        |
| ------- | ---------------------------- | ------------------------------ |
| `pwd`   | Mostra o diretório atual     | `pwd` → `/home/usuario`        |
| `ls`    | Lista arquivos e pastas      | `ls -l` (lista detalhada)      |
| `cd`    | Muda de diretório            | `cd /var/www`                  |
| `mkdir` | Cria uma pasta               | `mkdir projetos`               |
| `touch` | Cria um arquivo vazio        | `touch arquivo.txt`            |
| `cat`   | Exibe conteúdo de um arquivo | `cat arquivo.txt`              |
| `cp`    | Copia arquivos/pastas        | `cp arquivo.txt backup/`       |
| `mv`    | Move/renomeia arquivos       | `mv antigo.txt novo.txt`       |
| `rm`    | Remove arquivos/pastas       | `rm arquivo.txt` (⚠️ Cuidado!) |
| `man`   | Manual de um comando         | `man ls`                       |

## Exemplo de Fluxo

```bash
cd ~/Documentos      # Entra na pasta Documentos
ls                   # Lista arquivos
touch teste.txt      # Cria um arquivo
echo "Olá, Linux!" > teste.txt  # Escreve no arquivo
cat teste.txt        # Mostra o conteúdo
```

---


---
