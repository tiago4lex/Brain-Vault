2025-08-29 10:24

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Ponteiros]]

----
# Operador `->`

## Quando ele aparece?

O `->` é usado quando temos um ponteiro para uma `struct` e queremos acessar os campos (membros) dela.

- Sem ponteiro, usamos o `.` (ponto).
- Com ponteiro, usamos o `->`.

---
## Exemplo Básico

```c
#include <stdio.h>

struct Pessoa {
	char nome[20];
	int idade;
};

int main() {
	struct Pessoa p1 = {"Maria", 23};
	struct Pessoa *ptr = &p1;
	
	// Acessando com ponto:
	printf("Nome: %s\n", p1.nome);
	prtinf("Idade %d\n", p1.idade);
	
	// Acessando com seta:
	printf("Nome: %s\n", ptr->nome);
	printf("Idade: %d\n", ptr->idade);
	
	return 0;
}
```

**Saída:**

```txt
Nome: Maria
Idade: 23
Nome: Maria
Idade: 23
```

---
## O que acontece na memória

Suponde que `p1` esteja no endereço `0x2000`:

| Endereço | Variável | Conteúdo  |
| -------- | -------- | --------- |
| `0x2000` | p1.nome  | `"Maria"` |
| `0x2014` | p1.idade | `23`      |
| `0x3000` | ptr      | `0x2000`  |

- `p1.nome` → acessa diretamente o campo da struct
- `ptr->nome` → segue o ponteiro `ptr` (0x2000) e acessa o campo `nome`

---
## Equivalência entre `->` e `*`

A linha:

```c
ptr->idade
```

é exatamente a mesma coisa que:

```c
(*ptr).idade
```

Ou seja:

- `*ptr` → pega o objeto que o ponteiro aponta (no caso, a struct `p1`).
- `(*ptr).idade` → acessa o campo `idade` dessa struct.
- `ptr->idade` → forma simplificada para isso.

---
## Exemplo Prático (lista encadeada)

```c
#include <stdio.h>
#include <stdlib.h>

struct Nodo {
	int valor;
	struct Nodo* prox;
}

int main() {
	// Criando dois nós
	struct Nodo* n1 = malloc(sizeof(struct Nodo));
	struct Nodo* n2 = malloc(sizeof(struct Nodo));
	
	n1->valor = 10;  // equivale a (*n1).valor = 10
	n2->valor = 20;
	
	n1->prox = n2;   // n1 aponta para n2
	n2->prox = NULL;
	
	printf("n1->valor = %d\n", n1->valor);
	printf("n1->prox->valor = %d\n", n1->prox->valor);
	
	free(n1);
	free(n2);
	
	return 0;
}
```

Aqui:

- `n1->valor` → acessa o campo `valor` do nó `n1`
- `n1->prox->valor` → acessa o valor do nó que está logo após `n1` (ou seja, `n2`)

**Saída:**

```txt
n1->valor = 10
n1->prox->valor = 20
```

---
## Representação da Memória

Supondo que o sistema alocou os blocos de memória assim:

|Endereço|Variável|Conteúdo (valor)|
|---|---|---|
|`0x1000`|n1|`0x2000`|
|`0x1008`|n2|`0x3000`|
|`0x2000`|n1->valor|`10`|
|`0x2004`|n1->prox|`0x3000`|
|`0x3000`|n2->valor|`20`|
|`0x3004`|n2->prox|`NULL (0)`|

### Explicando o acesso

- `n1` está em `0x1000` e guarda `0x2000` → ou seja, aponta para a struct alocada em `0x2000`.
- `n2` está em `0x1008` e guarda `0x3000` → aponta para a struct alocada em `0x3000`.

**Passo a passo dos acessos:**

1. `n1->valor`
	- `n1` → `0x2000`
	- acessa o campo `valor` da struct em `0x2000`
	- resultado: `10`

2. `n1->prox`
	- dentro de `n1` (endereço `0x2004`) temos `0x3000`
	- ou seja, `n1->prox` aponta para `n2`

3. `n1->prox->valor`
	- `n1->prox` → `0x3000`
	- acessa o campo `valor` da struct em `0x3000`
	- resultado: `20`

**Visual gráfico da lista encadeada**

```css
n1 (0x1000) ---> [ valor: 10 | prox: 0x3000 ] ---> [ valor: 20 | prox: NULL ]
```

>[!note] Observação:
>Perceba que o `->` serve para **navegar pelos ponteiros e acessar os campos das structs** de forma simplificada.

---
## Resumo

- Use `.` → quando tem a struct **direta**
- Use `->` → quando tem um **ponteiro para struct**
- `a->b` é apenas uma forma curta de `(*a).b`