
2026-02-20 12:47

Status: #developed #javascript 

Tags: [[JavaScript]]

----
# Introdução

A captura e contagem de palavras é um dos primeiros passos no processamento de texto em aplicações modernas. Seja para gerar estatísticas, criar mecanismos de busca, analisar frequência de termos ou iniciar estudos em Processamento de Linguagem Natural (NLP), entender como transformar texto bruto em dados estruturados é uma habilidade fundamental para quem trabalha com JavaScript no ambiente Node.js.

## Código

```javascript
const fs = require("fs");
const { text } = require("stream/consumers");
const caminhoArquivo = process.argv;
const link = caminhoArquivo[2];
fs.readFile(link, "utf-8", (erro, texto) => {
  if (erro) {
    console.log("ERRO:", erro);
    return;
  }
  contaPalavras(texto);
});

function contaPalavras(texto) {
  const paragrafos = extraiParagrafos(texto);

  const contagem = paragrafos.flatMap((paragrafo) => {
    if (!paragrafo) return [];

    return verificaPalavarasDuplicadas(paragrafo);
  });

  console.log(contagem);
}

function extraiParagrafos(texto) {
  return texto.toLowerCase().split("\n");
}

function limpaPalavras(palavra) {
  return palavra.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g, "");
}

function verificaPalavarasDuplicadas(texto) {
  const listaPalavras = texto.split(" ");

  const resultado = {};

  listaPalavras.forEach((palavra) => {
    if (palavra.length >= 3) {
      const palavraLimpa = limpaPalavras(palavra);

      resultado[palavraLimpa] = (resultado[palavraLimpa] || 0) + 1;
    }
  });

  return resultado;
}
```

---
# 1. Leitura de Arquivo

```javascript
const fs = require('fs');
const caminhoArquivo = process.argv;
const link = caminhoArquivo[2];
```

### O que acontece aqui:

- `require('fs')` importa o módulo de sistema de arquivos do Node.js
- `process.argv` captura argumentos passados no terminal
- `caminhoArquivo[2]` pega o caminho do arquivo informado

### Exemplo de execução no terminal:

```bash
node index.js texto.txt
```

## Leitura assíncrona

```javascript
fs.readFile(link, 'utf-8', (erro, texto) => {
	if (erro) {
		console.log('ERRO:', erro);
		return;
	}
	contaPalavras(texto);
});
```

### Importante entender:

- `readFile` lê o arquivo
- `'utf-8'` garante leitura como texto
- A função callback recebe:
    - `erro` → caso haja problema        
    - `texto` → conteúdo do arquivo


Se não houver erro, o texto é enviado para `contaPalavras`.

---
# 2. Função Principal: `contaPlavras`

```javascript
function contaPalavras(texto) {
	const paragrafos = extraiParagrafos(texto);
	const contagem = paragrafos.flatMap((paragrafo) => {
		if (!paragrafo) return [];
		return verificaPalavarasDuplicadas(paragrafo);
	});
	console.log(contagem);
}
```

## Etapas importantes:

1. Extrai parágrafos
2. Processa cada parágrafo
3. Conta palavras
4. Exibe o resultado

---
# 3. Extração de Parágrafos

```javascript
function extraiParagrafos(texto) {
	return texto.toLowerCase().split('\n');
}
```

### O que acontece:

- `toLowerCase()` → transforma tudo em minúsculo evitando que "Casa" e "casa" sejam diferentes
- `split('\n')` → divide o texto por quebra de linha

### Exemplo:

Texto original:

```text
Olá mundo
Olá JavaScript
```

Resultado:

```javascript
["olá mundo", "olá javascript"]
```

---
# 4. Limpeza de Palavras

```javascript
function limpaPalavras(palavra) {
	return palavra.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g, '');
}
```

### O que faz:

Remove pontuação usando **Expressão Regular (Regex)**.

### Exemplo:

```javascript
limpaPalavras("casa.")
// "casa"
```

Isso evita que `"casa"` e `"casa."` sejam contadas como palavras diferentes.

---
# 5. Contagem de Palavras

```javascript
function verificaPalavarasDuplicadas(texto) {
	const listaPalavras = texto.split(' ');
	const resultado = {};

	listaPalavras.forEach((palavra) => {
		if (palavra.length >= 3) {
			const palavraLimpa = limpaPalavras(palavra);
			resultado[palavraLimpa] = (resultado[palavraLimpa] || 0) + 1;
		}
	});
	return resultado;
}
```

## O que acontece aqui:

### 1. Divide o texto em palavras

```javascript
texto.split(' ')
```

Exemplo:

```text
"eu gosto de javascript"
```

Resultado:

```javascript
["eu", "gosto", "de", "javascript"]
```

### 2. Ignora palavras pequenas

```javascript
if (palavra.length >= 3)
```

Palavras com menos de 3 letras são ignoradas  (ex: "de", "a", "é").

### 3. Usa um objeto para contar

```javascript
resultado[palavraLimpa] = (resultado[palavraLimpa] || 0) + 1;
```

Essa linha faz:

- Se a palavra ainda não existe → começa com 0
- Soma +1 a cada ocorrência

## Exemplo prático

```text
casa casa carro
```

Resultado:

```javascript
{
  casa: 2,
  carro: 1
}
```

---
# 6. Uso do `flatMap`

```javascript
paragrafos.flatMap(...)
```

### O que ele faz?

- Executa a função em cada parágrafo
- "Achata" o resultado

Ele evita que o retorno fique algo como:

```javascript
[ { casa: 2 }, { carro: 1 } ]
```

Mas ainda assim, no código atual, cada parágrafo gera um objeto separado.

---
# Observação Importante

O código **não soma as palavras entre parágrafos**, ele retorna um objeto para cada um.

Exemplo:

```javascript
[
  { casa: 2 },
  { casa: 1 }
]
```

Se quisermos total geral, precisaríamos usar `reduce`.

---
# Exemplo Mais Simples

Contagem básica:

```javascript
function contarSimples(texto) {
	const palavras = texto.split(' ');
	const contagem = {};

	for (let palavra of palavras) {
		contagem[palavra] = (contagem[palavra] || 0) + 1;
	}

	return contagem;
}
```

---
# Exemplo Mais Avançado (Contagem Global com `reduce`)

```javascript
function contaTotal(texto) {
	return texto
		.toLowerCase()
		.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g, '')
		.split(/\s+/)
		.reduce((acc, palavra) => {
			if (palavra.length >= 3) {
				acc[palavra] = (acc[palavra] || 0) + 1;
			}
			return acc;
		}, {});
}
```

---
# Estrutura Geral do Processo

```text
Arquivo → Texto → Parágrafos → Palavras → Limpeza → Contagem
```

---
# Conceitos Fundamentais Envolvidos

- Leitura de arquivos com `fs`
- Argumentos de linha de comando
- Callbacks
- Manipulação de strings
- Expressões regulares
- Objetos como estrutura de contagem
- Métodos de array:
    - `split`
    - `forEach`
    - `flatMap`
    - `reduce`

---
# Conclusão

O código implementa um **processador simples de texto**, aplicando:

✔ Normalização  
✔ Tokenização (separação em palavras)  
✔ Limpeza  
✔ Filtro  
✔ Contagem

Esse padrão é muito usado em:

- Análise de texto
- Processamento de linguagem natural (NLP)
- Sistemas de busca
- Indexadores
- Estatísticas de conteúdo