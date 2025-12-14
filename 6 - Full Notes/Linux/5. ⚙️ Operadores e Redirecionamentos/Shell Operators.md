2025-06-06 19:12

Status: #developed #Linux 

Tags: [[Linux]] | [[&]] | [[&&]] | [[>]] | [[>>]]

----
# Introdução

Operadores Linux são uma maneira fantástica de aprimorar seu conhecimento sobre Linux. Existem alguns operadores importantes que valem a pena mencionar. Abordaremos o básico e os dividiremos em partes menores.

| Símbolo / Operador | Descrição                                                                                                                                                           |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `&`                | Este operador permite que você execute comandos em segundo plano no seu terminal.                                                                                   |
| `&&`               | Este operador permite que você combine vários comandos em uma linha do seu terminal.                                                                                |
| `>`                | Este operador é um redirecionador, o que significa que podemos pegar a saída de um comando (como usar `cat` para gerar um arquivo) e direcioná-la para outro lugar. |
| `>>`               | Este operador executa a mesma função do operador `>`, mas acrescenta a saída em vez de substituí-la (o que significa que nada é sobrescrito).                       |

---
# Operador `&`

Este operador nos permite executar comandos em segundo plano. Por exemplo, digamos que queremos copiar um arquivo grande. Isso obviamente levará bastante tempo e nos deixará impossibilitados de fazer qualquer outra coisa até que o arquivo seja copiado com sucesso.

O operador de shell `&` nos permite executar um comando em segundo plano (como esta cópia do arquivo), permitindo-nos fazer outras coisas!

---
# Operador `&&`

Este operador de shell é um pouco enganoso no sentido de quão familiar é com seu parceiro `&`. Ao contrário do operador `&`, podemos usar `&&` para criar uma lista de comandos a serem executados, por exemplo, `comando1 && comando2`. No entanto, vale a pena notar que `comando2 `só será executado se `comando1` for bem-sucedido.

---
# Operador `>`

Este operador é o que conhecemos como um redirecionador de saída. O que isso significa essencialmente é que pegamos a saída de um comando que executamos e a enviamos para outro lugar.

Um ótimo exemplo disso é redirecionar a saída do comando `echo` que aprendemos na Tarefa 4. É claro que executar algo como `echo howdy` retornará "howdy" de volta ao nosso terminal — isso não é muito útil. O que podemos fazer em vez disso é redirecionar "howdy" para algo como um novo arquivo!

Digamos que queremos criar um arquivo chamado "welcome" com a mensagem "hey". Podemos executar `echo hey > welcome` onde queremos que o arquivo seja criado com o conteúdo "hey" assim:

![[Pasted image 20250608105657.png]]

>[!note] Obeservação:
>Se o arquivo "welcome" já existir, o conteúdo será sobrescrito!

---
# Operador `>>`

Este operador também é um redirecionador de saída, como o operador anterior (`>`) que discutimos. No entanto, o que o diferencia é que, em vez de sobrescrever qualquer conteúdo dentro de um arquivo, por exemplo, ele apenas coloca a saída no final.

Continuando com nosso exemplo anterior, onde temos o arquivo "welcome" que contém o conteúdo "hey". Se usássemos echo para adicionar "hello" ao arquivo usando o operador `>`, o arquivo agora teria apenas "hello" e não "hey".

O operador `>>` permite anexar a saída ao final do arquivo — em vez de substituir o conteúdo como:

![[Pasted image 20250608105906.png]]

