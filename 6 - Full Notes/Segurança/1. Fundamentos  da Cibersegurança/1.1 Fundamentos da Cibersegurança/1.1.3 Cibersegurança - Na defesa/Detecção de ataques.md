2025-06-10 08:54

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[IA]]

----
# Introdução

Se as defesas de uma organização não conseguirem impedir um ataque cibernético com êxito, a próxima prioridade da organização será detectar o ataque cibernético. Espera-se que a detecção ocorra enquanto o ataque estiver em andamento ou,  melhor ainda, antes que a violação ocorra.

---
# Software antimalware

Um método padrão para atacar um sistema é o malware e uma medida padrão para detectar malware é o software antimalware. **O software antimalware**, ou software antivírus, é um software especializado que detecta, coloca em quarentena e até destrói malware em computadores ou redes. Alguns programas antimalware conhecidos são Malwarebytes, McAfee Antivirus e Windows Defender Antivirus. Você pode instalar o software no local em um único dispositivo ou executar e gerenciar o software em um servidor centralizado.

O software antimalware detecta malware verificando todos os arquivos do dispositivo em busca de assinaturas. Uma **assinatura de malware** é um padrão de atributos que corresponde a um malware conhecido. Depois de identificar uma assinatura em um arquivo, o software exclui o arquivo, transfere para a área de quarentena ou alerta que o arquivo pode estar infectado.

---
# Registro de atividades

Um dos métodos mais essenciais para a detecção de ataques é o registro de atividades. O **registro de atividades** é o procesesso em que as ações são registradas com precisão em um local seguro. Os registros deve ser à prove de adulteração e agir como um registro permanente do que ocorreu em uma rede. Você pode fazer o registro em máquinas ou aplicações individuais.

Os tipos de ações registradas dependem dos sistemas e das necessidades de segurança da organização. As ações comumente registradas são entradas e saídas de usuários no sistema, tentativas de acesso malsucedidas, alterações na configuração do sistema, tráfego de pacotes e iniciação de processos ou serviços. Além disso, os registros geralmente registram alterações em arquivos ou bancos de dados.

Embora uma única entrada de registro posso não ser altamente valiosa isoladamente, uma quantidade maior ajuda a rastrear atividades de usuários legítimos e agentes maliciosos. Esses registros proporcionam uma trilha de auditoria inestimável para diagnosticar problemas e identificar atividades maliciosas ou violações de segurança.

>[!example] Exemplo
>A entrada de registro a seguir mostra o formato de log que os servidores web Apache utilizam.
>
>```bash
>9.12.156.2 - bob [11/Jan/2020:14:16:34 -0700] “OBTER /index.html HTTP/1.0” 200 4066
>```
>
>Observe que esta entrada de registro descreve um usuário chamado bob que está acessando uma página web específica com o status e a hora anotados.

---
# Monitoramento de Rede

Além de registrar eventos que acontecem em servidores, as organizações podem monitorar as comunicações em sua rede. Essa abordagem, conhecida como análise de tráfego, pode identificar atividades de rede, até mesmo atividades criptografadas. A análise de tráfego envolve o acompanhamento de diferentes métricas relacionadas à rede. Alguns exemplos dessas métricas incluem a origem e o destino do tráfego, os protocolos de rede utilizadas, a largura de banda utilizada e o tamanho do pacote. A análise de tráfego avançada também pode identificar aplicações ou serviços específicos em uso, a presença de qualquer código maliciosos e comportamentos incomuns ou anomalias que possam indicar um ataque cibernético.

Alguns tipos de *malware* se movem de dispositivo para dispositivo, então boas ferramentas de monitoramento de rede podem identificar com facilidade.

>[!example] Exemplo
>Imagine que uma ferramenta de monitoramento de rede está em uso. Se alguém usar um dispositivo de rede para transmitir vídeo, a ferramenta mostrará alto consumo de largura de banda do dispositivo em um período prolongado. Por outro lado, se alguém usar um dispositivo de rede para baixar um arquivo grande, a ferramenta mostrará um pico de demand alto para o dispositivo e, em seguida, pouco ou nada depois desse ponto.

---
# Ferramentas de gerenciamento e eventos de segurança (SIEM)

![[Pasted image 20250610190339.png]]

