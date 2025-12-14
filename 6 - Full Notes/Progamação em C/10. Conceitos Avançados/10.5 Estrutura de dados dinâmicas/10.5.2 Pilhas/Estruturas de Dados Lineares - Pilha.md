2025-08-19 08:18

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Estrutura de Dados]] | [[Pilha]]

----
# Conceito Geral

Uma **estrutura de dados linear** organiza seus elementos de forma **sequencial**, ou seja, cada item está conectado ao seu **antecessor** e ao seu **sucessor** (exceto o primeiro e o último).

O acesso aos dados segue **uma ordem bem definida**, que pode ser:

- **Sequencial**: percorrendo do primeiro ao último.
- **Baseada em índice**: acessando diretamente pela posição.

📌 **Características principais:**

- Todos os elementos estão em **uma única sequência**.
- Geralmente armazenados de forma **contígua na memória** (listas, arrays).
- **Navegação previsível**: sempre existe um próximo ou anterior.

## Tipos de Estruturas Lineares

As principais estruturas lineares são:

1. **Array (Vetor)**
2. **Lista Ligada (Linked List)**
3. **Pilha (Stack)**
4. **Fila (Queue)**

---
# Pilha *(Stack)*

Segue o princípio **LIFO** (_Last In, First Out_).

- As **inserções** ocorrem no **topo** da pilha.
- As **exclusões** ocorrem no **topo** da pilha.
- Utiliza a mesma lógica de uma pilha de pratos, papéis, etc.

![[Pasted image 20250807210054.png]]


## 📌 **Operações principais:**

- **Função inicializar uma Pilha**
	- É preciso apenas acertar o valor do campo **topo**.
	- **Topo** indica a posição no arranjo do elemento que está no topo da pilha.
	- É preciso sinalizar que a pilha está vazia. Para isso basta atribuir o valor `-1`.

- **push**: inserir no topo.

![[Pasted image 20250807210735.png]]

- **pop**: remover do topo.

![[Pasted image 20250807210647.png]]

- **peek**: acessar o elemento do topo sem remover.

## 📌 **Aplicações:**

Sua principal aplicação é o **armazenamento** de dados em que é importante **preservar a ordem** (neste caso, FILO) de entradas e saídas.

**Exemplos de aplicações de Pilha:**

- Editores de texto - opção desfazer.
- Execução de chamadas de funções por um programa de computador.
- Algoritmos que envolvem Grafos (Árvores).
- Calculadores HP (expressões pós-fixadas).
- Controle de chamadas de funções.
- Conversão e avaliação de expressões.

---
# Performance quanto ao tipo de Implementação de uma Pilha

Não existe diferenças significativas em termos de eficiência, uma vez que a estruturas só admite estas operações no topo da estrutura.

Isto acontece por que todas as operações só acontecem com o conteúdo presente no **Topo**, "ignorando" assim todo o restante de conteúdo que está abaixo do topo.


---
# Exemplo de PILHA em código

```c
/*
Escrever um programa em C que realize Empilhar, Desemplilhar e Mostrar uma PILHA.

Como a representação da PILHA é Estática, o que devo imaginar que exista?:
    - não ter/usar Ponteiros;
    - a representação da Pilha vazia dever ser -1
*/

#include <stdio.h>
#define MAX 10      // Definindo o tamanho máximo da pilha para 10 elementos

int st[MAX];        // "st" é uma Array para armazenar os elementos da pilha com tamanho máximo MAX = 10

int top = -1;       // "top" é um inteiro que indica o topo da pilha, começando em -1 para indicar que a pilha está vazia
  
// Definição das funções para manipulação da pilha usadas no código(main)
```
