2025-10-16 19:47

Status: #developed #C 

Tags: [[Programação em C]] | [[Ponteiros]] | [[Alocação Dinâmica]]

----
# Definição (conceito geral)

Uma árvore é uma estrutura de dados não-linear composta por nós (ou vértices) e arestas que conectam pares de nós, com as seguintes propriedades fundamentais.

- Existe um nó especial chamado **raiz *(root)***.
- Cada nó pode ter zero ou mais **filhos.**
- Não existem ciclos: seguindo arestas a partir da raiz nunca se volta para um nó já visitado (estrutura acíclica).
- Cada nó (exceto a raiz) tem exatamente um **pai**.

![[Pasted image 20251016195017.png]]

Elementos importantes:

- **Nó** *(node)*: contém dados e referências para seus filhos.
- **Filho** *(child)*: e **pai** *(parent)*.
- **Folha** *(leaf)*: nó sem filhos.

![[Pasted image 20251016195313.png]]

- **Altura** *(height)*: comprimento do caminho mais longo da raiz até uma folha (em números de arestas ou nós, dependendo da convenção).
- **Profundidade** *(depth)*: distância da raiz até um nó.

![[Pasted image 20251016195559.png]]

Árvores são usadas para representar hierarquias (sistemas de arquivos), expressões (árvores de expressão), índices (B-trees, BSTs), entre outros.

---
# Árvore Binária

Uma **árvore binária** *(binary tree)* é uma árvore em que cada nó tem **no máximo dois filhos**, geralmente chamados **filho esquerdo** *(left)* e **filho direito** *(right)*.

![[Pasted image 20251016195631.png]]


Propriedades e conceitos específicos:

- **Árvore binária completa:** todos os níveis, exceto talvez o último, estão completamente preenchidos e todos os nós do último nível estão o mais à esquerda possível.
- **Árvore binária cheia (strict / proper / full)**: cada nó tem 0 ou 2 filhos (nunca 1).
- **Árvore binária perfeita**: árvore cheia onde todos os níveis têm o número máximo de nós (todos os caminhos da raiz até folhas têm o mesmo comprimento).

![[Pasted image 20251016201029.png]]

- **BST (Binary Search Tree)**: árvore binária com a propriedade de pesquisa: para cada nó, todos os valores no subárvore esquerda < valor do nó, e todos os valores no subárvore direita > valor do nó (assumindo chaves únicas). Isto permite busca, inserção e remoção em tempo médio O(h), onde h é a altura.

---
# Representações em memória

Existem duas formas comuns de implementar árvores em C:

## 1. Alocação Estática *(array)*

Ideal para árvores binárias completas ou quase completas (ex.: *heaps*). Usa-se índice do array para navegar entre pai/filhos:

- índice do nó `i`
- filho da esquerda: `2 * i + 1`
- filho da direita: `2 * i + 2`
- pai: `(i - 1) / 2` (inteiro)

![[Pasted image 20251016201611.png]]

**Vantagem:**

- Acesso rápido por índice; simples.

**Desvantagem:**

- Desperdício de memória para árvores esparsas; limite de tamanho fixo.

## 2. Alocação Dinâmica (ponteiros / lista encadeada)

Cada nó tem ponteiros `left` e `right` para os filhos. Ideal para árvores arbitrárias, BTSs, AVL, etc.

![[Pasted image 20251016202000.png]]

**Vantagens:**

- Flexibilidade, cresce conforme necessidade.

**Desvantagens:**

- Mais overhead por alocação, acesso indireto via ponteiros.

---
# Operações básicas

Operações comuns em árvores binárias.

- `create` / inicializar.
- `insert` (inserir dados).
- `search` (buscar).
- `delete` (remover).
- travessias *(traversals)*: **pre-order**, **in-order**, e **level-order** (BFS).

**Explicação rápida das travessias (recursivas):**

