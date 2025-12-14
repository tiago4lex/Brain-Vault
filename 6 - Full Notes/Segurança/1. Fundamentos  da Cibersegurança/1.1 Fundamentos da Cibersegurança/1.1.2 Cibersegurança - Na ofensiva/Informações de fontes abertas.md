2025-06-07 15:54

Status: #developed #segurança 

Tags: [[CyberSecurity]]

----
# Introdução

O interesse pela inteligência de código aberto (OSINT) cresceu na última década, tanto no setor governamental quanto no privado. **Inteligência de código aberto (OSINT)** é a inteligência coletada de fontes publicamente disponíveis. Essas fontes incluem blogs, sites de notícias e outros sites disponíveis publicamente. Qualquer pessoa com acesso confiável à Internet, incluindo jornalistas, pesquisadores e atacantes, pode conduzir investigações de código aberto. Você pode coletar facilmente o OSINT sem métodos de coleta ativos, como hackeamento ou escutas telefônicas.

Neste módulo, você examinará os benefícios e as fontes do OSINT. Você também aprenderá sobre as preocupações que isso representa para organizações e pessoas. Você entenderá como os atacantes coletam informações sobre uma organização ou pessoa utilizando essas fontes no domínio público.

---
# Informações de fontes abertas vs Alternativas

As formas tradicionais de coleta de informações podem ser caras, complexas e ilegais. Exemplos dessas abordagens incluem o hacking em banco de dados privados, a realização de campanhas por e-mail de *phishing* e a criação e implementação de *malware* que monitora a atividade do usuário.

Por outro lado, informações abertas podem ser consideravelmente fáceis e até mesmo gratuitas.

>[!example] Exemplo
>E se um jornalista quiser determinar a localização de um membro do partido político a qualquer momento?
>
>Eles podem tentar colocar um malware no celular da pessoa ilegalmente para adquirir coordenadas de GPS. Mas monitorar a conta de rede social da pessoa pode ser muito mais simples. Tudo que essa abordagem leva é para um dos assessores do político publicar uma mensagem marcada por localização ou uma foto com um ponto de referência reconhecível.
>
>Embora este exemplo pareça simples, as unidades militares têm utilizado as mesmas técnicas para rastrear suas contrapartes em países estrangeiros, e a polícia as utilizou para rastrear criminosos e fugitivos.


Outro benefício de fontes abertas é que ela geralmente é **indetectável para a vítima**.

>[!example] Exemplo
>E se um invasor quiser coletar informações sobre os sistemas de controle dentro de uma usina?
>
>Se tentarem varrer a rede externa da central eléctrica, o atacante poderá ser detectado, possivelmente comprometendo o sigilo da sua infraestrutura.
>
>Opcionalmente, o invasor pode encontrar um engenheiro de sistema discutindo planos confidenciais em um blog. A plataforma de blog pode ter registros de acesso utilizáveis para identificar usuários como o invasor. No entanto, a empresa proprietária da usina não o faria.

---
# Fontes abertas de informações

Imagine que um invasor queira coletar informações básicas sobre uma organização ou pessoa. Por onde poderiam começar?

## 1. Site da empresa

O site de uma empresa é uma fonte óbvia. O exame do tipo de informação que a empresa escolhe para disponibilizar publicamente pode ser revelador. Pode revelar informações úteis, como pontos de contato, perfis externos de redes sociais e endereços de construção. E as empresas podem publicar erroneamente mais detalhas do que deveriam.

