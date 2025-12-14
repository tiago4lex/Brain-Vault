2025-08-20 17:03

Status: #developed #Linux 

Tags: [[Linux]] | [[Regex]]

----
# Introdução

As **expressões regulares** (ou regex) são padrões utilizadas para **buscar, comparar e manipular texto**.

Elas são aplicadas em diversos comandos do Linux, como `grep`, `sed`, e `awk`, além de linguagens de programação (Python, Java, C, etc.).

---
# Tipos de Expressões Regulares

No Linux, existem duas variações principais:

1. **BRE *(Basic Regular Expressions)*** → usado por padrão no `grep`.
2. **ERE *(Extended Regular Expressions)*** → usado com `egrep` ou `grep -E`, inclui operadores adicionais.

---
# Metacaracteres Básicos

Os **metacaracteres** são símbolos especiais usados para criar padrões.

| **Símbolo** | **Significado**                                       | **Exemplo**                                       |
| ----------- | ----------------------------------------------------- | ------------------------------------------------- |
| `.`         | Representa **qualquer caractere** (exceto nova linha) | `c.t` → casa, cet, cat                            |
| `^`         | Início da linha                                       | `^ola` → corresponde a "ola" apenas no início     |
| `$`         | Fim da linha                                          | `fim$` → corresponde a "fim" apenas no final      |
| `*`         | Zero ou mais ocorrências                              | `ab*` → a, ab, abb, abbb                          |
| `+`         | Uma ou mais ocorrências (ERE)                         | `ab+` → ab, abb, abbb                             |
| `?`         | Zero ou uma ocorrência (ERE)                          | `ab?` → a ou ab                                   |
| `[]`        | Classe de caracteres                                  | `[abc]` → a, b ou c                               |
| `[^]`       | Negação dentro de colchetes                           | `[^0-9]` → qualquer caractere que não seja número |
| `{n}`       | Exatamente `n` repetições                             | `a{3}` → aaa                                      |
| `{n,}`      | `n` ou mais repetições                                | `a{a,}` → aa, aaa, aaaa                           |
| `{n,m}`     | Entre `n` e `m` repetições                            | `a{2,4}` → aa, aaa, aaaa                          |
| \|          | OU (ERE)                                              | `casa\|carro` → casa ou carro                     |
| `()`        | Agrupamento                                           | `(ab)+` → ab, abab, ababab                        |

---
# Classe de Caracteres Pré-Definidas

Algumas classes prontas facilitam a escrita:

| **Classe** | **Equivalente** | **Significado**                       |
| ---------- | --------------- | ------------------------------------- |
| `\d`       | `[0-9]`         | Dígitios                              |
| `\D`       | `[^0-9]`        | Não dígitos                           |
| `\w`       | `[A-Za-z0-9_]`  | Caracteres alfanuméricos + underscore |
| `\W`       | `[^Z-Za-z0-9_]` | Não alfanuméricos                     |
| `\s`       | `[ \t\n\r\f\v]` | Espaços em branco                     |
| `\S`       | Negação de `\s` | Não espaço                            |

> [!warning] Atenção!
> Em alguns comandos Linux (`grep`), pode ser necessário usar `[:digit:]`, `[:alpha:]`, etc.

**Exemplo:**

```bash
grep "[[:digit:]]" arquivo.txt
```

Procura por qualquer número.

---
# Exemplos Práticos no Linux

## 1. Buscar linhas que começam com "root"

```bash
grep "^root" /etc/passwd
```

**Explicação:**

- `"^root"` → a expressão regular
	- `^` significa o **início da linha**
	- `root` é o texto literal

✅ **O que faz:**  
Vai mostrar apenas as linhas do arquivo `/etc/passwd` que **começam com a palavra "root"**.

Exemplo de saída:

```text
root:x:0:0:root:/root:/bin/bash
```

## 2. Procurar endereços de e-mail

```bash
grep "[a-zA-Z0-9._%+-]\+@[a-zA-Z0-9.-]\+\.[a-zA-Z]\{2,4\}" arquivo.txt
```

**Explicação:**

- `[a-zA-Z0-9._%+-]\+` → parte antes do `@` (nome do usuário do e-mail).
    - Pode conter letras, números e caracteres como `.`, `_`, `%`, `+` e `-`.