- **Pré-Order:** visita nó, depois esquerda, depois direita *(root, left, right)*.
- **In-order**: esquerda, visite nó, direita. (left, root, right) — em BST produz chaves ordenadas.
- **Post-order**: esquerda, direita, visite nó. (left, right, root)
- **Level-order**: por níveis, geralmente usando fila (BFS).

---
# Implementação - Árvore Binária com Array

## Quando usar?

Use quando a árvore é aproximadamente completa e tem um limite superior conhecido de nós (por exemplo: implementação de heap binário).

## Estrutura e convenções

- Representamos a árvore com um array `int tree[MAX]`.
- Um indicador especial (por exemplo `INT_MIN` ou `-1`) pode indicar posição vazia se quisermos representa árvores esparsas.
- Para simplicidade, no exemplo abaixo usaremos `-1` como "vazio" e `MAX` como capacidade.

## Código completo (array) - `binary_tree_array.c`

```c
#include <stdio.h>
#include <limits.h>

#define MAX 100
#define EMPTY INT_MIN

// Representa a árvore em um array
int tree[MAX];
int size = 0;  //  número de elementos efetivos (opcional)

// Inicializa o array com EMPTY
void init_tree(){
	for (int i = 0; i < MAX; i++) tree[i] = EMPTY;
}

// Função de inserção simples: insere na primeira posição livre (útili para árvore completa simulada)
int insert_array(int value) {
	if (size >= MAX) return -1; // cheio
	tree[size] = value;
	size++;
	return size - 1; // índice onde inseriu
}

// Acesso aos filhos e pai
int left_index(int i) { return 2*i + 1; }
int right_index(int i) { return 2*1 + 2; }
int parent_index(int i) { return (i - 1) / 2; }

// Travessias recursisvas (verificam se o índice está dentro do limite e não EMPTY)
void preorder_array(int i) {
	if (i >= MAX || tree[i] == EMPTY) return;
	printf("%d ", tree[i]);
	preorder_array(left_index(i));
	preorder_array(right_index(i));
}

void inorder_array(int i) {
	if (i >= MAX || tree[i] == EMPTY) return;
	inorder_array(left_index(i));
	printf("%d ", tree[i]);
	inorder_array(right_index(i));
}

void postorder_array(int i) {
	if (i >= MAX || tree[i] == EMPTY) return;
	postorder_array(left_index(i));
	postorder_array(right_index(i));
	printf("%d ", tree[i]);
}

int main() {
	init_tree();
	// Exemplo: montar a árvore a partir desse array
	//        10
	//      /    \
	//     5      20
	//    / \    /
	//   3   7  15
	
	insert_array(10); // índice 0
	insert_array(5); // índice 1
	insert_array(20); // índice 2
	insert_array(3); // índice 3
	insert_array(7); // índice 4
	insert_array(15); // índice 5
	
	printf("Pre-order: "); preorder_array(0); printf("\n");
	printf("In-order: "); preorder_array(0); printf("\n");
	printf("Post-order: "); postorder_array(0); printf("\n");
	
	return 0;
}
```

### Explicação do código

- `#define MAX 100` define capacidade do array para no máximo 100 valores.
- `EMPTY` é usado para indicar posições vazias (aqui usamos `INT_MIN`).
- `init_tree()` preenche o array com `EMPTY`.
- `insert_array(int value)` coloca `value` na primeira posição livre (simples) e incrementa `size++`.
- `left_index`, `right_index`, `parent_index` implementas as fórmulas de conversão índice ↔ relação pai/filho.
- As funções de travessia (`preorder_array`, `inorder_array`, `postorder_array`) são recursivas: recebem o índice do nó atual e verificam se o índice é válido e contém um valor.
- `main()` monta manualmente um pequeno exemplo e imprime as travessias.

>[!note] Observação:
>Esse método de "inserir na primeira posição livre" não respeita ordenação de BST. Para árvores de busca, a versão em array não é a prática exceto para árvores quase completas. Para BST use alocação dinâmica.

---
# Implementação - Árvore Dinâmica com ponteiros

