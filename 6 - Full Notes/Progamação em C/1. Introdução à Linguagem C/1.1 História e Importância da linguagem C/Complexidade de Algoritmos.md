---

---
Tags: #developed #C 

Tags: [[Programação em C]] | [[C]]

---
# Quem é Donald Knuth?

- Nascido em 10 de janeiro de 1938 - 87 anos
- É um cientista computacional
- Formado na Universidade de Stanford
- Autor do livro A Arte da programação de computadores
- Criou o campo de análise de algoritmos
- Criou o sistema tipográfico TeX (sistema tipográfico)
- Criou o sistema de criação de fontes METAFONT
- Foi pioneiro do conceito de programação literária
- Desenvolveu o conceito de número surreal.

---
# Qual sua principal contribuição para a complexidade de algoritmos?

A principal contribuição de Donald Knuth para a complexidade de algoritmos foi estabelecer as bases teóricas e práticas para a análise rigorosa de algoritmos, ou seja, estudar e comparar o desempenho dos algoritmos de forma matemática, especialmente em termos de tempo e espaço.

## Formalização da Análise Assintótica

Knuth popularizou o uso das notações assintóticas como O(grande), Ω (Ômega) e Θ (Theta), que descrevem o comportamento de algoritmos em função do tamanho da entrada, especialmente em sua obra monumental:

>**"The Art of Computer Programming"** (TAOCP) — uma série de livros que começou a ser publicada nos anos 1960 e ainda está em andamento. Neles, ele introduz não apenas algoritmos, mas também:

- **Notações assintóticas**: Knuth popularizou o uso da notação O-grande (O(n)), que descreve o comportamento do tempo de execução de algoritmos em função do tamanho da entrada.

- **Análise matemática detalhada**: Ele aplicou métodos matemáticos rigorosos, como somas assintóticas, recorrências e funções geradoras, para avaliar o desempenho de algoritmos.

- **Classificação de algoritmos**: Knuth estabeleceu critérios para comparar algoritmos com base em sua eficiência, considerando o pior caso, o melhor caso e o caso médio.

---
# Sprint 1: Conceitos básicos

## O que é complexidade de algoritmos?

> [!quote] Complexidade de algoritmos
> "A complexidade de um algoritmo é analisada em termos de **tempo** e **espaço**. Normalmente, o algoritmo terá um desempenho diferente com base no processador, disco, memória e outros parâmetros de hardware. A complexidade é usada para medir a velocidade de um algoritmo. Sendo o algoritmo um agrupamento de etapas para se executar uma tarefa, o tempo que leva para um algoritmo ser executado é baseado no número de passos.
> Digamos que um algoritmo percorre um array de dez posições somando o índice das posições a 200. A complexidade seria de 10x<sup>t</sup>, sendo que <sup>t</sup> representa o tempo necessário para atualizar cada elemento do array com a operação de soma. Cada computador pode ser muito diferente: o tempo varia de acordo com o hardware, a linguagem utilizada e o sistema operacional."

**Fonte:** [Análise da Complexidade de Algoritmos](https://www.iugu.com/blog/analise-complexidade-algoritmos)

**Resumindo:**

- A complexidade de algoritmo é a quantidade de recurso de memória ou processador para resolver um problema, é a medida de quão eficiente um algoritmo é.

## Qual a diferença entre as notações Big O, Big Θ e Big Ω?

### Big O - **O pior caso:** complexidade muito grande

- É uma notação matemática que descreve o limite da complexidade temporal ou espacial de um algoritmo. É usada para entender como o desempenho de um algoritmo aumenta à medida que o tamanho da entrada aumenta.

- Representa o pior caso de desempenho de um algoritmo, tem limite superior do tempo/memória usado e o tempo de execução cresce proporcionalmente a n.

### Big Ω - **O melhor caso:** complexidade menor que a entrada de n.

- Descreve o menor limite de crescimento de uma função, representando o melhor cenário possível. Em outras palavras, indica que a função usará a menor quantidade de recursos computacionais necessária para ser executada

- Representa o melhor caso de desempenho, tem limite inferior (o mínimo que o algoritmo pode gastar) e o algoritmo levará pelo menos um tempo proporcional a n.

### Big Θ  - **O caso médio**

- Descreve o crescimento exato da complexidade de um algoritmo em relação ao tamanho da entrada. Ele representa tanto o melhor quanto o pior caso dentro de um mesmo limite, ou seja, mostra que a função cresce proporcionalmente à entrada.

- Representa um caso médio de desempenho, o tempo de execução está entre o limite inferior e superior e o tempo cresce exatamente proporcional a n.

---
# Sprint 2: Classificação de Algoritmos
## Classificação de diferentes algoritmos

### Complexidade constante - O(1):
O tempo de execução não varia com o tamanho da entrada.

```c
int acessarPrimeiro(int vetor[]) {
    return vetor[0];
}

int main() {
    int numeros[] = {10, 20, 30, 40, 50};
    int resultado = acessarPrimeiro(numeros);
    printf("O(1): Primeiro elemento do vetor = %d\n", resultado);
    return 0;
}
```

### Complexidade Linear - O(n):
O tempo cresce proporcionalmente ao tamanho da entrada.

```c
int main(){
    int n, i;
    int soma = 0;

    printf("Digite um numero para saber a soma dele: ");
    scanf("%d", &n);

    for(i = 0; i <= n; i++){
        soma = soma + i;
    }
    printf("A soma de 0 ate %d e igual a : %d", n, soma);
    
    return 0;
}
```

### Complexidade Quadrática - O(n<sup>2</sup>):
O tempo cresce proporcional ao quadrado do tamanho da entrada.

```c
int main() {
    int n = 5;
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("i = %d, j = %d\n", i, j);
        }
    }

    return 0;
}
```

### Complexidade Logarítmica - O(log n):
Aumentos na entrada geram crescimento lento no tempo de execução.

```c
int buscaBinaria(int v[], int t, int x) {
    int i = 0, f = t - 1;
    while (i <= f) {
        int m = (i + f) / 2;
        if (v[m] == x) return m;
        if (v[m] < x) i = m + 1;
        else f = m - 1;
    }
    return -1;
}

int main() {
    int v[] = {1, 3, 5, 7, 9};
    int pos = buscaBinaria(v, 5, 7);
    printf("Posição: %d\n", pos);
    return 0;
}
```

### Complexidade Exponencial - O(2<sup>n</sup>):
O tempo cresce muito rápido, inviável para entradas grandes. 

```c
int fibonacci(int n) {
    if (n <= 1)
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n = 5;
    printf("Fibonacci de %d é %d\n", n, fibonacci(n));
    return 0;
}
```

### Complexidade Fatorial - O(n!)
Tempo explode com o aumento da entrada. Usado em problemas como permutações.

```c
void trocar(int *a, int *b) {
    int t = *a; *a = *b; *b = t;
}

void permutar(int v[], int ini, int n) {
    if (ini == n) {
        for (int i = 0; i < n; i++) printf("%d ", v[i]);
        printf("\n");
        return;
    }
    for (int i = ini; i < n; i++) {
        trocar(&v[ini], &v[i]);
        permutar(v, ini + 1, n);
        trocar(&v[ini], &v[i]); // desfaz a troca
    }
}

int main() {
    int v[] = {1, 2, 3};
    permutar(v, 0, 3);
    return 0;
}
```
