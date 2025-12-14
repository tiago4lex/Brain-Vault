2025-08-29 10:47

Status: #developed #C 

Tags: [[Programação em C]] | [[C]]  | [[typdef]]

----
# Introdução

## O que é `typedef` ?

Em C, a palavra-chave `typedef` **é usada para criar um novo nome *(alias)*** para um tipo de dado já existente.

Ele **não cria um novo tipo**, mas **renomeia um tipo existente** para facilitar a leitura e escrita do código.

---
# Sintaxe geral

```c
typedef tipo_existente novo_nome;
```

**Exemplo básico:**

```c
typedef unsigned int uint;
```

Agora, ao invés de escrever:

```c
unsigned int idade;
```

Podemos escrever:

```c
uint idade;
```

---
# Por que usar `typedef?`

## 1. Código mais legível

Facilita a leitura, principalmente com tipos longos.

```c
unsigned long long int numero_grande;
typdef unsigned long long int ulli;
ulli numero_grande;
```

## 2. Trabalhar melhor com structs

Evita precisar escrever `struct` toda vez que usar.

```c
struct Pessoa {
	char nome[50];
	int idade;
};

typdef struct Pessoa Pessoa;
```

Agora você pode usar:

```c
Pessoa p1;
```

Ao invés de:

```c
struct Pessoa p1;
```

## 3. Mais portabilidade

Facilita trocar tipos em projetos grandes.

```c
typdef int inteiro;
```

Se quiser trocar depois para `long`, basta mudar **apenas a linha do typedef**.

---
# Exemplos práticos

## 1. Tipos numéricos customizados

```c
#include <stdio.h>

typdef unsigned int uint;
typdef long long ll;

int main() {
	uint idade = 25;
	ll populacao = 7800000000;
	
	printf("Idade: %u\n", idade);
	printf("População: %lld\n", populacao);
	
	return 0;
}
```

## 2. Uso em structs

```c
#include <stdio.h>

typedef struct {
	char nome[50];
	int idade;
} Pessoa;

int main() {
	Pessoa p1 = {"Maria", 23};
	printf("Nome: %s, Idade: %d\n", p1.nome, p1.idade);
	
	return 0;
}
```

>[!note] Observação:
>Repare que não precisamos escrever `struct` ao declarar `p1`.

## 3. Ponteiros com `typedef`

`typedef` também pode ser usado para simplificar ponteiros.

```c
#include <stdio.h>

typedef int* IntPtr;

int main() {
	int x = 10;
	intPtr p = &x;
	
	printf("Valor: %d\n", *p);
	
	return 0;
}
```

Aqui, `IntPtr` é um atalho para `int*`.

## 4. Ponteiro para função com `typedef`

Quando usamos funções como parâmetros, `typedef` simplifica muito.

Sem `typedef`:

```c
int soma(int a, int b) { return a + b; }

int main() {
	int (*func)(int, int) = soma;
	printf("Resultado: %d\n", func(2, 3));
}
```

Com `typedef`:

```c
typdef int (*FuncSoma)(int, int);

int soma(int a, int b){ return a + b; }

int main() {
	FuncSoma f = soma;
	printf("Resultado: %d\n", f(2, 3));
}
```

---
# Resumindo

- `typedef` = cria **apelidos** para tipos já existentes.
- Útil para **códigos mais legível, simplificar `struct` e organizar ponteiros/funções**.
- Muito usado em **projetos grandes e bibliotecas** (exemplo: no Linux Kernel, `typedef` aparece o tempo todo).

