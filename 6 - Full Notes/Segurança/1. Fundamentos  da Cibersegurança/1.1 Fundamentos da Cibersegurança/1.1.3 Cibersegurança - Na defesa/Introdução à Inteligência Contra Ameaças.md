2025-06-15 11:15

Status: #developed #segurança 

Tags: [[CyberSecurity]]

----
# Introdução

Nas operações militares, os oficiais geralmente examinam a inteligência como um multiplicador de força. Com inteligência, um comandante pode usar seus recursos para obter o maior impacto.

>[!quote]
>"Se você conhecer seus inimigos e a si mesmo, não correrá perigo em cem batalhas. Se você não conhecer seus inimigos, mas conhecer a si mesmo, ganhará uma e perderá outra."
>
>Sun Tzu, [The Art of War](https://www.gutenberg.org/cache/epub/132/pg132-images.html)
>
>![[Pasted image 20250615111656.png]]

Em segurança cibernética, conhecer os inimigos é o domínio da inteligência de ameaças.

---
# O que é inteligência de ameaças?

Para entender a inteligência contra ameaças, é necessário entender o que é inteligência.

>[!note] O que é Inteligência
>**Inteligência** é o produto resultante da coleta e do processamento direcionados de informações sobre o ambiente e os recursos e intenções dos atores para identificar ameaças e outras oportunidades de exploração por parte dos tomadores de decisão.
>- [Ministério da Defesa do Reino Unido](https://assets.publishing.service.gov.uk/media/653a4b0780884d0013f71bb0/JDP_2_00_Ed_4_web.pdf)

Então **inteligência de ameaças cibernéticas**, ou simplesmente **inteligência de ameaças**, são dados que uma organização coletou e analisou para entender os motivos e o comportamento dos agentes de ameaças. A inteligência normalmente se concentra em **táticas, técnicas e procedimentos do invasor (TTPs)** ou outros **indicadores de comprometimento (IoCs)**.

- As **táticas** são o *porquê*, o que significa o objetivo tático do adversário ou o motivo para executar uma ação. Por exemplo, um adversário pode querer elevar os privilégios.

- **Técnicas** são o *como*, ou seja, as maneiras pelas quais um adversário atinge um objetivo tático ao executar uma ação. Por exemplo, um adversário pode ignorar os controles de acesso para aumentar os privilégios.

- **Procedimentos** são a implementação específica que o adversário utiliza para técnicas. Por exemplo, um adversário pode utilizar uma ferramenta ou programa específico para aumentar os privilégios.

- **Indicadores de compretimento (IoCs)** são assinaturas relacionadas à atividade do invasor. Por exemplo, alguns endereços IP podem estar associados a grupos de atores de ameaças ou a determinados arquivos. A presença de um IoC pode indicar que uma organização já foi comprometida.

---
# Benefícios da inteligência contra ameaças.

As organizações podem se beneficiar da inteligência contra ameaças nas seguintes áreas amplas:

## Emissão de aviso

Um dos principais benefícios da inteligência contra ameaças é que ela ajuda as organizações a se prepararem para ataques. Certos desenvolvimento geopolíticos ou técnicos podem alterar rapidamente o perfil de risco de uma organização. Mas com aviso prévio, as organizações podem preparar melhor as suas defesas para impedir a ocorrência de um ataque.

## Apresentação de indicadores de comprometimento (IoCs)

A inteligência de ameaças auxilia nas atividades de detecção fornecendo IoCs. Alguns exemplos desses IoCs são endereços IP, hashes de arquivos ou domínios associados a invasores. Um analista de segurança da organização pode pesquisar essas sinais e adicionar regras de detecção que acionam um alerta quando são detectados.

## Contexto

Quando atacada de um local ou grupo desconhecido, uma organização pode usar fontes de inteligência para começar a conhecer o invasor. Contexto podem ser informações úteis para ajudar na atribuição e na orientação sobre o que esperar a seguir.

## Aprendizado com colegas

As organizações podem compartilhar informações sobre como os invasores os atacaram, como se defenderam e quão eficazes foram suas abordagens. Compartilhar essas histórias ajuda a fortalecer todo o setor.

---
# Fontes de inteligência sobre ameaças

Reunir e desenvolver inteligência de ameaças pode ser complexo. As organizações podem reunir informações diretamente ou usar informações de outras fontes.

## **Plataformas de Troca de Ameaças**

- Os profissionais de segurança cibernética podem utilizar várias plataformas online para acessar bancos de dados de informações e análises coletadas. Algumas dessas plataformas são livremente acessíveis a qualquer pessoa, embora outras estejam disponíveis somente para assinantes ou grupos fechados do setor. Um exemplo de uma plataforma de troca de ameaças padrão do setor é o [IBM X-Force Exchange](https://exchange.xforce.ibmcloud.com/).

## **Conferências**

- Profissionais de segurança cibernética podem compartilhar os últimos desenvolvimentos do setor em conferências. Para obter mais publicidade em uma conferência, alguns pesquisadores evitam revelar suas descobertas ao público. As conferências também oferecem oportunidades para coletar informações por meio de conversas informais e de networking. São exemplos de conferências relevantes [Black Hat](https://www.blackhat.com/), [RSA Conference](https://www.rsaconference.com/) e [CYBERUK](https://www.cyberuk.uk/).

## **Artigos e Notícias**

- Alguns meios de comunicação, como o [Security Intelligence](https://securityintelligence.com/), dedicam uma cobertura considerável aos desenvolvimentos no mundo da TI. E à medida que algumas questões de segurança ganham maior visibilidade, a cobertura aumenta consideravelmente. Muitos sites menores e meios de comunicação tradicionais atendem especialistas em segurança cibernética. Exemplos de blogs de segurança cibernética incluem [Krebs on Security](https://krebsonsecurity.com/) e [Graham Cluley](https://grahamcluley.com/).

## **Fornecedores de Produtos**

- Organizações como Microsoft, Google e Apple, que produzem muitos software, divulgam avisos periódicos de segurança relacionados aos seus produtos. Esses avisos podem ser informações críticas de segurança e são leituras essenciais para administradores de sistemas.

---
# Inteligência Artificial (IA) e Inteligência Contra Ameaças

Os sistemas de computadores podem reunir e processar dados muito mais rápido do que os humanos, tornando a inteligência artificial (IA) especialmente valiosa para gerar inteligência contra ameaças.

- ### Processamento de Linguagem Natural (PLN)
    
    Os sistemas de **processamento de linguagem natural (PLN)** com recursos de IA podem reconhecer e extrair automaticamente os principais pontos de dados sobre ameaças. Particularmente, os sistemas PLN extraem esses pontos de **dados não estruturados**. São dados como imagens e mensagens de texto sem a estrutura integrada que os computadores típicos leem com facilidade. Ferramentas e métodos de dados convencionais têm dificuldades para processá-los e analisá-los. Mas os sistemas PLN podem analisar efetivamente fontes de dados não estruturados, como feeds de mídias sociais e artigos de notícias, para coletar informações relevantes sobre ameaças. A tecnologia ajuda as organizações a se manterem atualizadas sobre IoCs e métodos de ataque.<sup>1</sup>

- ### Compartilhamento de inteligência contra ameaças
    
    O combate às ameaças emergentes não é um esforço individual e exige que organizações e equipes de segurança compartilhem inteligência sobre ameaças. Os métodos tradicionais de compartilhamento envolvem processos manuais e muitas vezes demorados. Mas com a IA, as organizações podem automatizar o compartilhamento. Além disso, a tecnologia é sofisticada o suficiente para compartilhar informações pertinentes à ameaça sem revelar informações de identificação pessoal, planos estratégicos ou outros dados confidenciais.<sup>1</sup>

- ### Análise de dados preditiva
    
    A IA é especialmente útil para funções analíticas preditivas. A **análise de dados preditiva** é um tipo de análise em que você combina dados históricos com técnicas como modelagem estatística e machine learning para fazer previsões.<sup>2</sup> Com a IA, as organizações podem criar modelos preditivos mais eficazes, ajudando-as a prever e abordar ameaças antes que elas surjam.

---
# Principais conclusões

Com a inteligência contra ameaças, as organizações podem agir de forma sistemática e planejada em vez de utilizarem estimativas ou dependerem de padrões. O resultado são defesas projetadas para atender aos ataques que sofrerão, em vede de defesas projetadas para atender a um padrão normativo ou do setor. Essa distinção é particularmente importante para as organizações que operam de forma complexa ou anômala e para as quais os regulamentos geralmente não fornecem orientação suficiente.

---
# Referências

<sup>1</sup> Arora, Beenu. [How AI-Enabled Threat Intelligence Is Becoming Our Future](https://www.forbes.com/sites/forbestechcouncil/2023/07/21/how-ai-enabled-threat-intelligence-is-becoming-our-future/?sh=7c1d027d727e). _Forbes_, 21 de julho de 2023.

<sup>2</sup> [What is predictive analytics?](https://www.ibm.com/topics/predictive-analytics) _IBM_, acessado em 7 de dezembro de 2023.