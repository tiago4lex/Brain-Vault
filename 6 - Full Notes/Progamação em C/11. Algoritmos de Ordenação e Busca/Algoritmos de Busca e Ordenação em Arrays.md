2025-09-05 23:16

Status: #developed #C 

Tags: [[Programação em C]] | [[Arrays]]

----
# Introdução

## Estrutura base (print e exemplo)

Em todos os exemplos será usado a mesma função auxiliar para imprimir o array.

```c
#include <stdio.h>

void printArray(int *V, int N) {
	for(int i = 0; i < N; i++) {
	printf("%d ", V[i])
	}
	printf("\n\n");
}
```

E como array de exemplo será usado:

```c
int vetor[] = {64, 34, 25, 12, 22, 11, 90};
int N = sizeof(vetor) / sizeof(vetor[0]); // N == 7;
```

---
# Buscas

## Busca linear (sequencial)

Procura elemento `x` anda do início ao fim.

![[Pasted image 20250905232415.png]]

**Exemplo:**

```c
int buscaLinear(int *V, int N, int x) {
	for(int i = 0; i < N; i++)
		if (V[i] == x) return i; // retorna índice da primeira ocorrência
	return -1; // não encontrado
}
```

- Complexidade: **O(n)**
- Uso: arrays não ordenadas ou quando N é pequeno.

## Busca binária (em array ordenado)

Procura `x` dividindo o intervalo pela metade (requer array ordenado).

![[Pasted image 20250905233046.png]]

**Exemplo:**

```c
int buscaBinaria(int *V, int N, int x) {
	int l = 0, r = N - 1;
	while (l <= r) {
		int m = l + (r - l) / 2;
		if (V[m] == x) return m;
		else if (V[m] < x) l = m + 1;
		else r = m - 1;
	}
	return -1;
}
```

**Variáveis:**

- `int x` → valor a ser encontrado.
- `int l = 0;` → representa o **índice da esquerda** (início do array, *left*).
- `int r = N - 1;` → representa o **índice da direita** (fim da array, *right*)
- `int m;` → representa o **índice do meio** entre `l` e `r`.

>[!note] Nota
>Para definir o índice da direita `int r` é feito o cálculo `N - 1` pelo fato de que o **array começa no índice zero**.
>
>No nosso exemplo, o vetor tem 7 elementos, logo `N = 7`, mas os índices válidos são de `0` até `6`. Então quando é feito `N - 1` o código está calculando `7 - 1` definindo assim o índice final como `6`.


- Complexidade: **O(log n).**
- Uso: quando array já está ordenado e queremos buscas rápidas.

---
# Ordenação: exemplos e explicações

## Bubble Sort
  
É um algoritmo de ordenação simples que compara elementos adjacentes e os troca de posição se estiverem fora de ordem.

A cada passagem pelo array, o maior elemento “sobe” para o final, como uma bolha em um copo de água (daí o nome _bubble_). Esse processo é repetido até que não seja mais necessário fazer trocas, o que significa que o array está ordenado. É fácil de entender, mas pouco eficiente para grandes quantidades de dados.

### Exemplo

```c
void bubbleSort(int *V, int N) {
    int i, continua, aux, fim = N;
    do {
        continua = 0;                 // assume que não houve trocas
        for (i = 0; i < fim - 1; i++) {
            if (V[i] > V[i + 1]) {
                // Faz a troca entre V[i] e V[i+1]
                aux = V[i];
                V[i] = V[i + 1];
                V[i + 1] = aux;
                
                continua = i;        // marca última posição onde houve troca
            }
        }
        fim--;                        // último elemento já está no lugar
    } while (continua != 0);         // repete enquanto houver trocas
}
```

#### Explicação

-  `fim = N`: indica até onde o `for` interno precisa comparar (na primeira passagem é todo o array).
- `do {...} while (continua !=0;` garante pelo menos uma passagem e só para se **nenhuma troca ocorrer** (array já está ordenado).
- No `for`, comparamos `V[i]` e `V[i+1]` e trocamos se estão fora de ordem, atribuímos `continua = i` para saber que houve troca.
- Após cada passagem completa, fazemos `fim--`, porque o maior elemento daquela passagem foi "borbulhado" até o final (já está no lugar).
- Se durante uma passagem nenhuma troca ocorreu (`continua` permanece 0), terminando antes de fazer todas as iterações possíveis.

### Exemplo visual passo a passo usando `{23, 4, 67, -8, 21}`

#### Passo 1 (`fim = 5`): compara os pares e troca quando necessário

