2025-06-10 22:43

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Criptografia]]

----
# Introdução

A criptografia é fundamental para conceitos vitais de segurança da informação e todos os profissionais de segurança cibernética devem entendê-la para serem bem-sucedidos.

---
# O que é criptografia?

> [!note] Definição
> Criptografia são os principais, meios e métodos de transformação de dados para ocultar seu conteúdo, evitar seu uso não autorizado ou evitar modificações não detectadas.
> 
>> - [Instituto Nacional de Padrões e Tecnologia](https://csrc.nist.gov/glossary/term/cryptography)

Um dos objetivos mais importantes da segurança cibernética é manter os dados **confidenciais**. Manter e compartilhar segredos tem sido um desafio há milhares de anos. Embora os métodos para preservar a confidencialidade tenham mudado consideravelmente com o passar dos anos, o objetivo permanece exatamente o mesmo.

----
# Definição de comunicações seguras

Para ilustrar os principais conceitos de criptografia, os profissionais de segurança cibernética geralmente utilizam três personagens fictícios: **Alice**, **Bob** e **Eve**. Alice e Bob querem se comunicar com segurança, mas Eve quer escutar a conversa.

![[Pasted image 20250610225038.png]]

Comunicações seguras e confiáveis têm três propriedades: confidencialidade, autenticidade e integridade.

### **Confidencialidade**

- Alice pode enviar uma mensagem para Bob sem Eve entender o conteúdo. A mensagem permanece privada.

### **Autenticidade**

- Eve não pode enviar uma mensagem para Bob alegando ser Alice. A autenticidade garante que a falsificação ou representação seja impossível.

### **Integridade**

Se a Eve modificar uma mensagem entre Alice e Bob, o destinatário poderá detectar que a mensagem foi modificada. Observe que você pode adulterar as mensagens sem saber o conteúdo. Por exemplo, as pessoas podem falar alto para interromper uma conversa presencial em um idioma que não entendem.

## Conclusão

A obtenção dessas três propriedades ocorre por meio de vários algoritmos matemáticos e outras técnicas. Historicamente, as técnicas incluíam caixas trancadas e selos de cera.

---
# Criptografia

Um método padrão para preservar a confidencialidade de uma mensagem é criptografia. **Criptografia** é o processo de conversão de uma mensagem em algo compreensível somente para quem dispõe uma chave de descriptografia para reverter o processo. Uma mensagem convertida em um estado ilegível é **criptografada**.

Quando você criptografa dados, utiliza uma cifra. Uma **cifra** é um conjunto de transformações que converte **texto simples**, os dados inteligíveis e legíveis por humanos, em **texto** cifrado, a forma criptografada dos dados. Para converter o texto simples, a cifra segue um **chave**, o mapa das transformações a serem feitas.

Em um nível mais alto, a criptografia moderna vem em duas formas: simétrica e assimétrica.

## **Criptografia simétrica**

Na **criptografia simétrica**, o algoritmo para criptografar informações utiliza a mesma chave que o processo de descriptografia. A criptografia simétrica é rápida e fácil de implementar. O remetente e o destinatário precisam ter acesso à mesma chave, semelhante a uma senha ou segredo compartilhado, para mantar um link de informações privadas.

>[!example] Exemplo
>Um exemplo simples é uma cifra baseada em rotação na qual os caracteres são deslocados para cima ou para baixo em um número fixo de posições no alfabeto. O número de posições para avançar e retroceder funciona como a chave. Se o remetente usar uma chave de +1 , ele deslocará os caractere uma posição à frente e, em seguida, o receptor usará um deslocamento de -1 para receber a mensagem original.
>
>Na cifra a seguir, a palavra *HOLIDAY* está criptografada por um deslocamento de +1 no alfabeto passando a *IPMJEBZ*.

![[Pasted image 20250615104849.png]]

O ***Advanced Encryption Standard (AES)*** é um algoritmo comumente utilizado em criptografia simétrica. Ele utiliza uma chave secreta para transformar texto simples em texto cifrado. As organizações utilizam o AES para proteger dados confidenciais, como senhas e transações financeiras.

## **Criptografia assimétrica**

Na **criptografia assimétrica**, também conhecida como criptografia de chave pública, é utilizado uma chave para criptografar dados e outra chave para descriptografá-los. Essas chaves são conhecidas como **chaves públicas** e **chaves privadas** e você as gera simultaneamente. É possível compartilhar a chave pública com outras pessoas. Qualquer pessoa com uma cópia dessa chave pode utilizá-la para criptografar uma mensagem antes de enviá-la para você. Mas a descriptografia dessa mensagem exige o uso da chave privada, que você deve manter em segredo.

>[!example] Exemplo
>No diagrama a seguir, Alice é o remetente e Bob é o destinatário. O diagrama representa o processo de transmissão.
>
>1. Alice criptografa uma mensagem com uma chave pública de Bob. Depois que a mensagem for criptografada, ela só poderá ser descriptografada com a chave privada de Bob.
>2. Alice envia a mensagem criptografada para Bob.
>3. Bob descriptografa a mensagem com sua chave privada.
>4. Finalmente, Bob pode ler a mensagem.
>
>Bob não deve compartilhar sua chave privada com ninguém. Caso contrário, outras pessoas poderão ler todas as mensagens recebidas.

![[Pasted image 20250615105542.png]]

O principal benefício da criptografia assimétrica é que as organizações podem se comunicar de forma segura com uma entidade com a qual elas não trocaram uma chave anteriormente. Além disso, esse tipo de criptografia ajuda a garantir que uma mensagem seja enviada ao receptor correto.

>[!example] Exemplo
>Um benefício da criptografia assimétrica vem das compras on-line. Você pode comprar produtos de lojas sem ir fisicamente ao local para criar uma chave simétrica exclusiva e compartilhada.
>
>Se a criptografia simétrica fosse a única opção, a chave simétrica acordada seria necessária para criptografar a descriptografar todas as transações futuras entre você e a loja.
>
>Em contrapartida, o uso da criptografia assimétrica é conveniente e economiza tempo porque você não precisa se encontrar pessoalmente. Sem esse benefício, as compras on-line seguras são praticamente impossíveis.

---
# Criptografia Quântica

Os computadores atuais não têm poder e estabilidade para decifrar as tecnologias modernas de criptografia. Mas a computação quântica pode ser capaz de fazer isso em breve.

>[!quote]
>**Computação quântica** é uma tecnologia em rápida evolução que aproveita as leis da mecânica quântica para resolver problemas complexos demais para computadores clássicos.
>
>[O que é computação quântica?(opens in a new tab)](https://www.ibm.com/topics/quantum-computing) _IBM_

A computação quântica processa informações utilizando mecânica quântica. Consequentemente, fazem cálculos complexos muito mais rápido do que os métodos de computação tradicionais.

![[Pasted image 20250615110631.png]]

Então, qual a relação da computação quântica com a criptografia? É uma ameaça nas mãos dos ciberatacantes. Sua capacidade de fatorar grandes números primos, base da criptografia atual, pode tornar os métodos de criptografia atuais ineficazes. As organizações precisam de estratégias novas para se defenderem contra essa nova ameaça. Entra então em a cena a criptografia com resistência quântica, ou *quantum-safe*.

**Criptografia com resistência quântica** refere-se a métodos e protocolos de segurança resistentes a ataques de computação quântica. Os especialistas propuseram muitas alternativas de criptografia pós-quântica para se defenderem contra ataques de computação quântica. 

## **Criptografia baseada em reticulados**

A **criptografia baseada em reticulados** utiliza estruturas geométricas multidimensionais para criptografar dados, criando um quebra-cabeça de difícil solução até mesmo para computadores quânticos.

## **Criptografia baseada em Hash**

A **criptografia baseada em hash** transforma dados em uma string de caracteres utilizando uma função de hash. O resultado é uma saída única cuja engenharia reversa é difícil até mesmo para computadores quânticos.

## **Criptografia multivariada**

**Criptografia multivariada** utiliza várias equações matemáticas e varáveis diferentes ao mesmo tempo. Essa abordagem é altamente complexa e difícil para os computadores quânticos quebrarem.

## **Criptografia baseada em código**

A **criptografia baseada em código** transforma dados em mensagens codificadas difíceis de decodificar sem o algoritmo correto, mesmo para computadores quânticos.

---
