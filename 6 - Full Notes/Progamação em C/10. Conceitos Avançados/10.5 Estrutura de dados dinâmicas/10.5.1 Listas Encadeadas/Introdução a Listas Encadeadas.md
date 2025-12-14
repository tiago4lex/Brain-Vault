2025-08-30 10:22

Status: #developed  #C 

Tags: [[Programação em C]] | [[Ponteiros]]

----
# Entendendo ponteiros antes de listas

Criando um programa pequeno com:
- `int a = 10;`
- `int* p = &a;`
- `*p = 20;` (modifica o valor de `a` via ponteiro)
- `printf("%d\n", *p);`

```makefile
a = 10
p -> endereõ de a
*p = 20 (modifica a)
```

---
# Entendendo o `->`

O `->` é só <font color="#ffc000"><strong>uma abreviação para acessar membros de uma struct via ponteiro</strong></font>:

```c
L->it = L->it->next;
```

Se você expandir com `*` e parênteses, é igual a:

```c
(*L).it = (*L).it->next;  // L->it = L->it->next
(*L).it = (*((*L).it)).next;  // L->it->next
```

> [!tip] Dica prática:
> Desenhe o ponteiro na memória:
> 
> ```rust
> List L:
> head -> N1 -> N2 -> NULL
> tail -> N2
> it   -> N1
> 
> L->it = L->it->next
> // agora it aponta para N2
> ```

----
# Fazendo diagramas passo a passo

Sempre que escrever código com structs e ponteiros:

1. Desenhe a memória: cada nó, `head`, `tail`, `it`
2. Mostre com setas de ponteiro
3. Atualize o diagrama após cada operação (`next`, `add`, `delete`)

Isso transforma o abstrato (endereços) em visual.

---
# Escrevendo um programa de mini-lista

```c
typedef struct Node {
	int value;
	struct Node* next;
} Node;

int main() {
	Node n1 = {10, NULL};
	Node n2 = {20, NULL};
	n1.next = &n2;
	
	Node* p = &n1;
	printf("%d\n", p->value);
	p = p->next;
	printf("%d\n", p->value);
}
```

**Saída:**

```
10
20
```

## Passo a passo

### 1. Definição da `struct Node`

```c
typedef struct Node {
	int value;
	struct Node* next;
} Node;
```

- `Node` é um **tipo de struct** que representa um **nó da lista encadeada**.
- Cada nó guarda:
	- `value` → o valor inteiro que o nó armazena.
	- `next` → um ponteiro para o próximo nó. Se for o último nó, `next = NULL`.
- `typedef` permite usar `Node` ao invés de `struct Node` toda hora.

### 2. Criação de nós

```c
Node n1 = {10, NULL};
Node n2 = {20, NULL};
```

- `n1` tem valor `10` e `next = NULL` (não aponta para ninguém ainda).
- `n2` tem valor `20` e `next = NULL`.

### 3. Ligando os nós

```c
n1.next = &n2;
```

- `n1.next` agora aponta para o endereço de `n2`.
- A lista agora tem dois elementos:

```css
n1(value=10) -> n2(value=20) -> NULL
```

### 4. Usando ponteiros para percorrer a lista

```c
Node* p = &n1;
printf("%d\n", p->value);
p = p->next;
printf("%d\n", p->value);
```

- `Node* p = &n1;` → cria um ponteiro `p` que aponta para o primeiro nó (`n1`).
- `p->value` é uma **abreviação** de `(*p).value`, ou seja: pega o `value` do nó que o `p` aponta.
- `p = p->next;` → avança `p` para o próximo nó (`n2`).
- Imprime o valor do segundo nó: `20`.

Visualização

```css
p -> n1(value=10) -> n2(value=20) -> NULL
```

Depois de `p = p->next`:

```css
p -> n2(value=20) -> NULL
```

---
# Usando o modo Debug no VS Code

Use um **debugger** como o do VS Code ou `gdb`:
- Coloque **breakpoints** e veja os valores de `L->it`, `L->head`, `N->next`
- Execute passo a passo (`step over`) para ver exatamente **quem aponta para quem**
- Visualizar ponteiros em tempo de execução ajuda muito a fixar a ideia de memória

### Passo a passo para depurar

1. **Abra seu código no VS Code**
    - Salve como `mini_lista.c`.

2. **Instale a extensão C/C++ da Microsoft**
    - Procure por `C/C++` no marketplace do VS Code.
    - Ela fornece suporte a debug, IntelliSense e compilação.

3. **Compile seu programa com flags de debug**
    - Abra o terminal e rode:

```bash
gcc -g mini_lista.c -o mini_lista
```

- O `-g` adiciona informações de debug.

4. **Configurar o debugger**
    - Vá em **Run and Debug** (ou Ctrl+Shift+D)
    - Clique em **create a launch.json file**
    - Escolha **C/C++: (gdb) Launch** (Linux) ou **C/C++: (Windows)** se estiver no Windows
    - Configure `"program": "${workspaceFolder}/mini_lista"`

5. **Adicionar breakpoints**
    - Clique à esquerda do número da linha no editor para adicionar um **ponto de interrupção**.
    - Exemplo: coloque em `Node* p = &n1;` e em `p = p->next;`.

6. **Iniciar depuração**
    - Clique em **Start Debugging** (F5)
    - O programa vai parar no primeiro breakpoint.

7. **Usar o painel de variáveis**
    - No lado esquerdo do VS Code, veja os valores de:
        - `n1`, `n2` → structs
        - `p` → ponteiro
    - Você pode expandir `p` e ver `value` e `next`.

8. **Avançar passo a passo**
    - **Step Over (F10)** → executa a próxima linha, útil para ver mudanças sem entrar em funções.
    - **Step Into (F11)** → entra dentro de funções.
    - **Step Out (Shift+F11)** → sai da função.

9. **Visualizar ponteiros**
    - Por exemplo, após `p = p->next;`:
        - `p` aponta para `n2`
        - `p->value = 20`
        - `p->next = NULL`