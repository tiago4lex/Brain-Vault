2025-06-06 14:57

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[DoS]] | [[DDoS]] | [[Phishing]] | [[Spear Phishing]] | [[Malware]] | [[MitM]] | [[SQL Injection]] | [[IA]]

----
# Introdução

Os invasores podem usar vários métodos para entrar explorar sistemas. Alguns ataques têm como alvo vulnerabilidades na tecnologia. Outros exploram vulnerabilidades em humanos, especificamente as formas com que os humanos interagem com os sistemas.

---
# Ataque DoS *(Denial of Service)*

- Um **ataque de negação de serviço (DoS)** é qualquer ataque que cause interrupção completa ou parcial do sistema.

- O DoS pode ocorrer quando uma pessoa ou sistema inunda um site ou serviço online com muito tráfego de rede, como um engarrafamento em uma estrada. Esse excesso de tráfego faz com que o site ou serviço fique lento ou desligue completamente, negando acesso a usuários legítimos.

- O DDoS também pode ocorrer quando o tráfego consome recursos suficientes do sistema para desacelerar ou travar o sistema.

>[!example] Exemplo
>O atacante utiliza um ataque de um bilhão de risadas, também conhecido como bomba XML, em que o atacante cria um pequeno trecho de código aparentemente inofensivo em um documento XML. Em seguida, o atacante envia esse documento para o sistema da organização de destino. Quando o sistema processa o código, ele se replica continuamente. As replicações consomem cada vez mais recursos do sistema e acaba diminuindo a velocidade ou até mesmo travando o sistema.

---
# [[Ataques DDoS]] *(Distributed Denial of Service)*

- Um **ataque distribuído de negação de serviço (DDoS)** é um ataque com origem em várias fontes simultâneas para causar uma interrupção completa ou parcial do sistema.

- Para realizar ataque de DDoS, os atacantes utilizam bots. Um **bot**, ou **zumbi**, é um dispositivo conectado à internet infectado com malware que permite ao atacante controlar o dispositivo remotamente. Para araques de DDoS, os atacantes manipulam vários bots na mesma instância, formando uma rede de bots chamada ***botnet***. Uma *botnet* pode conter centenas ou até milhares de bots, cada um enviando dados ou solicitando acesso do servidor de destino simultaneamente. Esse aumento repentino de tráfego sobrecarrega o servidor, causando uma negação de serviço a vários usuários.

- Os invasores podem usar IA para analisar padrões e prever o número ideal de bots necessários para sobrecarregar efetivamente o servidor de um alvo sem desperdiçar recursos. A IA também ajuda invasores a monitorar o desempenho de cada bot em tempo real para maximizar a eficácia.

> [!Example] Exemplo
> Um invasor pode enviar muitas solicitações de página para um servidor da web em um breve período, sobrecarregando o servidor. Da mesma forma, picos na demanda de usuários em sites de venda de ingressos podem sobrecarregar os sistemas.

---
# *Phishing*

- ***Phishing*** é a prática de enviar mensagens, de fonte aparentemente confiável, para enganar os usuários e levá-los a realizar uma ação específica.

- Combina engenharia social e truques técnicos

- Depois de abrir a mensagem, os usuários desavisados podem instalar malware, ativar acesso remoto ou divulgar informações confidenciais.

> [!example] Exemplo
> Um invasor pode enviar um e-mail com um anexo de arquivo ou link para um site falso.
> Quando o destinatário clica no anexo ou link, instala involuntariamente um malware em seu computador.

---
# *Spear Phishing*

- ***Spear phishing*** é um tipo de *phishing* destinado a uma pessoa, grupo ou organização específica.

- Os atacantes passam tempo pesquisando seus alvos. Utilizam essa pesquisa para criar mensagens pessoais e relevantes, tornando-as mais eficazes.

- Alguns invasores utilizam IA para automatizar o processo de criação de e-email. Geram e-mails personalizados e convincentes que têm mais chances de enganar os usuários e levá-los a revelar informações confidenciais.

>[!example] Exemplo
>O invasor coleta detalhes de um alvo nas redes sociais e, em seguida, chama o alvo fingindo ser um representante bancário. O invasor afirma que a conta do alvo está comprometida e solicita que transfira dinheiro para uma conta bancária segura. O ataque é convincente porque o invasor utiliza conhecimento legítimo sobre o cliente.

