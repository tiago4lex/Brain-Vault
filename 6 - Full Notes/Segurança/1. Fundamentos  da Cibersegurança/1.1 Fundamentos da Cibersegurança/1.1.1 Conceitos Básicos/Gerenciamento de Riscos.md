2025-06-05 18:56

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Avaliação de Risco]] | [[Resposta ao Risco]] | [[Apetite ao Risco]]

----
# Introdução

Os riscos fazem parte da vida cotidiana e todos nós estamos instintivamente familiarizados.

O gerenciamento de riscos está no centro da maioria das empresas e do núcleo de muitos setores. Por exemplo, no setor de seguros. Uma seguradora avalia o risco associado à garantia de uma pessoa ou entidade. Primeiro, determina as chances de um incidente e a probabilidade de alguém fazer uma reclamação caso o incidente ocorra. Em seguida, define os valores das apólices adequadamente. Ele absorve o risco financeiro em potencial de seus clientes em troca dos pagamentos regulares dessas apólices.

Boas empresas entendem e gerenciam os riscos de forma eficaz para gerar vantagem competitiva. Neste módulo, você conhecerá alguns conceitos importantes sobre riscos e como se aplicam à cibersegurança.

---
# Avaliação de Risco

Nem todos os riscos têm a mesma importância. Alguns riscos exigem atenção urgente, enquanto outros podem ser ignorados. Os riscos mais significativos são conhecidos como **alto risco**. Pode ser usado uma equação básica para calcular o valor de um risco:

$$
ValorDoRisco = Consequência * Probabilidade
$$

- **Consequência** é o impacto e os danos associados.
- **Probabilidade** é a frequência com que o impacto do risco ocorre.

A equação do valor do risco quantifica a importância de um risco. É o produto da possível consequência da ocorrência de um risco e da probabilidade de sua ocorrência. Se a consequência de um for elevada <font color="#ff0000"><strong>(impacto grave)</strong></font> e sua probabilidade também for elevada <font color="#ff0000"><strong>(muito provável)</strong></font>, então o valor do riser será **considerável**. Esse alto risco exigiria atenção e mitigação imediatas. Um risco com baixa consequência ou probabilidade não exigiria atenção tão imediata.

Por razões matemáticas, seria ótimo se houvesse boas informações estatísticas para cada risco. Se, por exemplo, você souber que um em cada 10 carros terá um pneu furado em um determinado ano, poderá calcular facilmente o valor do risco associado.

> [!example] Exemplo
> Um exemplo da equação do valor do risco aplicado ao cenário anterior de pneus furados pode ser o seguinte: alguém pode ter sua produtividade afetada em um dia porque teve um pneu furado no caminho para o trabalho. A **consequência** desse risco é a perda de um dia de trabalho. Embora essa consequência seja irritante, lembre-se de qua a **probabilidade** do risco é baixa: um em cada 10 carros por ano. Portanto você pode avaliar o valor geral do risco como baixo.

Na cibersegurança, é difícil medir a probabilidade diretamente devido à constante evolução da tecnologia e ao envolvimento de invasores externos. Geralmente a probabilidade de uma organização sofrer um ataque depende parcialmente de três atributos:

$$
Probabilidade = CapacidadeAdversário * MotivaçãoAdversário * GravidadeVulnerabilidade
$$

Vamos examinar alguns termos importantes nesta equação.

---
## Adversário

**Adversário** é um termo geral para uma entidade que deseja comprometer um sistema de informações.

> [!example] Exemplo
> Vamos considerar um exemplo para demonstrar como funciona a equação da probabilidade. Imagine que um grupo de hackers recentemente formado tenha como alvo um banco. O grupo malicioso está interessado em roubar dados de login e senhas bancárias dos usuários.

- Você pode avaliar a **capacidade do adversário** como <font color="#ffc000">baixa</font> porque sua organização é nova e pode não ter a tecnologia ou os recursos mais recentes para desenvolver suas próprias ferramentas, se necessário.

- Você pode avaliar **a motivação** deles como <font color="#ff0000">alta</font> porque podem tentar vários ataques durante um período de tempo.

- Você pode avaliar uma **vulnerabilidade** identificada como <font color="#ff0000">alta</font> porque é comparativamente fácil de explorar. Por exemplo, algumas vulnerabilidade têm descrições públicas online, permitindo que os invasores espelhem os ataques com facilidade.

> [!info] Observação
> O uso dos termos de classificação *baixa*, *média* e *alta* é um exemplo de análise de risco qualitativo. Em um mundo ideal, você usaria números ou porcentagens exatos. No entanto, pode ser difícil encontrá-los, portanto muitas vezes as estimativas são tudo o que se tem.

---
## Exemplo Prático

### Informações gerais