![[Pasted image 20250906000404.png]]

- `fim--` (agora `fim = 4`). O maior (`67`) está no final.

#### Passo 2 (`fim = 4`)

![[Pasted image 20250906001135.png]]

- `fim--` (agora `fim = 3`)

#### Passo 3 (`fim = 3`)

![[Pasted image 20250906001415.png]]

- `fim--` (agora `fim = 2`)

#### Passo 4 (`fim = 4`)

![[Pasted image 20250906001621.png]]

### Complexidade

- Pior/ médio: **O(n²)**, Melhor (optimizado, já ordenado): **O(n)**.
- Espaço: **O(1)** (in-place).
- Estável: sim (mantém ordem relativa de elementos iguais).

---
## Selection Sort

É um algoritmo que seleciona repetidamente o menor (ou maior) elemento da parte não ordenada e o coloca na posição correta.

Ele divide o array em duas partes: a ordenada e a não ordenada. A cada iteração, encontra o menor elemento da parte não ordenada e o coloca no final da parte ordenada. Esse processo continua até que todo o array esteja organizado. É simples de implementar, mas também não é muito eficiente em grandes listas.

`selectionSort` trabalha em **passos**. Em cada passo `i`:

1. Assume que o menor elemento da parte não-ordenada está em `menor = i`.
2. Varre **toda** a parte não-ordenada (índices `j = i+1 .. N-1`) procurando um valor menor.
3. Se achar um valor menor, atualiza `menor = j`.
4. Ao final do scan, troca `V[i]` com `V[menor]`.  
    Resultado: o elemento correto para a posição `i` fica no lugar.
5. Repete com `i+1`.

**Invariante**: Após a iteração `i`, os primeiros `i+1` elementos (`V[0..i]`) já estão ordenados e são os menores do vetor.

### Exemplo

```c
void selectionSort(int *V, int N){
    int i, j, menor, troca;

    // percorre todas as posições do vetor (menos a última)
    for(i = 0; i < N-1; i++){
        menor = i;  // assume que o menor valor está na posição i

        // procura o menor valor na parte não ordenada
        for(j = i+1; j < N; j++){
            if(V[j] < V[menor])
                menor = j; // atualiza a posição do menor valor
        }

        // se encontrou um menor valor em posição diferente, troca
        if(i != menor){
            troca = V[i];
            V[i] = V[menor];
            V[menor] = troca;
        }
    }
}

```

### Variáveis

- `i` → controla a posição atual do vetor que será preenchida com menor valor.
- `j` → percorre o restante do vetor para procurar o menor valor.
- `menor` → guarda o índice do menor valor encontrado.
- `troca` → variável auxiliar usada para fazer a troca de valores.

### Laço externo (`for i = 0 até N-1`)

- Percorre o vetor da esquerda para a direita.
- Em cada iteração, a posição `i` será ocupada pelo menor elemento encontrado na parte não ordenada.

### Laço interno (`for j = i+ até N`)

- Compara todos os elementos à frente de `i`.
- Atualiza `menor` se encontrar um valor mais baixo.

### Troca (`if(i !=menor)`)

- Se o menor valor não está na posição `i`, faz a troca.
- Colocar o menor valor encontrado em `V[i]`

### Exemplo visual passo a passo

#### Passo 1: Procurando o vetor

![[Pasted image 20250906091720.png]]

- `j` percorreu todo o vetor e encontrou o menor valor `-8` e troco com `i` que estava no primeiro índice.

- Após passar para o próximo índice (`i++`) o algoritmo percebeu que nenhuma posição á frente do índice `i=1` era menor que o valor `4` então ele manteve o valor.

#### Passo 2

![[Pasted image 20250906092218.png]]

- Quando no índice `i=2`, o algoritmo percorreu todo e vetor encontrou o menor valor no quarto índice e fez a troca.
- Depois de passar para o índice `i=3` o algoritmo manteve as posições, por que o valor da último posição disponível era maior que o valor do índice `i`.

### Complexidade

- Pior/médio/melhor: **O(n²)** (não melhora em arrays quase ordenados).
- Espaço: **O(1)**.
- Estável: **não é estável por padrão** (pode quebrar ordem relativa iguais).

Quando usar: simples de implementar, útil quando as trocas custam muito (pois faz exatamente N swaps) — mas em geral outros algoritmos são melhores.

---
## Insertion Sort

É um algoritmo de ordenação que constrói a lista ordenada gradualmente, inserindo cada novo elemento na posição correta da parte já ordenada.

