2025-10-02 15:25

Status: #developed #C 

Tags: [[Programação em C]] 

----
# O que é Complexidade de Algoritmos?

A **complexidade de um algoritmo** é uma medida que indica o **desempenho** do algoritmo em termos de **tempo de execução** e/ou **uso de memória**, considerando o **tamanho da entrada.**

Em outras palavras, ela nos ajuda a responder perguntas como:

- *"Este algoritmo é rápido o suficiente para entradas muito grandes?"*
- *"Quanto de memória este algoritmo consome?"*

Existem dois tipos principais:

1. **Complexidade de Tempo** → mede quanto tempo o algoritmo leva para rodas.
2. **Complexidade de espaço** → mede quanta memória o algoritmo utiliza.

---
# Notação Big-O

A **Notação Big-O** é usada para representar a complexidade de algoritmos de forma abstrata, ignorando constantes e termos menos significativos.

Exemplo:

- Se um algoritmo faz `3n + 5` operações para uma entrada de tamanho `n`, sua complexidade é **O(n)**, pos o termo dominante é `n`.

## Principais classes de complexidade:

- **O(1)** → Constantes → independente do tamanho da entrada.
- **O(log n)** → Logarítmica → cresce lentamente mesmo com entradas grandes.
- **O(n)** → Linear → cresce proporcionalmente ao tamanho da entrada.
- **O(n log n)** → Quase linear → comum em algoritmos eficientes de ordenação.
- **O(n²)** → Quadrática → comum em algoritmos com dois laços aninhados.
- **O(2<sup>n</sup>)** → Exponencial → cresce muito rápido, inviável para entradas grandes.
- **O(n!)** → Fatorial → Extremamente ineficiente, usado em problemas combinatórios.

---
# Como calcular complexidade?

Para determinar a complexidade de um algoritmo:

1. **Identifique o tamanho da entrada** → geralmente chamada de `n`.
2. **Conte o número de operações básicas** → comparações, atribuições, etc.
3. **Encontre o termo dominante** → o que cresce mais rápido conforme `n` aumenta.
4. **Ignora constantes** → pois no Big-O só importa a taxa de crescimento.

---
# Exemplos em C

## Exemplo 1: O(1) - Complexidade Constante

```c
int main() {
	int numeros[] = {10, 20, 30, 40, 50};
	printf("Primeiro elemento: %d\n", numeros[0]); // Acesso direto
	return 0;
}
```

A operação de acessar um elemento no array não depende do tamanho do array.

- **Complexidade:** O(1).

## Exemplo 2: O(n) - Complexidade Linear

```c
int main() {
	int numeros[] = {1, 2, 3, 4, 5};
	int n = 5;
	for (int i = 0; i < n; i++) {
		printf("%d ", numeros[i]);
	}
	return 0;
}
```

O laço `for` percorre todos os `n` elementos.

- **Complexidade:** O(n).

## Exemplo 3: O(n²) - Complexidade Quadrática

```c
int main() {
	int n = 3;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			printf("(%d,%d)", i, j);
		}
		printf("\n");
	}
	return 0;
}
```

Dois laços aninhados → para cada `i`, é percorrido todos os `j`.

- **Complexidade:** O(n²).

## Exemplo 4: O(log n) - Busca Binária

```c
int buscaBinaria(int arr[], int n, int chave) {
	int inicio = 0, fim = n - 1;
	while (inicio <= fim) {
		int meio = (inicio + fim) / 2;
		if (arr[meio] == chave)
			return meio;
		else if (arr[meio] < chave)
			inicio = meio + 1;
		else fim = meio -1;
	}
	return -1;
}

int main() {
	int arr[] = {1, 3, 5, 7, 9, 11};
	int n = 6;
	int chave = 7;
	
	int resultado = buscaBinaria(arr, n , chave);
	
	if (resultado != -1)
		printf("Elemento encontrado no índice %d\n", resultado);
	else
		printf("Elemento não encontrado\n");
	return 0;
}
```

A cada passo, o algoritmo divide o problema pela metade.

- **Complexidade:** O(log n).

## Exemplo 5: O(n log n) - Merge Sort (Ordenação Eficiente)

```c
void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    i = 0; j = 0; k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }

    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

int main() {
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = 7;

    mergeSort(arr, 0, n - 1);

    printf("Array ordenado: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

O array é dividido recursivamente em duas partes (log n divisões), e cada fusão percorre os elementos (n operações).

- **Complexidade:** O(n log n).

---
# Conclusão

- A **complexidade de algoritmos** é uma forma de prever eficiência antes de executar o código.
    
- Usamos **Big-O** para descrever o crescimento do tempo/memória em função do tamanho da entrada.
    
- Exemplos práticos mostram que algoritmos eficientes como **O(log n)** ou **O(n log n)** são preferíveis a algoritmos de **O(n²)** ou pior.