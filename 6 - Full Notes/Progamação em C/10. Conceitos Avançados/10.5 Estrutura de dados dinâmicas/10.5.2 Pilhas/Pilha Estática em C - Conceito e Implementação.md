2025-08-19 08:19

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Pilha]] | [[Memória Estática]]

---
# O que é uma  Pilha

Um **pilha *(stack)*** é uma estrutura de dados linear que segue o princípio **LIFO** *(Last In, First Out)*, ou seja:

- O <font color="#ffc000"><strong>último elemento inserido</strong></font> é o <font color="#ffc000"><strong>primeiro a ser removido</strong></font>.
- Imagine uma pilha de pratos: você coloca um prato no topo e só consegue retirar o de cima.

---
# Pilha Estática

Quando dizemos quem uma pilha é **estática**, significa que:

- O **tamanho máximo** da pilha é definido **antes da execução** (em tempo de compilação).
- A pilha é representada por um **array de tamanho fixo**.
- Não são usados ponteiros para alocação dinâmica de memória.
- Quando a pilha atinge o tamanho máximo, ocorre **estouro de pilha** (_stack overflow_).
- Quando está vazia e tentamos remover um elemento, ocorre **underflow** (_pilha vazia_).

📌 **Representação da pilha:**

- Um **array** para armazenar os elementos.
- Uma variável `top` para indicar a posição do elemento mais recente.
- Quando `top == -1`, a pilha está vazia.
- Quando `top == MAX - 1`, a pilha está cheia.

---
# Código de Pilha Estática - Estrutura Geral

O código é dividido em partes:

## 1. Inclusão de bibliotecas e constantes

```css
#include <stdio.h>
#define MAX 10
```

- `stdio.h`: usada para funções de entrada e saída (`printf`, `scanf`).
- `MAX`: define a capacidade máxima de pilha (10 elementos).

## 2. Declaração das variáveis globais

```c
int st[MAX];   // array que representa a pilha
int top = -1;  // indica que a pilha começa vazia
```

- `st`: a estrutura onde os dados serão armazenados.
- `top`: guarda o índice do elemento no topo da pilha.
	- `-1`: significa que a pilha está vazia.

## 3. Protótipos das funções

```c
void push(int st[], int val);  // Empilhar
int pop(int st[]);             // Desempilhar
void display(int st[]);        // Mostrar elementos
```

- **push**: insere elemento no topo.
- **pop**: remove elemento do topo.
- **display**: exibe toda a pilha.

## 4. Função principal (`main`)

```c
int main()
{
    int val, option;
    do {
        printf("\n *****MAIN MENU*****");
        printf("\n 1. Empilhar (push)");
        printf("\n 2. Desempilhar (pop)");
        printf("\n 4. Mostrar");
        printf("\n 5. Sair");
        printf("\n Entre com sua opcao: ");
        scanf("%d", &option);

        switch(option)
        {
            case 1:
                printf("\n Numero a ser empilhado na Pilha: ");
                scanf("%d", &val);
                push(st, val);
                break;
            case 2:
                val = pop(st);
                if(val != -1)
                    printf("\n O valor desempilhado da Pilha foi: %d", val);
                break;
            case 4:
                display(st);
                break;
        }
    } while (option != 5);
    return 0;
}
```

📌 **O que acontece aqui:**

- É exibido um menu interativo.
- O usuário escolhe se quer empilhar, desempilhar, mostrar ou sair.
- As funções são chamadas conforme a escolha.
- O loop `do...while` mantém o programa rodando até que a opção **5 (Sair)** seja escolhida.

## 5. Função `push` - Inserir elemento

```c
void push(int st[], int val){
	if(top == MAX-1)  // Pilha cheia?
	{
		printf("\n ESTOURO DE PILHA");
	}
	else
	{
		top++;
		st[top] = val;
	}
}
```

📌 **Como funciona:**

- Se `top == MAX-1`, a pilha está cheia e não é possível inserir.
- Caso contrário:
	- Incrementa `top` para apontar para a próxima posição livre.
	- Armazena o novo valor nessa posição.

## 6. Função `pop` - Remover elemento

```c
int pop(int st[])
{
    int val;
    if(top == -1) // Pilha vazia?
    {
        printf("\n PILHA VAZIA");
        return -1;
    }
    else
    {
        val = st[top];
        top--;
        return val;
    }
}
```

📌 **Como funciona:**

- Se `top == 1`, não há elementos para remover (underflow).
- Caso contrário:
	- Guarda o valor no topo.
	- Decrementa `top` para "remover" o elemento.
	- Retorna o valor removido.

## 7. Função `display` - Mostrar elementos

```c
void display(int st[])
{
    int i;
    if(top == -1)
        printf("\n PILHA VAZIA");
    else
    {
        for(i = top; i >= 0; i--)
            printf("\n %d", st[i]);
    }
}
```

📌 **Como funciona:**

- Se `top == -1`, não há nada para mostrar.
- Caso contrário:
    - Percorre o array da posição `top` até 0.
    - Exibe cada elemento (mostrando do topo para a base).

---
# Resumo Visual do Funcionamento

```css
[Pilha Vazia]      top = -1
[Push 5]           top = 0   -> [5]
[Push 8]           top = 1   -> [5, 8]
[Pop]              remove 8  -> [5], top = 0
[Display]          mostra: 5
```

---
# Vantagens e Desvantagens da Pilha Estática

| **Vantagens**                           | **Desvantagens**                          |
| --------------------------------------- | ----------------------------------------- |
| Simples de implementar                  | Tamanho fixo definido antes da execução   |
| Acesso rápido ao topo (`0(1)`)          | Pode desperdiçar memória se sobrar espaço |
| Não precisa de gerenciamento de memória | Pode causar overflow facilmente           |
