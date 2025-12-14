2025-08-19 08:16

Status: #developed #C 

Tags: [[Programação em C]] | [[C]] | [[Memória Estática]] | [[Memória Dinâmica]]

---
# Representação Estática

A representação estática ocorre quando a estrutura de dados tem **tamanho fixo** definido em **tempo de compilação** (ou de alocação inicial), e sua posição na memória é **contígua**.

## Características principais:

- **Tamanho fixo:** não pode ser alterado depois de criado.
- **Alocação contígua:** todos os elementos são armazenados lado a lado na memória.
- **Acesso rápido:** o índice é convertido diretamente para um endereço de memória.
- **Alocação em tempo de compilação ou inicialização.**

## Exemplo: *Array* (Vetor)

```c
int numeros[5];  // C: Cria um array de 5 inteiros (20 bytes se int  = 4 bytes)
```

O compilador já sabe exatamente:
- Onde começa (`endereço base`).
- Qual o tamanho total.
- Quantos bytes cada elemento ocupa

## ✅ Vantagens

- Acesso muito rápido (`0(1)`).
- Simples de implementar.
- Menos sobrecarga de ponteiros.

## ❌ Desvantagens

- Uso ineficiente de memória se o tamanho escolhido for maior que o necessário.
- Falta de flexibilidade - não é possível crescer ou reduzir sem criar outro array.
- Possibilidade de *overflow* se tentar acessar além do tamanho.

---
# Representação Dinâmica

A **representação dinâmica** ocorre quando a estrutura de dados é criada e gerenciada **em tempo de execução**, permitindo **alterar o tamanho conforme necessário**.

Os elementos não precisam estar todos **contíguos na memória** - oque é comum em listas ligadas.

## Características principais

- **Tamanho variável**: cresce ou diminui sob demanda.
- **Alocação dispersa**: nós podem estar espalhados pela memória.
- **Acesso indireto**: usa ponteiros para localizar o próximo elemento.
- **Alocação em tempo de execução** (_heap memory_).

## Exemplo: Lista Ligada


```c
struct No {
	int valor;
	struct No* proximo.
};
```

Cada nó é alocado quando necessário usando, por exemplo, `malloc` em C, e o ponteiro `proximo` aponta para o próximo nó.

## ✅ Vantagens

- Flexibilidade para crescer ou diminuir.
- Uso mais eficiente da memória em cenários de tamanho variável.
- Inserções/remoções podem ser mais rápidas se já tiver a referência ao ponto de inserção.

## ❌ Desvantagens

- Acesso mais lento (`0(n)`) pois é necessário percorrer os ponteiros.
- Mais uso da memória devido ao armazenamento dos ponteiros.
- Sobrecarga de gerenciamento de memória (*malloc/free, garbage collector*).

---
# Comparação Geral

| **Característica**     | **Estática (Array)**                        | **Dinâmica (Lista Ligada, Fila Ligada)**           |
| ---------------------- | ------------------------------------------- | -------------------------------------------------- |
| Tamanho                | Fixo                                        | Variável                                           |
| Localização na memória | Contígua                                    | Dispersa                                           |
| Velocidade de acesso   | Muito rápida (`0(1)`)                       | Mais lenta (`0(n)`)                                |
| Flexibilidade          | Baixa                                       | Alta                                               |
| Sobrecarga de memória  | Baixa                                       | Maior (armazenamento de ponteiros)                 |
| Inserção/Remoção       | Custosa em posições intermediárias (`0(n)`) | Mais eficiente se tiver referência direta (`0(1)`) |

---
# Analogia Simples

- **Estática:** como uma fila de cadeiras fixas no cinema - todas juntas e já preparadas, mas você não pode mudas a quantidade depois que o cinema foi construído.
- **Dinâmica:** como cadeiras soltas que você pode adicionar ou retirar de uma sala conforme a quantidade de pessoas muda.