> Esta captura de tela mostra a interface de um serviço SIEM chamado [IBM Security QRadar SIEM](https://www.ibm.com/products/qradar-siem). Esse software de análise e inteligência de segurança de rede monitora ameaças e ataques internos.

É difícil entender todos os dados coletador por meio do monitoramento de rede. Para obter ajuda, muitos profissionais de segurança cibernética recorrem a informações de segurança e ferramentas de gerenciamento de eventos (SIEM).

Uma ferramenta de **gerenciamento de eventos e informações de segurança (SIEM)** coleta todos os dados em todas as infraestruturas de tecnologia de uma organização e agrega esses dados para que a equipe de segurança cibernética possa identificar e analisar eventos e padrões de possíveis ataques.

>[!example] Exemplo
>Imagine que uma equipe de segurança cibernética suspeite que um invasor está tentando comprometer a conta de um usuário por meio de ataques de força bruta. Eles podem usar uma ferramenta SIEM para detectar tentativas de acesso por força bruta para essa conta. Por isso, podem definir um alerta para ser acionado se ocorrerem cinco ou mais tentativas de acesso malsucedidas por minuto na conta. Suponha que um invasor tente comprometer a conta trabalhando com milhões de combinações de nome de usuário ou senha. Nesse caso, o invasor ultrapassará o limite, acionando o alerta da ferramenta SIEM e notificando a equipe.

---
# Centro de Operações de Segurança (SOC)

O grupo responsável pela segurança de uma organização geralmente fas parte do centro de operações de segurança. Um **centro de operações de seguranca (SOC)** é uma equipe dedicada de profissionais de segurança cibernética que utiliza software especializado para monitorar, detectar, investigar e responder ativamente às possíveis ameaças e incidentes de segurança de uma organização em tempo real. Um dos principais objetivos do SOC é detectar ataques em andamento utilizando o SIEM e outras ferramentas de monitoramento.

Os analistas de segurança em SOC são responsáveis por avaliar a segurança de uma organização. Se detectarem um ataque ou um possível ataque, eles decidirão como responder a ela seguindo os procedimentos organizacionais.

## Alarmes falsos

Um dos desafios dos SOCs é determinar os melhores limites para os alertas. Seu objetivo é reduzir os **falsos positivos**, eventos legítimos registrados incorretamente como mal-intencionados.

Se um evento legítimo específico disparar muitos falsos positivos, o analista deverá considerar a possibilidade de definir limites mais altos.

>[!example] Exemplo
>Considere uma funcionária que volta ao trabalho após um longo feriado e esquece sua senha. Se ela tentar lembrar da senha, suas tentativas repetidas poderão ultrapassar o limite, acionando um alerta.

---
# Inteligência Artificial (IA)

A inteligência artificial está aprimorando a detecção e a defesa de ataques das organizações.

## Registro de atividades

- A IA automatiza o processo de registro e análise de grandes volumes de dados de várias fontes. Essa tarefa manual levaria um tempo enorme para os humanos, mas IA pode fazê-lo muito rápido, permitindo detecção e prevenção de ameaças em tempo real.

## Monitoramento de rede

- A IA pode analisar padrões de tráfego e identificar anomalias que podem indicar um ataque. Por exemplo, um aumento repentino no tráfego de rede pode indicar um ataque distribuído de negação de serviço (DDoS). Com a IA, as organizações podem detectar essas anomalias instantaneamente e iniciar contramedidas apropriadas.

## Ferramentas de SIEM

- As  ferramentas de SIEM utilizam IA para reunir e analisar dados na rede de uma organização. Essas ferramentas identificam padrões e correlações, ajudando  a identificar possíveis ameaças à segurança. Por exemplo, o QRadar SIEM define limites de alerta para atividades anormais, como várias tentativas de login malsucedidas.

## SOCs

- Em um SOC, a IA pode ajudar os analistas de segurança a trabalhar com mais eficiência. Em vez de examinarem anualmente toneladas de dados para identificar atividades possivelmente mal-intencionadas, os analistas podem se concentrar em responder aos alertas gerados pelo sistema de IA. A IA não apenas economiza o tempo dos analistas, mas também ajuda a mitigar as ameaças com  mais rapidez.

## Aprendizado de máquina (ML)

As organizações podem treinar sistemas de IA para distinguir entre comportamento normal e incomum. A IA treina com base em dados históricos que incluem ameaças legítimas e falsos positivos. Com a ajuda de algoritmos de aprendizado de máquina, o sistema de IA aprende a reconhecer padrões associados a falsos positivos.

Por exemplo, o sistema pode determinar que um determinado número de tentativas de login malsucedidos a partir de um endereço IP interno confiável durante o horário de trabalho é um padrão comum de esquecimento de senha, e não uma ação maliciosa. Portanto o sistema aprende  a não disparar um alerta nesta situação. Com o tempo, ele pode melhorar na redução de falsos positivos, ajustando assim os limites e  a sensibilidade dos alertas. Pode até reduzir o tempo gasto em falsos positivos, automatizando o processo de verificação.

---
# Exemplo: Executando uma análise de registros

A tabela mostra um registro dos **arquivos de uma organização sendo alterados** **em um determinado período de tempo**. Por experiência própria, sabe-se que essa atividade geralmente é previsível com altos níveis de automação. Portanto um número incomum de alterações pode indicar atividade desconhecida ou não autorizada.

|Hora|Número de arquivos atualizados|
|---|---|
|01:00|12|
|02:00|23|
|03:00|33|
|04:00|47|
|05:00|62|
|06:00|75|
|07:00|92|
|08:00|104|
|09:00|114|
|10:00|128|
|11:00|173|
|12:00|207|
|13:00|220|
|14:00|232|
|15:00|243|
![[Pasted image 20250610192546.png]]

Neste conjunto de dados, uma quantidade incomum de atividade ocorre entre 10h e 12h. É possível observar a tendência mais facilmente no gráfico.