2025-11-13 19:25

Status: #developed #C 

Tags: [[Programação em C]] | [[Estrutura de Dados]] | [[Grafos]]

----
# O que é um Grafo?

Um **grafo** é uma estrutura de dados usadas para representer **relações** entre elementos. Ele é formado por:

- **Vértices** (ou nós) - entidades
- **Arestas** - conexões entre vértices

![[murabei.com_grafos11.png]]

Um grafo é definido como:

>$G = (V,E)$ , onde $V$ é o conjunto de vértices e $E$ é o conjunto de arestas.

**Na imagem, conjunto de vértices:**
$$
V = \{1,2,3,4\}
$$
**Conjunto de Arestas:**
$$
A = \{\{1,2\}, \{1, 3\}, \{1, 4\}, \{4, 5\}\}
$$

Grafos são usados em praticamente todas as áreas da computação:

- Sistema de distribuição de água

![[Pasted image 20251113194320.png]]

- Redes sociais

![[Pasted image 20251113194104.png]]

- Compiladores
- Sistemas de recomendação
- Redes de computadores
- Mapas e GPS

---
# Conceitos Básicos

## 1. Vértices e Arestas

- Um **vértice** representa um elemento.
- Uma **arestas** é a ligação entre dois vértices.

## 2. Grafo Direcionado e Não Direcionado

- **Não direcionado:** a aresta não possui direção. Ex.: A — B
- **Direcionado** (dígrafo): a aresta possui direção. E.: A → B

![[Pasted image 20251113194409.png]]

## 3. Grafo Ponderado

As arestas possuem um **peso**, geralmente representando custo, tempo ou distância.

## 4. Grau dos vértices

- **Grau de entrada:** nº de arestas que chegam ao vértice.
- **Grau de saída:** nº de arestas que saem do vértice.
- **Grau total:** soma das duas.

![[Pasted image 20251113194452.png]]

## 5. Laços

Uma aresta  é chamada de laço se seu vértice de partida é o mesmo que o da chegada.

- A aresta conecta o vértice a ele mesmo.

![[Pasted image 20251113195139.png]]

## 6. Caminho

Comprimento do caminho: número de vértices que precisamos percorrer de um vértice até o outro.

![[Pasted image 20251113195234.png]]

## 7. Ciclo

Caminho onde o vértice inicial e o final são o mesmo vértice.

![[Pasted image 20251113200118.png]]

>[!note] Nota:
>Um ciclo é um caminho fechado sem vértices repetidos.

---
# Tipos de Representação de Grafos

## 1. Matriz de Adjacência
Representa um grafo com uma matriz $n \times n$  

---

# Tipos de Grafos

## Grafo Trivial
- Possui um único vértice e nenhuma aresta.
![[Pasted image 20251113195823.png]]
## Grafo simples
- Grafo não direcionado, sem laços e sem arestas paralelas.
![[Pasted image 20251113195850.png]]

## Grafo completo
- Grafo simples onde cada vértice se conecta a todos os outros vértices do grafo.
![[Pasted image 20251113200322.png]]

## Multigrafo
- Pode ter múltiplas arestas.

## Grafo regular
- Grafo onde todos os seus vértices possuem o mesmo grau (número de arestas ligadas a ele).
- Todo grafo completo é também regular.
![[Pasted image 20251113200440.png]]

## Subgrafo
- $G_s(V_s, A_s)$ é um subgrafo de $G(V, A)$ se o conjunto de vértices $V_s$ for um subconjunto de $V$, $V_s \subseteq V$, e se o conjunto de arestas $A_s$ for um subconjunto de $A$, $A_s \subseteq A$.

![[Pasted image 20251114113939.png]]

## Grafo bipartido

- Um grafo $G(V,A)$ onde o seu conjunto de vértices pode ser divididos em dois subconjuntos $X$ e $Y$ sem interseção. 
- As arestas conectar apenas os vértices que estão em subconjuntos diferentes.

## Grafo Ponderado
- É um grafo que possui **pesos** (valor numérico) associados a cada uma de suas arestas.
![[Pasted image 20251113200252.png]]


- **Grafo direcionado (digrafo)**.
- **Grafo bipartido** – vértices separados em dois conjuntos.
- **Grafo árvore** – não há ciclos e possui exatamente _n-1_ arestas.