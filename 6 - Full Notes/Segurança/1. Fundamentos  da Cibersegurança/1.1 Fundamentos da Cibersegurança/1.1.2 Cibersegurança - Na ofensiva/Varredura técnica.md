2025-06-07 20:41

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Ping]] | [[Traceroute]] | [[Nmap]]

----
# Introdução



As técnicas de varredura desempenham um papel essencial na administração e na análise de rede de uma organização. Pense em como os invasores reúnem informações sobre computadores e redes. Investigando um dispositivo alvo em uma rede, um invasor pode querer saber mais sobre a configuração técnica do dispositivo. Ponde tentar descobrir informações como:

- Qual sistema operacional está em uso?
- Quais serviços estão sendo executados no dispositivo?
- Algum dos serviços é vulnerável a explorações bem conhecidas?

---
# Teste de ping

![[Pasted image 20250607205611.png]]

## Como funciona?

Um **teste de ping** mede o tempo que um pacote leva para viajar de um dispositivo ou servidor para outro. Um **pacote**, ou ping, é uma pequena quantidade de dados formatados de forma análoga à versão digita de um cartão postal.

Em um teste de ping, um dispositivo de varredura envia um pacote ICMP *(Internet Control Message Protocol)* para o endereço IP *(Internet Protocol)* do dispositivo alvo. Esse pacote de saída é chamado de pacote de **solicitação de eco**. Se o dispositivo de destino responder com um pacote de **resposta de eco**, o dispositivo de verificação saberá que o dispositivo de destino provavelmente está ativo e ligado.

## O que isso oferece?

Um teste de ping indica se uma máquina responde e, quando repetido em uma varredura, quantos dispositivos há em um rede.

Muitas vezes, as organizações utilizam um teste de ping para depurar problemas de rede. Ele identifica o status de um dispositivo. Ele também indica a "distância" de uma rede ou dispositivo utilizando uma propriedade conhecida como **tempo de ativação (TTL)** de um pacote. Cada roteador que encaminha o pacote em diante diminui o tempo de ativação por um.

>[!example] Exemplo
>Considere um pacote que começa com um TTL de 120. Se chegar ao destino com 108 restantes, então ele passou por 12 estágios. Você pode utilizar esse recurso na próxima verificação. No Windows, o teste ping pode ser executado pelo prompt de comando utilizando o seguinte comando: `ping target_name`

---
# Traceroute

## Como funciona?

![[Pasted image 20250607205643.png]]

**Traceroute** é outra ferramenta de diagnóstico de rede. Quando você executa um traceroute, o dispositivo de varredura envia pacotes para o dispositivo de destino. Esses pacotes têm TTLs crescente ou decrescentes. Quando um pacote está em trânsito o seu TTL diminui para zero, o dispositivo que está processando o pacote envia de volta uma mensagem de erro para o dispositivo de varredura, indicando que o pacote não atingiu o seu destino.

## O que isso oferece?

O comando traceroute pode ser utilizado para mapear uma rede e determinar quantos roteadores e switches há entre você e o seu destino. Um roteador é a conexão de hardware de uma rede com a internet. Um comutador integra todos os dispositivos em uma rede, incluindo o roteador, permitindo o compartilhamento contínuo e a transferência de dados entre eles.

>[!example] Exemplo
>Imagine que um alvo esteja a 12 saltos de distância. Se você enviar um pacote com TTL 11 em direção ao destino, o pacote falhará na etapa final do roteamento. O dispositivo de digitalização receberá um pacote de mensagem de erro e a mensagem revelará o endereço IP do dispositivo a 11 passos de distância. À medida que o TTL é reduzido a um após alguns novos testes, o comando traceroute produz uma lista completa dos nós da rede entre o scanner e o alvo. No Windows, você pode executar um traceroute com o seguinte comando: `tracert target_name`.

---
# Digitalização de portas

## Como funciona?