## Estrutura básica

Cada nó é representado por uma `struct` com um campo `data` e dois ponteiros `left` e `right`:

```c
typdef struct Node {
	int data;
	struct Node *left;
	struct Node *right;
} Node;
```

Ela define um **tipo de dado composto** com três campos:

- `data` → guarda o número,
- `left` → ponteiro para o filho da esquerda,
- `right` → ponteiro para o filho da direita.

## Exemplo: BST simples com operações básicas

Código completo: `bst_dynamic.c`

 ```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *left;
    struct Node *right;
} Node;

// Cria um novo nó com valor 'value'
Node* create_node(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (!newNode) {
        perror("malloc falhou");
        exit(EXIT_FAILURE);
    }
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Insere em uma BST (recursivo)
Node* insert_bst(Node* root, int value) {
    if (root == NULL) return create_node(value);
    if (value < root->data) {
        root->left = insert_bst(root->left, value);
    } else if (value > root->data) {
        root->right = insert_bst(root->right, value);
    } // se igual, aqui optamos por não inserir duplicatas
    return root;
}

// Busca em BST (recursivo)
Node* search_bst(Node* root, int value) {
    if (root == NULL || root->data == value) return root;
    if (value < root->data) return search_bst(root->left, value);
    else return search_bst(root->right, value);
}

// Travessias
void inorder(Node* root) {
    if (root == NULL) return;
    inorder(root->left);
    printf("%d ", root->data);
    inorder(root->right);
}

void preorder(Node* root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    preorder(root->left);
    preorder(root->right);
}

void postorder(Node* root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    printf("%d ", root->data);
}

// Encontra o mínimo (usado em remoção)
Node* find_min(Node* root) {
    while (root->left != NULL) root = root->left;
    return root;
}

// Econtra o máximo
Node* find_max(Node* root) {
    while (root->right != NULL)
        root = root->right;
    return root;
}

// Remove um nó de uma BST (recursivo)
Node* delete_bst(Node* root, int value) {
    if (root == NULL) return NULL;
    if (value < root->data) {
        root->left = delete_bst(root->left, value);
    } else if (value > root->data) {
        root->right = delete_bst(root->right, value);
    } else {
        // Nó encontrado
        if (root->left == NULL && root->right == NULL) {
            free(root);
            return NULL;
        } else if (root->left == NULL) {
            Node* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            Node* temp = root->left;
            free(root);
            return temp;
        } else {
            // dois filhos: substituir pelo sucessor (mínimo da subárvore direita)
            Node* temp = find_min(root->right);
            root->data = temp->data;
            root->right = delete_bst(root->right, temp->data);
        }
    }
    return root;
}

// Libera toda a árvore
void free_tree(Node* root) {
    if (!root) return;
    free_tree(root->left);
    free_tree(root->right);
    free(root);
}

int main() {
    Node* root = NULL;
    int values[] = {50, 30, 70, 20, 40, 60, 80};
    int n = sizeof(values)/sizeof(values[0]);

    for (int i = 0; i < n; i++) root = insert_bst(root, values[i]);

    printf("In-order (deve estar ordenado): "); inorder(root); printf("\n");
    printf("Pre-order: "); preorder(root); printf("\n");
    printf("Post-order: "); postorder(root); printf("\n");

    printf("Removendo 70...\n");
    root = delete_bst(root, 70);
    printf("In-order apos remocao: "); inorder(root); printf("\n");

    // Busca
    int key = 60;
    Node* found = search_bst(root, key);
    if (found) printf("Encontrado: %d\n", found->data);
    else printf("Nao encontrado: %d\n", key);

    free_tree(root);
    return 0;
}
 ```

### Explicação do código

O código constrói uma **árvore binária de busca (BST), onde:**

- Cada nó contém um valor inteiro (`data`);
- Cada nó tem dois ponteiros (`left` e `right`), que apontam para seus filhos esquerdo e direito;
- Os valores menores ficam à esquerda e os maiores à direita (regra da BST);
- As funções permitem inserir, buscar, percorrer e remover elementos.

