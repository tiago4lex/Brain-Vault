2025-08-30 08:27

Status: #developed #C 

Tags: [[Programação em C]] | [[C]]

----
# Introdução

## O que é uma lista encadeada?

Uma **lista encadeada *(singly linked list)*** é uma estrutura de dados formada por **nós**.

Cada nó guarda:
- um **valor** (o dados em si).
- um **ponteiro para o próximo nó**.

A lista mantém referências para:
- o **início** (cabeça, `head`).
- opcionalmente o **fim** (cauda, `tail`, útil para inserir rápido no final).
- (opcional) um **iterador** interno para percorrer com "próximo" (`next`).

![[Pasted image 20250830082814.png]]

### Por que usar?

- Tamanho **dinâmico** (cresce/diminui em tempo de execução).
- Inserções/remoções no começo **O(1)**.
- Inserções/remoções em posições arbitrárias **O(n)** (precisa caminhar).

### Quando evitar?

- Quando é necessário o **acesso aleatório rápido** (um array é melhor).
- Quando quer **alta localidade de cache** (arrays tendem a ser melhores).

---
# Anatomia de um nó e da lista

```c
typedef struct Node {
	int value;
	struct Node* next;
} Node;

typedef struct List {
	Node* head;  // Primeiro nó
	Node* tail;  // Último nó (para add em O(1))
	Node* it;    // Iterador interno para "next"
	size_t size; // Quantidade de nós
} List;
```

---
# Operações essenciais

- *add(valor)*: adiciona no **final** (usa `tail`, O(1)).
- *insert(pos, valor)*: insere no **índice** (0..size).
	- Casos especiais: início (0) e fim (size).
- *delete(valor)*: remove a **primeira ocorrência** do valor (O(n)).
- *next()*: percorre a lista usando um **iterador interno**.
	- (primeiro `next`) vai para o `head`; subsequentes vão avançado)
- *last()*: retorna/mostra o **último nó** (vai `tail`, O(1)).
- *info()*: mostra **tamanho**, cabeça, cauda e posição do iterador.
- *reset()*: resta o iterador para começar do início no próximo `next`.
- *clear()*: libera todos os nós (evita vazamento da memória).

---
# Complexidade *(singly)*

- add no final (com `tail`): **O(1)**
- insert no início: **O(1)**
- insert no meio/fim (índice): **O(n)**
- delete (por valor): **O(n)**
- next / last / info / print: **O(1)** (exceto `print`, que é O(n) por percorrer)

---
# Programa completo (interativo)

- Comandos suportados:
	- `add X` → adiciona X no final
	- `insert POS X` → insere X na posição POS (0-based)
	- `delete X` → remove a **primeira ocorrência** de X
	- `next` → avança o iterador e mostra o valor atual
	- `reset` → reseta o iterador (próximo `next` volta ao início)
	- `last` → mostra o último valor
	- `info` → mostra tamanho, head, tail e estado do iterador
	- `print` → imprime a lista
	- `clear` → apaga toda a lista
	- `help` → mostra ajuda
	- `quit` → sai

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

typedef struct Node {
    int value;
    struct Node* next;
} Node;

typedef struct List {
    Node* head;
    Node* tail;
    Node* it;    // iterador interno para "next"
    size_t size;
} List;

/* ---------- API da lista ---------- */
void  list_init(List* L);
void  list_clear(List* L);
bool  list_add(List* L, int value);                      // push back
bool  list_insert(List* L, size_t index, int value);     // insere em [0..size]
bool  list_delete_value(List* L, int value);             // remove 1a ocorrência
Node* list_last(const List* L);                          // acesso à cauda
Node* list_iter_next(List* L);                           // avanço do iterador
void  list_iter_reset(List* L);
void  list_print(const List* L);
void  list_info(const List* L);

/* ---------- Implementação ---------- */
void list_init(List* L) {
    L->head = L->tail = L->it = NULL;
    L->size = 0;
}