Na rede, os aplicativos são acessíveis externamente por meio de serviços em portas digitais. Uma porta é um ponto de conexão que envia ou recebe dados de um serviço de rede específico, como e-mail. Cada porta recebe um número no **Protocolo de Controle de Transmissão (TCP)**, uma coleção de protocolos de internet que possibilita criar e manter a comunicação entre dispositivos conectados à Internet. Cada porta também está associada a um endereço IP. A relação entre endereços IP e portas é como aquela entre um edifício e seus andares: um endereço IP é como um edifício e números de porta são como pisos diferentes nesse edifício.

O objetivo usual da verificação de portas é identificar as portas abertas de um servidor

- Um **servidor** é um dispositivo, como um servidor, estação de trabalho, laptop ou outro dispositivo inteligente, que pode se comunicar com outros dispositivos em uma rede e conceder acesso a dispositivos fora da rede.
    
- Uma **porta aberta** é aquela que aceita uma conexão. Considerando que o número da porta é como um andar em um prédio, uma porta aberta é como um andar que você pode acessar por meio de uma porta aberta.

Os atacantes querem encontrar e explorar portas abertas em hosts. Por outra lado, os administradores de rede desejam fechar ou bloquear essas portas, garantindo que os usuários legítimos ainda tenha acesso.

![[Pasted image 20250607210631.png]]

>Este diagrama retrata um scanner de porta verificando um servidor. O scanner testa uma porta de cada vez para determinar se um serviço específico está disponível na porta. No entanto, cada porta rejeita a conexão, o que significa que é uma porta fechada.

O scanner relata que uma porta está **fechada** se a porta rejeitar a conexão ou **filtrada** se o host não apresentar resposta à verificação. Nenhuma resposta significa que um filtro de pacote, um tipo de firewall, está bloqueando acesso à porta.

## O que isso oferece?

Analisando a lista de portas conhecidas de um host, um scanner geralmente pode determinar para que o proprietário do host utiliza o dispositivo. O TCP contém 65.536 portas. As portas TCP de 0 a 1.023 são chamadas de **portas conhecidas**: cada uma tem um serviço específico associado e essa associação é reconhecida internacionalmente. Algumas das portas de 1.024 a 49.151 também podem ter usos de interesse registrados oficialmente.

>[!example] Exemplo
>A atividade HTTP da web sempre ocorre na porta TCP 80. Se uma varredura revelar que a porta 80 está aberta, o investigador saberá que algum aplicativo baseado na web pode a estar utilizando. Outro exemplo: o compartilhamento de arquivos do Windows ocorre na porta TCP 445. Se os invasores souberem que essa porta está aberta, poderão tentar explorá-la com malware. Ataques de ransomware famosos, como os ataques WannaCry, tiveram como alvo esta porta.
>
>Uma porta notável fora da lista de portas conhecidas é a porta TCP 3389, a porta padrão para o Microsoft Remote Desktop Protocol (RDP). Se os invasores souberem que essa porta está aberta e disponível, poderão tentar hackear o software de desktop remoto.

---
# Verificação de vulnerabilidades

## Como funciona?

![[Pasted image 20250607211812.png]]

Outra forma de teste é a verificação de vulnerabilidades. Um de seus recursos é a **verificação dinâmica**, que simula técnicas de hackers, como injeção de SQL, para descobrir vulnerabilidades a serem exploradas.

Outras técnicas de verificação de vulnerabilidade padrão incluem detecção de versão e sistema operacional:

- **detecção de versão** revela o número de versão do software, como o servidor web Apache, em execução no host.
- **detecção de sistema operacional** revela o sistema operacional do dispositivo, como o macOS.

## O que isso oferece?

A verificação de vulnerabilidades é uma ferramenta poderosa para as organizações identificarem vulnerabilidades em sua rede e para os atacantes encontrarem possíveis vítimas. Algumas organizações executam essas verificações periodicamente para identificar erros que precisam ser corrigidos.

