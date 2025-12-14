2025-05-05 15:49

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Arrays]] | [[Estrutura de Dados]] 

Source: [[Arrays.pdf]]

----
# Conceito Geral

## Introdução

- Um array é uma coleção de elementos de dados semelhantes.
- Esses elementos de dados têm o mesmo tipo de dado.
- Os elementos de um array são armazenados em posições de memória consecutivas e são referenciados por um índice (também conhecido como subscrito).
- Declarar um array significa especificar três coisas: 
	- Tipo de dado - que tipo de valores ele pode armazenar. Por exemplo, int, char, float
	- Nome - para identificar o array
	- Tamanho - o número máximo de valores que o array pode conter.

- Os arrays são declarados usando a seguinte sintaxe:

![[Pasted image 20250505155630.png]]

## Acessando Elementos de um Array

- Para **acessar todos os elementos de um array**, devemos usar um laço (loop)
- Ou seja, podemos acessar todos os elementos de uma matriz variando o valor do subscrito na matriz
- Mas observe que o subscrito deve ser um valor integral ou uma expressão avaliada como um valor integral

![[Pasted image 20250505155811.png]]

## Calculando o Endereço dos Elementos de um Array

- Endereço do elemento de dados:
	- `A[k] = BA(A) + w (k - limite_inferior)`
	- `A` é a matriz
	- `k` é o índice do elemento cujo endereço temos que calcular
	- `BA` é o endereço básico da matriz A
	- `w` é o tamanho da palavra de um elemento na memória

Por exemplo, o tamanho do int é 2

![[Pasted image 20250505160122.png]]

## Armazenamento de valores em Arrays

Inicializando Arrays durante a declaração `int valor [5] = {90, 98, 78, 56, 23}`

![[Pasted image 20250505160310.png]]

Entrada de valores do teclado:

![[Pasted image 20250505160341.png]]

Atribuição de valores a elementos individuais: 

![[Pasted image 20250505160417.png]]

## Calculando o comprimento de um Array

``comprimento = limite_superior - limite_inferiro + 1`

Onde:

`limite_superior` é o índice do último elemento
`limite inferior` é o índice do primeiro elemento da array

![[Pasted image 20250505160607.png]]

Perceba que: `limite inferior = 0` e `limite_superior = 7`
Logo, `comprimento = 7 - 0 + 1 = 8`

## Ler e Mostrar *N* números usando um array

```c
#include <stdio.h>