Harper Family Care é um pequeno consultório médico que atende a comunidade local há 40 anos. O fundador, Orlando Harper, também é o médico-chefe. Sua filha, Heidi, é gerente administrativa. Orlando é um médico excelente e respeitado, mas não acompanha as últimas tendências da tecnologia, nem mesmo as que afetam sua prática. Um fato particularmente preocupante é que ele não acompanha as tendências de cibersegurança e as medidas necessárias para proteger os dados dos pacientes. Mas Heidi explica por que a clínica deveria passar por uma avaliação de risco de cibersegurança. Ele reluta mas concorda. 

Heidi contrata a Data Defense, empresa de consultoria em cibersegurança, para realizar a avaliação. Você é o representante da Data Defense que cuida do caso da Harper Family Care. Primeiro, você analisa a infraestrutura de cibersegurança da organização e identifica as seguintes áreas de risco.

![[Pasted image 20250605231200.png]]

### Perguntas para determinar o valor do risco

#### **Risco 1: Sistema operacional desatualizado**

Os computadores da clínica funcionam em um sistema operacional (SO) desatualizado. O fornecedor do sistema operacional não oferece mais suporte e não disponibiliza atualizações de segurança.

**Pergunta:**

> Que impacto negativo esse sistema operacional desatualizado pode ter na segurança do sistema e dos dados?

**Justificativa:**

> Sistemas operacionais desatualizados têm maior probabilidade de apresentar vulnerabilidades conhecidas, aumentando a probabilidade de um invasor explorar o sistema. E quanto maior as possíveis consequências de alguém explorar essa fraqueza, maior será o valor do risco.

#### **Risco 2: Autenticação de fator único para contas de e-mail**

O sistema de e-mail da clínica utiliza autenticação de fator único. Os usuários precisam de apenas uma forma de autenticação, uma senha, para acessar. O padrão atual do setor para autenticação é **autenticação multifator**, em que um login exige pelo menos dois tipos de credenciais. Por exemplo, fazer login em sua conta bancária utilizando um novo dispositivo pode exigir uma senha e a resposta a uma pergunta de segurança.

**Pergunta:**

> Como a autenticação de um único fator pode comprometer a segurança de e-mail da clínica?

**Justificativa:**

> Para determinar o valor de risco da autenticação de um único fator, você deve conhecer suas vulnerabilidades e saber como alguém pode explorá-las para comprometer a segurança. Quanto mais fácil for explorar as vulnerabilidades, maior será a probabilidade de os invasores explorarem, aumentando o valor do risco.

#### **Risco 3: O software antimalware não é atualizado regularmente**

O software antimalware da organização não é atualizado regularmente. O software não está configurado para atualização automática e a administradora do sistema, Heidi, atualiza o software manualmente de forma irregular.

**Pergunta:**

> Qual a probabilidade de um vírus ou outro malware atacar esse sistema?

**Justificativa:**

> A probabilidade de ocorrer um impacto de um risco é um componente chave do valor do risco. Nesse cenário, quanto maior for a probabilidade de o malware atacar o sistema da clínica, maior será o valor do risco.

#### **Risco 4: Arquivos importantes não são armazenados em backup** 

A organização não tem rotina de backup regular para arquivos de dados importantes.

**Pergunta:**

> Quais danos podem resultar da perda de dados dos pacientes?

**Justificativa:**

> A perda de dados dos pacientes é uma consequência em potencial de não fazer backup dos dados regularmente. Por exemplo, se ocorrer uma falha de hardware ou um ataque cibernético, a clínica poderá perder registros importantes dos pacientes e não ter como restaurá-los. Os danos resultantes podem incluir a interrupção do atendimento ao paciente e danos à reputação da clínica. Pode até incluir multas e penalidades pelo não cumprimento das leis e regulamentos relevantes que protegem os dados, como a Lei de Responsabilidade e Portabilidade de Seguros de Saúde dos EUA (HIPAA).

#### **Risco 5: Hardware antigo**

A clínica depende de hardware antigo. Alguns computadores são bastante antigos e não são compatíveis com as atualizações ou o software mais recentes. Os funcionários utilizam esses computadores somente para tarefas básicas que não exigem alto poder de processamento e os computadores não armazenam dados confidenciais.

**Pergunta:**

> Os computadores antigos estão acessíveis através da rede da clínica?

**Justificativa:**

> A consequência ou o impacto de um risco ocorrer é um componente importante do valor do risco. Nesse cenário, os computadores desatualizados não contêm dados confidenciais. Então alguns podem assumir que um comprometimento desse hardware tem pouca consequência de um ponto de vista de segurança. Mas se os computadores estiverem conectados à rede, os invasores poderão usá-los como pontos de entrada facilmente exploráveis. A partir daí, os invasores podem atacar dispositivos que contêm dados confidenciais.