>[!example] Exemplo
>Um scanner pode tentar conectar a um servidor e verificar se está executando uma versão desatualizada de um aplicativo. Se o aplicativo estiver desatualizado com uma vulnerabilidade conhecida, o scanner poderá tentar explorar a vulnerabilidade para confirmar sua existência e relatar esse achado.

## Observação importante

Esteja ciente de que a verificação dinâmica pode executar automaticamente ações consideradas ilegais em alguns países. Digitalize um alvo somente se o proprietário tiver dado consentimento. Uma verificação de vulnerabilidade de rede será frequentemente interpretada como o estágio de planejamento de um ataque.

---
# Sistema de busca para a internet

Outra ferramenta para verificação técnica é o [sistema de busca Shodan](https://www.shodan.io/). O site do sistema descreve a ferramenta como "o primeiro sistema de busca do mundo para dispositivos conectados à Internet". Ela é interessante para invasores mal-intencionados e pesquisadores de segurança. Oferece um vasto catálogo de resultados de verificação coletados, abrangendo bilhões de registros. As pessoas podem utilizar esses registros armazenados para rastrear aplicativos em escala em todo mundo.

---
# Varredura de rede

**As varreduras de rede** reúnem informações sobre uma rede visando um host. Os administradores de rede e de sistemas contam com varreduras de rede para avaliar o status e a segurança da rede de sua organização. Infelizmente os ciberataques podem utilizar essas mesmas ferramentas para fins maliciosos.

Há muitos aplicativos de digitalização em rede, mas o scanner mais conhecido é o Nmap.

[Nmap](https://nmap.org/), abreviação de Network Mapper, é um scanner de rede gratuito e de código aberto disponível para Windows, macOS, Linux e outros sistemas operacionais. Embora a varredura de portas seja seu recurso principal, o Nmap oferece outros recursos valiosos para investigar redes.

## Sobre o Nmap

- Ele pode revelar o caminho da rede do dispositivo de varredura para host, incluindo todos os outros hosts encontrados ao longo do caminho.
- Ele pode realizar detecção de versão e sistema operacional.
- Ele pode identificar firewalls em uso.

O Nmap é um programa de linha de comando, mas a maioria das versões também inclui o Zenmap, a interface gráfica oficial do usuário (GUI) do Nmap. O [Zenmap](https://nmap.org/zenmap/) facilita o aprendizado do Nmap para iniciantes. Com o Nmap, você deve determinar o comando preciso necessário para realizar sua varredura, e o número de opções e requisitos sintáticos pode tornar isso desafiador. Mas com o Zenmap, você pode simplesmente selecionar opções de uma interface fácil de utilizar para personalizar sua varredura. E se você ainda quiser aprender as opções de linha de comando do Nmap, o Zenmap exibe o comando e as opções reais do Nmap por trás da varredura.

---
# IA na varredura técnica

A inteligência artificial (IA) tornou-se valiosa para a varredura de rede. Com os algoritmos de aprendizado de máquina (ML), os scanner de rede podem realizar análises mais profundas e úteis.

- Os verificadores podem analisar e categorizar vulnerabilidades de rede de forma independente.
- Os verificadores podem priorizar vulnerabilidades com base em sua gravidade.
- Os verificadores podem aprender com verificações passadas  e identificar padrões e tendências para prever ameaças futuras.

A IA também pode simplificar o processo de varredura. Ela pode reduzir o tempo necessário para examinar grandes redes e reduzir a possibilidade de erros humanos.

Um exemplo de uma ferramenta de varredura de rede orientada por IA é o QRadar® Advisor da IBM com o aplicativo Watson™. Ela analisa incidentes de segurança, identifica ameaças em potencial e apresenta insights acionáveis. O QRadar Advisor utiliza ML e IA para analisar grandes quantidades de dados, investigar ofensas e eliminar falsos positivos. Consequentemente, os analistas estão livres para se concentrarem em ameaças confirmadas, otimizar o tempo e recursos.

---
# Referências

- [[Transcrição de simulação - Execute o reconhecimento de rede com ferramentas de varredura de rede.pdf]]
