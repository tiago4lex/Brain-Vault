2025-06-05 06:40

Status: #developed #Linux 

Tags: [[Linux]] | [[find]] | [[grep]]

----
# Procurando por arquivos

Embora não pareça até agora, um dos recursos mais vantajosos do Linux é a sua eficiência. Dito isso, você só pode ser tão eficiente quanto estiver familiarizado com ele, é claro. À medida que você interage com sistemas operacionais como o Ubuntu ao longo do tempo, comandos essenciais como os que já abordamos começarão a se tornar memória muscular.

Uma maneira fantástica de mostrar o quão eficiente você pode ser com sistemas como este é usar um conjunto de comandos para pesquisar rapidamente por arquivos em todo o sistema ao qual nosso usuário tem acesso. Não há necessidade de usar `cd` e `ls` constantemente para descobrir o que está onde. Em vez disso, podemos usar comandos como `find` para automatizar coisas como essa para nós!

É aqui que o Linux começa a se tornar um pouco mais intimidador de abordar.

## Usando `Find`

O comando `find` é fantástico no sentido de que pode ser usado tanto de forma simples quanto complexa, dependendo do que você deseja fazer exatamente. No entanto, vamos nos ater ao básico primeiro.

Veja o trecho abaixo: podemos ver uma lista de diretórios disponíveis para nós:

![[Pasted image 20250604231401.png]]

1. Desktop
2. Documents
3. Pictures
4. folder1

Agora, é claro, diretórios podem conter ainda mais diretórios. Torna-se uma dor de cabeça quando temos que procurar em cada um deles apenas para tentar encontrar arquivos específicos. Podemos usar o comando `find` para fazer exatamente isso!

Vamos começar de forma simples e assumir que já sabemos o nome do arquivo que estamos procurando — mas não conseguimos lembrar onde ele está exatamente! Neste caso, estamos procurando por "passwords.txt".

Se nos lembrarmos do nome do arquivo, podemos simplesmente usar `find -name passwords.txt`, onde o comando procurará em todas as pastas do nosso diretório atual por aquele arquivo específico, assim:

![[Pasted image 20250604231555.png]]

O comando "Find" conseguiu encontrar o arquivo — ele está localizado em folder1/passwords.txt — ótimo. Mas digamos que não sabemos o nome do arquivo ou queremos procurar por todos os arquivos com uma extensão como ".txt". O comando "Find" também nos permite fazer isso!

Podemos simplesmente usar o que é conhecido como curinga (`*`) para procurar por qualquer coisa que tenha .txt no final. No nosso caso, queremos encontrar todos os arquivos .txt que estão no nosso diretório atual. Vamos construir um comando como `find -name *.txt`. Onde o comando "Find" conseguiu encontrar todos os arquivos .txt e nos forneceu a localização de cada um:

![[Pasted image 20250604231746.png]]

O Find conseguiu encontrar:

- "passwords.txt" localizado em "folder1"
- "todo.txt" localizado em "Documents"

## Usando o `grep`

Outro ótimo utilitário que vale a pena conhecer é o uso do `grep`. O comando `grep` nos permite pesquisar o conteúdo de arquivos em busca de valores específicos que estejamos procurando.

Veja, por exemplo, o log de acesso de um servidor web. Neste caso, o access.log de um servidor web possui 244 entradas.

![[Pasted image 20250604232005.png]]

Usar um comando como `cat` não vai funcionar muito bem aqui. Digamos, por exemplo, que quiséssemos pesquisar neste arquivo de log para ver as coisas que um determinado usuário/endereço IP visitou? Examinar 244 entradas não é tão eficiente, considerando que queremos encontrar um valor específico.

Podemos usar o comando `grep` para pesquisar todo o conteúdo deste arquivo em busca de quaisquer entradas do valor que estamos procurando. Seguindo o exemplo do log de acesso de um servidor web, queremos ver tudo o que o endereço IP "81.143.211.90" visitou (observe que isso é fictício).

![[Pasted image 20250604232112.png]]

`grep` pesquisou neste arquivo e nos mostrou todas as entradas do que fornecemos e que estão contidas neste arquivo de log para o IP.

---

# Referências

- [Linux Fundamentals Part 1](https://tryhackme.com/room/linuxfundamentalspart1)