- `@` → símbolo obrigatório do e-mail.    
- `[a-zA-Z0-9.-]\+` → parte do domínio (ex.: `gmail`, `hotmail`, etc.).
- `\.` → o ponto literal (`.` sozinho pega qualquer caractere, então usamos `\.` para "escapar").
- `[a-zA-Z]\{2,4\}` → extensão do domínio (ex.: `com`, `org`, `net`, `br`).

✅ **O que faz:**  
Encontra **endereços de e-mail válidos** dentro de um arquivo de texto.

Exemplo de correspondências encontradas:

```text
joao.silva@gmail.com
maria_123@empresa.com.br
```

## 3. Encontrar números de telefone no formato (XX) XXXX-XXXX

```bash
grep "(..)\s[0-9]\{4\}-[0-9]\{4\}" arquivo.txt
```

**Explicação:**

- `( .. )` → dois caracteres dentro de parênteses (normalmente DDD, ex.: `(11)`).
- `\s` → espaço em branco depois do DDD.
- `[0-9]\{4\}` → exatamente 4 dígitos (ex.: `9876`).
- `-` → hífen literal.
- `[0-9]\{4\}` → mais 4 dígitos (ex.: `1234`).

✅ **O que faz:**  
Procura números de telefone no padrão brasileiro antigo:

```css
(11) 9876-1234
(21) 2345-6789
```

## 4. Substituir palavras usando `sed` com regex

```bash
sed -E 's/[0-9]{4}-[0-9]{4}/TELEFONE_REDACTED/g' contatos.txt
```

**Explicação:**

- `sed -E` → executa o `sed` (editor de fluxo) no modo de **expressões regulares estendidas**.
- `s/.../.../g` → comando de substituição (`s` de substitute):
    - Padrão a encontrar: `[0-9]{4}-[0-9]{4}`
        - `[0-9]{4}` → 4 dígitos seguidos.
        - `-` → hífen literal.
        - `[0-9]{4}` → mais 4 dígitos.
    - Texto de substituição: `TELEFONE_REDACTED`.

- `g` → aplica a substituição em todas as ocorrências da linha (não só na primeira).    

✅ **O que faz:**  
Substitui todos os números de telefone do arquivo `contatos.txt` pelo texto **TELEFONE_REDACTED**.

Exemplo:

```css
Maria: (11) 9876-1234
Pedro: (21) 2345-6789
```

Vira:

```css
Maria: (11) TELEFONE_REDACTED
Pedro: (21) TELEFONE_REDACTED
```

## 5. Exemplo com logins falhos no auth.log

```bash
grep "Failed password.*root" /var/log/auth.log
```

**Explicação:**

- `"Failed password.*root"` → padrão regex:
    - `"Failed password"` → trecho fixo que aparece quando há uma senha incorreta.
    - `.*` → significa **qualquer coisa (.) repetida zero ou mais vezes (*)**.
    - `"root"` → palavra que queremos verificar se aparece depois.

- `/var/log/auth.log` → arquivo que guarda logs de autenticação no Linux.    

✅ **O que faz:**  
Filtra o log para mostrar **tentativas de login falhadas usando o usuário root**.

Exemplo de saída:

```nginx
Aug 20 11:34:56 ubuntu sshd[2345]: Failed password for root from 192.168.1.15 port 54321 ssh2
```

---
# Dicas de uso

- Teste regex em ferramentas online como regex101.com para validar padrões.
- Use `grep -E` para ter acesso às **expressões regulares estendidas (ERE)**.
- Combine regex com `sed`, `awk` e `sort` para **processamento avançado de texto**.

---
# Ferramentas

Existem diversas ferramentas gratuitas disponíveis na web para auxiliar na criação e validação de expressões regulares. Entre as mais populares estão:

- [Regex101](https://regex101.com/), que oferece um editor interativo com explicações detalhadas de cada parte da regex;
- [RegExr](https://regexr.com/), que permite testar e salvar expressões regulares enquanto exibe dicas e exemplos;
- [RegexPal](https://www.regexpal.com/), ideal para testar padrões simples rapidamente.

Essas ferramentas são boas tanto para iniciantes quanto para pessoas que já dominam regex e buscam criar padrões precisos e eficientes.