#### 1. Inclusão de bibliotecas e definição da estrutura:

```c
#include <stdio.h>
#include <stdlib.h>
  
typedef struct Node {
	int data;
	struct Node *left;
	struct Node *right;
} Node;
```

- `#include <stdio.h>`: permite usar funções de entrada e saída como `printf()` e `scanf()`.
- `#include <stdlib.h>`: inclui funções como `malloc()` e `free()` (necessárias para alocação dinâmica de memória).
- A `struct Node` define como será cada nó da árvore:
    - `data`: guarda o valor do nó (inteiro).
    - `left` e `right`: ponteiros para os filhos esquerdo e direito.

- `typedef` renomeia `struct Node` para apenas `Node`, facilitando a declaração.

#### 2. Criando um novo nó

```c
Node* create_node(int value) {
	Node* newNode = (Node*)malloc(sizeof(Node));
	if(!newNode) {
		perror("malloc falhou");
		exit(EXIT_FAILURE);
	}
	newNode->data = value;
	newNode->left = newNode->right = NULL;
	return newNode;
}
```

- `malloc(sizeof(Node))`: aloca dinamicamente espaço na memória para um novo nó.
- Verifica se a alocação foi bem-sucedidada, se `malloc` retornar `NULL`, imprime erro e encerra o programa.
- Inicializa:
	- `data` com o valor recebido (`value`),
	- `left` e `right` como `NULL` (nó recém-criado ainda não tem filhos).

- Retorna o endereço do novo nó.

#### 3. Inserindo nós (função recursiva)

```c
Node* insert_bst(Node* root, int value) {
	if (root == NULL) return create_node(value);
	if (value < root->data) {
		root->left = insert_bst(root->left, value);
	} else if (value > root->data) {
		root->right = insert_bst(root->right, value);
	}
	return root;
}
```

Esta função insere um novo valor **mantendo a regra da BST**.

1. **Caso base:**
	- Se `root == NULL`, quer dizer que chegamos em uma posição onde o novo nó deve ser inserido.
	- Chamamos `create_node(value)` e retornamos o novo nó.

2. **Recursão:**
	- Se `value < root->data`, o valor é menor - deve ir para o **lado esquerdo**. Chamamos `insert_bst` novamente, passando `root->left`.
	- Se `value > root->data`, o valor é maior - vai para o **lado direto.**

![[e0684f0c5f932acc8c4e2fe5724352ce32d9c7c7.gif]]

3. **Retorno:**
	- A função sempre retorna o `root` atualizado, pois em chamadas recursivas é preciso manter o encadeamento entre nós.

#### 4. Buscando um valor na árvore

```c
Node* search_bst(Node* root, int value) {
	if (root == NULL || root->data == value) return root;
	if (value < root->data) return search_bst(root->left, value);
	else return search_bst(root->right, value);
}
```

- Se a árvore está varia (`root == NULL`) ou encontramos o valor (`root-> data == value`), retornamos o nó encontrado.
- Se o valor buscado é menor que o atual, procuramos na **subárvore esquerda**.
- Caso contrário, buscamos na **subárvore direita**.

![[4444cd9c90c911ca04e02c54921b5d1b5e7aa6fa.gif]]

A busca se a lógica de um "mapa" binário, comparando e escolhendo o caminho certo.

#### 5. Encontrar o menor valor da árvore

```c
Node* find_min(Node* root) {
	while (root->left != NULL) root = root->left;
	return root;
}
```

- O menor valor de uma BST está **sempre no canto mais à esquerda**.
- Enquanto houver filho à esquerda, seguimos até o último.
- Retornamos o ponteiro do nó mínimo encontrado.

Percorre a árvore pela esquerda até o fim.

![[d64adbb6c52d13341884a3c557377b65b2cd91c7.gif]]

#### 6. Encontrar o maior valor da árvore

