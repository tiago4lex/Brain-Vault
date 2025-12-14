2025-05-05 12:17

Status:  #developed #C

Tags: [[Programação em C]] |[[C]] | [[Estrutura de Dados]]

Source: [[Design de Estruturas de Busca e Armazenamento.pdf]]

----
# Conceito Geral

### 1. Compilação de Programas

- Compilação: "tradução" de código fonte (PC) para linguagem de máquina (M)
- Compilador (CM), escrito em M: lê o programa PC e traduz cada instrução para M, escrevendo o programa objeto (PM).

![[Pasted image 20250505122609.png]]

### 2. Ciclo de Desenvolvimento

- Programas em C geralmente são divididos em vários arquivos:
- Cada arquivo pode ser compilado separadamente;
- Para gerar um executável, precisamos reunir os códigos dos arquivos separados (juntamente com as bibliotecas usadas) ***Ligador*** ;
- Bibliotecas: permitem que funções de interesse geral sejam usadas por vários programas;
- O ligador pode ser usado automaticamente pelo compilador (biblioteca padrão), ou deve ser explicitamente acionado.

![[Pasted image 20250505123147.png]]

### 3. Tipos de Dados

##### **Definição:** Um tipo de dado nada mais é que algo do mundo real que pode ser representado computacionalmente. Por exemplo, os números que pertencem ao conjunto dos números inteiros, os números que pertencem ao conjunto dos números reais, letras, caracteres especiais, acentuação, pontuação, palavras, etc.

- O objetivo principal de qualquer computador é a resolução de problemas através da manipulação de dados, que pode ser de vários tipos.
- Em computação, dado é algo que pode ser representado, armazenado.
- Os dados pode ser de tipo primitivo ou derivado:
	- **Tipos primitivos:** tipos de dados básicos utilizados na construção de algoritmos. São utilizados no algoritmo, porque já vêm definidos na linguagem. A maioria das linguagens utilizam os quatro tipos básicos de dados.
	- **Tipos derivados:** tipos de dados que derivam dos tipos de dados básicos (primitivos).

| **Tipo**           | **Tamanho** | **Menor Valor**    | **Maior Valor**    |
| ------------------ | ----------- | ------------------ | ------------------ |
| char               | 1 byte      | - 128              | + 127              |
| unsigned char      | 1 byte      | 0                  | + 255              |
| short int (short)  | 2 bytes     | - 32.768           | + 32.767           |
| unsigned short int | 2bytes      | 0                  | +65.535            |
| int (*)            | 4 bytes     | - 2.147.483.648    | + 2.147.483.647    |
| long int (long)    | 4 bytes     | - 2.147.483.648    | + 2.147.483.647    |
| usigned long int   | 4 bytes     | 0                  | + 4.294.967.295    |
| float              | 4 bytes     | - 10<sup>38</sup>  | + 10<sup>38</sup>  |
| double             | 8 bytes     | - 10<sup>308</sup> | + 10<sup>308</sup> |

### 4. Operadores de incremento e Decremento

#### ++ e --
- Incremento ou decrementa o valor de uma variável de uma unidade
- O incremento/decremento pode ser antes ou depois da variável ser usada

- N++ , incrementa n depois de ser usado
-  ++N, incrementa n antes de ser usado
![[Pasted image 20250505125133.png]]

### 5. Entrada e saída

São feitas com uso de funções

#### Função ***printf***:

- `%c` especifica um char
- `%d` especifica um int
- `%u` especifica um unsigned int
- `%f` especifica um double (ou float)
- `%e` especifica um double (ou float) no formato científico
- `%g` especifica um double (ou float) no formato mais apropriado (%f ou %e)
- `%s` especifica uma cadeia de caracteres
	
- Exemplo:
	- `printf ("Inteiro = %d Real = %g", 33, 5.3);`
	- saída:
		- `Inteiro = 33 Real = 5.3`

#### Caracteres de escape:
- `\n` caractere de nova linha
- `\t` caractere de tabulação
- `\r` caractere de retrocesso
- `\"` caractere "
 - `\\` Caractere \

#### Especificação do tamanho do campo:
![[Pasted image 20250505130057.png]]