---
# Resposta ao risco

Depois que uma organização avalia todos os seus riscos, inicia o gerenciamento ou a resposta ao riscos. Geralmente as organizações podem escolher entre as quatro respostas a um risco.

## Aceitação

A organização **aceita** o risco em sua forma atual. Ela reconhece as possíveis consequências do risco e está preparada para lidar com elas se ocorrerem. Uma pessoa sênior da organização, chamada de proprietário de risco, toma a decisão de aceitar um risco.

## Redução

A organização decide que um risco é grande demais para ser aceito e pretende **reduzi-lo** de alguma forma. Para reduzir o risco, a organização pode reduzir a sua probabilidade ou consequência. Isso é feito implementando controles de segurança ou corrigindo vulnerabilidades do sistema.

## Transferência

A organização opta por **transferir** o risco. Ela pode ter um terceiro aceitando parte ou todo o risco em vez de aceitar o próprio risco. A transferência geralmente ocorre por meio de seguro ou terceirização. Embora o risco permaneça, outra entidade gerencia o seu impacto, reduzindo a ameaça direta à organização.

## Rejeição

A organização decide que um risco é muito alto e o **rejeita**, o que significa que a organização deixa de ser afetada por ele. Rejeitar o risco pode mudar consideravelmente as operações comerciais. Por exemplo, a rejeição pode envolver fechar sites, evitar mercados ou evitar atividades que levem ao risco.

> [!example] Exemplo
> Vamos ilustrar essas quatro resposta a um risco. Imagine que você esteja pensando em abrir uma padaria em casa. Um risco em qualquer padaria é um incêndio, que pode causar grandes danos. Considere as seguintes respostas a esse risco.

- **Aceitação:** você examina o risco e, com fé em suas habilidades de confeiteiro, assume a chance de que é improvável que haja algum problema. Se sua panificação for malsucedida, você poderá consertar a cozinha e ficar preparado para isso.

- **Redução:** você decide que prefere não colocar sua cozinha e seu forno em um alto nível de risco e decide reduzi-lo. Você pode reduzir a probabilidade de incidentes relacionados a incêndios instalando um detector de fumaça para apresentar um alerta antecipado. Você pode reduzi as consequências de um incêndio instalando um sistema de combate a incêndios. Ambas as opções terão um pequeno custo, mas você acredita que valem a pena.

- **Transferência:** você vai à sua seguradora e atualiza seu seguro para cobrir incêndios relacionados à cozinha doméstica. A empresa faz sua própria avaliação do risco. Juntos, vocês chegam a um acordo sobre o custo a ser pago à empresa para cobrir o risco. Se o forno pegar fogo, a empresa cobrirá os custos. Esse contrato incorre em um custo inicial, mas limita sua responsabilidade.

- **Rejeição:** você decide que o risco de incêndio relacionado ao forno é muito alto. Você pode alterar as receitas para fazer bolos sem usar forno ou não iniciar o negócio.

Esse exemplo mostra que, mesmo em situações simples, há muitos fatores a considerar. Na medida em que a tecnologia de TI muda rapidamente, empresas enfrentam muitos riscos em constante evolução. O gerenciamento de riscos é um trabalho de tempo integram em muitas empresas e orienta muitas decisões estratégicas e táticas.

---
# Apetite ao Risco

O **apetite ao risco** é o nível de risco que uma organização está disposta a aceitar.

- Uma organização tem um <font color="#ff0000">alto</font> apetite ao risco se estiver disposta a aceitar um nível de risco.
- Uma organização tem um <font color="#ffc000">baixo</font> apetite ao risco se não gostar de aceitar riscos.

No risco de cibersegurança, o apetite refere-se à disposição de uma organização de aceitar as possíveis consequências de ataques cibernéticos. Uma organização com alto apetite ao risco pode tomar iniciativas ousadas, usando a tecnologia mais recente e sistemas possivelmente vulneráveis para ter vantagens competitivas consideráveis. Elas aceitam o risco de possíveis ataques cibernéticos, mas também têm contingências robustas para quando ocorrem violações.

Por outro lado, as organizações com baixo apetite ao riso são mais cautelosas em sua abordagem à cibersegurança. Podem priorizar a estabilidade e a confiabilidade em detrimento da vantagem competitiva, concentrando-se mais em medidas de proteção, como firewall, criptografia e atualizações regulares do sistema. Essa organização visam minimizar o risco de ataques cibernéticos o máximo possível, mesmo que isso signifique perder certas oportunidades.

Observe que nenhuma das abordagens é melhor. O nível de apetite ao risco de uma organização deve estar alinhado às suas metas estratégicas gerais e seus recursos. Ela também deve variar de acordo com o possível impacto dos ataques cibernéticos em suas operações e em sua reputação.