```c
Node* find_max(Node* root) {
    while (root->right != NULL)
        root = root->right;
    return root;
}
```

- O maior valor em um árvore **estará sempre no nó mais á direita**.
- O laço `while (root->right != NULL)` vai caminhando para a direita até encontrar o último nó.
- Quando `root->right` for `NULL`, significa que `root` é o nó mais à direita da árvore → **maior valor**.
- A função retorna o ponteiro desse nó.

![[44dbb778ffb54dc8158b458a8351f530ab530ea5.gif]]

#### 7. Remover um nó da árvore

```c
Node* delete_bst(Node* root, int value) {
	if (root == NULL) return NULL;
	
	if (value < root->data) {
		root->left = delete_bst(root->left, value);
	} else if (value > root->data) {
		root->right = delete_bst(root->right, value);
	} else {
		if (root->left == NULL && root->right == NULL) {
		free(root);
		return NULL;
		} else if (root->left == NULL) {
			Node* temp = root->right;
			free(root);
			return temp;
		} else if (root->right == NULL) {
			Node* temp = root->left;
			free(root);
			return temp;
		} else {
			Node* temp = find_min(root->right);
			root->data = temp->data;
			root->right = delete_bst(root->right, temp->data);
		}
	}
	return root;
}
```

1. Se a árvore está vazia, retorna `NULL`.
2. Busca o nó:
	- Se o valor é menor, vai para a esquerda.
	- Se for maior, vai para a direita.

3. Quando o valor é encontra, há **3 casos possíveis**:
	- **Caso 1:** nó **sem filhos** → libera com `free()` e retorna `NULL`.
	![[05adca6027a013195d7e92d4ab0c3d6d4a41886a.gif]]
	- **Caso 2:** nó com **um filho** → substitui o nó pelo filho e libera o nó atual.
	![[8576debd517d1741cde6db150b00f34cc21465cc.gif]]
	- **Caso 3:** nó com **dois filhos**:
		- Encontra o menor valor na subárvore direita (`find_min()`),
		- Copia o valor para o nó atual,
		- Remove o nó duplicado na subárvore direita.	
	![[96256aca74f4070eea31cad71c2e3e70534ba7aa.gif]]
	- **Caso 4:** nó com dois filhos e sucessor não é filho direto direito:
		- Encontrar o sucessor percorrendo os nós à esquerda até o último possível,
		- Ajusta o ponteiro do pai sucesso, se o sucessor **não for o filho direto direito,** o seu pai ainda aponta para ele pela esquerda.
		- Atualizar o ponteiro do pai do nó removido, se houver um ponteiro pai, ele deve passar a apontar para o sucesso do nó removido.
	![[845e2d066fa05c6fbc07ec801e0aade5e620b3a6.gif]]

O algoritmo garante que a propriedade da BST continue válida após remoção.

#### 8. Travessias da árvore

```C
void inorder(Node* root) {
	if (root == NULL) return;
	inorder(root->left);
	printf("%d ", root->data);
	inorder(root->right);
}
```

O *in-order* percorre: **esquerda → raiz → direita**.
- Isso significa que em uma BST ele imprime os valores **em ordem crescente**.
- Ao percorrer *in-order* a árvore de busca binária, estamos visitando os nós de maneira ordenada do menor para o maior valor.

![[50380e82dfe5c8481e3945e55251de5816a20081.gif]]

```c
void preorder(Node* root) {
	if (root == NULL) return;
	printf("%d ", root->data);
	preorder(root->left);
	preorder(root->right);
}
```

- *Pre-order*: **raiz → esquerda → direita** (útil para salvar estrutura da árvore).
- *Pre-Order* percorre dando prioridade para os nós pai antes dos filhos.
- Quando percorremos a árvore de busca binária na ordem de precedência, temos então que os pais são impressos / retornados antes de seus filhos.

![[0f3e29aef6658f0c98dfeab1cdad75e990162226.gif]]

