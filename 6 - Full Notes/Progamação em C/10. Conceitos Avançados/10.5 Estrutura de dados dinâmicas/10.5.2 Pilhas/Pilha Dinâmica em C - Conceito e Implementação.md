2025-08-19 08:19

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Pilha]] | [[Memória Dinâmica]]

---
# O que é uma Pilha Dinâmica?

Uma **pilha dinâmica** é uma estrutura de dados linear que segura o princípio **LIFO *(Last In, First Out)*** - o último elemento inserido é o primeiro a ser removido.

A diferença entre a pilha estática é que <font color="#31859b"><strong>a alocação de memória é feita em tempo de execução, usando ponteiros e alocação dinâmica</strong></font> (`malloc` ou funções equivalentes).

## 📌 Características principais

- **Tamanho variável:** cresce ou diminui conforme elementos são inseridos ou removidos.
- **Uso eficiente de memória**: aloca apenas o necessário.
- **Implementada com ponteiros:** cada elemento (nó) aponta para o próximo.
- Não existe risco de **estouro fixo de capacidade** (como na estática), mas pode falhar se a memória disponível acabar.

![[Pasted image 20250814203653.png]]

---
# Como funciona?

Na pilha dinâmica:

- Cada elemento é um **nó** alocado dinamicamente com:
    - Um **campo de dado** (o valor armazenado).
    - Um **ponteiro para o próximo nó**.

- O **topo** é um ponteiro que sempre aponta para o elemento mais recente.    
- Operações principais:
    - **push**: cria um novo nó, coloca o valor e ajusta o ponteiro do topo.
    - **pop**: remove o nó apontado pelo topo e ajusta o ponteiro.
    - **display**: percorre a pilha imprimindo os elementos.

---
# Código da Pilha Dinâmica

## 1. Inclusão de bibliotecas

```css
#include <stdio.h>
#include <stdlib.h>
#include <malloc.h>
```

- `stdio.h`: Funções de entrada e saída (`printf`, `scanf`).
- `stdlib.h`: Funções de alocação e liberação de memória (`malloc`, `free`).
- `malloc.h`: Declaração da função `malloc` (em alguns compiladores antigos).

## 2. Estrutura do nó da pilha

```c
struct pilha
{
	int dado;
	struct pilha *proximo;
};
```

- `dado`: valor armazenado no nó.
- `proximo`: ponteiro para o próximo nó na pilha (o nó abaixo dele).


## 3. Ponteiro global para o topo

```c
struct pilha *topo = NULL;
```

- Inicia com `NULL` indicando que a pilha está vazia.

## 4. Função `push` - Inserir elemento

```c
struct pulha *push (struct pilha *topo, int val)
{
	struct pilha *ptr;
	ptr = (struct pilha *)malloc(sizeof(struct pilha));
	ptr->dado = val;
	if (topo == NULL)
	{
		ptr->proximo = NULL;
		topo = ptr.
	}
	else
	{
		ptr->proximo = topo;
		topo = ptr;
	}
	return topo;
}
```

📌 Passo a passo:

1. Aloca memória para um novo nó (`malloc`).
2. Armazena o valor (`dado`).
3. Se a pilha está vazia:
	- `proximo` recebe `NULL`.
	- `topo` passa a apontar para o novo nó.

4. Se já existem elementos:
	- O campo `proximo` do novo nó aponta para o atual topo.
	- `topo` é atualizado para o novo nó.

## 5. Função `display` - Mostar elementos

```c
struct pilha *display(struct pilha *topo)
{
    struct pilha *ptr;
    ptr = topo;
    if (topo == NULL)
        printf("\n pilha VAZIA");
    else
    {
        while (ptr != NULL)
        {
            printf("\n%d", ptr->dado);
            ptr = ptr->proximo;
        }
    }
    printf("\n");
    system("pause");
}
```

📌 **Passo a passo:**

1. Cria um ponteiro auxiliar `ptr` para percorrer a pilha.
2. Se `topo` for `NULL`, exibe mensagem de pilha vazia.
3. Caso contrário, percorre do topo até o final (`NULL`), exibindo cada valor.
4. Usa `system("pause")` para esperar o usuário antes de continuar.

## 6. Função `pop` - Remover elemento

```c
struct pilha *pop(struct pilha *topo)
{
	struct pilha *ptr;
	ptr = topo;
	if (topo == NULL)
		printf("\n PILHA VAZIA");
	else
	{
		topo = topo->proximo;
		printf("\n O valor desempilhado foi: %d", ptr->dado);
		free(ptr);
	}
	return topo;
}
```

📌 **Passo a passo:**

1. Usa `ptr` para apontar para o nó atual do topo.
2. Se `topo` for `NULL`, a pilha está vazia.
3. Caso contrário.
	- Move `top` para o próximo nó.
	- Exibe o valor desempilhado.
	- Libera a memória do nó removido (`free`).

## 7. Função `main` - Controle do programa

```c
int main()
{
    int val, opcao;
    do
    {
        system("cls");
        printf("\n *****MAIN MENU*****");
        printf("\n 1. Empilhar");
        printf("\n 2. Desempilhar");
        printf("\n 3. Mostrar toda pilha");
        printf("\n 4. Sair");
        printf("\n Enter com a opcao : ");
        scanf("%d", &opcao);
        switch (opcao)
        {
        case 1:
            printf("\n Entre com o valor a ser empilhado:");
            scanf("%d", &val);
            topo = push(topo, val);
            break;
        case 2:
            topo = pop(topo);
            break;
        case 3:
            topo = display(topo);
            break;
        }
    } while (opcao != 4);
    return 0;
}
```

📌 **O que faz:**

- Mostra um menu para o usuário.
- Lê a  opção e executa:
	- `1` → Empilhar (`push`).
	- `2` → Desempilhar (`pop`).
	- `3` → Mostrar pilha (`display`).
- Continua até que a opção `4` seja escolhida.

---
# Comparação: Pilha Estática vs Pilha Dinâmica

| **Característica**         | **Pilha Estática**      | **Pilha dinâmica**    |
| -------------------------- | ----------------------- | --------------------- |
| Tamanh                     | Fixo                    | Variável              |
| Estrutura de armazenamento | Array                   | Lista encadeada       |
| Uso de memória             | Pode desperdiçar espaço | Aloca só o necessário |
| Overflow                   | Quando `top == MAX -1`  | Quando memória acaba  |
| Ponteiros                  | Não usa                 | Usa                   |

---
# Fluxo de execução visual

Exemplo de operações:

```css
[Push 10] -> Topo: 10
[Push 20] -> Topo: 20 -> 10
[Pop]     -> Remove 20 -> Topo: 10
[Display] -> Mostra 10
```

