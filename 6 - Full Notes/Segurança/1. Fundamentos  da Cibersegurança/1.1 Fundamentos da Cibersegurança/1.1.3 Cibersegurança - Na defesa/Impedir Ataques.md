2025-06-10 07:54

Status: #developed #segurança 

Tags: [[CyberSecurity]]

----
# Introdução

A primeira área de interesse da organização em segurança cibernética é impedir a ocorrência de um ataque bem-sucedido.

---
# Objetivo das estratégias de prevenção contra ataques

Não existe uma estratégia de segurança perfeita e imbatível. Os invasores sempre desenvolvem novas técnicas para contornar as medidas de segurança, tornando obsoletas as defesas atuais.

Uma estratégia de segurança mais realista e eficaz concentra-se em dificultar os ataques bem-sucedidos. Fazendo isso, as organizações podem dissuadir todos os invasores, exceto os mais determinados. Imagine que para comprometer o sistema de uma determinada organização isso custaria ao invasor US$ 100 mil em recursos. Se o sistema comprometido valer apenas US$ 80 mil para o invasor, é improvável que o invasor ataque. Portanto a defesa pode funcionar apesar das imperfeições.

Uma estratégia de segurança prática, mas eficaz, muitas vezes envolver Camadas de defesas, atualização e correção de sistemas regularmente e investimento em inteligência contra ameaças para ficar à frente das ameaças emergentes. Essas medidas aumentam o tempo, o custo e o esforço necessários para concluir um ataque bem-sucedido, reduzindo drasticamente a probabilidade de uma violação.

>[!note] Nota:
>O objetivo da segurança cibernética é reduzir o risco operacional a um nível aceitável, introduzindo a combinação correta de educação, processos e tecnologias.

Com esse objetivo em mente, vamos examinar algumas estratégias que as organizações utilizam para evitar ataques cibernéticos.

---
# Redução da superfície de ataque

Um dos primeiros conceitos a considerar é a superfície de ataque. Uma **superfície de ataque** são todos os pontos em um sistema onde um invasor pode tentar entrar, impactá-lo ou obter dados. A superfície de ataque inclui todos os pontos de vulnerabilidade, como interfaces, protocolos e serviços.

 Quanto maior a superfície de ataque, maior o risco de infiltração. Portanto o objetivo principal de qualquer boa estratégia de segurança é manter a superfície de ataque tão pequena quanto possível. Isso minimiza as vulnerabilidades, tornando o sistema menos atraente e mais difícil de ser violado por invasores.

>[!example] Exemplo
>Considere uma organização que utiliza um sistema de registro de pagamentos. Para reduzir a superfície de ataque do sistema, a organização restringe o acesso dos funcionários ao sistema a vários locais do escritório. Consequentemente, sua equipe de segurança cibernética pode ignorar o tráfego externo da internet no perímetro, reduzindo consideravelmente a superfície de ataque para possíveis invasores.

As organizações continuam oferecendo aos funcionários mais maneiras de acessar os sistemas internos. Por exemplo, muitas organizações oferecem métodos de acesso remoto e permitem que os funcionários acessem aos sistemas a partir de dispositivos pessoais. Esses recursos ajudaram a melhorar a acessibilidade, as ofertas de serviços e a flexibilidade de emprego. Mas também expandiram a superfície de ataque.

Consequentemente, ficou mais difícil estabelecer um perímetro seguro. As organizações devem estar cientes de seu perímetro e monitorá-lo de forma proativa.

---
# Criação de uma zona desmilitarizada (DMZ)

Uma parte vital do projete de um sistema seguro é uma zona desmilitarizada. Uma **zona desmilitarizada (DMZ)** é um segmento de rede entre a rede interna e privada de uma organização e a internet. É uma zona de reserva que adiciona uma camada extra de segurança. Para acessar a rede interna, os invasores devem passar pela DMZ. Mesmo que violem a DMZ, a rede interna ainda está segura.

Normalmente, os servidores da área DMZ que precisam estar acessíveis a partir da internet mais ampla ainda precisam de proteção. Esses servidores podem ser servidores web, e-mail, protocolo de transferência de arquivos (FTP) e DNS. Esses servidores contêm dados públicos, não dados internos confidenciais.

![[Pasted image 20250610083013.png]]