```c
void postorder(Node* root) {
	if (root == NULL) return;
	postorder(root->left);
	postorder(root->right);
	printf("%d ", root->data);
}
```

- *Post-order*: **esquerda → direita → raiz** (útil para liberar memória ou calcular altura).
- E o *Post-order* sempre dá preferência para os filhos antes do pai.
- A forma *post-order* percorre a árvore de busca binária visitando / retornando as folhas em cada nível de profundidade da árvore para somente depois retornar os pais. Essa é uma operação muito utilizada para balancear a árvore binária.

![[5b1920750c027b8ade7a2697343532d6007e70a6.gif]]

#### 8. Liberar toda a árvore da Memória

```c
void free_tree(Node* root) {
	if (!root) return;
	free_tree(root->left);
	free_tree(root->right);
	free(root);
}
```

- Usa a **recursão pós-ordem** *(post-order)*: libera primeiro os filhos, depois o pai.
- Isso evita acessos a ponteiros já liberados.
- Limpa toda a memória alocada da árvore evitando vazamentos.

#### 9. Função principal (`main`)

```c
int main() {
	Node* root = NULL;
	int values[] = {50, 30, 70, 20, 40, 60, 80};
	int n = sizeof(values)/sizeof(values[0]);
	
	for (int i = 0; i < n; i++) root = insert_bst(root, values[i]);
	
	printf("In-order (ordernado): "); inorder(root); printf("\n");
	printf("Pre-order: "); preorder(root); printf("\n");
	printf("Post-order: "); postorder(root); printf("\n");
	
	printf("Removendo 70...\n");
	root = delete_bst(root, 70);
	printf("In-order apos remocao: "); inorder(root); printf("\n");
	
	int key = 60;
	Node* found = search_bst(root, key);
	if (found) printf("Encontrado: %d\n", found->data);
	else printf("Nao encontrado: %d\n", key);
	
	free_tree(root);
	return 0;
}
```

- Cria a raiz `root = NULL` (árvore vazia).
- Insere vários valores no vetor `values` na ordem indicada.
- Exibe as travessias da árvore (*in-order*, *pre-order* e *post-order*).
- Remove o valor `70` e mostra a árvore atualizada.
- Busca o valor `60` e informa se foi encontrado.
- Ao final, libera toda a árvore com `free_tree()`.
- O `main` demonstra todas as funções funcionando juntas.

---
# Conclusão

O código da árvore binária dinâmica (BST) em C mostra conceitos essenciais de **estruturas de dados com ponteiros**:

- Manipulação de memória dinâmica (`malloc`, `free`);
- Recursão para inserir, buscar e percorrer;
- Manutenção da propriedade de ordenação da BST.

Compreender cada parte é fundamental para estudar estruturas mais avançadas como **AVL**, **Red-Black Trees** e **Heaps**.

---
# Dicas de uso, complexidade e boas práticas

- **Complexidade (BST básico):** operações de busca/inserção/removal têm tempo O(h) onde h é altura da árvore. No pior caso (árvore degenerada) h = n e custo é O(n). Em média, se a árvore estiver balanceada, h = O(log n).
- **Balanceamento:** para garantir h = O(log n) precisamos de árvores balanceadas (AVL, Red-Black, B-trees para armazenamento em disco). Essas implementações exigem rotações e regras adicionais.
- **Memória:** alocação dinâmica requer `free` correto para evitar vazamentos.
- **Recursão:** travessias e muitas operações são naturalmente recursivas; cuidado com profundidade de recursão em árvores muito profundas (stack overflow). Para evitar isso, use versões iterativas ou balanceie a árvore.
- **Dados genéricos:** se quiser armazenar tipos genéricos em C, use `void*` e funções de comparação.

---
# Referências

[Tipos Abstratos de Dados - Árvore de Busca Binária (Binary Search Tree)](https://blog.pantuza.com/artigos/tipos-abstratos-de-dados-arvore-de-busca-binaria-binary-search-tree)