int main()
{
    int i = 0, n, arr[20];

    printf("\nEntre com o número de elementos (máx. 20): ");
    scanf("%d", &n);

    if (n > 20 || n < 1)
    {
        printf("\nNúmero inválido. O número de elementos deve estar entre 1 e
         20.\n");
        return 1;
    }

    printf("\nEntre com os elementos:\n");

    for (i = 0; i < n; i++)
    {
        printf("arr[%d] = ", i);
        scanf("%d", &arr[i]);
    }

    printf("\nElementos do vetor:\n");

    for (i = 0; i < n; i++)
    {
        printf("arr[%d] = %d\n", i, arr[i]);
    }
    
    return 0;
}
```

## Inserindo um Elemento em um Array

Passos para inserir um novo elemento no final de um array:
- 1. Faça `limite superior = limite_superior + 1`
- 2. Faça `A[limite_superior] = VAL`
- 3. Sair

## Deletando um Elemento de um Array

Algoritmo para excluir um elemento do final do array
- 1. Faça `limite_superior = limite_superior -1` 
- 2. Sair

## Passando Arrays para Funções

![[Pasted image 20250505190712.png]]

Passando **valores** de dados:

![[Pasted image 20250505190745.png]]

Passando **endereços**

![[Pasted image 20250505190809.png]]

Passando **todo** o array

![[Pasted image 20250505190834.png]]

## Ponteiros e Arrays

- O conceito de **array** está muito associado ao conceito de **ponteiro**
- O nome de um array é, na verdade, um ponteiro que aponta para o primeiro elemnto do array

```c
int *ptr;
ptr = &arr[0]
```


- Se a variável ponteiro `ptr` contém o endereço do primeiro elemento do array, então o endereço dos elementos sucessivos pode ser calculado escrevendo `ptr++`

```c
int *ptr = &arr[0];
ptr++;
printf("O valor do 2º elemento do array é: %d", *ptr);
```

## Arrays de Ponteiros

- Um array de ponteiros pode ser declarado como: `int *ptr[10];`
- A instrução acima declara um array de 10 ponteiros, onde cada um dos ponteiros aponta para uma variável inteira. Por exemplo:

```c
int *ptr[10];
int p=1, q=2, r=3, s=4, t=5;
ptr[0]=&p; ptr[1]=&q; ptr[2]=&r; ptr[3]=&s; ptr[4]=&t;
```

## Arrays Bidimensionais

- Um array bidimensional é especificado usando dois subscritos, onde um subscrito denota linha e outro denota coluna.
- Para C, um array bidimensional é como um <span style="background:#fff88f">array de arrays unidimensionais</span>
- Um array bidimensional é declarada como: `tipo_dado nome_array[tam_linhas][tam_colunas];`

![[Pasted image 20250505191706.png]]

- Portanto, uma matriz bidimensional `m x n` é uma matriz que contém elementos de dados `m x n` e cada elemento é acessado usando dois subscritos, `i` e `j`, onde `i <= m` e `j <= n` `int valor[3][5];`

![[Pasted image 20250505191917.png]]

### Representação da Memória de um Array Bidimensional

Existem duas maneiras de armazenar um array 2D na memória:

- Ordem principal da linha

![[Pasted image 20250506190336.png]]

- Ordem principal da coluna

![[Pasted image 20250506190408.png]]

#### Ordem Principal de Linha

- Os elementos da 1ª linha são armazenados antes dos elementos da segunda e terceira linhas
- Ou seja, os elementos do arrya são <span style="background:#fff88f">armazenadas linha por linha</span>, onde **n** elementos da primeira linha ocuparão as primeiras enésimas posições.

![[Pasted image 20250506190717.png]]

`(0,0) (0,1) (0,2) (0,3) (1,0) (1,1) (1,2) (1,3) (2,0) (2,1) (2,2)(2,3)`

#### Ordem principal da coluna

- Os elementos os elementos da primeira coluna são armazenados antes dos elementos da segunda e terceira colunas;
- Ou seja, os elementos da matriz são <span style="background:#fff88f">armazenados coluna por coluna</span>, onde **n** elementos da primeira coluna ocuparão as primeira enésimas posições

![[Pasted image 20250506212945.png]]

`(0,0)(1,0)(2,0) (0,1)(1,1)(2,1) (0,2)(1,2)(2,2) (0,3)(1,3)(2,3)`

### Inicializando Arrays Bidimensionais

Um array bidimensional é inicializado da mesma forma que um array unidimensional é incializado. 

Por exemplo:

```c
int valor[6] = {90, 87, 78, 68, 62, 71};
int valor[2] [3] = {{90, 87, 78}, {68, 62, 71}};
```

### Quando usar

**Quando usar vetor unidimensional vs matriz bidimensional**

- **Vetor Unidimensional:**
1. Use quando os dados são uma simples lista ou sequência
2. Exemplo: Lista de notas de alunos, temperaturas diárias, etc. 

- **Matriz bidimensional:**
1. Use quando os dados têm uma estrutura tabular (linhas e colunas)
2. Exemplo: Tabela de notas de alunos por disciplina, matriz de pixels de uma imagem, etc.

## Passando Arrays 2D para Funções

![[Pasted image 20250507060926.png]]

### Explicação dos métodos

#### Passando elementos individuais:

- Cada elemento da matriz é passado individualmente para a função
- Útil quando você precisa processar elementos de forma independente

#### Passando uma linha da matriz

- Uma linha da matriz (um array unidimensional) é passada para a função
- Útil quando você precisa processar uma linha inteira de cada vez

#### Passando a matriz inteira:

- A matriz 2D inteira é passada para a função
- No padrão C89/C90, é necessário especificar o tamanho das colunas na declaração da função

#### <font color="#ff0000">Observações</font>

- No padrão C89/90, não é possível passar uma matriz 2D para uma função sem especificar o tamanho das colunas. Por exemplo, `int matriz[][]` não é válido.
- Se o tamanho da matriz for dinâmico (não conhecido em tempo de compilação), você precisará usar alocação dinâmica de memória (com malloc free), mas isso foge ao escopo do padrão C89/90

## Ponteiros e Arrays 2D - Resumo das técnicas

| **TÉCNICA**        | **DESCRIÇÃO**                                                  |
| ------------------ | -------------------------------------------------------------- |
| Acesso a elementos | Use aritmética de ponteiros para acessar elementos individuais |
| Acesso a linhas    | Use um ponteiro para uma linha (`int(*ptr)[colunas]`)          |
| Passar toda matriz | Use `int(*matriz)[colunas]` para passar a matriz inteira       |

**Dicas importantes**

1.**Tamanho das colunas:**
- Ao trabalhar com arrays 2D, o tamanho das colunas deve ser conhecido em tempo de compilação
- Por exemplo, `int(*matriz)[3]` só funciona para matrizes com 3 colunas

**2. Aritmética de ponteiros**
- A aritmética de ponteiros é baseada no tipo de ponteiro. Por exemplo `ptr + 1` avança para o próximo elemento do tipo apontado

**3. Evitar confusão**
- `int *ptr` é um ponteiro para um  int
- `int (*ptr)[3]` é um ponteiro para um array de 3 int

## Matrizes 2D

Resumo das Situações Reais

| **Passagem**        | **Exemplo Prático**                 | Quando Usar                              |
| ------------------- | ----------------------------------- | ---------------------------------------- |
| Elemento Individual | Validar notas de alunos             | Processar itens um a um (ex.: validação) |
| Uma linha           | Calcular vendas mensais             | Operações em linhas completas            |
| Matriz inteira      | Verificar vencedor no jogo da velha | Análise global da matriz                 |

**Por que esses exemplos são úteis?**

1. **Elementos individuais:**
	1. Permite aplicar regras ou transformações específicas a cada dado (ex.: validar notas, converter unidades).
2. **Uma Linha:**
	1. Otimiza operações em conjuntos de dados relacionados (ex.: totalizar vendas, calcular médias)
3. **Matriz inteira:**
	1. Facilita a análise de estruturas completas (ex.: tabuleiros, imagens, mapas)

### 1. Elementos Individuais: Planilha de Notas de Alunos

**Cenário:**
Você é um professor e quer calcular a média de cada aluno em uma planilha de notas (linhas = alunos, colunas = notas de provas). Cada nota precisa ser validade antes do cálculo.

**Aplicação:**
- Cada nota é passada individualmente para a função `validarNotas`.
- Útil quando você precisa <span style="background:#fff88f">processar cada elemento de forma isolada</span> (ex.: validação, formatação).

### 2. Uma Linha: Análise de Vendas por Mês

**Cenário:**
Você gerencia uma loja e quer calcular o total de vendas de cada mês (cada linha da matriz representa um mês, e as colunas são semanas)..

**Aplicação:**
- A função recebe uma linha inteira `vendas[mes]` para calcular o total.
- Ideal para <span style="background:#fff88f">operações em linhas específicas</span> (ex.: totalizar, filtrar).

### 3. Matriz Inteira: Jogo da Velha

**Cenário:**
Você está desenvolvendo um jogo da velha e precisa verificar se há um vencedor após cada jogada (a matriz 3x3 representa o tabuleiro).

**Aplicação:**
- A função `verificarVencedor()` recebe a matriz inteira para analisar o tabuleiro.
- Necessário quando <span style="background:#fff88f">a lógica depende de todos os elementos</span> (ex.: jogos, processamento de imagens)

## Ponteiros e Array Tridimensionais

- Declarando um ponteiro para uma matriz tridimensional:

```c
int arr[2][2][2] = {1, 2, 3, 4, 5, 6, 7, 8};
int (*parr)[2][2];

parr = arr;
```

- Pode-se acessar um elemento de um array 3D escrevendo:

```c
arr[i][j][k] = *(*(*(*(arr + i) + j) + k))
```

**Array 3D:**

```c
int myFirst3DArray[3][4][2] =
{
{{10,11}, {12,13}, {14,15}, {16,17}},
{{18,19}, {20,21}, {22,23}, {24,25}},
{{26,27}, {28,29}, {30,31}, {32,33}}
};
```

## Arrays Multidimensionais

- É um array de arrays
- Assim como temos 1 índice para array unidimensional, 2 índices para array bidimensional, da mesma forma temos `n` índices em um array multidimensional 

![[Pasted image 20250507064046.png]]

### Inicializando Arrays Multidimensionais

- Um array multidimensional é declarado e inicializado da mesma maneira que declaramos e inicializamos arrays unidimensionais e bidimensionais.

## Aplicações de Arrays

- Amplamente usadas para implementar vetores matemáticos, matrizes e outros tipos de tabelas retangulares.
- Também são usadas para **implementar outras Estruturas de Dados** como tabelas hash, deques, filas, pilhas e strings.
- Também podem ser usadas para **alocação de memória dinâmica**.










----

# Referências
