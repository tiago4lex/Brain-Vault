
2026-02-20 11:56

Status: #developed #javascript 

Tags: [[JavaScript]] | [[Node.js]]

----
# Introdução

No ambiente do **Node.js**, podemos ler e manipular arquivos do sistema usando o módulo nativo chamado `fs` *(File System)*.

O `fs` permite:

- Ler arquivos
- Criar arquivos
- Editar arquivos
- Apagar arquivos
- Trabalhar com diretórios

Tudo isso usando **JavaScript** no backend.

---
# 1. Importando o Módulo `fs`

Antes de usar o `fs, é necessário importá-lo:

```javascript
const fs = require('fs');
```

> Esse módulo já vem instalado com o Node.js, então não é necessário instalad nada com `npm`.

---
# 2. Leitura de Arquivos

Existem duas formas **principais** de ler arquivos:

1. Forma Assíncrona (recomendada)
2. Forma Síncrona

---
# 3. Leitura Assíncrona (`fs.readfile`)

Essa é a forma utilizada, pois **não bloqueia a execução do programa**.

## Sintaxe

```javascript
fs.readFile(caminho, encoding, callback)
```

- `caminho` → caminho do arquivo
- `encoding` → tipo de codificação (ex: `utf-8`)
- `callback` → função que será executado quando a leitura terminar

## Exemplo Prático

Supondo que temos um arquivo chamado `dados.txt`:

```text
Olá!
Aprendendo Node.js.
```

### Código

```javascript
const fs = require('fs');

fs.readFile('dados.txt', 'utf8', (erro, dados) => {
	if (erro) {
		console.log("Erro ao ler o arquivo:", erro);
		return
	}
	
	console.log("Conteúdo do arquivo:");
	console.log(dados);
});
```

#### O que acontece aqui?

1. Node inicia a leitura do arquivo.
2. O código continua rodando enquanto o arquivo é lido.
3. Quando termina, a função callback é executada.
4. Se houver erro → `erro` terá valor.
5. Se der certo → `dados` contém o conteúdo do arquivo.

---
# 4. Leitura Síncrona (`fs.readFileSync`)

A versão síncrona **bloqueia o programa até terminar a leitura**.

## Sintaxe

```javascript
const dados = fs.readFileSync(caminho, encoding);
```

## Exemplo

```javascript
const fs = require('fs');

try {
	const dados = fs.readFileSync('dados.txt', 'utf8');
	console.log("Conteúdo do arquivo:");
	console.log(dados);
} catch (erro) {
	console.log("Erro ao ler o arquivo:", erro);
}
```

## Diferença Importante

| Assíncrono              | Síncrono                  |
| ----------------------- | ------------------------- |
| Não bloqueia o programa | Bloqueia a execução       |
| Usa callback            | Retorna direto            |
| Melhor para produção    | Útil para scripts simples |

> Em aplicações reais (APIs, servidores), prefira a versão assíncrona.

---
# 5. Usando Promises (`fs.promises`)

O Node.js também oferece suporte a Promises, deixando o código mais moderno.

## Exemplo com `async/await`

```javascript
const fs = require('fs').promises;

async function lerArquivo() {
	try {
		const dados = await fs.readFile('dados.txt', 'utf8');
		console.log(dados);
	} catch (erro) {
		console.log("Erro:", erro);
	}
}

lerArquivo();
```

## Vantagens

- Código mais limpo
- Sem callbacks aninhadas
- Melhor organização

---
# 6. Lendo Arquivos JSON

Se houver um arquivo `dados.json`:

```json
{
	"nome": "Maria",
	"idade": 22
}
```

Pode se fazer:

```javascript
const fs = require('fs');

fs.readFile('dados.json', 'utf8', (erro, dados) => {
	if (erro) {
		console.log(erro);
		return;
	}
	
	const objeto = JSON.parse(dados);
	console.log(objeto.nome); // Maria
});
```

> Importante usar `JSON.parse()` para converter o texto JSON em objeto JavaScript.

---
# 7. Caminhos de Arquivos

Pode se usar:

- Caminho relativo:

```javascript
'dados.txt'
```

- Caminho absoluto:

```javascript
'/home/usuario/projeto/dados.txt'
```

Para maior segurança, é comum usar o módulo `path`:

```javascript
const path = require('path');

const caminho = path.join(__dirname, 'dados.txt');
```

---
# 8. Boas Práticas

- Sempre tratar erros
- Preferir leitura assíncrona
- Usar `utf8` para arquivos de texto
- Usar `try/catch` com `async/await`
- Não usar versão síncrona em servidores

---
# Conclusão

- O módulo `fs` permite manipular arquivos no Node.js.
- `readFile()` → leitura assíncrona (recomendado).
- `readFileSync()` → leitura síncrona.
- `fs.promises` → versão moderna com `async/await`.
- Pode ser usado para ler arquivos de texto, JSON e outros formatos.