Este diagrama apresenta uma DMZ em ação. Um usuário externo legítimo pode acessar servidores e aplicações contidas na DMZ, o segmento entre os firewalls externo e interno. Mas esse usuário não pode acessar servidores e aplicações mais confidenciais na rede interna, atrás do firewall interno. Por exemplo, um cliente pode conseguir fazer pedidos em um sistema de pagamento digital ou acessar o e-mail. Ainda assim, não consegue acessar os registros dos funcionários ou os dados financeiros de outros clientes na rede interna.

---
# Siga o princípio do privilégio mínimo

As organizações devem decidir os níveis apropriados de permissão de aplicações de funcionários. Devem fazer isso seguindo o princípio do **menor privilégio:** conceder a um usuário ou aplicações o menor número de permissões necessárias para concluir sua função.

>[!example] Exemplo
>Uma organização configura seu banco de dados de recursos humanos (RH) para que os gerentes tenham acesso somente à leitura dos dados das funções que gerenciam. Se um invasor roubar as credenciais de um determinado gerente, ele poderá comprometer somente a confidencialidade desses registros específicos. O invasor não poderá modificá-los porque são somente para leitura. Além disso, o invasor não poderá acessar aplicações de outras áreas do negócio.

Com a introdução desse controle, a organização reduz as consequências de um ataque bem-sucedido em comparação com um sistema menos restrito. E reduzindo as consequências, a organização reduz o valor de risco. Talvez você veja o termo militar *raio de impacto* aplicado nesse contexto, no qual o raio indica a área de efeito de um ataque. A redução das permissões é uma maneira eficaz de imitar o raio de explosão.

---
# Gerenciar vulnerabilidades de software

O **gerenciamento de vulnerabilidades de software** envolve monitorar e mitigar vulnerabilidades em sistemas de software. Inclui **gerenciamento de correções**, o processo de aplicação de correções e atualização de sistemas à medida que as correções são disponibilizadas.

Quando um fornecedor cria uma nova versão de um software, pode optar por deixar de oferecer suporte à versão mais antiga. Por exemplo, a Microsoft não oferece mais suporte a versões mais antigas do Windows, como o Windows 7. Consequentemente, a empresa não lança mais correções de segurança, tornando os dispositivos com Windows 7 alvos fáceis para invasores. Sempre que possível, as organizações devem usar versões de software com suporte do fornecedor. Caso contrário, deverão implementar **controles compensatórios** que reduzem o risco associado às vulnerabilidades conhecidas. Esses controles podem ser desativação de determinados recursos, o aumento da segurança da rede ou o aumento do monitoramento para detectar atividades suspeitas.

Geralmente, a atualização de software e aplicações com as versões mais recentes reduz consideravelmente o risco de um ataque bem-sucedido. Ainda assim, versões novas de software também podem introduzir vulnerabilidades. As organizações devem verificar com os fornecedores quais e quando as correções estão disponíveis. Se um fornecedor não tiver uma solução para uma vulnerabilidade, as organizações podem implementar controles de compensação temporários, como desabilitar um recurso ou voltar para um versão anterior.

Uma organização pode usar uma varredura de vulnerabilidade para avaliar qual software é vulnerável a um ataque específico. Um **verificador de vulnerabilidade** é uma aplicação que verifica um sistema em busca de vulnerabilidades conhecidas, como software desatualizado, correções ausentes, configurações incorretas ou senhas fracas. Alguns scanners de vulnerabilidade são baseados em rede, examinando vulnerabilidades por meio de testes ativos. Outros examinam o código-fonte estático em busca de possíveis erros. Ambos os scanners produzem informações valiosas para identificar falhas antes que um invasor o faça.

---
# Utilização da defesa em profundidade

![[Pasted image 20250610085011.png]]

Outra consideração importante para a defasa é que as organizações utilizem uma abordagem em camadas. O termo **defesa em profundidade** deriva das forças armadas. Em vez de confiar em uma única forma de defesa, você as coloca em camadas. O significado é semelhante em TI. A **defesa em profundidade** é uma estratégia na qual você utiliza várias camadas de controles para proteger os ativos.

Por exemplo, uma organização pode aplicar as seguintes camadas de segurança:

- Defesas de rede, como firewalls
- Defesas do dispositivo, como verificadores de malware
- Defesas de dados, como criptografia

Para que uma ataque seja bem-sucedido, deve comprometer ou contornar todas essas camadas, o que é um desafio.