---
# *Malware*

- *Malware* é um termo abrangente para software malicioso. ***Malware*** é um software projetado para danificar dados ou sistemas sem o consentimento embasado do usuário.

- Geralmente é acionado secretamente quando um usuário executa um programa ou faz download de um arquivo. Essa ação do usuário geralmente não é intencional.

- Uma vez ativado, o malware pode bloquear o acesso a dado e programas, roubar informações e tornar os sistemas inoperantes.

- A IA pode ajudar o malware a se adaptar para evitar a detecção, permitindo que ele cause mais danos em um sistema infectado.

>[!example] Exemplo
>Há muitos tipos de malware e, muitas vezes, o nome do malware indica sua função. Por exemplo, os ***keyloggers*** capturam as teclas de uma vítima e o ***ransomware*** mantém os arquivos de uma vítima cativos em troca de um pagamento de resgate.

---
# Ataque de intermediário *(Man-in-the-Middle - MitM)*

- Um **ataque *man-in-the-middle (MitM)*** ocorre quando os invasores se inserem em comunicações entre um cliente e um servidor.

- Com esse ataque, os invasores podem ver tudo o que ambos os lados enviam e recebem.

>[!example] Exemplo
>Um invasor pode configurar um hotspot Wi-Fi gratuito em um local público popular. Se alguém se conectar a essa rede, o invasor poderá examinar suas comunicações.
>Por sua vez, o invasor pode redirecionar a vítima para uma tela de login falsa ou inserir anúncios em páginas da web.

---
# Ataque do Sistema de Nome de Domínio (DNS)

- O **Sistema de Nomes de Domínio (DNS)** é um dos principais protocolos usados na Internet. Com protocolo DNS, um computador pode resolver um domínio para um endereço IP. Por exemplo, imagine que um usuário digite `bmw.com` na barra de pesquisa do navegador e pressione **Enter**. O protocolo DNS resolve esse nome de domínio para o endereço IP do site principal da BMW, levando o usuário ao site. Essa função é conveniente porque os nomes de domínio são muito mais fáceis de lembrar do que os endereços IP.

- Um **ataque DNS** tem como alvo o DNS, manipulando ou interrompendo a resolução de nomes de domínio e possivelmente redirecionando usuários ou impedindo o acesso a sites. Envolve táticas como sequestro de domínio e envenenamento de cache.

>[!example] Exemplo
>Os invasores associadas à gangue criminosa Roaming Mantis comprometeram os roteadores sem fio para que a inserção do URL para um site válido redirecionasse o usuário para um site malicioso. Esse site disponibilizava um malware chamado *Wroba* para o dispositivo do usuário. Quando o dispositivo é infectado, os invasores podem utilizá-lo como bot e, em seguida, utilizá-lo para comprometer outros roteadores sem fio. <sup>1</sup>

><sup>1</sup> Lakshmanan, Ravie. [Roaming Mantis spread mobile malware that hijacks Wi-Fi routers' DNS settings](https://thehackernews.com/2023/01/roaming-mantis-spreading-mobile-malware.html). _The hacker news_, 20 de janeiro de 2023.

---
# [[Injeção de linguagem de consulta estruturada (SQL Injection)]]

- **Linguagem de consulta estruturada (SQL)** é uma linguagem de programação para acessar, gerenciar e consultar bancos de dados.

- ***SQL Injection*** é a inserção de códigos maliciosos em consultas de SQL, geralmente via entrada de páginas da web. Com um ataque bem-sucedido, os invasores podem executar comandos comuns, inclusive comandos para excluir o próprio banco de dados!

- A injeção de SQL é uma das técnicas mais comuns de hacking na web.

- Os invasores podem usar IA para automatizar o processo de descoberta e exploração de vulnerabilidades na segurança de um banco de dados.

>[!example] Exemplo
>No Reino Unido, dois adolescentes conseguiram segmentar o site da TalkTalk em 2015. Utilizando injeção de SQL, roubaram centenas de milhares de registros de clientes de um banco de dados acessível remotamente.
