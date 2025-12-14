2025-10-29 21:23

----
## 1. Introdução ao Cross-Site Scripting (XSS)

### O que é XSS?

*Cross-Site Scripting* (XSS) é um vulnerabilidade de segurança que permite a atacantes injetar scripts maliciosos em páginas web visualizadas por outros usuários.
Esses scripts são executados no contexto do navegador da vítima, permitindo que o atacante roube cookies, sessões de usuário, ou execute ações em nome do usuário.

![[Pasted image 20251029212631.png]]

### Como funciona o XSS?

O XSS ocorre quando uma aplicação web:

- Recebe dados não confiáveis;
- Processa esses dados sem validação adequada;
- Envia esses dados de volta ao navegador sem sanitização.

### Tipos de XSS

1. ***Reflected XSS***: O script malicioso é refletido imediatamente na resposta do servidor;

![[Pasted image 20251029212939.png]]

2. ***Stored XSS***: O script é armazenado no servidor e executado sempre que a página é acessada;

![[Pasted image 20251029213028.png]]

3. ***DOM-based XSS***: A vulnerabilidade está no código JavaScript do lado do cliente.

![[Pasted image 20251029213057.png]]

---
## 2. Configuração do Ambiente

### Ferramentas Recomendadas

#### Navegadores

- **Burp Suite Browser** (integrado com Burp Suite)
- **Mozilla Firefox** com extensões de segurança
- **Google Chrome** DevTools

#### Extensões Úteis

- **Cookie Editor** (para manipulação de cookies)
- **Hack-Tools** (para testes de segurança)
- **XSS Hunter** (para detecção de XSS)

#### Ferramentas de Teste

- **Burp Suite** (Community ou Professional)
- **OWASP ZAP**
- **XSS Strike**
- **BeEF** (Browser Exploitation Framework)

---
## 3. Resolução dos Laboratórios PortSwigger - Nível Apprentice

### Laboratório 1: Reflected XSS em Contexto HTML

**Objetivo**: Executar um alerta usando `alert()` através de um parâmetro de URL.

**Passo a passo**:

1. Acesse o laboratório

![[Pasted image 20251029213457.png]]

2. Inspecione a barra de pesquisa
3. É possível notar que ao pesquisar por algo (ex.: teste) o parâmetro é refletido na página:

![[Pasted image 20251029214258.png]]

Em outro exemplo:

```html
<!-- Antes da busca -->
<div class="search-message">Digite sua busca</div>

<!-- Depois de buscar por "teste" -->
<div class="search-results">
    <h1>Resultados para: teste</h1>
    <p>Você pesquisou por: <strong>teste</strong></p>
</div>
```

Aqui é também é possível notar que "teste" foi **refletido** em dois lugares: no `<h1>` e no `<strong>`.

4. Agora ao digitar no campo de busca a tag HTML `<script>` é possível notar que a aplicação não sanitiza este tipo de entrada feita pelo o usuário, permitindo assim que seja feito a execução de um script.

Neste exemplo ao digitar no campo de busca:

```html
<script>alert('XSS')</script>
```

É possível visualizar o script em execução ao abrir uma janela de alerta.

![[Pasted image 20251029214815.png]]

### Laboratório 2: Stored XSS em Comentários

**Objetivo:** Fazer um comentário que executa `alert()` quando a página for carregada.

**Passo a Passo:**

1. Entre em uma postagem e navegue até a seção de comentários.

![[Pasted image 20251029215228.png]]

![[Pasted image 20251029215256.png]]

2. Nos campos do comentário, insira:

```html
<script>alert('XSS')</script>
```

![[Pasted image 20251029215454.png]]

3. Poste o Comentário
4. Recarrega a página

Ao recarregar a página o script é executado. Isso acontece porque o comentário com código malicioso foi armazenado no banco dedos e ele é executado sempre que a página é executada.

![[Pasted image 20251029215648.png]]

**Explicação:** O comentário é armazenado no banco de dados e executado sempre que a página é carregada.

### Laboratório 3: DOM XSS em Sink de Escrita

**Objetivo:** Explorar vulnerabilidade DOM-based XSS

**Passo a passo:**

1. Faça uma pesquisa na barra de pesquisa
2. Abrir as ferramentas de desenvolvedor (F12 ou CTRL + SHIFT + C)
3. Analisar o código JavaScript
4. É possível identificar no código JavaScript onde os parâmetros da URL são processados

![[Pasted image 20251119212520.png]]

5. Ao passar o seguinte payload, é possível garantir a vulnerabilidade

```js
"><img src=x onerror=alert('XSS')>
```

![[Pasted image 20251119212809.png]]

**Explicação:** O JavaScript processa dadas da URL sem sanitização e os escreve no DOM.

### Laboratório 4: XSS com Atributos HTML

**Objetivo:** Usar atributos HTML para executar JavaScript.

**Passo a Passo:**

1. Localizar um campo que reflete entrada no atributo de uma tag. Neste exemplo o campo de entrada é  a barra de pesquisa.

Exemplo de atributos HTML:

```html
<!-- Exemplo vulnerável -->
<input type="text" value="ENTRADA_DO_USUÁRIO_AQUI">
<img src="ENTRADA_DO_USUÁRIO_AQUI">
<div class="ENTRADA_DO_USUÁRIO_AQUI">
```

No caso do laboratório, ao inserir um valor como `test123` na barra de pesquisa, esse dado é recuperado a partir do parâmetro `search` da URL e armazenado na variável `query`. Em seguida, esse valor é inserido diretamente no elemento HTML por meio de `innerHTML`. Como o conteúdo é colocado sem qualquer validação ou sanitização, **qualquer valor fornecido — inclusive código HTML ou JavaScript — será interpretado pelo navegador**, e não tratado apenas como texto.

![[Pasted image 20251119213644.png]]

O problema surge porque o valor do parâmetro `search` é colocado em `innerHTML` **sem qualquer validação ou sanitização**.

Isso permite que um invasor injete código HTML ou JavaScript arbitrário.

2. Use o payload:

```html
<img src=x onerror=alert('XSS')>
```

**Explicação:** ao definir `src` como `x` (um valor inexistente) ele vai chamar a função `onerror` gerando assim um alerta.

### Laboratório 5: XSS em URLs

**Objetivo:** Injetar XSS através de parâmetros de URL.

**Passo a passo:**

1. Ao entrar na página `Submite Feedback` é possível notar que na URL existe um campo para parâmetros logo após `returnPath=`.

![[Pasted image 20251119215149.png]]

2. Ao alterar o parâmetro de `/` para `teste` é possível notar através das ferramentas de desenvolvedor, que o valor digitado foi inserido dentro do atributo `href`.

![[Pasted image 20251119215334.png]]

3. Agora é possível inserir um payload dentro da URL.

```html
javascritpt:alert(document.cookie)
```

4. Após inserir o payload na URL e dar enter, depois clicar em `<Back` é possível notar que o alerta foi ativado.

**Explicação:** Ao substituir o valor padrão `/` por um payload como `javascript:alert(document.cookie)`, o link `<Back` passa a apontar para um JavaScript URI. Assim, ao clicar no link, o navegador executa o código presente no atributo `href`, resultando na execução do alerta.

