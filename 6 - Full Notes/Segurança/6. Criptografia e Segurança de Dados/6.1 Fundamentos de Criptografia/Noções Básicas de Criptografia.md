**2025-07-01 17:37**

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Criptografia]]

----
# Introdução

A criptografia estabelece a base para o nosso mundo digital. Enquanto os protocolos de rede possibilitaram a comunicação entre dispositivos espalhados pelo mundo, a criptografia tornou possível a confiança nessa comunicação.

![[Pasted image 20250701174029.png]]

---
# Importância da Criptografia

O objetivo final da criptografia é garantir a comunicação segura na presença de adversários. O termo "seguro" inclui a confidencialidade e a integridade dos dados comunicados. A criptografia pode ser definida como a prática e o estudo de técnicas para comunicação segura e proteção de dados onde esperamos a presença de adversários e terceiros. Em outras palavras, esses adversários não devem ser capazes de divulgar ou alterar o conteúdo das mensagens.

A criptografia é usada para proteger a confidencialidade, a integridade e a autenticidade. Hoje em dia, criptografia é usada diariamente e quase certamente. Considerando os seguintes cenários em que a criptografia é presente:

- Quando você faz login no TryHackMe, suas credenciais são criptografadas e enviadas ao servidor para que ninguém possa recuperá-las bisbilhotando sua conexão.
- Quando você se conecta via SSH, seu cliente SSH e o servidor estabelecem um túnel criptografado para que ninguém possa espionar sua sessão.
- Ao realizar operações bancárias online, seu navegador verifica o certificado do servidor remoto para confirmar que você está se comunicando com o servidor do seu banco e não com o de um invasor.
- Ao baixar um arquivo, como verificar se ele foi baixado corretamente? A criptografia oferece uma solução por meio de funções de hash para confirmar que o arquivo é idêntico ao original.

