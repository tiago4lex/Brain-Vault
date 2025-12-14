2025-06-04 20:20

Status: #developed #Linux 

Tags: [[Linux]] | [[ls]] | [[cd]] | [[echo]] | [[cat]] | [[pwd]]

----
# Introdução

Assim como o Windows, iOS e MacOS, o Linux é um sistema operacional e um dos mais populares no mundo, sendo ele usado em smart cars, dispositivos android, supercomputadores, servidores empresariais, etc.

![[Pasted image 20250604202305.png]]

----
# Onde o Linux é Usado?

É justo dizer que o Linux é muito mais intimidador de se abordar do que sistemas operacionais (SOs) como o Windows. Ambas as variantes têm suas próprias vantagens e desvantagens. Por exemplo, o Linux é consideravelmente mais leve e você ficaria surpreso em saber que há uma boa chance de você já ter usado o Linux de uma forma ou de outra todos os dias! O Linux potencializa coisas como:

- Servidores de websites
- Painéis de controle/entretenimento automotivo
- Sistemas de ponto de venda (PoS), como caixas registradoras e caixas em lojas
- Infraestruturas críticas, como controladores de semáforos ou sensores industriais

---
# Sabores do Linux

O nome "Linux" é, na verdade, um termo abrangente para diversos sistemas operacionais baseados no UNIX (outro sistema operacional). Graças ao Linux ser de código aberto, existem variantes do Linux em todos os formatos e tamanhos, mais adequadas para a finalidade do sistema.

Por exemplo, Ubuntu e Debian são algumas das distribuições mais comuns do Linux devido à sua alta extensibilidade. Ou seja, você pode executar o Ubuntu como um servidor (como sites e aplicativos web) ou como um desktop completo.

> **Observação:** o Ubuntu Server pode ser executado em sistemas com apenas 512 MB de RAM!

Assim como existem diferentes versões do Windows (7, 8 e 10), existem muitas versões/distribuições diferentes do Linux.

---
# Iniciando no Linux (primeiros comandos)

Um grande atrativo do uso de sistemas operacionais como o Ubuntu é o quão leves eles podem ser. Isso, é claro, tem suas desvantagens, como, por exemplo, a ausência frequente de uma GUI (Interface Gráfica do Usuário) ou o que também é conhecido como ambiente de trabalho que possamos usar para interagir com a máquina (a menos que ela esteja instalada). Grande parte da interação com esses sistemas se dá por meio do "Terminal".

O "Terminal" é puramente baseado em texto e pode ser intimidante no início. No entanto, se analisarmos alguns dos comandos, com o tempo, você rapidamente se familiarizará com o uso do terminal!

![[Pasted image 20250604205636.png]]

Precisamos ser capazes de executar funções básicas, como navegar até arquivos, exibir seus conteúdos e criar arquivos! Os comandos para isso são autoexplicativos (depois que você souber o que são, é claro...).

Vamos começar com dois dos primeiros comandos, que descrevi na tabela abaixo:

| **Comando** | **Descrição**                                           |
| ----------- | ------------------------------------------------------- |
| `echo`      | Produza qualquer texto que fornecemos                   |
| `whoami`    | Descubre com qual usuário estamos conectados no momento |

**Exemplo:**

![[Pasted image 20250604210204.png]]

Como mostrado no terminal acima, quando é usado o comando `echo` não é necessário usar aspas duplas, por exemplo, `echo Hello`. No entanto, a string deve ser colocada entre aspas duplas se um ou mais espaços estiverem presentes, por exemplo, `echo "Hello friend!"`.

O comando `whoami` pode ser usado para localizar o username do usuário logado na máquina.

![[Pasted image 20250604210427.png]]

---
# Interagindo com os arquivos do sistema

Para poder navegar na máquina em que você está conectado sem depender de um ambiente de desktop é muito importante saber mais alguns comandos do terminal.

| **Comando** | **Nome**                  | **Descrição**                                                                             |
| ----------- | ------------------------- | ----------------------------------------------------------------------------------------- |
| `ls`        | *listing*                 | Lista os arquivos e diretórios do diretório atual (ou de um diretório especificado).      |
| `cd`        | *change directory*        | Navega entre diretórios, alterando o diretório atual.                                     |
| `cat`       | *concatenate*             | Exibe o conteúdo de arquivos no terminal. Também pode ser usado para concatenar arquivos. |
| `pwd`       | *print working directory* | Mostra o caminho completo (absoluto) do diretório atual.                                  |