Os invasores podem aumentar as pesquisas com recursos de pesquisa avançada, uma prática muitas vezes chamada de "hacking" do Google. Essa técnica os ajuda a encontrar informações mais avançadas e arquivos revelados sem intenção. Eles também podem explorar opções, como a *[WaybackMachine](https://archive.org/web/)*, para recuperar o site legado de uma empresa. Essas ferramentas podem ajudar os invasores a determinar o que um site foi utilizado em determinados momentos.

## 2. Mídia e notícias

Se alguém já fez o trabalho difícil, por que repetir o esforço? Alguns bons jornalistas são hábeis no processamento de informações abertas. É improvável que um invasor encontre um artigo que contenha todas as informações que procura. Ainda assim, alguns artigos provavelmente entregarão informações úteis para investigações futuras.

Outras fontes de informações processadas previamente ou fundamentais podem incluir analistas do setor, agências de classificação e outros órgãos de avaliação.

## 3. Redes sociais

As pessoas compartilham alegremente informações nas redes sociais, tornando-as amplamente disponíveis. Ao reunir várias informações de mídia social, os invasores podem obter uma perspectiva precisa sobre a vida pessoal e profissional de alguém. Algumas vítimas tornam esse trabalho muito fácil. Por exemplo, sabe-se que os funcionários compartilham fotos de crachás de identificação, diagramas de rede e até *post-its* com senhas.

Cada pequena informação pode contribuir com credibilidade para um ataque de engenharia social. Por exemplo, considere um invasor que descobre que uma vítima participou recentemente de uma conferência. O invasor pode criar um e-mail de *spear phishing* convincente. Pode dizer que o remetente encontrou o nome da vítima na lista de participantes e deseja fazer o acompanhamento.

## 4. Registros governamentais públicos

Muitos países mantêm registros detalhados de cidadãos e empresas. Esses registros podem entregar informações altamente valiosas aos invasores. Por exemplo, os registros hospitalares podem conter o local e a data de nascimento de alguém, e os boletins eleitorais podem conter o endereço de alguém.

Outras entidades podem ter registros públicos úteis para os invasores. Por exemplo, muitas bolsas de valores exigem que as empresas disponibilizem uma certa quantidade de informações financeiras.

## 5. Fóruns de discussão

Plataformas online, como Reddit, Quora e áreas de mensagens específicos de tecnologia podem conter uma infinidade de informações úteis. As pessoas muitas vezes compartilham conhecimentos, experiências e *insights* sobre essas plataformas, revelando inadvertidamente informações valiosas sobre pessoas, tecnologias ou segurança de uma organização.

## 6. Publicações de emprego

As postagens de emprego podem conter vários detalhes úteis no planejamento de um ataque. Por exemplo, uma postagem pode listar softwares que os candidatos devem dominar, indicando que os funcionários utilizam esse software. Um invasor pode pesquisar vulnerabilidades conhecidas para ajudar a planejar um ataque eficaz.

Outras informações úteis sobre a empresa podem incluir tecnologias proprietárias, projetos futuros e estrutura organizacional.

## 7. Registros do DNS

Um invasor pode utilizar várias ferramentas online para examinar os registros DNS de uma organização. Por exemplo, **WHOIS** é um protocolo que você pode utilizar para consultar bancos de dados que armazenam usuários registrados ou responsáveis por um recurso da Internet, com um nome de domínio. Ele apresenta informações sobre a organização ou pessoa que registrou um domínio, incluindo seus dados de contato. Os invasores também podem descobrir subdomínios que podem revelar a infraestrutura da rede da organização.

---
# Diretrizes para coleta de informações abertas

Lembre-se de que os atacantes não sao os únicos que utilizam o OSINT. Por exemplo, jornalistas e especialistas em segurança cibernética podem utilizar essa pesquisa para fins benéficos, como investigações criminais.

## Receba muitas informações

Quantidade é valiosa.

- Quanto mais informações, melhor.
- As ferramentas analíticas que procuram links entre conjuntos de dados funcionam melhor com mais informações.

**Lembre-se:** você nunca sabe qual será a informação principal, então salve tudo inicialmente antes do refinamento.

## Varie as informações

Construa uma imagem de muitas perspectivas.

- Nem tudo que está online é verdade
- Não confie em uma única fonte. Alguém pode falsificar uma única fonte com facilidade, como um perfil de mídia social com muitas fotos. No entanto, falsificar fontes múltiplas é muito mais difícil.

**Lembre-se:** você pode descobrir que uma vítima excluiu ou tentou ocultar informações. Este mesmo fato pode ser valioso.

## Não fique preso

Esteja preparado para falhar e não fique frustrado.

- As informações de fontes abertas são muito poderosas. Mas você encontrará  muitos becos sem saída e a quantidade e o tipo de informações abertas sobre uma vítima dependem um pouco da sorta.
- Talvez seja necessário adotar outro método ou explorar outra área.

**Lembre-se:** equipes de pesquisadores treinados geralmente precisam de algumas semanas para conclui uma investigação bem-sucedida.

>[!note] Nota:
>Muitas vezes não é possível obter informações abertas. Algumas organizações e pessoas não terão tanta informação pública como outros. Uma boa segurança operacional pode ser um dos motivos.

---
# Por que a informação de fontes aberta é uma área de interesse para todos?

Em nosso mundo altamente conectado, as pessoas compartilham demais o tempo todo. Todos devem estar cientes de que o que compartilham online é praticamente permanente.

Alguém pode combinar algumas pequenas informações para revelar algo de interesse externo. Esse processo é chamado de **agregação de informações**. Embora seu local de trabalho, suas informações de deslocamento e seus planos noturnos típicos possam ser inofensivos isoladamente, alguém pode combiná-los para mapear sua vida.

>[!example] Exemplo:
>Considere uma organização em que 100 funcionários revelam, cada um, 1% de uma informação sensível. Se uma parte externa combinar estas divulgações, poderá fazer avanços ou descobertas consideráveis.

Elaborando políticas de gerenciamento de informações, as organizações devem considerar as técnicas de OSINT que os invasores empregam. O ponto principal é que o vazamento de informações prejudica as organizações. As organizações devem agir para garantir que o mínimo possível de informações seja divulgado involuntariamente e se torne vulnerável à coleta. Muitas vezes, as organizações precisam tornar certas informações acessíveis ao público, portanto, devem tomar cuidado para evitar o compartilhamento excessivo.