#### ***scanf*** (formato, lista de endereços das variáveis):
- `%c` especifica um char
- `%d` especifica um int
- `%u` especifica um unsigned int
- `%f, %, %g` especificam um float
- `%lf, %le, %lg` especificam um double
- `%s` especifica uma cadeia de caracteres

#### Comando de definição de uma função

`Tipo_retorno nome_funcao (lista de parametros)`
`{`
`   Corpo da função`
`}`

#### Definição de funções

![[Pasted image 20250505151959.png]]


#### Pilha de execução

- Varipaveis locais têm escopo local
- Funções são independentes entre si
- Transferência de dados entre funções através de:
	- Passagem de parâmetros
	- Valor de retorno
- Parâmetros em C <span style="background:#ff4d4f">são passados por valor</span>
- <span style="background:#ff4d4f">Pilha de execução:</span> Coordena comunicação entre a função que chama e a função chamada
	- Permite passagem de parâmetros e valores de retorno

#### Esquema representativo da memória

![[Pasted image 20250505152300.png]]

##### Exemplo fat (5)

![[Pasted image 20250505152702.png]]

##### Pilha de execução

![[Pasted image 20250505152748.png]]

#### Ponteiro de variáveis

- Pode ser necessário comunicar mais de um valor de retorno para a função que chama
- Por exemplo uma função que deve calcular a some e produto de dois números:

![[Pasted image 20250505153057.png]]

#### Ponteiros

- Permitem manipulação direta de endereços de memória no C
- Variáveis do tipo ponteiro:
	- Armazenam endereços de memória
	- É possível definir um ponteiro para cada tipo do C que seja capaz de armazenar endereços de memória em que existem valores do tipo correspondente
	- int a;
	- int* p (armazena endereço de memória em que há valor inteiro)

#### Operadores de ponteiros

- Operador ***&*** ("endereço de")
	- Aplicado a variáveis, retorna o endereço da posição de memória reservada para variável
	
- Operador * ("conteúdo de")
	- Aplicado a ponteiros, acessa o conteúdo de memória do endereço armazenado pela variável ponteiro 

- **Exemplo:**

![[Pasted image 20250505153550.png]]

#### Passando ponteiros para função

- Ponteiros permitem modificar o valor das variáveis indiretamente
- Possível solução para passagem por ref!

![[Pasted image 20250505153729.png]]

- **Exemplo**

![[Pasted image 20250505153801.png]]

#### Variáveis Globais

 - Declaradas fora do escopo das funções
 - São visíveis a todas as funções
 - Existem enquanto o programa existir (não estão na pilha de execução)
 - Utilização:
	 - Devem ser usadas com critério
	 - Pode criar muita dependência entre as funções
	 - Dificulta o entendimento e o reuso de código

- **Exemplo de Variáveis Globais:**

![[Pasted image 20250505154029.png]]

#### Variáveis Estáticas

- Declaradas no escopo de funções
- Existem enquanto o programa existir (não estão na pilha de execução)
- Somente são visíveis dentro das funções nas quais são declaradas
- Utilização:
	- Quando for necessário recuperar o valor de uma variável na execução passada da função

- **Exemplo de variável estática:**
	- Função que imprime números reais
		- Imprime um número por vez (máximo de 5 números por ilha)

![[Pasted image 20250505154247.png]]

#### Sobre variáveis estáticas e globais

- Variáveis estáticas e globais são inicializadas com zero, quando não forem explicitamente inicializadas
- Variáveis globais estáticas:
	- São visíveis para todas funções subsequentes
	- Não pode ser acessadas por funções de outros arquivos

- Funções estáticas
	- Não pode ser acessadas por funções de outros arquivos


#### Pré-processador e Macros

- Código C antes de ser compilado é passado pelo pré-processador
- O pré-processador:
	- Reconhece diretivas
	- Altera o código e envia para o compilador

- Diretiva `#include`
	- O pré-processador substitui pelo corpo do arquivo especificado

- `#include "nome_do arquivo"`
	- Procura o arquivo do diretório local
	- Caso não encontre, procura nos diretórios de include especificados para compilação

- `#include <nome_do_arquivo>`
	- Não procura no diretório local

----

# Referências