## Listando arquivos no diretório atual (`ls`)

Antes de fazermos qualquer coisa, como descobrir o conteúdo de arquivos ou pastas, é necessário saber o que existe em primeiro lugar. Isso pode ser feito usando o comando `ls` (abreviação de *"listing"* ou "listar").

![[Pasted image 20250604223806.png]]

No screenshot é possível ver os seguintes diretórios/pastas:

- ``Importante Files``
- ``My Documents``
- ``Notes``
- ``Pictures``

## Alterando o diretório atual (`cd`)

Agora que sabemos quais pastas existem, precisamos usar o comando `cd` (abreviação de *"change directory"*) para acessar esse diretório. Digamos que eu quisesse abrir o diretório "Imagens" - eu usaria "`cd Imagens`. Novamente, queremos descobrir o conteúdo desse diretório "Imagens" e, para isso, usaríamos `ls` novamente:

![[Pasted image 20250604224635.png]]

Neste caso, no diretório `Pictures` existem 4 fotos de cachorro.

## Exibindo o Conteúdo de um Arquivo (`cat`)

Embora saber sobre a existência de arquivos seja ótimo, não é tão útil a menos que consigamos visualizar o conteúdo deles.

"Cat" é a abreviação de concatenar e é uma maneira fantástica de exibir o conteúdo de arquivos (não apenas arquivos de texto!).

Na captura de tela abaixo, você pode ver como combinei o uso de "ls" para listar os arquivos dentro de um diretório chamado "Documentos":

![[Pasted image 20250604230432.png]]

Aplicamos alguns conhecimentos adquiridos anteriormente nesta tarefa para fazer o seguinte:

1. Usamos `ls` para nos informar quais arquivos estão disponíveis na pasta "Documents" desta máquina. Neste caso, ela se chama "todo.txt".
2. Em seguida, usamos `cat todo.txt` para concatenar/exibir o conteúdo deste arquivo "todo.txt", onde o conteúdo é "Aqui está algo importante para eu fazer mais tarde!".

> Dica profissional: Você pode usar cat para exibir o conteúdo de um arquivo dentro de diretórios sem precisar navegar até ele usando cat e o nome do diretório. Por exemplo, cat /home/ubuntu/Documentos/todo.txt

Às vezes, coisas como nomes de usuário, senhas, sinalizadores ou definições de configuração são armazenadas em arquivos onde "cat" pode ser usado para recuperá-los.

## Descobrindo o Caminho Completo para o Nosso Diretório de Trabalho Atual (`pwd`)

Você notará que, à medida que avança na navegação em sua máquina Linux, o nome do diretório em que você está trabalhando será listado em seu terminal.

É fácil perder a noção de onde exatamente estamos no sistema de arquivos, e é por isso que quero apresentar `pwd`. Isso significa imprimir diretório de trabalho.

Usando a máquina de exemplo anterior, estamos atualmente na pasta "Documents" — mas onde exatamente isso está no sistema de arquivos da máquina Linux? Podemos descobrir isso usando o comando `pwd`, como na captura de tela abaixo:

![[Pasted image 20250604230724.png]]

**Vamos analisar:**

1. Já sabemos que estamos em "Documents" graças ao nosso terminal, mas, neste momento, não temos ideia de onde "Documents" está armazenado para que possamos voltar a ele facilmente no futuro.
2. Usando o comando `pwd` (exibir diretório de trabalho) para encontrar o caminho completo do arquivo desta pasta "Documents".
3. O Linux nos informa, convenientemente, que este diretório "Documents" está armazenado em `/home/ubuntu/Documents` na máquina — ótimo saber!
4. Agora, no futuro, se estivermos em um local diferente, podemos simplesmente usar `cd /home/ubuntu/Documents` para alterar nosso diretório de trabalho para este diretório "Documentos".

---

# Referências

- [Linux Fundamentals Part 1](https://tryhackme.com/room/linuxfundamentalspart1)
