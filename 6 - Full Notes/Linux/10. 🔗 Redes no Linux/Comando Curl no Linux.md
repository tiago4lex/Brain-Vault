2025-08-22 10:37

Status: #developed #Linux 

Tags: [[Linux]] | [[curl]]

----
# Introdução

## O que é o `curl`?

O `curl` *(Client URL)* é uma ferramenta de linha de comando utilizada para transferir dados de ou para servidor, suportando diversos protocolos como **HTTP, HTTPS, FTP, SCP, SFTP, LDAP, IMAP, SMTP, POP3, SMB**, entre outros.

Ele é muito utilizada para **testar APIs, baixar arquivos, enviar formulários, realizar requisições autenticadas e verificar conectividade com servidores.**

---
# Sintaxe Básica

```bash
curl [opções] [URL]
```

- `[opções]` → parâmetros que modificam o comportamento do `curl`.
- `[URL]` → o endereço do recurso que você quer acessar.

---
# Exemplos Práticos

## 1. Baixar o conteúdo de uma página web

```bash
curl https://example.com
```

> Mostra o HTML da página no terminal.

## 2. Salvar o conteúdo em um arquivo

```bash
curl -o pagina.html https://example.com
```

>O conteúdo será salvo no arquivo `pagina.html`

- `-o arquivo` → salva com o nome definido.
- `-O` → salva com o mesmo nome do arquivo do servidor.

## 3. Baixar múltiplos arquivos

```bash
curl -O https://example.com/arquivo1.txt -O https://example.com/arquivo2.txt
```

## 4. Seguir redirecionamentos

```bash
curl -L https://example.com
```

> O `-L` garante que o `curl` siga automaticamente redirecionamentos (`301`, `302`).

## 5. Exibir apenas cabeçalhos da resposta

```bash
curl -I https://example.com
```

> Mostra **somente os headers HTTP** (útil para verificar status, servidor, cookies, etc.).

## 6. Realizar um download silencioso

```bash
curl -s -O https://example.com/arquivo.zip
```

> O `-s` *(silent)* evita a exibição da barra de progresso.

## 7. Testar uma API com `GET`

```bash
curl https://api.github.com/users/usuario
```

> Retorna os dados da API pública do GitHub.

## 8. Enviar dados com `POST`

```bash
curl -X POST -d "usuario=admin&senha=1234" https://example.com/login
```

> `-X POST` → método HTTP.
> `-d` → dados enviados

## 9. Enviar dados em formato JSON

```bash
curl -X POST https://api.exemplo.com/login \
     -H "Content-Type: application/json" \
     -d '{"usuario":"admin","senha":"1234"}'
```

> Muito usado em **APIs REST**.

## 10. Baixar arquivos com autenticação

```bash
curl -u usuario:senha https://example.com/area-restrita/arquivo.zip -O
```

> O `-u` envia **usuário e senha** (Basic Auth).

## 11. Limitar a velocidade do Download

```bash
curl --limite-rate 200k -O https://example.com/arquivo.iso
```

> Útil para não sobrecarregar a rede.

---
# Opção mais usadas no `curl`

| Opção                | Função                                        |
| -------------------- | --------------------------------------------- |
| `-o arquivo`         | Salva a saída em um arquivo específico        |
| `-O`                 | Salva com o nome original do arquivo remoto   |
| `-L` ou `--location` | Segue redirecionamentos                       |
| `-I` ou `--head`     | Mostra apenas cabeçalhos HTTP                 |
| `-s`                 | Modo silencioso (sem barra de progresso)      |
| `-u user:senha`      | Autenticação básica                           |
| `-X`                 | Define o método HTTP (GET, POST, PUT, DELETE) |
| `-d` ou `--data`     | Envia dados em requisições POST               |
| `-H`                 | Define headers personalizados                 |
| `--limit-rate`       | Limita a taxa de download                     |

---
# Exemplos de Script com `curl`

Um script simples para monitorar se um site está no ar:

```bash
#!/bin/bash

SITE="https://example.com"
STATUS=$(curl -o /dev/null -s -w "%{http_code}\n" $SITE)

if [ "$STATUS" -eq 200 ]; then
	echo "O site $SITE está online."
else
	echo "O site $SITE retorou status $STATUS."
fi
```

- O `-w "%{http_code}"` retorna apenas o código HTTP.
- `-eq` significa "igual a",  ou seja, o shell está verificando se o valor da variável `$STATUS` é **igual a** `200`.

---
# Conclusão

O **`curl`** é uma ferramenta extremamente poderosa para desenvolvedores, administradores de sistemas e profissionais de segurança. Ele permite testar conectividade, depurar APIs, baixar arquivos e até automatizar verificações em scripts de monitoramento.