void list_clear(List* L) {
    Node* cur = L->head;
    while (cur) {
        Node* nxt = cur->next;
        free(cur);
        cur = nxt;
    }
    L->head = L->tail = L->it = NULL;
    L->size = 0;
}

static Node* make_node(int value) {
    Node* n = (Node*)malloc(sizeof(Node));
    if (!n) return NULL;
    n->value = value;
    n->next  = NULL;
    return n;
}

bool list_add(List* L, int value) {
    Node* n = make_node(value);
    if (!n) return false;

    if (L->size == 0) {
        L->head = L->tail = n;
    } else {
        L->tail->next = n;
        L->tail = n;
    }
    L->size++;
    return true;
}

bool list_insert(List* L, size_t index, int value) {
    if (index > L->size) return false; // fora do intervalo
    // inserir no início
    if (index == 0) {
        Node* n = make_node(value);
        if (!n) return false;
        n->next = L->head;
        L->head = n;
        if (L->size == 0) L->tail = n;
        L->size++;
        return true;
    }
    // inserir no final (equivalente a add)
    if (index == L->size) {
        return list_add(L, value);
    }
    // inserir no meio: achar (index-1)
    Node* prev = L->head;
    for (size_t i = 0; i < index - 1; i++) {
        prev = prev->next;
    }
    Node* n = make_node(value);
    if (!n) return false;
    n->next = prev->next;
    prev->next = n;
    L->size++;
    return true;
}

bool list_delete_value(List* L, int value) {
    if (L->size == 0) return false;

    Node* prev = NULL;
    Node* cur  = L->head;

    while (cur) {
        if (cur->value == value) {
            // ajustar iterador se apontava para o nó removido
            if (L->it == cur) {
                L->it = prev; // volta para o anterior (ou NULL se removendo head)
            }
            if (prev == NULL) {
                // removendo primeira posição
                L->head = cur->next;
                if (L->tail == cur) L->tail = cur->next; // lista tinha 1 nó
            } else {
                prev->next = cur->next;
                if (L->tail == cur) L->tail = prev;
            }
            free(cur);
            L->size--;
            if (L->size == 0) {
                L->head = L->tail = L->it = NULL;
            }
            return true;
        }
        prev = cur;
        cur  = cur->next;
    }
    return false; // não achou
}

Node* list_last(const List* L) {
    return L->tail;
}

void list_iter_reset(List* L) {
    L->it = NULL; // próximo next começa do head
}

Node* list_iter_next(List* L) {
    if (L->size == 0) return NULL;
    if (L->it == NULL) {
        L->it = L->head;
    } else {
        L->it = L->it->next;
    }
    return L->it;
}

void list_print(const List* L) {
    printf("[size=%zu] ", L->size);
    Node* cur = L->head;
    while (cur) {
        printf("%d -> ", cur->value);
        cur = cur->next;
    }
    printf("NULL\n");
}

void list_info(const List* L) {
    printf("---- info ----\n");
    printf("size : %zu\n", L->size);
    if (L->head) printf("head : %d\n", L->head->value);
    else         printf("head : (null)\n");
    if (L->tail) printf("tail : %d\n", L->tail->value);
    else         printf("tail : (null)\n");
    if (L->it)   printf("iter : %d (proximo next avanca)\n", L->it->value);
    else         printf("iter : (none) (proximo next vai ao head)\n");
    printf("-------------\n");
}

/* ---------- Interface de linha de comando ---------- */
static void help(void) {
    puts("Comandos:");
    puts("  add X            - adiciona X no final");
    puts("  insert POS X     - insere X na posicao POS (0..size)");
    puts("  delete X         - remove a primeira ocorrencia de X");
    puts("  next             - avanca o iterador e mostra o valor atual");
    puts("  reset            - reseta o iterador (proximo next vai ao head)");
    puts("  last             - mostra o ultimo valor");
    puts("  info             - mostra tamanho/head/tail/iterador");
    puts("  print            - imprime a lista completa");
    puts("  clear            - remove todos os elementos");
    puts("  help             - mostra esta ajuda");
    puts("  quit             - sai");
}

