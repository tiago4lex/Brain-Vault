2025-08-22 11:50

Status: #developed #Linux 

Tags: [[Linux]] | [[Shell Script]]

----
# Introdução

## O que é Shell Script?

Um **Shell Script** é um arquivo de texto que contém uma séria de comandos que podem ser executados no **terminal Linux** de forma automática.

Ele permite automatizar tarefas repetitivas, monitorar sistemas, manipular arquivos, fazer, backups, tester conexões de rede, entre outros.

O shell mais comum no Linux é o **Bash *(Bourne Again SHell)***, mas existem outros como `sh`, `zsh`, `ksh`, e `fish`.

---
# Estrutura Básica de um Shell Script

Um script começa com o **shebang**, que indica ao sistema qual interpretador usar:

```bash
#!/bin/bash
```

- `#!` → Shabang, obrigatório para scripts executáveis.
- `/bin/bash` → caminho para o interpretador Bash.

**Exemplo simples:**

```bash
#!/bin/bash
# Este script imprime uma mensagem

echo "Olá, mundo!"
```

**Para executar:**

```bash
chmod +x meu_script.sh  # Torna o script executável
./meu_script.sh         # Executa o scipt
```

---
# Comentários

- Comentários começam com `#` e não são executados.

```bash
# Este é um comentário
```

- Úteis para documentação e explicações dentro do script.

---
# Variáveis

- Armazenam valores que podem ser reutilizados.

```bash
NOME="José"
echo "Olá, $NOME"
```

- Não use espaços ao atribuir valores (`NOME = "José"` está errado).

## Variáveis especiais:

| Variável    | Significado                       |
| ----------- | --------------------------------- |
| `$0`        | Nome do script                    |
| `$1, $2...` | Argumentos passados ao script     |
| `$#`        | Número de argumentos              |
| `$?`        | Código de saída do último comando |
| `$$`        | PID do script                     |

---
# Estruturas de controle

## 1. Condicional `if`

```bash
if [ "$USUARIO" == "root" ]; then
    echo "Você é o root"
else
    echo "Você não é root"
fi
```

- `-eq`, `-ne`, `-gt`, `-lt` → operadores numéricos.
- ` == ` → operador de igualdade para strings.

## 2. Laços `for`

```bash
for i in 1 2 3; do
	echo "Núnmero: $i"
done
```

## 3. Laços `while`

```bash
contador=0
while [ $contador -lt 5 ]; do
    echo "Contador: $contador"
    ((contador++))
done
```

---
# Funções

Permitem agrupar comandos reutilizáveis:

```bash
minha_funcao() {
    echo "Executando função"
}

minha_funcao  # Chamada da função
```

---
# Redirecionamento e Pipes

- `>` → redireciona saída para arquivo (sobrescreve)
- `>>` → adiciona saída a arquivo existente
- `<` → lê de arquivo
- `2>` → redireciona erros
- `|` → envia saída de um comando como entrada de outro

Exemplo:

```bash
ls -l > lista_arquivos.txt
cat lista_arquivos.txt | grep ".sh"
```

---
# Comandos comuns em scripts

- `echo` → imprime mensagens no terminal
- `read` → lê entrada do usuário
- `date` → exibe data e hora
- `grep`, `awk`, `sed` → processam texto e logs
- `curl`, `ping` → monitoramento de rede

---
# Boas Práticas

1. Sempre use **comentários** para explicar o que cada parte faz.
2. Teste scripts em um ambiente seguro antes de rodar em produção.
3. Use **variáveis e funções** para deixar o script organizado.
4. Trate erros e códigos de saída para evitar falhas silenciosas.

---
# Exemplo de script completo

```bash
#!/bin/bash
# Script de monitoramento simples

LOG="monitoramento_$(date +%F).txt"

# Função para testar conexão
testar_internet() {
    if ping -c 1 8.8.8.8 > /dev/null 2>&1; then
        echo "$(date): Internet ativa" >> $LOG
    else
        echo "$(date): Sem conexão" >> $LOG
    fi
}

# Executa função
testar_internet

echo "Relatório gerado em: $LOG"
```