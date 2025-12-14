

## **Ponteiros**

- **Oque são:** Variáveis que guardam endereços de memória
- **Para que serve:** Acessar modificar dados

**Símbolos:**

- `*` (asterisco):
	- Declara um ponteiro: `int *p`
	- Acessa o valor do endereço (desreferencia): `*p = 10`
- `&` (e comercial):
	- Pega o endereço da variável: `p = &x`

---
## **Manipulação de Arquivos**

## Arquivo

- É armazenado em um dispositivo de **memória secundária**.
- Pode ser lido e escrito por um programa.
- O arquivo é uma sequencia de bytes que reside em um dispositivo de armazenamento durável, como:
	- Disco Rígido, CD, Pendrive, SSD, etc.

### Arquivos em Linguagem C

- `stdin`: entrada de dados padrão
- `stdout`: saída de dados padrão
- `stderr`: saída de erros padrão

- Em C, o tipo de dados que implementa uma stream é o `FILE`
- `FILE` é uma struct definida pela biblioteca `<stdio.h>`

**Funções:**

- ``fopen()`` = abre um arquivo
- ``fclose()`` = fecha um arquivo
- ``ferror()`` = retorna verdadeiro se ocorreu um erro
- ``fputc()`` = escreve um caracter em um arquivo
- ``fgetc()`` = lê um caracter de um arquivo
- ``fputs()`` = escreve uma string em um arquivo
- ``fgets()`` = lê uma string de um arquivo
- ``fwrite()`` = escreve uma estrutura (struct) em um arquivo
- ``fread()`` = lê uma estrutura (struct) de um arquivo
- ``fseek()`` = posiciona o arquivo em um byte específico

**Exemplo:**

1. Abertura do arquivo

```c
#include <stdio.h>
FILE *fp = fopen("arquivo.txt", "modo");
```

- Modos comuns:
	- `r` - leitura
	- `w` - escrita (apaga conteúdo anterior)
	- `a` - acrescentar *(append)*
	- `r+`, `w+`, `a+` - leitura + escrita

2. Escrever no arquivo

```c
fprintf(fp, "Texto\n");     // texto formatado
fputc('A', fp);             // caractere
fputs("Linha", fp);         // string simples
```

3. Ler o arquivo:

```c
fscanf(fp, "%", str);        // lê texto formatado
fgetc(fp);                   // lê caractere
fgets(linha, tamanh, fp);    // lê linha
```

4. Fechar o arquivo

```c
fclose(fp);
```

---
## **STRUCT em C**

- **O que é:** Uma `struct` (estrutura) é um tipo de dado que **agrupa várias variáveis** (de tipos diferentes) sob **um único nome**.

- **Para que serve:** Organizar dados complexos, como representar uma pessoa, produto, ponto 2D, etc.

**Exemplos:**

```c
struct Pessoa {
	char nome [50];
	int idade;
	float altura;
};
```

**Como usar:**

```c
struct Pessoa p1;

p1.idade = 25;
p1.altura - 1.75;
strcpy(p1.nome, "Tiago")   // precia da biblioteca string.h
```

