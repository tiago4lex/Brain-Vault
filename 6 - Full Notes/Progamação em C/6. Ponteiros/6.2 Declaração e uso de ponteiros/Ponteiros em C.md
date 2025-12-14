2025-08-28 20:30

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Ponteiros]]

----
# Introdução

Na linguagem C, um **ponteiro** é uma variável que **armazena o endereço de memória de outra variável**.

Isso permite manipular dados de forma indireta, além de possibilita:
- Passagem por referência para funções.
- Manipulação de arrays e strings.
- Alocação dinâmica de memória.
- Implementação de estrutura complexas (listas, pilhas, filas, árvores).

---
# Declaração e Uso Básico

## Declaração

```c
int* p;   // p é um ponteiro para inteiro
char* c;  // c é um ponteiro para char
float* f; // f é um ponteiro para float
```

## Operadores

- `&` (endereço de) → retorna o endereço de uma variável.
- `*` (desreferência) → acessa o valor contido no endereço armazenado no ponteiro.

## Exemplo simples

```c
#include <stdio.h>

int main() {
	int x = 10;
	int* p = &x;  // p guarda o endereço de x
	
	printf("Valor de x: %d\n", x);
	printf("Endereço de x: %p\n", &x)
	printf("Valor de p (endereço armazenado): %p\n", p);
	printf("Valor apontado por p: %d\n", *p);
	
	return 0;
}
```

**Saída esperada:**

```yaml
Valor de x: 10
Endereço de x: 0x7ffeefbff5ac
Valor de p (endereço armazenado): 0x7ffeefbff5ac
Valor apontado por p: 10
```

---
# Ponteiros e Funções

## Passagem por valor

Em C, os parâmetros de funções **são passados por valor** (cópia).

**Exemplo:**

```c
void incrementa(int n) {
	n++;
}
```

Isso **não altera** a variável origina.

## Passagem por referência (com ponteiros)

Para alterar a variável original, usamos ponteiros:

```c
#include <stdio.h>

void incrementa(int* n) {
	(*n)++;  // altera o valor no endereço
}

int main() {
	int x = 5;
	incrementa(&x);         // passa o endereço
	printf("x = %d\n", x);  // agora vale 6
}
```

---
# Ponteiros e Arrays

## Arrays como ponteiros

Um array em C é tratado como um **ponteiro para seu primeiro elemento**.

```c
#include <stdio.h>

int main() {
	int v[3] = {10, 20, 30};
	int* p = v; // p aponta para v[0]
	
	printf("%d\n", *p);     // 10
	printf("%d\n", *(p+1)); // 20
	printf("%d\n", *(p+2)); // 30
	
	return 0;
}
```

## Strings e ponteiros

Strings em C são arrays de `char`

```c
#include <stdio.h>

int main(){
	char* s = "Linguagem C"
	printf("%c\n", *s);     // L
	printf("%c\n", *(s+1)); // i
	return 0;
}
```

---
# Ponteiros e Alocação Dinâmica

Com ponteiros é possível reservar memória em tempo de execução:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int* v = (int*) malloc(5 * sizeof(int)); // aloca espaço para 5 inteiros
	if(v == NULL) return 1; // sempre verificar alocação
	
	for(int i = 0; i < 5; i++) v[i] = i+1;
	
	for(int i = 0; i < 5; i++) printf("%d ", v[i]);
	
	free(v);  // libera memória
	return 0;
}
```

---
# Ponteiros para Funções

Ponteiros também podem armazenar o endereço de funções, permitindo **callbacks e funções genéricas**.

```c
#include <stdio.h>

int soma(int a, int b) { return a + b; }
int mult(int a, int b) { return a * b; }

int calcula(int x, int y, int(*op)(int, int)) {
	return op(x, y);  // chama a função via ponteiro
}

int main() {
	printf("Soma: %d\n", calcula(3, 4, soma));
	printf("Multiplicação: %d\n", calcula(3, 4, mult));
}
```

---
# Exemplos Avançados

## Lista encadeada

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct lista {
    int valor;
    struct lista* prox;
} Lista;

Lista* criaNo(int v) {
    Lista* novo = (Lista*) malloc(sizeof(Lista));
    novo->valor = v;
    novo->prox = NULL;
    return novo;
}

int main() {
    Lista* l1 = criaNo(10);
    l1->prox = criaNo(20);
    l1->prox->prox = criaNo(30);

    for(Lista* p = l1; p != NULL; p = p->prox) {
        printf("%d ", p->valor);
    }

    return 0;
}
```

## Função que retorna ponteiro

```c
#include <stdio.h>

int* maior(int* a, int* b) {
    return (*a > *b) ? a : b;
}

int main() {
    int x = 7, y = 15;
    int* p = maior(&x, &y);
    printf("Maior valor: %d\n", *p);
    return 0;
}
#include <stdio.h>

int* maior(int* a, int* b) {
    return (*a > *b) ? a : b;
}

int main() {
    int x = 7, y = 15;
    int* p = maior(&x, &y);
    printf("Maior valor: %d\n", *p);
    return 0;
}
```

---
# Exemplo Prático

Iniciando um código e criando a variável `idade` com o valor `20`:

```c
int idade = 20;
```

O que acontece:

| Memória | Variável | Valor |
| ------- | -------- | ----- |
| 0x1000  | idade    | `20`  |
Ao definir um ponteiro `p`:
- Ele é uma variável especial que guarda **endereços**.
- Ao escrever `&idade`, pegamos o **endereço de memória da variável `idade`**.
- Então `p` recebe esse endereço.

```c
int *p = &idade;
```

O que acontece:

| Memória  | Variável | Valor    | Observação                   |
| -------- | -------- | -------- | ---------------------------- |
| `0x1000` | idade    | `20`     | Valor armazenado normalmente |
| `0x1004` | p        | `0x1000` | Guarda o endereço de `idade` |

Se usamos `*p`, acessamos o **conteúdo do endereço guardado em `p`**.

```c
printf("%d\n", *p);  // imprime 20
```

- `p` → contém `0x1000` (endereço de `idade`)
- `*p` → acessa o valor guardado em `0x1000`, que é `20`.

Resumo visual:

```css
[p] --------> [idade = 20]
```

- `p` aponta para `idade`
- `*p` acessa o valor dentro de `idade`

## Exemplo de Código

```c
#include <stdio.h>

int main()
{
	int idade = 20;
	int *p = &idade; // Ponteiro para 'idade'
	
	printf("====== Valores e Enderecos ======\n");
	printf("Valor da idade: %d\n", idade);
	printf("Endereco de memoria de idade: %p\n", &idade);
	
	printf("\nValor armazenado no ponteiro: %p\n", p);
	printf("Valor apontado pelo ponteiro: %d\n", *p);
	printf("Endereco de memoria do ponteiro: %p\n", &p);
	return 0;
}
```

**Saída:**

```css
====== Valores e Enderecos ======
Valor da idade: 20
Endereco de memoria de idade: 0x1000

Valor armazenado no ponteiro: 0x1000
Valor apontado pelo ponteiro: 20
Endereco de memoria do ponteiro: 0x1002
```

---
# Resumo

- Ponteiros armazenam **endereços de memória**.
- São usados para manipular variáveis, arrays, strings e funções.
- Permitem **passagem por referência**, **alocação dinâmica** e **estruturas de dados complexas**.
- Mal utilizados, podem causar **erros graves** (segfault, memory leaks).
- Bem utilizados, tornam o C **poderoso e eficiente**.