2025-08-26 08:44

Status:

Tags: [[Programação em C]] | [[C]] | [[strcpy]] | [[memcpy]] | [[Struct]]

----
# Introdução

Na linguagem C, a manipulação de strings e blocos de memória é feita principalmente através de funções da **biblioteca `<string.h>`**.

Duas das função mais utilizadas são:

- `strcpy()` → usada para copia **strings terminadas em `\0`** (cadeia de caracteres).
- `memcpy()` → usada para copia **blocos de memória arbitrários**, sem depender do caractere nulo `\0`.

Apesar de parecerem semelhantes, cada uma tem usos, vantagens e riscos específicos.

---
# Função `strcpy()`

## Sintaxe

```c
char *strcpy(char *destino, const char *origem);
```

- `destino` → ponteiro para a área de memória onde a string será copiada.
- `origem` → ponteiro para a string a ser copiada.
- **Retorno** → ponteiro para `destino`.

## Características

- Copia **caractere por caractere**  até encontrar o **caractere nulo** (`\0`).
- É usada **exclusivamente para strings terminadas em `\0`**
- O programador deve garantir que o destino tenha **espaço suficiente** para receber a string.

## Exemplo de uso

```c
#include <stdio.h>
#include <string.h>

int main() {
	char origem[] = "Linguagem C";
	char destino[20]; // espaço suficiente  para armazenar a cópia
	
	strcpy(destino, origem);
	
	printf("String copiada: %s\n", destino);
	
	return 0;
}
```

**Saída:**

```text
String copiada: Linguagem C
```

## Possíveis Problemas

- **Buffer overflow:** se `destino` não tiver espaço suficiente, a função sobrescreve a memória.
- **Sem checagem de tamanho:** a função não verifica se `destino` pode conter a string completa.

>[!note] Nota:
>Para mais segurança, costuma-se usar `strcpy()`, que permite limitar o número de caracteres copiados.

---
# Função `memcpy()`

## Sintaxe

```c
void *memcpy(void *destino, const void *origem, size_t n);
```

- `destino` → ponteiro para o bloco de memória que receberá os dados.
- `origem` → ponteiro para o bloco de memória de onde os dados serão copiados.
- `n` → número de **bytes** a serem copiados.
- **Retorno** → ponteiro para `destino`.

## Características

- Copia **exatamente `n` bytes** da origem para o destino.
- Não depende de strings nem de caracteres nulos (`\0`).
- Pode copia **qualquer tipo de dado** (inteiros, floats, structs, arrays, etc.).

## Exemplo de uso

```c
#include <stdio.h>
#include <string.h>

int main() {
	int origem[5] = {1, 2, 3, 4, 5};
	int destino[5];
	
	// Copiando 5 inteiros (5 * sizeof(int) bytes)
	memcpy(destino, origem, 5 * sizeof(int));
	
	printf("Array copiado: ");
	for(int i = 0;i < 5; i++) {
		printf("%d ", destino[i]);
	}
	printf("\n");
	
	return 0;
}
```

**Saída:**

```txt
Array copiado: 1 2 3 4 5
```

## Possíveis Problemas

- **Sobreposição de memória:** se `destino` e `origem` se sobrepõem, o comportamento é indefinido.

>[!note] Nota:
>Nesse caso, deve-se usar `memmove()` em vez de `memcpy()`.

---
# Comparação entre `strcpy()` e `memcpy()`

| Aspecto                | `strcpy()`                             | `memcpy()`                                           |
| ---------------------- | -------------------------------------- | ---------------------------------------------------- |
| Uso principal          | Copiar **strings** (`char[]`)          | Copiar **blocos de memória** (qualquer tipo de dado) |
| Critério de parada     | Até encontrar `\0`                     | Número de bytes (`n`) especificado                   |
| Tipo de dado suportado | Apenas `char` (strings C)              | Qualquer tipo (`int`, `float`, `struct`, etc.)       |
| Risco principal        | Buffer overflow (se não houver espaço) | Comportamento indefinido se houver sobreposição      |
| Alternativas seguras   | `strncpy()`                            | `memmove()`                                          |

---
# Conclusão

- Use **`strcpy()`** apenas quando estiver lidando com **strings terminadas em `\0`**, garantindo espaço suficiente no destino.
- Use **`memcpy()`** para copiar **dados genéricos** ou quando precisar copiar apenas uma parte da memória.
- Em casos de sobreposição de memória, prefira **`memmove()`**.
- Em aplicações críticas, dê preferência a **versões seguras** (`strncpy`, `memcpy_s`, etc.), quando disponíveis.