Funciona de forma parecida com o jeito que organizamos cartas na mão em um jogo: começamos com uma carta (já ordenada), pegamos a próxima e colocamos na posição certa em relação às anteriores, e assim por diante. É eficiente para pequenas quantidades de dados ou listas que já estão quase ordenadas.

### Exemplo

```c
void insertionSort(int *V, int N){
    int i, j, aux;

    // percorre o vetor a partir da segunda posição
    for(i = 1; i < N; i++){
        aux = V[i];  // elemento atual que será inserido
        j = i;

        // desloca os elementos maiores que aux para a direita
        while(j > 0 && aux < V[j - 1]){
            V[j] = V[j - 1];
            j--;
        }

        // insere o elemento na posição correta
        V[j] = aux;
    }
}
```

### Variáveis

- `i` → percorre o vetor do segundo elemento em diante.
- `j` → percorre a parte já ordenada para encontrar a posição correta.
- `aux` → armazena temporariamente o valor atual que será inserido.

### Laço externo (`for i = 1 até N-1`)

- Cada iteração considera o elemento `V[i]` como novo item a ser inserido na parte ordenada (que vai de `0` até `i-1`).

### Guarda o valor (`aux = V[i]`)

- O valor de `V[i]` é guardado em `aux` porque o conteúdo dessa posição pode ser sobrescrito durante os deslocamentos.

### Laço interno (`while j > 0 && aux < V[j-1]`)

- Enquanto `aux` for menor que o elemento anterior `V[j-1]`, os elementos são deslocados uma posição para a direita (`V[j] = V[j-1]`).
- Isso abre espaço para inserir `aux` no lugar correto.

### Inserção (`V[j] = aux`)

- Quando o laço termina, significa que `j` é a posição correta.
- Então o valor de `aux` é colocado em `V[j]`.

### Exemplo visual passo a passo

#### Passo 1

![[Pasted image 20250906102442.png]]

- `i` começa da posição 1 logo seu valor é do `aux` é `4`.
- `4` < `23` → desloca o `23`
- insere `4` na primeira posição.
- depois o algoritmo compara se o valor à esquerda do índice `i=2` é maior que o valor do índice anterior (`64` > `23`), como o valor de `i=2` é maior ele mantem a posição.

#### Passo 2

![[Pasted image 20250906102855.png]]

- na posição do índice `i=3` o valor é `-8`, o algoritmo compara com o valor à esquerda e vai trocando as posições até chegar no índice `0`.
- o mesmo acontece quando o algoritmo está na posição do índice `i=4` até chegar em na posição onde o valor `21` deixa de ser menor que o valor à esquerda (`4 > 23`)

### Complexidade

- Melhor: **O(n)** (se já ordenado); Médio/pior: **O(n²)**.
- Estável: sim.
- Espaço: **O(1)**.

Quando usar: pequenos arrays, inserções dinâmicas; ótimo em arrays quase ordenados.

---
## Merge Sort

É um algoritmo de ordenação baseado na técnica de **divisão e conquista**.

Primeiro divide o array em duas metades menores. Ordena cada metade recursivamente e depois junta (_merge_) essas metades em um único array ordenado. É muito eficiente mesmo em grandes conjuntos de dados, pois sempre divide o problema em partes menores antes de resolver.

```c
void mergeSort(int *V, int inicio, int fim) {
    int meio;
    if (inicio < fim) {
        meio = floor((inicio + fim) / 2); // divide o vetor ao meio

        // ordena a primeira metade
        mergeSort(V, inicio, meio);

        // ordena a segunda metade
        mergeSort(V, meio + 1, fim);

        // combina as duas metades ordenadas
        merge(V, inicio, meio, fim);
    }
}
```

### Condição de parada (`if (inicio < fim)`)

- O algoritmo só continua se o intervalo tiver **mais de um elemento**.
- Se `inicio == fim`, significa que o vetor tem apenas **um elemento**, que já está ordenado.

### Cálculo do meio (`meio = flor ((inicio + fim) / 2)`)

- Divide o vetor em duas partes:
	- Da posição `início` até `meio`.
	- Da posição `meio+1` até `fim`.

### Chamadas recursivas (`mergeSort`)

- A função se chama novamente para ordenar a primeira metade.
- Depois, chama novamente para ordenar a segunda metade.

### Explicação passo a passo

![[Pasted image 20250906161842.png]]

- Primeiro divide o vetor em duas partes: `{23, 4, 67, -8}` e `{90, 54, 21}`
- Depois divide novamente os dois vetores `{23, 4}`, `{67, -8}`, `{90, 54}` e `{21}`