int main(void) {
    List L;
    list_init(&L);

    puts("Lista Encadeada (interativa). Digite 'help' para comandos.");

    char line[256];
    help();

    while (1) {
        printf("> ");
        if (!fgets(line, sizeof(line), stdin)) break;

        // remover \n
        line[strcspn(line, "\n")] = '\0';

        if (strncmp(line, "quit", 4) == 0) {
            break;
        } else if (strncmp(line, "help", 4) == 0) {
            help();
        } else if (strncmp(line, "print", 5) == 0) {
            list_print(&L);
        } else if (strncmp(line, "info", 4) == 0) {
            list_info(&L);
        } else if (strncmp(line, "clear", 5) == 0) {
            list_clear(&L);
            puts("lista limpa.");
        } else if (strncmp(line, "reset", 5) == 0) {
            list_iter_reset(&L);
            puts("iterador resetado.");
        } else if (strncmp(line, "last", 4) == 0) {
            Node* t = list_last(&L);
            if (t) printf("last = %d\n", t->value);
            else   printf("(lista vazia)\n");
        } else if (strncmp(line, "next", 4) == 0) {
            Node* n = list_iter_next(&L);
            if (n)  printf("iter = %d\n", n->value);
            else    printf("(lista vazia ou fim alcancado)\n");
        } else {
            int x; size_t pos;
            if (sscanf(line, "add %d", &x) == 1) {
                if (!list_add(&L, x)) puts("erro: malloc falhou.");
            } else if (sscanf(line, "insert %zu %d", &pos, &x) == 2) {
                if (!list_insert(&L, pos, x)) puts("erro: posicao invalida ou malloc falhou.");
            } else if (sscanf(line, "delete %d", &x) == 1) {
                if (!list_delete_value(&L, x)) puts("valor nao encontrado.");
            } else {
                puts("comando invalido. digite 'help'.");
            }
        }
    }

    list_clear(&L);
    return 0;
}
```

## Explicação

### 1. Cabeçalho e tipos

```c
#include <stdio.h>   // entrada/saída (printf, fgets, sscanf)
#include <stdlib.h>  // malloc, free, NULL
#include <string.h>  // strncmp, strcspn
#include <stdbool.h> // bool, true, false
```

- `stdio.h`: para imprimir, ler e usar `fgets`.
- `stdlib.h`: para `malloc`/`free` (alocação e liberação de memória).
- `string.h`: para comparar e manipular strings.
- `stdbool.h`: para usar `bool` (legível e claro).

**Tipos principais:**

```c
typedef struct Node {
	int value;
	struct Node* next;
} Node;

