2025-06-07 00:08

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Cyber Kill Chain]] | [[MITRE ATT&CK]]

----
# Introdução

À medida que os sistemas de computador mudam, também mudam as maneiras pelas quais podem seer comprometidas. Por exemplo, um tipo específico de *malware* pode funcionar somente em um computador que esteja executando uma versão desatualizada de um navegador da web.

Mesmo que as técnicas de ataque cibernético tenham evoluído com o tempo e hoje usem recursos de IA, você ainda pode examinar a **estrutura** geral de um ataque cibernético típico.

---
# Estrutura *Lockheed Martin Cyber Kill Chain*

![[Pasted image 20250607001323.png]]

A [Lockheed Martin Corporation](https://www.lockheedmartin.com/en-us/index.html) é uma empresa americana global aeroespacial, de defesa, segurança e tecnologias avançadas. Pesquisadores da Lockheed Martin identificaram paralelos entre o conceito militar dos EUA de *kill chain*, que se refere à estrutura de um ataque militar, e invasões em redes digitais. Aqui, a palavra cadeia refere-se a uma série de etapas que os invasores devem seguir para se infiltrar em um sistema com sucesso.

Os profissionais de segurança cibernética utilizam esta estrutura para compreender e prevenir ataques cibernéticos. Cada etapa da cadeia representa um estágio diferente de um ataque, e as etapas devem ocorrer em ordem porque cada etapa depende da conclusão da etapa anterior. Com esta estrutura, você pode ver o ataque como um processo, não como um evento único.

Agora, será examinado as sete etapas da [estrutura cadeia de eliminação cibernética](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html) para entender melhor uma sequência típica de ataque cibernético.

> [!note] **Etapa 1:** Reconhecimento
> Durante essa etapa, o invasor coleta informações sobre o alvo. Eles podem fazer isso sondando servidores digitais, conversando com pessoas próximas ao alvo ou apenas lendo as notícias.

> [!bug] **Etapa 2:** Armamento
> Após identificar uma vulnerabilidade específica, o invasor cria um *malware* para explorá-la. Esse processo pode variar desde o download de uma amostra de banco de dados, a compra de uma ferramenta de um terceiro ou o desenvolvimento de algo personalizado.

> [!abstract] **Etapa 3:** Entrega
> O invasor deve enviar o *malware* escolhido para o alvo de alguma forma. Apesar dos desenvolvimentos tecnológicos mais recentes, o e-mail ainda é o método de entrega mais comum. Outros métodos incluem downloads de sites e pendrives USB infectados ou modificados.

> [!info] **Etapa 4:** Exploração
> Quando o alvo ativa o malware abrindo o anexo infectado no e-mail ou acessando a unidade flash USB, o malware executa uma série de etapas instruídas. Este processo varia consideravelmente e depende de muitos detalhes sobre os programas e o sistema operacional. Esse processo é conhecido como exploração de uma vulnerabilidade e o software utilizado para fazer isso é conhecido como **código de exploração** ou **exploração**.

> [!error] **Etapa 5:** Instalação
> O malware tenta obter algum elemento de persistência no sistema de destino. Isso pode ser feito criando ***backdoors***, como por meio dos seguintes métodos:
> 
> - Criação de novas contas
> 
> - Instalação de programas de acesso remoto
> 
> - Introdução de novas vulnerabilidades no sistema
> 
> Esses fatores significam que, mesmo que a vulnerabilidade original seja corrigida, é tarde demais porque o invasor ainda pode acessar o sistema por meio de os *backdoors* que o *malware* criou .

> [!warning] **Etapa 6:** Comando e controle (C2)
> O invasor deve estabelecer um método para comunicar-se com os sistemas comprometidos. Ao fazer isso, o invasor pode enviar instruções e atualizações para o alvo e receber dados de volta do alvo. O invasor pode estabelecer comunicação por meio de sites, conexões diretas e até mesmo sites de mídias sociais, como o X.

> [!success] **Etapa 7:** Ações sobre objetivos
> Depois que todas as etapas anteriores forem concluídas, o invasor poderá atingir seus objetivos. Por exemplo, poderá roubar dados, modificar dados ou destruir elementos chave do sistema.

---
# Matriz MITRE ATT&CK

A [MITRE](https://www.mitre.org/) é uma organização americana sem fins lucrativos que resolve problemas mundiais com soluções baseadas em dados. Suas áreas de foco incluem compartilhamento de informações sobre ameaças cibernéticas e resiliência cibernética.

O MITRE coletou um conjunto de **táticas, técnicas e procedimentos (TTP)** que os ciberatacantes utilizam. Ele utilizou essa visão de pesquisa para desenvolver o **ATT & CK**, que significa <font color="#ffff00"><strong><i>Adversarial Tactics</i></strong></font>, <font color="#ffff00"><strong><i>Techniques and Common Knowledge</i></strong></font>. Essa sigla é pronunciada como *“attack”*. A MITRE criou uma matriz com base nesse conhecimento coletado para ajudar as organizações a examinar os ataques cibernéticos de forma simplificada. A **matriz ATT & CK** é aberta e está disponível gratuitamente para qualquer pessoa ou organização.

O gráfico a seguir mostra um trecho da matriz ATT & CK. Acesse [https://attack.mitre.org](https://attack.mitre.org/) para examinar toda a matriz.

![[Pasted image 20250607003734.png]]

- Os cabeçalhos das colunas identificam uma **tática do invasor**, como persistência. Você pode pensar em cada tática como um **objetivo do invasor**.

- Os itens listados para cada coluna são as muitas **técnicas** que o invasor pode usar para alcançar a tática ou o objetivo. Você pode selecionar cada técnica para saber mais sobre ela.

> [!example] Exemplo
> Imagine o seguinte ataque cibernético:
> 
> 1. Um invasor deseja obter [acesso credenciado](https://attack.mitre.org/tactics/TA0006/) a um sistema.
> 2. O acesso credenciado é a tática.
> 3. Se o invasor identificar mecanismos de segurança ruins para fazer login no sistema e descobrir que nenhum bloqueio de conta está em uso, poderá usar a técnica de força bruta. A [força bruta](https://attack.mitre.org/techniques/T1110/) é uma das muitas técnicas para obter acesso credenciado listadas na matriz ATT&CK. Nessa técnica, o invasor executa um programa que pode tentar milhões de combinações de nome de usuário e senha até que uma bem-sucedida seja identificada.
> 4. Se a técnica escolhida falhar, o atacante pode alternar para outra técnica e continuar tentando.

---
# A importância de conhecer os ataques cibernéticos

Os invasores pode ser persistentes. Raramente desistem após uma única interrupção no ataque. Pense em um ataque cibernético como parte de uma campanha mais longa. Muitos ataques duram meses, com os invasores espalhando sua influência e defensores tentando identificá-los e interrompê-los. Bons defensores tentam prever a próxima mudança de um atacante. Estruturas como a matriz MITRE ATT&CK ajudam a fazê-lo.

## Caso de Exemplo
### Introdução

Janina, profissional de segurança cibernética, trabalha para uma grande empresa de tecnologia. Ocorre uma violação de dados. O invasor obteve acesso, mas ainda não atingiu totalmente seus objetivos.

### Etapa 1: Primeiro acesso

As duas primeira táticas da matriz MITRE ATT&CK <font color="#ffff00"><strong>reconhecimento</strong></font> e <font color="#ffff00"><strong>desenvolvimento de recursos</strong></font>. Como a violação já ocorreu, Janina inicia sua investigação com a próxima tática: [acesso inicial](https://attack.mitre.org/tactics/TA0001/). Ela identifica o ponto de violação inicial.

### Etapa 2: *Phishing*

Janina investiga ainda mais o acesso inicial para descobrir a técnica utilizada. Ela determina que o invasor utilizou a [técnica de phishing](https://attack.mitre.org/techniques/T1566/), listada como uma das técnicas sob o acesso inicial. Especificamente, o invasor empregou *spear phishing*. Adaptou seu e-mail de *phishing* para um executivo da empresa, enganando essa pessoa para informar suas credenciais de login.

### Etapa 3: Execução

Em seguida, Janina recorre à matriz MITRE ATT&CK para prever os prováveis próximos passos do invasor. Ela examina a tática que segue o acesso inicial na matriz:[execução](https://attack.mitre.org/tactics/TA0002/). Ela lê que, nessa fase, os invasores utilizam vários tipos de comandos e *scripts* para executar códigos maliciosos nos sistemas. Como profissional de segurança cibernética, ela sabe que a criação de *scripts* é uma técnica comum após o *spear phishing*. Juntando todas essas informações, Janina prevê que o invasor utilizou scripts para automatizar suas operações maliciosas e avançar no sistema.

### Etapa 4: Criação de *scripts*

Janina verifica imediatamente se há sinais de *script* nos logs do sistema. Ela encontra evidências de que o invasor utilizou um *script PowerShell* para executar comandos mal-intencionaods. Esse achado confirma sua hipótese de que o invasor utilizou *scripts* para ir além para o sistema.

### Etapa 5: Persistência e ampliação de privilégios

Tendo identificado as táticas e técnicas atuais do invasor, Janina utiliza a matriz MITRE ATT&CK para preparar-se para os próximos passos prováveis. Ela se concentra nas táticas de [persistência](https://attack.mitre.org/tactics/TA0003/) e [escalada de privilégios](https://attack.mitre.org/tactics/TA0004/); essas táticas normalmente seguem a execução. Ela combate o ataque cibernético com as estratégias de mitigação listadas para ambas as técnicas.

### Conclusão

Ao antecipar os movimentos do invasor e usar a matriz como guia, Janina combateu eficazmente a violação, limitou os danos e protegeu os sistemas da empresa.