### Complexidade

- Pior/médio/melhor: **O(n log n)**.
- Espaço: **O(n)** (uso de arrays temporários).
- Estável: sim (se implementado com `<=` na comparação como aqui).

Quando usar: arrays grandes, quando estabilidade e complexidade garantida são importantes.

---
## Combinação (`merge`)

- Quando ambas as metades estão ordenadas, a função `merge()` é chamada para **juntar** as duas partes em ordem crescente.
- É nessa etapa que acontece a ordenação "de fato", comparando elementos das duas sublistas e colocando-os em ordem no vetor original.

```c
// Função que combina duas partes ordenadas do vetor
void merge(int *V, int inicio, int meio, int fim) {
    int i, j, k;
    int n1 = meio - inicio + 1;  // tamanho da primeira metade
    int n2 = fim - meio;         // tamanho da segunda metade

    // Vetores temporários
    int *L = (int *)malloc(n1 * sizeof(int));
    int *R = (int *)malloc(n2 * sizeof(int));

    // Copia os elementos para os vetores auxiliares
    for (i = 0; i < n1; i++)
        L[i] = V[inicio + i];
    for (j = 0; j < n2; j++)
        R[j] = V[meio + 1 + j];

    // Intercala os vetores L e R de volta em V
    i = 0; 
    j = 0; 
    k = inicio;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            V[k] = L[i];
            i++;
        } else {
            V[k] = R[j];
            j++;
        }
        k++;
    }

    // Copia o que sobrou do vetor L (se houver)
    while (i < n1) {
        V[k] = L[i];
        i++;
        k++;
    }

    // Copia o que sobrou do vetor R (se houver)
    while (j < n2) {
        V[k] = R[j];
        j++;
        k++;
    }

    // Libera memória auxiliar
    free(L);
    free(R);
}
```

### Explicação da combinação `merge`

1. **Separação em vetores auxiliares**
	- O vetor principal `V` está dividido em duas partes já ordenadas:
		- `V[inicio ... meio]`
		- `V[meio+1 ... fim]`
	- Criamos dois vetores temporários (`L` e `R`) para armazenar essas partes.

2. **Intercalação ordenada**
	- Usamos três índices:
		- `i` percorre o vetor `L`.
		- `j` percorre o vetor `R`.
		- `k` percorre o vetor `V` original (onde a fusão acontece).
	- Comparamos `L[i]` e `R[j]`:
		- O menor vai para `V[k]`.
		- Avançamos no vetor de onde tiramos o elemento.

3. **Tratamento dos elementos restantes**
	- Se um vetor acabar primeiro (por exemplo, `L` termina e `R` ainda tem valores):
		- Copiamos todos os elementos restantes do outro vetor para `V`.

4. **Memória dinâmica**
	- Como  não sabemos o tamanho fixo de `L` e `R`, usamos `malloc` para criar vetores temporários.
	- Ao final, liberamos com `free()` para evitar vazamento de memória.

### Explicação

#### Passo 1

![[Pasted image 20250906162526.png]]

- Após separar todos os elementos, o algoritmo compara qual o maior e o menor e os junta novamente.
- `23 > 4` e `67 > 8` e combina para os vetores  `{4, 23}` e `{-8, 67}`

#### Passo 2

- O algoritmo continua comparando os elementos e trocando os calores maiores e menores até ficar ordenado.

---
# Tabela resumida (complexidade / estabilidade / espaço)

| Algoritmo     | Melhor     | Médio      | Pior       | Estável? | Espaço |
| ------------- | ---------- | ---------- | ---------- | -------- | ------ |
| Bubble (otim) | O(n)       | O(n²)      | O(n²)      | Sim      | O(1)   |
| Selection     | O(n²)      | O(n²)      | O(n²)      | Não      | O(1)   |
| Insertion     | O(n)       | O(n²)      | O(n²)      | Sim      | O(1)   |
| Merge         | O(n log n) | O(n log n) | O(n log n) | Sim      | O(n)   |

---
# Recomendações práticas

- Se N é pequeno (ou quase ordenado) → `insertion sort` é ótimo.
- Se precisa garantir **O(n log n)** e tem espaço → `merge sort`.
- Se que **implementação simples e trocas limitadas** → `selection sort` (mas geralmente não é o preferido).
- `bubble sort` é útil para ensino e pequenos casos; raramente usado em produção (a não ser para demonstração/diagnóstico).

---