Raramente é necessário interagir diretamente com a criptografia, mas suas soluções e implicações estão por toda parte no mundo digital. Considerando o caso em que uma empresa deseja lidar com informações de cartão de crédito e processar transações relacionadas. Ao lidar com cartões de crédito, a empresa deve seguir e aplicar o Padrão de Segurança de Dados da Indústria de Cartões de Pagamento (PCI DSS). Nesse caso, o PCI DSS garante um nível mínimo de segurança para armazenar, processar e transmitir dados relacionados aos créditos do cartão. Ao consultar o [PCI DSS para Grandes Organizações](https://listings.pcisecuritystandards.org/documents/PCI_DSS_for_Large_Organizations_v1.pdf), é possível notar que os dados devem ser criptografados tanto durante o armazenamento (em repouso) quanto durante a transmissão (em movimento).

Da mesma forma que o manuseio de dados de cartão de pagamento exige a conformidade com o PCI DSS, o manuseio de registros médicos exige a conformidade com seus respectivos padrões. Ao contrário dos cartões de crédito, os padrões para o manuseio de registros médicos variam de um país para outro. Exemplos de leis e regulamentos que devem ser considerados ao lidar com registros médicos incluem HIPAA (Lei de Portabilidade e Responsabilidade de Seguros de Saúde) e HITECH (Tecnologia da Informação em Saúde para Saúde Econômica e Clínica) nos EUA, GDPR (Regulamento Geral sobre a Proteção de Dados) na UE e DPA (Lei de Proteção de Dados) no Reino Unido. Embora a lista não seja exaustiva, ela dá uma ideia dos requisitos legais que os provedores de saúde devem considerar dependendo do país. Essas leis e regulamentos mostram que a criptografia é uma necessidade que deve estar presente, embora geralmente oculta do acesso direto do usuário

---
# Texto Simples para Texto Cifrado

Vamos começar com uma ilustração antes de introduzir os termos-chave. Começamos com o texto simples que queremos criptografar. O texto simples são os dados legíveis; pode ser qualquer coisa, desde um simples "olá", uma foto de gato, informações de cartão de crédito ou registros médicos. Da perspectiva da criptografia, todas essas são mensagens de "texto simples" aguardando para serem criptografadas. O texto simples é passado pela função de criptografia juntamente com uma chave apropriada; a função de criptografia retorna um texto cifrado. A função de criptografia faz parte da cifra; uma cifra é um algoritmo para converter um texto simples em um texto cifrado e vice-versa.

A função de criptografia recebe o texto simples e a chave como entrada e retorna o texto cifrado como saída.

![[Pasted image 20250701174817.png]]

Para recuperar o texto simples, precisamos passar o texto cifrado juntamente com a chave apropriada por meio da função de descriptografia, o que nos daria o texto simples original. 

![[Pasted image 20250701174835.png]]

- **Texto simples** é a mensagem ou dado original e legível antes de ser criptografado. Pode ser um documento, uma imagem, um arquivo multimídia ou qualquer outro dado binário.

- **Texto cifrado** é a versão embaralhada e ilegível da mensagem após a criptografia. Idealmente, não podemos obter nenhuma informação sobre o texto simples original, exceto seu tamanho aproximado.

- **Cifra** é um algoritmo ou método para converter texto simples em texto cifrado e vice-versa. Uma cifra geralmente é desenvolvida por um matemático.

- **Chave** é uma sequência de bits que a cifra usa para criptografar ou descriptografar dados. Em geral, a cifra usada é de conhecimento público; no entanto, a chave deve permanecer secreta, a menos que seja a chave pública na criptografia assimétrica. Abordaremos a criptografia assimétrica em uma tarefa posterior.

- **Criptografar** é o processo de conversão de texto simples em texto cifrado usando uma cifra e uma chave. Ao contrário da chave, a escolha da cifra é revelada.

- A **descriptografia** é o processo inverso da criptografia, convertendo o texto cifrado de volta em texto simples usando uma cifra e uma chave. Embora a cifra seja de conhecimento público, recuperar o texto simples sem o conhecimento da chave deveria ser impossível (inviável).

---
# Cifras Históricas

A história da criptografia é longa e remonta ao antigo Egito, em 1900 a.C. No entanto, uma das cifras históricas mais simples é a **Cifra de César**, do século I a.C. A ideia é simples: deslocar cada letra por um determinado número para criptografar a mensagem.

**Exemplo:**

- Texto simples: `TRYHACKME`
- Chave: 3 (Suponha que seja um deslocamento de 3 para a direita.)
- Cifra: Cifra de César

Podemos facilmente descobrir que T se torna W, R se torna U, Y se torna B e assim por diante. Como você notou, ao chegarmos a Z, começamos tudo de novo, como mostrado na figura abaixo. Consequentemente, obtemos o texto cifrado de `WUBKDFNPH`.

![[Pasted image 20250701175512.png]]

A Cifra de César desloca cada letra por um determinado número para criptografar a mensagem.

Para descriptografar, precisamos das seguintes informações:

- Texto cifrado: `WUBKDFNPH`
- Chave: 3
- Cifra: Cifra de César

![[Pasted image 20250701175610.png]]

Para a criptografia, deslocamos três vezes para a direita; para a descriptografia, deslocamos três vezes para a esquerda e recuperamos o texto original, como ilustrado na imagem acima. No entanto, se alguém lhe der um texto cifrado e disser que ele foi criptografado usando a Cifra de César, recuperar o texto original seria uma tarefa trivial, pois existem apenas 25 chaves possíveis. O alfabeto inglês tem 26 letras, e deslocar 26 manterá a letra inalterada; portanto, 25 chaves válidas para criptografia com a Cifra de César. A figura abaixo mostra como a descriptografia será bem-sucedida ao tentar todas as chaves possíveis; neste caso, recuperamos a mensagem original com Chave = 5. Consequentemente, pelos padrões atuais, onde a cifra é publicamente conhecida, a Cifra de César é considerada insegura.

A Cifra de César é suscetível a ataques de força bruta.

![[Pasted image 20250701175748.png]]

Existem muito mais cifras históricas em filmes e livros de criptografia. Exemplos incluem:

- A cifra de Vigenère do século XVI
- A máquina Enigma da Segunda Guerra Mundial
- O bloco de notas de uso único da Guerra Fria

---
# Tipos de Criptografia

As duas principais categorias de criptografia são simétrica e assimétrica.

## Criptografia Simétrica

A **criptografia simétrica**, também conhecida como **criptografia simétrica**, usa a mesma chave para criptografar e descriptografar os dados. Manter a chave em segredo é essencial; também é chamada de **criptografia de chave privada**. Além disso, comunicar a chave aos destinatários pode ser desafiador, pois requer um canal de comunicação seguro. Manter o sigilo da chave pode ser um desafio significativo, especialmente se houver muitos destinatários. O problema se torna mais grave na presença de um adversário poderoso; considere a ameaça de espionagem industrial, por exemplo.

A criptografia simétrica usa a chave secreta compartilhada para criptografar e descriptografar.

![[Pasted image 20250701180257.png]]

Considere o caso simples em que você criou um documento protegido por senha para compartilhá-lo com seu colega. Você pode facilmente enviar o documento criptografado por e-mail para ele, mas provavelmente não poderá enviar a senha por e-mail. O motivo é que qualquer pessoa com acesso à sua caixa de correio acessaria tanto o documento protegido por senha quanto sua senha. Portanto, você precisa pensar em uma maneira diferente, ou seja, um canal, para compartilhar a senha. A menos que você pense em um canal seguro e acessível, uma solução seria se encontrar pessoalmente e comunicar a senha.

Exemplos de criptografia simétrica são DES (Padrão de Criptografia de Dados), 3DES (DES Triplo) e AES (Padrão de Criptografia Avançada).

- O **DES** foi adotado como padrão em 1977 e utiliza uma chave de 56 bits. Com o avanço da capacidade computacional, em 1999, uma chave DES foi quebrada com sucesso em menos de 24 horas, motivando a mudança para o 3DES.

- O **3DES** é o DES aplicado três vezes; consequentemente, o tamanho da chave é de 168 bits, embora a segurança efetiva seja de 112 bits. O 3DES era mais uma solução ad hoc quando o DES deixou de ser considerado seguro. O 3DES foi descontinuado em 2019 e foi substituído pelo AES; no entanto, ainda pode ser encontrado em alguns sistemas legados.

- O **AES** foi adotado como padrão em 2001. Seu tamanho de chave pode ser de 128, 192 ou 256 bits.

Existem muitas outras cifras de criptografia simétrica usadas em diversas aplicações; no entanto, elas não foram adotadas como padrões.

## Criptografia Assimétrica

Ao contrário da criptografia simétrica, que usa a mesma chave para criptografar e descriptografar, a **criptografia assimétrica** usa um par de chaves, uma para criptografar e a outra para descriptografar, como mostrado na ilustração abaixo. Para proteger a confidencialidade, a criptografia assimétrica, ou criptografia assimétrica, criptografa os dados usando a chave pública; por isso, também é chamada de **criptografia de chave pública**.

![[Pasted image 20250701180638.png]]

Exemplos são RSA, Diffie-Hellman e criptografia de curva elíptica (ECC). As duas chaves envolvidas no processo são chamadas de chave pública e chave privada. Dados criptografados com a chave pública podem ser descriptografados com a chave privada. Sua chave privada precisa ser mantida em sigilo, daí o nome.

A criptografia assimétrica tende a ser mais lenta e muitas cifras de criptografia assimétrica usam chaves maiores do que a criptografia simétrica. Por exemplo, a RSA usa chaves de 2048 bits, 3072 bits e 4096 bits; 2048 bits é o tamanho mínimo de chave recomendado. A Diffie-Hellman também tem um tamanho mínimo de chave recomendado de 2048 bits, mas usa chaves de 3072 bits e 4096 bits para maior segurança. Por outro lado, a ECC pode alcançar segurança equivalente com chaves mais curtas. Por exemplo, com uma chave de 256 bits, a ECC fornece um nível de segurança comparável a uma chave RSA de 3072 bits.

A criptografia assimétrica baseia-se em um grupo específico de problemas matemáticos que são fáceis de calcular em uma direção, mas extremamente difíceis de reverter. Nesse contexto, extremamente difícil significa praticamente inviável. Por exemplo, podemos nos basear em um problema matemático que levaria muito tempo, milhões de anos, para ser resolvido usando a tecnologia atual.

Abordaremos várias cifras de criptografia assimétrica na próxima sala. Por enquanto, o importante a ser observado é que a criptografia assimétrica fornece uma chave pública que você compartilha com todos e uma chave privada que você mantém protegida e secreta.

---
# Matemática Básica

Os blocos de construção da criptografia moderna residem na matemática. Para demonstrar alguns algoritmos básicos, abordaremos duas operações matemáticas usadas em vários algoritmos:

- Operação XOR
- Operação Módulo

## Operação XOR

XOR, abreviação de "OU exclusivo", é uma operação lógica em aritmética binária que desempenha um papel crucial em diversas aplicações de computação e criptografia. Em binário, o XOR compara dois bits e retorna 1 se os bits forem diferentes e 0 se forem iguais, conforme mostrado na tabela verdade abaixo. Essa operação é frequentemente representada pelo símbolo ⊕ ou ^.

| A   | B   | A ⊕ B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 0     |

Se esta é a primeira vez que você trabalha com uma tabela verdade, ela mostra todos os resultados possíveis. A tabela verdade XOR acima indica todos os quatro casos: 0 ⊕ 0 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1 e 1 ⊕ 1 = 0.

Considerando um exemplo em que é necessário aplicar XOR aos números binários 1010 e 1100. Neste caso é realizado através de uma operação bit a bit: 1 ⊕ 1 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1 e 0 ⊕ 0 = 0, resultando em 0110.

O XOR possui diversas propriedades interessantes que o tornam útil em criptografia e detecção de erros. Uma propriedade fundamental é que aplicar XOR a um valor com ele mesmo resulta em 0, e aplicar XOR a qualquer valor com 0 o mantém inalterado. Isso significa que A ⊕ A = 0 e A ⊕ 0 = A para qualquer valor binário A. Além disso, XOR é comutativo, ou seja, A ⊕ B = B ⊕ A. E é associativo, ou seja, (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C).

Considerando os valores binários **P** ​​e **K**, onde: 

- P é o **texto simples**
- K é a **chave secreta**. 
- O texto cifrado é **C = P ⊕ K**.

Agora, se conhecemos C e K, podemos recuperar P. 

1. Começamos com C ⊕ K = (P ⊕ K) ⊕ K.
2. Mas sabemos que (P ⊕ K) ⊕ K = P ⊕ (K ⊕ K) porque XOR é associativo. Além disso, sabemos que K ⊕ K = 0.
3. Consequentemente, (P ⊕ K) ⊕ K = P ⊕ (K ⊕ K) = P ⊕ 0 = P.
4. Em outras palavras, XOR serviu como um algoritmo de criptografia simétrica simples. Na prática, é mais complicado, pois precisamos de uma chave secreta tão longa quanto o texto simples.

### Exemplo

- Qual o resultado de 1001 ⊕ 1010?

| 1º Bit | 2º Bit | Resultado (XOR) |
| ------ | ------ | --------------- |
| 1      | 1      | 0               |
| 0      | 0      | 0               |
| 0      | 1      | 1               |
| 1      | 0      | 1               |

## Operação de Módulo

Outra operação matemática que encontramos frequentemente em criptografia é o operador de módulo, comumente escrito como *%* ou *mod*. O operador de módulo, *X%Y*, é o resto quando X é dividido por Y. Em nossos cálculos diários, focamos mais no resultado da divisão do que no resto. O resto desempenha um papel significativo na criptografia.

É precisa trabalhar com números grandes ao resolver alguns exercícios de criptografia. Se sua calculadora falhar, é sugerido usar uma linguagem de programação como Python. Python possui um tipo `int` integrado que pode lidar com inteiros de tamanho arbitrário e alterna automaticamente para tipos maiores conforme necessário. Muitas outras linguagens de programação têm bibliotecas dedicadas para inteiros grandes. Se preferir fazer seus cálculos online, considere o [WolframAlpha](https://www.wolframalpha.com).

Vamos considerar alguns exemplos.

- 25%5 = 0 porque 25 dividido por 5 é 5, com resto 0, ou seja, 25 = 5 × 5 + 0
- 23%6 = 5 porque 23 dividido por 6 é 3, com resto 5, ou seja, 23 = 3 × 6 + 5
- 23%7 = 2 porque 23 dividido por 7 é 3, com resto 2, ou seja, 23 = 3 × 7 + 2

Uma coisa importante a lembrar sobre o módulo é que ele não é reversível. Se nos for dada a equação x%5 = 4, infinitos valores de x a satisfariam.

A operação de módulo sempre retorna um resultado não negativo menor que o divisor. Isso significa que, para qualquer inteiro a e inteiro positivo n, o resultado de a%n estará sempre no intervalo de 0 a n − 1.

### Exemplos

- O que é 118613842%9091?

$$
118613842 mod 9091
$$
Ou seja, queremos saber **qual é o resto da divisão de 118.613.842 por 9.091**

#### Passo a Passo:

1. **Dividindo** 118.613.842 por 9.091:

$$
118613842 ÷ 9091 ≈ 13052,63
$$
Ou seja, o quociente inteiro é 13.052 (a parte inteira da divisão).

2. Agora, **multiplicamos** esse quociente pelo divisor:

$$
13.052 × 9.091 = 118610732
$$
3. Agora, **subtraímos** esse valor do número original para encontrar o **resto**:

$$
118613842−118610732=3110​
$$
- Resposta final:

O resto da divisão de 118.613.842 por 9.091 é **3110**.