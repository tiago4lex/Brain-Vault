2025-08-30 07:40

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[malloc]]

----
# Introdução
## O que é `malloc`?

`malloc` significa ***Memory Allocation*** é uma função da biblioteca `<stdlib.h>` usada para **alocar memória dinamicamente** durante a execução de um programa em C.

- Ao contrário das variáveis comuns (alocadas em **memória estática ou automática**), a memória criada com `malloc` vem da ***Heap*** (uma região especial da memória).
- Isso permite criar estruturas de dados cujo tamanho só é conhecido **em tempo execução**, como vetores, matrizes ou listas dinâmicas.

---
# Sintaxe

```c
void* malloc(size_t tamanho);
```

- **Parâmetro:** `tamanho` → quantidade de bytes a serem alocados.
- **Retorno:** um **ponteiro** `void*` para o início da região alocada.
	- Caso a alocação falhe, retorna `NULL`.

> Como o retorno é `void*`, normalmente fazemos um *casting* para o tipo desejado.

---
# Exemplo básico

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int *p;
	
	// Alocando memória para 1 inteiro
	p = (int*) malloc(sizeof(int))
	
	if (p == NULL) {
		printf("Erro ao alocar memória!\n");
		return 1;
	}
	
	*p = 42; // Acessando a memória alocada
	printf("Valor armazenado: %d\n", *p);
	
	free(p); // Liberar memória alocada
	return 0;
}
```

### Explicação

1. `malloc(sizeof(int))` → pede ao sistema espaço suficiente para armazenar **1 inteiro**.
2. `p` recebe o endereço dessa memória.
3. `if (p == NULL)` → se a alocação falhar (por falta de memória ou outros problemas), `malloc` retorna `NULL`
4. `return 1` → programa finalizado com erro.
5. `*p = 42` → armazenamos um valor dentro do espaço criado.
6. `free(p)` → sempre devemos liberar a memória após p uso.
7. `return 0` → programa finalizado com sucesso.

---
# Exemplo com Vetor Dinâmico

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int n, i;
	int *vetor;
	
	printf("Digite o tamanho do vetor: ");
	scanf("%d", &n);
	
	// Aloca espaço para n inteiros
	vetor = (int*) malloc(n * sizeof(int));
	
	if(vetor == NULL) {
		printf("Erro de alocação!\n");
		return 1;
	}
	
	// Preenchendo o vetor
	for (i = 0; i < n; i++) {
		vetor[i] = i + 1;
	}
	
	// Exibindo o vetor
	printf("Valores armazenados:\n");
	for (i = 0; i < n; i++) {
		printf("%d ", vetor[i]);
	}
	
	free(vetor); // Liberação da memória
	return 0;
}
```

### Explicação

- `malloc(n * sizeof(int))` → aloca memória para **n inteiros**.
- Usamos `vetor[i]` normalmente, como se fosse um array comum.
- Essa abordagem é essencial quando **não sabemos o tamanho do array em tempo de compilação**.

---
# Uso em  Estrutura Dinâmicas

O `malloc` também é a base para estruturas como **listas encadeadas, pilhas e filas**.

Exemplo: criar um nó de lista encadeada.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct No {
	int valor;
	struct No* prox;
} No;

int main() {
	No* primeiro = (No*) malloc(sizeof(No));
	
	if(primeiro == NULL) {
		printf("Erro de alocação!\n");
		return 1;
	}
	
	primeiro->valor = 10;
	primeiro->prox = NULL;
	
	printf("Valor do primeiro no: %d\n", primeiro->valor);
	
	free(primeiro);
	return 0;
}
```

---
# Boas práticas com `malloc`

✅ Sempre verificar se `malloc` retornou `NULL`.  
✅ Usar `sizeof(tipo)` ao calcular o tamanho da alocação.  
✅ Liberar memória com `free()` depois do uso.  
✅ Evitar “memory leaks” (quando esquecemos de liberar).  
✅ Para inicializar a memória com zeros, usar `calloc` em vez de `malloc`.

---
# Comparação `malloc` vs `calloc` vs `realloc`

- **`malloc(tamanho)`** → aloca memória mas deixa o conteúdo **indefinido** (lixo de memória).
- **`calloc(qtd, tamanho)`** → aloca memória e **zera** todos os bytes.
- **`realloc(ptr, novo_tamanho)`** → realoca memória previamente alocada.

---
# Resumo

- `malloc` é usado para **alocar memória em tempo de execução**.
- Útil quando o tamanho das estruturas de dados não é conhecido durante a compilação.
- Essencial para implementar **estruturas dinâmicas** (listas, árvores, grafos, etc.).
- Deve ser usado com cuidado para evitar vazamentos de memória.