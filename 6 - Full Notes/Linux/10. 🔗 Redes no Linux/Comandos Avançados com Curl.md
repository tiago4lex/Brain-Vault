2025-08-22 11:00

Status: #developed #Linux 

Tags: [[Linux]] | [[curl]]

----
# Introdução

O `curl` é uma ferramenta poderosa de linha de comando usada para transferir dados de e para servidores, suportando diversos protocolos (HTTP, HTTPS, FTP, SMTP, SCP, entre outros).  

Além de requisições simples, ele permite testes avançados de rede, automação de APIs, debugging e até upload de arquivos.

---
# Verificando apenas o código de reposta HTTP.

```bash
curl -o /dev/null -s -w "%{http_code}\n" https://example.com
```

- `-o /dev/null` → descarta o corpo da resposta.
- `-s` → modo silencioso (não mostra o progresso).
- `-w "%{http_code}"` → imprime apenas o código HTTP (ex.: 200, 404, 500).

Útil para monitoramento de sites e scripts de saúde de aplicações.

**Saída:**

```bash
200
```

- `200` - Significa que a página respondeu corretamente.

---
# Salvando cabeçalhos de resposta

```bash
curl -D headers.txt -o /dev/null https://example.com
```

- `-D headers.txt` → salva os cabeçalhos HTTP no arquivo `headers.txt`.
- `-o /dev/null` → descarta o corpo da página.

Usado para analisar cookies, redirecionamentos e metadados da resposta.

**Saída do arquivo `headers.txt`:**

```
HTTP/1.1 200 OK
Date: Wed, 20 Aug 2025 12:00:00 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 1256
Connection: keep-alive
Server: Apache
```

---
# Enviando dados de uma requisição POST

```bash
curl -X POST -d "usuario=admin&senha=1234" https://example.com
```

- `-X POST` → define o método POST.
- `-d` → envia dados no corpo da requisição.

Também é possível enviar JSON:

```bash
curl -X POST -H "Content-Type: application/json" \
     -d '{"usuario":"admin","senha":"123"}' https://api.example.com/login
```

Muito usado para testar **APIs REST**.

**Saída (exemplo de reposta da API):**

```json
{
  "args": {},
  "data": "",
  "form": {
    "senha": "123",
    "usuario": "admin"
  },
  "headers": {
    "Content-Type": "aapplication/json",
    "Host": "example.com"
  },
  "json": null,
  "url": "https://api.example.com/login"
}
```

---
# Enviando cabeçalhos personalizados

```bash
curl -H "Authorization: Bearer TOKEN123" https://api.example.com/dados
```

- `-H` → adiciona um cabeçalho HTTP à requisição.

Essencial para APIs que exigem autenticação.

**Saída:**

```json
{
  "headers": {
    "Authorization": "Bearer TOKEN123",
    "Host": "example.com"
  }
}
```

---
# Download de múltiplos arquivos

```bash
curl -O https://example.com/arquivo1.zip \
     -O https://example.com/arquivo2.zip
```

- `-O` → salva o arquivo com o **mesmo nome** do servidor.

Útil para baixar pacotes ou backups de forma automatizada.

**Saída:**

```
arquivo1.zip
arquivo2.zip
```

---
# Seguir redirecionamento automaticamente

```bash
curl -L https://example.com
```

- `-L` → segure redirecionamentos `301` ou `302`.

Importante quando o site redireciona para HTTPS ou outro domínio.

**Saída (primeiras linhas):**

```html
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
</head>
<body>
    <h1>Example Domain</h1>
```

---
# Autenticação Básica *(HTTP Basic Auth)*

```bash
curl -u admin:123 https://httpbin.org/basic-auth/admin/123
```

- `-u usuario:senha` → envia credenciais codificadas em Base64.

Útil para testar sistemas com autenticação simples.

**Saída:**

```json
{
  "authenticated": true,
  "user": "admin"
}
```

---
# Upload de arquivos

```bash
curl -F "file=@/caminho/para/arquivo.txt" https://example.com/upload
```

- `-F "file=@arquivo.txt"` → faz upload de arquivo como multipart/form-data.

Muito usado em formulários de upload.

**Saída (parte do JSON):**

```json
{
  "files": {
    "file": "meu-arquivo\n"
  },
  "form": {}
}
```

---
# Debug e rastreamento de requisições

```bash
curl -v https://example.com
```

- `-v` → modo verboso, mostra todos os detalhes da requisição e resposta.
- `--trace-ascci log.txt` → salva um log completo em arquivo.

Excelente para troubleshooting de APIs e conexões HTTPs.

**Saída (trecho):**

```markdown
*   Trying 93.184.216.34:443...
* Connected to example.com (93.184.216.34) port 443 (#0)
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/8.0.1
> Accept: */*
< HTTP/1.1 200 OK
< Content-Type: text/html; charset=UTF-8
```

---
# Testando velocidade de download

```bash
curl -o /dev/null -s -w "Tempo Total: %{time_total}s\nVelocidade: %{speed_download} bytes/s\n" https://example.com/arquivo.zip
```

- `%{time_total}` → mostra tempo da transferência.    
- `%{speed_download}` → mostra taxa de download.

Serve como um mini **teste de performance de rede**.

**Saída:**

```
Tempo Total: 0.302s
Velocidade: 15900 bytes/s
```

---
# Verificando certificado SSL

```bash
curl --cacert /etc/ssl/certs/ca-certificates.crt https://secure.example.com
```

- `--cacert` → especifica qual arquivo de certificados usar.
- `-k` → (inseguro) ignora erros de certificado SSL.

Útil para ambientes de teste com certificados *self-signed*.

**Saída (trecho com SSL):**

```
* SSL connection using TLSv1.3 / AES256-GCM-SHA384
* Server certificate:
*  subject: CN=example.com
*  start date: Aug  1 00:00:00 2025 GMT
*  expire date: Aug  1 23:59:59 2026 GMT
```

---
# Criando scripts automatizados com `curl`

```bash
#!/bin/bash

URL="https://example.com"
STATUS=$(curl -o /dev/null -s -w "%{http_code}" $URL)

if [ "$STATUS" -eq 200 ]; then
    echo "$(date) - $URL está ONLINE (status $STATUS)" >> monitoramento.txt
else
    echo "$(date) - $URL está OFFLINE (status $STATUS)" >> monitoramento.txt
fi
```

Automatiza monitoramento de aplicações.

**Saída no arquivo `monitoramento.txt`:**

```
Wed Aug 20 09:15:23 -03 2025 - https://example.com está ONLINE (status 200)
```

---
# Conclusão

O `curl` vai muito além de um simples comando para baixar páginas. Ele é uma ferramenta essencial para:

- **Monitoramento de sites e APIs**
- **Debug de conexões**
- **Automação de uploads/downloads**
- **Testes de autenticação e performance**