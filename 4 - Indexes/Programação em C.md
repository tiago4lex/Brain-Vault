#C 

---
## 1. Introdução à Linguagem C

###  1.1 História e importância da linguagem C  
- [[História da Linguagem C]]
- [[6 - Full Notes/Progamação em C/1. Introdução à Linguagem C/1.1 História e Importância da linguagem C/Complexidade de Algoritmos]]

### 1.2 Estrutura básica de um programa em C  
- [[Design de Estruturas de Busca e Armazenamento]]

### 1.3 Compilação e execução (gcc, clang, IDEs, etc.)  
- [[Configuração de Ambiente para programação em C]]
- [[Programando em C no VSCode]]

1.4 Função `main()` e fluxo de execução  
1.5 Entrada e saída básica (`printf`, `scanf`)

---

## 2. Conceitos Fundamentais

2.1 Tipos de dados primitivos (`int`, `float`, `double`, `char`)  
2.2 Modificadores de tipo (`short`, `long`, `unsigned`, `signed`)  
2.3 Constantes e variáveis  
2.4 Operadores aritméticos, relacionais e lógicos  
2.5 Operadores de incremento e decremento  
2.6 Operadores de atribuição e operadores bit a bit  
2.7 Precedência e associatividade de operadores

---

## 3. Estruturas de Controle

3.1 Estruturas condicionais: `if`, `else if`, `else`  
3.2 Estrutura condicional múltipla: `switch-case`  
3.3 Estruturas de repetição: `for`, `while`, `do-while`  
3.4 Controle de laços: `break`, `continue`  
3.5 Operador ternário `?:`

---

## 4. Funções

4.1 Declaração e definição de funções  
4.2 Passagem de parâmetros (por valor e por referência)  
4.3 Escopo de variáveis (local, global e estático)  
4.4 Funções recursivas  
4.5 Protótipos de funções  
4.6 Funções da biblioteca padrão (`math.h`, `string.h`, etc.)

---

## 5. Arrays (Vetores e Matrizes)

### 5.1 Declaração e inicialização de vetores  
- [[Arrays em C]]

5.2 Acesso a elementos  
5.3 Arrays multidimensionais (matrizes)  
5.4 Strings em C (conceito de array de `char`)  
5.5 Funções úteis de manipulação de strings (`strlen`, `strcpy`, `strcmp`, etc.)

---

## 6. Ponteiros

6.1 Conceito de endereço de memória (`&` e `*`)  
### 6.2 Declaração e uso de ponteiros
- [[Ponteiros em C]]
- [[Operadores e Ponteiros]]

6.3 Ponteiros e arrays  
6.4 Ponteiros e strings  
6.5 Ponteiros para ponteiros  
6.6 Ponteiros e funções (passagem por referência)  
6.7 Ponteiros e alocação dinâmica

---

## 7. Estruturas de Dados em C

### 7.1 `struct` (estruturas)
- [[Estruturas - Struct]]

7.2 `typedef`  
7.3 `union`  
7.4 `enum`  
7.5 Arrays de structs  
7.6 Structs aninhadas  
7.7 Ponteiros para structs

---

## 8. Alocação Dinâmica de Memória

8.1 Biblioteca `<stdlib.h>`  
### 8.2 Funções `malloc`, `calloc`, `realloc`, `free`
- [[malloc em C - Alocação Dinâmica de Memória]]

### 8.3 Diferença entre memória estática e dinâmica  
- [[Memória Estática vs Dinâmica]]

8.4 Exemplos práticos de alocação

---

## 9. Arquivos (File Handling)

9.1 Tipos de arquivos (texto e binário)  
### 9.2 Funções para manipulação de arquivos
- [[Manipulando Arquivos em C]] - (`fopen`, `fclose`, `fgetc`, `fputc`, `fgets`, `fprintf`, `fscanf`)

9.3 Leitura e escrita em arquivos binários (`fread`, `fwrite`)  
9.4 Manipulação de ponteiros de arquivo (`fseek`, `ftell`, `rewind`)

---

## 10. Conceitos Avançados

10.1 Diretivas de pré-processador (`#define`, `#include`, `#ifdef`, `#ifndef`)  
10.2 Macros e constantes simbólicas  
10.3 Compilação condicional  
10.4 Modularização de programas (arquivos `.h` e `.c`)

### 10.5 Estruturas de dados dinâmicas (listas encadeadas, pilhas, filas, árvores)
- 10.5.1 Listas Encadeadas
	- [[Introdução a Listas Encadeadas]]
	- [[Avançando com Listas Encadeadas]]

- 10.5.2 Pilhas
	- [[Estruturas de Dados Lineares - Pilha]]
		- [[Pilha Estática em C - Conceito e Implementação]]
		- [[Pilha Dinâmica em C - Conceito e Implementação]]

- 10.5.3 Filas
- 10.5.4 Árvores
	- [[Árvores e Árvores Binárias]]

- 10.5.5 Grafos
	- 
10.6 Ponteiros para funções  
10.7 Estruturas genéricas (void pointers)

---

## 11. Algoritmos de Ordenação e Busca

- [[6 - Full Notes/Progamação em C/1. Introdução à Linguagem C/1.1 História e Importância da linguagem C/Complexidade de Algoritmos|Complexidade de Algoritmos]]
- [[Algoritmos de Busca e Ordenação em Arrays]]

11.1. Busca Linear  
11.2. Busca Binária  
11.3. Bubble Sort  
11.4. Selection Sort  
11.5. Insertion Sort  
11.6. Merge Sort



---

## 12. Boas Práticas e Otimização

12.1 Organização de código em múltiplos arquivos  
12.2 Documentação de código em C  
12.3 Convenções de nomenclatura  
12.4 Tratamento de erros e boas práticas com `errno`  
12.5 Depuração e uso de ferramentas (`gdb`, `valgrind`)

---

## 13. Projetos Práticos

13.1 Calculadora simples  
13.2 Manipulação de strings (validador de senhas, inversor de palavras)  
13.3 Sistema de cadastro (alunos, produtos, clientes)  
13.4 Agenda telefônica (usando arquivos)  
13.5 Mini banco de dados em C (arquivos + structs)  
13.6 Estruturas de dados: pilha, fila e lista encadeada