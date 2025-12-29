2025-12-28 21:02

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[HTTP]]

----
# Introdução

O **HTTP *(HyperText Transfer Protocol)*** é o protocolo base do ***World Wide Web***, responsável pela comunicação entre **clientes** (navegadores, apps) e **servidores web**. ele define como as requisições e respostas devem ser estruturadas e transmitidas.

Do ponto de vista da cibersegurança, o HTTP é extremamente relevante porque:

- Transporta dados sensíveis;
- É alvo frequente de ataques web;
- Serve como base para APIs e sistemas corporativos;
- Grande parte das vulnerabilidades exploradas na internet ocorre sobre HTTP.

---
# Em qual camada o HTTP atua?

- **Modelo OSI:** Camada 7 – Aplicação
- **Modelo TCP/IP:** Camada de Aplicação

O HTTP utiliza, tradicionalmente:

- **TCP porta 80** (HTTP)
- **TCP porta 443** quando combinado com TLS (HTTPS)

---
# Características do HTTP

**Principais características:**

- protocolo **stateless** (sem estado);
- modelo **cliente-servidor**.
- comunicação baseada em **requisição e resposta**;
- extensível por cabeçalhos;
- suporta múltiplos métodos.

Por ser stateless, mecanismos adicionais são usados para manter estado, como **cookies e sessões**.

---
# Como o HTTP funciona?

## 1. Fluxo básico de comunicação

1. O cliente envia uma requisição HTTP
2. O servidor processa a requisição
3. O servidor retorna uma resposta HTTP
4. A conexão pode ser encerrada ou reutilizada

![[Pasted image 20251228210958.png]]

## 2. Estrutura de uma requisição HTTP

Uma requisição HTTP possui:

- linha de requisição;
- cabeçalhos;
- corpo (opcional).

**Exemplo:**

```http
GET /login HTTP/1.1
Host: exemplo.com
User-Agent: Mozilla/5.0
Cookie: session=abc123
```

## 3. Estrutura de uma resposta HTTP

Uma resposta HTTP contém:

- linha de status;
- cabeçalhos;
- corpo.

**Exemplo:**

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234
```

---
# Métodos HTTP

| **Método** | **Função**          |
| ---------- | ------------------- |
| GET        | Obter recursos      |
| POST       | Enviar dados        |
| PUT        | Atualizar recursos  |
| DELETE     | Remover recursos    |
| PATCH      | Atualização parcial |
| HEAD       | Apenas cabeçalhos   |
| OPTIONS    | Métodos permitidos  |

O uso incorreto desses métodos pode gerar falhas de segurança.

---
# Códigos de status HTTP


| **Classe** | **Significado**  |
| ---------- | ---------------- |
| 1xx        | Informativo      |
| 2xx        | Sucesso          |
| 3xx        | Redirecionamento |
| 4xx        | Erro do cliente  |
| 5xx        | Erro do servidor |

**Exemplos importantes:**

- 200 OK
- 301 Moved Permanently
- 400 Bad request
- 401 Unauthorized
- 404 Not Found
- 500 Internal Server Error

---
# Versões do HTTP

## HTTP/1.0

- uma requisição por conexão;
- baixa performance.

## HTTP/1.1

- conexões persistentes;
- chunked transfer;
- amplamente utilizado

## HTTP/2

- multiplexação;
- compressão de cabeçalhos;
- melhor desempenho.

## HTTP/3

- baseado em QUIC (UDP);
- menor latência;
- novos desafios de segurança.

---
# Principais vulnerabilidades HTTP

## 1. Man-in-the-Middle (MITM)

O HTTP não possui criptografia nativa.

**Impacto**:

- interceptação de credenciais;
- modificação de conteúdo.

## 2. Sessions Hijacking

Roubo de cookies de sessão.

**Causas**:

- HTTP sem criptografia;
- cookies sem flags de segurança.

## 3. Injeção de Código (XSS)

Execução de scripts maliciosos.

**Tipos:**

- XSS Refletido
- XSS Armazenado
- XSS DOM-based

## 4. SQL Injection

Envio de comandos SQL via parâmetros HTTP.

## 5. CSRF *(Cross-Site Request Forgery)*

Força o navegador da vítima a executar ações indesejadas.

## 6. Directory Traversal

Acesso indevido a arquivos do servidor.

## 7. Insecure HTTP Headers

Ausência de cabeçalhos de segurança.

---
# Cabeçalhos HTTP importantes para segurança

- Content-Security-Policy (CSP)
- X-Frame-Options
- X-Content-Type-Options
- Strict-Transport-Security (HSTS)
- Referrer-Policy
- Permissions-Policy

---
# Ferramentas para Testes de Segurança HTTP
## Análise e Interceptação

- Burp Suite    
- OWASP ZAP
- Fiddler

## Pentest

- Nikto    
- SQLmap
- Nuclei
- Metasploit

## Monitoramento

- Wireshark
- tcpdump

---
# Mitigação e Boas Práticas de segurança HTTP

## 1. Uso de HTTPS

- criptografia com TLS;
- integridade e confidencialidade.

## 2. Configuração Segura de Cookies

- Secure
- HttpOnly
- SameSite

## 3. Validação de Entradas

- sanitização de dados;
- validação no servidor.

## 4. Implementação de Headers de Segurança

- reduzir superfície de ataque.

## 5. Autenticação e Autorização Fortes

- MFA;
- controle de acesso adequado.

## 6. Hardening do Servidor Web

- atualização de software;
- ocultar versões;
- permissões corretas.

---
# HTTP, APIs e Segurança

APIs REST utilizam HTTP como base.

Riscos comuns:

- exposição de endpoints;
- autenticação fraca;
- excesso de permissões.

Boas práticas:

- OAuth2;
- rate limiting;
- logs e monitoramento.

---
# Importância do HTTP para Cibersegurança

Compreender o HTTP permite:

- identificar ataques web;
- analisar tráfego malicioso;
- proteger aplicações e APIs;
- realizar testes de intrusão;
- responder a incidentes web.

---
# Conclusão

O protocolo HTTP é fundamental para a web moderna, mas também é um dos principais vetores de ataque da internet.

Sem mecanismos de segurança adicionais, ele expõe aplicações a interceptações e ataques diversos. Por isso, o uso correto de HTTPS, boas práticas de desenvolvimento e monitoramento contínuo são essenciais.

Para profissionais de cibersegurança, dominar HTTP é obrigatório para atuar em **pentest, SOC, AppSec e Blue Team**.