typedef struct List {
	Node* head;
	Node* tail;
	Node* int;   // iterador interno
	size_t size;
} List;
```

- `Node` representa **um nó da lista**: tem um `value` (dado) e `next` (ponteiro para o próximo nó).
- `List` contém ponteiros que apontam para:
	- `head` - primeiro nó;
	- `tail` - último nó (útil para anexar rápido no fim);
	- `it` - **iterador interno** usado pela função `next`;
	- `size` - quanto nós existem (facilita operações e verificações).

### 2. Inicialização e limpeza da lista

#### `list_init(List* L)`

```c
L->head = L->tail = L->it = NULL;
L->size = 0;
```

- Coloca a lista em estado **vazia**: sem nós, iterador inválido e tamanho zero.

#### `list_clear(List* L)`

Percorre todos os nós a partir de `head`, chama `free` em cada nó e depois reseta `head/tail/it/size`.

- Por que `free`? Por que nós foram criados em `malloc` - se não liberarmos, o programa "vaza" memória *(memory leak)*.
- O loop: pega `cur = L->head`, guarda `nxt = cur->next`, `free(cur)`, `cur = nxt` e continua até `cur == NULL`.

### 3. Criação do nó (fábrica interna)

#### `static Node* make_node(int value)`

```c
Node* n = (Node*) malloc(sizeof(Node));
if (!n) return NULL;
n->value = value;
n->next = NULL;
return n;
```

- Tenta alocar memória para um `Node`.
- Retorna o ponteiro para esse nó ou `NULL` se a alocação falhar.
- Inicializa `next` com `NULL` porque o nó ainda não aponta para ninguém.

>[!note] Nota:
>O cast `(Node*)` é opcional em C puro; alguns programadores omite. Está ok.

### 4. Adicionar no fim - `list_add`

Fluxo:
1. `Node* n = make_node(value);` → cria nó.
2. Se `L->size == 0` (lista vazia): `L->head = L->tail = n;`
3. Senão: liga `L->tail->next = n;` e atualiza `L->tail = n;`
4. `L->size++`.

Por que funciona em O(1)?
- Porque guardamos `tail`. Sem `tail`, teríamos que percorrer toda a lista para achar o fim (O(n)).

Exemplo:
- Lista vazia: `add(10)` → head->10->NULL, tail aponta para mesmo nó, size=1.
- `add(20)` → tail->next aponta para novo vó 20; tail atualiza; size=2.

### 5. Inserir em posição - `list_inser(List* L, size_t index, int value)`

Casos tratados:
- `index > L->size` → inválido (não permite "buracos").
- `index == 0` → inserir no início:
	- cria nó `n`, `n->next = L->head`, `L->head = n`.
	- se lista era vazia, também `L->tail = n`.
- `index == L->size` → inserir no final → chama `list_add`.
- inserir no meio:
	- anda `index-1` passos para char `prev` (o nó anterior à posição desejada).
	- cria `n`, faz `n->next = prev->next`, `prev->next = n`.

Detalhe importante: percorrer até `index-1` é feito com um `for`. Isso é O(index) - no pior caso O(n).

### 6. Remover por valor — `list_delete_value(List* L, int value)`

Fluxo:

1. Se `L->size == 0` retorna `false` (lista vazia).
2. Usa `prev = NULL` e `cur = L->head` para localizar o primeiro nó cujo `cur->value == value`.
3. Se achar:
    - **Ajusta o iterador (`L->it`)**: se `L->it == cur`, então `L->it = prev;`.
        - Por quê? Se o iterador apontava para o nó removido, colocamos o iterador de volta no anterior para que `next()` funcione coerentemente: próximo `next()` irá mover `it` para `prev->next` (o nó que veio depois do removido).
        - Se `prev == NULL` (remoção da cabeça), então `L->it = NULL` — assim o próximo `next()` volta a apontar para `head`.
    - Se `prev == NULL` (removendo a cabeça): `L->head = cur->next`.
        - Se `cur` também era `tail` (lista tinha 1 nó), então `L->tail = cur->next` (será NULL).
    - Senão (remoção no meio/fim): `prev->next = cur->next`, e se `cur` era `tail` atualiza `L->tail = prev`.
    - `free(cur); L->size--;`
    - Se `L->size == 0` após remoção: reseta `head`, `tail`, `it` para `NULL`.
4. Retorna `true` se removeu, `false` se não encontrou.

Pontos chave:

- Atualizar `tail` quando remove o último nó.
- Ajuste do iterador para não ficar "apontando para um nó liberado" (dangling pointer).


### 7. Função do iterador (next/reset)

#### `list_iter_reset(List* L)`

- Faz `L->it = NULL;` → indica que o iterador está antes do início. O próximo `list_iter_next` retornará o `head`.

#### `list_iter_next(List* L)`

```c
if (L->size == 0) return NULL;
if (L->it == NULL) L->it = L->head;
else L->it = L->it->next;
return L->it;
```

- Comportamento:
    - Se lista vazia retorna `NULL`.
    - Se `it == NULL` (iterador "no começo") → define `it = head` e retorna o primeiro nó.
    - Caso contrário, avança `it` para o próximo nó (`it = it->next`) e retorna.
    - Se `it` passar pelo último nó, `it` vira `NULL` e `next()` retorna `NULL` (indica fim).

- Isso permite percorrer a lista chamando `next` várias vezes, sem precisar gerenciar manualmente um `Node* cur` no `main`.

### 8. Funções de leitura/diagnóstico

#### `list_print(const List* L)`

- Percorre desde `head` imprimindo `value ->` até `NULL`.
- Útil para ver a sequência atual.

#### `list_info(const List* L)`

- Imprime:
    - `size`
    - valor da `head` (se existe)
    - valor da `tail` (se existe)
    - posição do iterador (`it`) — se está nulo diz que próximo `next` volta ao head.

### 9. Interface de linha de comando (o `main`)

Resumo do que `main` faz:

1. `List L; list_init(&L);` → cria a lista vazia.
2. Mostra ajuda e entra num laço de leitura de linha:

```c
while (1) {
    fgets(line, sizeof(line), stdin);    // lê comando do usuário
    line[strcspn(line, "\n")] = '\0';    // remove o '\n' do final
    // compara começo da string com comandos conhecidos:
    if (strncmp(line, "quit", 4) == 0) break;
    else if (strncmp(line, "print", 5) == 0) list_print(&L);
    // ... e assim por diante
    else { // tenta interpretar comandos que têm argumentos
        if (sscanf(line, "add %d", &x) == 1) list_add(&L, x);
        else if (sscanf(line, "insert %zu %d", &pos, &x) == 2) list_insert(&L, pos, x);
        else if (sscanf(line, "delete %d", &x) == 1) list_delete_value(&L,x);
        else puts("comando invalido. digite 'help'.");
    }
}
```

- `fgets` retorna `NULL` no EOF (Ctrl+D em Linux) ou erro — nesse caso o loop quebra.
- `strcspn(line, "\n")` encontra a posição do `\n` e coloca `\0` ali para remover a nova linha (boa prática para comparar strings).
- `strncmp` compara só os primeiros N caracteres (útil para detectar o comando mesmo que o usuário tenha espaços extras).
- `sscanf` tenta extrair inteiros/pos da string (retorna quantos itens foram extraídos com sucesso).

Depois do loop: `list_clear(&L); return 0;` — limpa memória e retorna 0 (sucesso).

### 10. Comportamento completo com exemplo prático (passo a passo)

Considere a execução dos comandos:

```perl
add 10
add 20
insert 1 15
print
next
next
next
delete 15
print
last
quit
```

Passos e estado interno:

1. `add 10`
    - cria nó N10(value=10), lista vazia → head=tail=N10, size=1.
    - memória: head->10->NULL.

2. `add 20`
    - cria N20, tail->next = N20, tail = N20, size=2.
    - agora: head->10->20->NULL.

3. `insert 1 15`
    - índice 1 é o meio: localiza prev=head (10), cria N15, N15->next = prev->next (20), prev->next = N15, size=3.
    - agora: head->10->15->20->NULL.

4. `print` → mostra `[size=3] 10 -> 15 -> 20 -> NULL`.
5. `next` #1
    - iter reset estava em NULL (início do programa), portanto `list_iter_next` define `it = head` e retorna nó 10. Imprime `iter = 10`.

6. `next` #2
    - `it` era N10 — agora `it = it->next` → N15. Retorna `15`.

7. `next` #3
    - `it` era N15 → `it = N20`. Retorna `20`.

8. `delete 15`
    - encontra N15 (prev = N10). Ajusta ponteiros: `prev->next = N15->next` (N20). Libera N15; size=2.
    - Se `it` estivesse apontando para N15, ele seria ajustado para `prev` (N10). No nosso caso, depois de ter chamado `next` 3 vezes, `it` estava em N20, então nada mudou.

9. `print` → `[size=2] 10 -> 20 -> NULL`.
10. `last` → imprime `last = 20` (valor do `tail`).
11. `quit` → sai e chama `list_clear` (libera N10 e N20) — sem memory leaks.

## 11. Erros comuns e dicas práticas (para evitar confusão)

- **Esquecer `free`**: sempre libere nós; senão o programa “vaza” memória.
- **Usar nó após `free`** (dangling pointer): nunca acesse `cur->value` depois de `free(cur)`.
- **Esquecer de atualizar `tail`** ao remover o último nó — então `tail` pode continuar apontando para memória liberada.
- **Não checar `malloc`**: `make_node` pode retornar `NULL` se memória acabar — por isso as funções retornam `false` e `main` imprime erro.
- **Iterador não ajustado**: se remover o nó que o iterador aponta, ajuste-o (como o código faz).
- **sscanf / inputs malformados**: `sscanf` retorna o número de valores lidos; sempre verifique o retorno para validar entrada.

### 12. Observações finais (boas práticas)

- Evite lançar exceções silenciosas: sempre trate retornos de `malloc`.
- Comente o código para que quem ler entenda a intenção de `it`, `tail`, etc.
- Para código de produção, considere testes unitários que exercitem insert/delete em bordas (vazio, 1 elemento, fim, meio).
- Se quiser tornar a lista genérica (aceitar `void*`), você pode, mas a complexidade aumenta (funções de destruição, cópia, comparador).

---
# Exemplo de Lista encadeada na prática

Se o usuário inserir os valores `10 → 20 → 30` na lista, a memória fica assim:

```css
[Head] → [10 | *] → [20 | *] → [30 | NULL]
```

## Explicando o diagrama

- **Head**
	- É um ponteiro especial que **guarda o endereço do primeiro nó** da lista.
	- Se a lista estiver vazia, `head = NULL`.

- **Cada nó (Node)**
	- Tem duas partes:
		- `data` → o valor armazenado (exemplo:`10`).
		- `next` → um ponteiro que guarda o endereço do próxima nó da lista.
		- Se for o último nó, `next = NULL`.

## Representação em tabela

| Endereço (fictício) | Nó       | Valor (`data`) | Ponteiro (`next`) |
| ------------------- | -------- | -------------- | ----------------- |
| 0x1000              | head     | -              | 0x2000            |
| 0x2000              | Node (1) | 10             | 0x3000            |
| 0x3000              | Node (2) | 20             | 0x4000            |
| 0x4000              | Node (3) | 30             | NULL              |

## Operações e como o diagrama muda

1. **Inserir no final *(addLast)***
	- O novo nó vai ser adicionado após o último.
	- Exemplo: adicionar `40`

```css
[Head] → [10 | *] → [20 | *] → [30 | *] → [40 | NULL]
```

2. **Remover nó *(delete)***
	- Se remover o `20`, o ponteiro do `10` passa a apontar direto para o `30`.

```css
[Head] → [10 | *] → [30 | *] → [40 | NULL]
```

3. **Navegar *(next)***
	- Quando usamos `current = current->next`, estamos "andando" para o próximo nó;
	- Assim saímos de `10` → `20` → `30` ...


---
# Pontos importantes e armadilhas

- **Sempre** verifique retorno de `malloc` (`NULL` em caso de falha).
- Atualize `head`/`tail` corretamente ao inserir/remover no início/fim.
- Ao remover um nó, **ajuste quem aponta para ele** e **libere a memória** (`free`).
- Evite usar nós após `free` (ponteiros “soltos” / _dangling_).
- Se usar iterador interno, lembre de **ajustá-lo** quando remover o nó apontado por ele.

---
# Extensões comuns (pra quando quiser evoluir)

- **Lista duplamente encadeada** (`prev` e `next`), facilita remoção no meio.
- **Lista circular** (tail->next = head), útil para buffers circulares.
- **Funções genéricas** com `void*` + _callbacks_ para comparação/impressão.
- **Testes automatizados** das operações (inserção, remoção, limites, etc.).