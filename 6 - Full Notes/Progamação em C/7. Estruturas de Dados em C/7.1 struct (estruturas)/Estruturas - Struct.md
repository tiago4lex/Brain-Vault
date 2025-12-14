2025-08-19 07:24

Status: #developed #C 

Tags: [[Programação em C]] |[[C]] | [[Struct]]

----
# Introdução

Na linguagem C, as ***structs*** (estruturas) são tipos de dados definidos pelo usuário que permitem agrupar diferentes variáveis sob um mesmo nome. Essas variáveis podem ser de tipos diferentes (inteiros, floats, chats, arrays, etc.) e são chamadas de **membros da estrutura**.

As `structs` são muito úteis quando precisamos **modelar objetos do mundo real** (como um aluno, produto, livro, funcionário, etc.), já que cada entidade pode conter diferentes informações em um único agrupamento.

---
# Sintaxe Básica

```c
struct NomeDaStruct {
	tipo membro1;
	tipo membro2;
	tipo membro3;
	// ... outros membros
};
```

**Exemplo simples:**

```c
#include <stdio.h>

// Definição de uma struct para representar um aluno
struct Aluno {
	char nome[50];
	int idade;
	float nota;
};

int main(){
	// Declaração e inicialização de uma variável do tipo struct Aluno
	struct Aluno  aluno1  = {"Maria", 23, 8.7};

	printf("Nome: %s\n", aluno1.nome);
	printf("Idade: %d\n", aluno1.idade);
	printf("Nota: %.2f\n", aluno1.nota);

	return 0;
}
```

**Saída esperada:**

```text
Nome: Maria
Idade: 23
Nota: 8.70
```

---
# Declaração e Inicialização

## a) Declarar variáveis depois da struct

```c
struct Ponto {
	int x;
	int y;
};

int main() {
	struct Ponto p1 = {10, 20};
	printf("Coordenadas: (%d, %d)\n", p1.x, p1.y);
	return 0;
}
```

## b) Declarar variáveis junto da definição

```c
struct Carro {
	char modelo[30];
	int ano;
	float preco;
} carro 1 = {"Fusca", 1972, 15000.0}; // já declarado e inicializado
```

---
# Acesso aos Membros

Para acessar os membros de uma struct usamos o **operador( . )**:

```c
carro1.ano = 1975;
printf("Ano do carro: %d\n", carro1.ano);
```

---
# Struct com Ponteiros

Quando usamos ponteiros para structs, acessamos os membros com o operador `->`.

```c
#include <stdio.h>
#include <string.h>

struct Pessoa {
	char nome[30];
	int idade;
};

int main() {
	struct Pessoa p1;
	struct Pessoa *ptr = &p1; // ponteiro para struct

	strcpy(ptr->nome, "Ana");
	ptr->idade = 20;

	printf("Nome: %s\n", ptr->nome);
	printf("Idade: %d\n", ptr->idade);

	return 0;
}
```

---
# Structs Aninhadas

É possível colocar uma struct dentro de outra:

```c
#include <stdio.h>

struct Endereco {
    char rua[50];
    int numero;
};

struct Pessoa {
    char nome[30];
    int idade;
    struct Endereco endereco; // struct aninhada
};

int main() {
    struct Pessoa p1 = {"Carlos", 25, {"Rua A", 123}};

    printf("Nome: %s\n", p1.nome);
    printf("Rua: %s, Número: %d\n", p1.endereco.rua, p1.endereco.numero);

    return 0;
}
```

---
# Typedef com Struct

Para simplificar o uso, podemos criar um **alias** para a struct com `typedef`:

```c
#include <stdio.h>

typedef struct {
    char titulo[50];
    int paginas;
} Livro;

int main() {
    Livro l1 = {"O Senhor dos Anéis", 1200};
    printf("Livro: %s (%d páginas)\n", l1.titulo, l1.paginas);
    return 0;
}
```

Assim, não é necessário usar `struct` toda vez que declaramos uma variável.

---
# Arrays de Structs

Podemos criar vetores de structs para armazenar várias entidades do mesmo tipo:

```c
#include <stdio.h>

struct Produto {
	char nome[30];
	float preco;
};

int main() {
	struct Produto estoque[3] = {
		{"Arroz", 5.50},
		{"Feijão", 7.20},
		{"Macarrão", 4.10},
	};

	for(int i = 0; i < 3; i++) {
		printf("%s - R$%.2f\n", estoque[i].nome, estoque[i].preco);
	}

	return 0;
}
```

---
# Resumo

- `struct` permite **agrupar dados diferentes** em um único tipo.
- Membros são acessados com `.` ou `->` (quando ponteiros). 
- Podem ser **aninhadas**, usadas em **arrays** e simplificadas com `typedef`.
- São fundamentais para criar programas **modulares e organizados**.