2025-06-05 15:14

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Tríade CIA]]

----
# Introdução

A proteção de dados digitais é o domínio da cibersegurança. Cibersegurança pode ser relacionado como a **segurança de sistemas digitais** ou a **segurança das comunicações**. Ambas esses definições corretas, mas não abrangem todos os componentes da cibersegurança. Considerando os seguintes exemplos

> [!example] Exemplo 1
> Um fraudador envia um e-mail para uma pessoa alegando ser do banco da pessoa. O fraudador solicita seu número de identificação (PIN). Isso é um problema de cibersegurança?

> [!example] Exemplo 2
> Um investigador particular liga para um funcionário de uma empresa. O investigador pede que ele imprima alguns arquivos confidencias e deixe os papéis na sala de correspondência para o investigador coletar. Isso é um problema de cibersegurança?


Como esses exemplos mostrar, os profissionais de cibersegurança devem considerar componentes não tecnológicos ou não digitais de ataques. A cibersegurança pode ter um ou mais dos três componentes a seguir: digital, humano ou físico.

## Segurança Digital

**A segurança digital** envolve a proteção dos seus dados e sistemas contra ameaças digitais. Essas ameaças variam desde ataques de malware, como vírus ou ransomware, a tentativas de hackers projetadas para infiltrar sistemas e roubar informações confidenciais. Alguns exemplos de medidas de segurança digital incluem firewalls e software de criptografia.

## Segurança Humana

**A segurança humana** envolve a proteção de dados contra ameaças em potencial causadas por comportamento ou ações humanas. Essas ameaças podem ser não intencionais, como um funcionário baixando inadvertidamente um anexo de e-mail malicioso. Outros são intencionais, como um funcionário que vaza intencionalmente dados confidenciais. Alguns exemplos de medidas de segurança humana incluem treinamento de segurança de funcionários e políticas de senhas fortes.

## Segurança Física

**A segurança física** envolve a proteção de ativos tangíveis contra ameaças. Esses ativos físicos dão suporte à infraestrutura digital, como estações de trabalho, salas de servidores e data centers. E as ameaças a esses ativos podem ser intencionais ou não, como roubo, adulteração ou desastres naturais. Alguns exemplos de medidas de segurança física são sistemas de vigilância, medidas de controle de acesso e planos de recuperação de desastres.

---
# Tríade CIA

A cibersegurança eficaz atende a três objetivos:

- **Confidencialidade**
- **Integridade**
- **Disponibilidade**

Esses objetivos compõem a **tríade CIA** *(**C**onfidentiality, **I**ntegrity, **A**vailability)*, um modelo bem conhecido e pilar fundamental da cibersegurança.

## Confidencialidade

**Confidencialidade** significa manter os dados em segredo, ou sejam somente pessoas autorizadas podem acessar ou divulgar dados. Por exemplo, empresas de software normalmente mantêm o código fonte de seus aplicativos em segredo para terem vantagem competitiva. Para reduzir as chances de vazamento de código fonte, elas restringem o acesso somente aos funcionários que precisam deles.

A confidencialidade também abrange dados privados das pessoas. Um exemplo é que o provedor de seus serviços de saúde deve garantir que os dados coletados durante o tratamento, como diagnósticos ou prescrições, permaneçam privados. Com poucas exceções, somente você, seu médico e sua equipe médica autorizada devem ter acesso a esses dados.

Na prática, a confidencialidade envolve a implementação de salvaguardas que proporcionam o nível certo de acesso ao conjunto certo de usuários no momento certo, utilizando os métodos certos.

![[Pasted image 20250605153405.png]]

## Integridade

**Integridade** significa garantir que os dados sejam confiáveis e precisos, protegendo-os contra modificação e destruição não autorizadas. Digamos que você gaste R$ 10 em uma pizza. Você pode não se importar se essa compra é ou não confidencial. Mas e se algo alterar o valor da transação e você acabar gastando R$ 10 mil? Observe que a integridade desta transação pode ter sido comprometida intencionalmente ou não.

Além disso considere que embora a causa do erro possa ser técnica, ela também pode ser humana. Talvez alguém tenha inserido o valor de pagamento errado.

Para preservar a integridade, você também deve impedir que pessoas não autorizadas editem os dados. Nesse sentido, a integridade e confidencialidade se sobrepõem.

![[Pasted image 20250605154214.png]]

## Disponibilidade

**Disponibilidade** significa garantir o acesso e o uso oportunos e confiáveis dos dados. Por exemplo, você espera ter acesso online 24 por dia e 7 dias por semana à sua conta bancária. Para atender a essa expectativa, seu banco deve implementar e manter recursos suficientes para manter o banco online disponível e funcionando corretamente. 

Mas acesso oportuno nem sempre significa acesso imediato e nem mesmo constante. Por exemplo, se você solicitar transcrições escolares, poderá ser necessário aguardar vários dias até que os funcionários da escola localizem, processem e enviem os documentos. E se a escola oferecer transcrições na forma eletrônica, isso poderá limitar o período durante o qual os destinatários poderão acessá-los. Independentemente disso, os dados ficam disponíveis por um determinado período de tempo razoável.

![[Pasted image 20250605154309.png]]

---
# Exemplos

Considere alguns exemplos para contextualizar os objetivos da tríade CIA. 

- **Confidencialidade** pode ser o objetivo mais crucial para as agências de inteligência do governo. Essas agências lidam com dados confidenciais relevantes para a segurança nacional, investigações em andamento, relatórios de inteligência e outras informações confidenciais. Um vazamento não autorizado dessas informações pode ajudar os criminosos a planejar atividades ilegais mais bem-sucedidas. Pode até mesmo colocar vidas em perigo. 
    
- **Integridade** pode ser o objetivo mais crucial para os bancos. As transações financeiras, fundamentais para os negócios dos bancos, dependem muito da precisão e da consistência dos dados. Modificações não autorizadas, deliberadas ou não, podem levar a perdas financeiras consideráveis ou a repercussões legais. 
    
- **Disponibilidade** pode ser o objetivo mais importante para um varejista online. Como cliente, você provavelmente espera poder comprar o que quiser online, a qualquer hora do dia. Qualquer tempo de inatividade, atraso ou interrupção nos serviços pode levar você a fazer uma compra ou pedido em outro lugar. Isso também pode reduzir a confiança em uma empresa e prejudicar sua reputação. As empresas querem garantir que seus sites mantenham a atividade constante, carreguem rapidamente e processem transações sem erros.

---
# Controles

Para cumprir todos os objetivos da tríade CIA, são necessários controles. Na cibersegurança, os controles são salvaguardas ou contramedidas para evitar, detectar, contornar ou minimizar os risos à segurança da propriedade física, tangível ou digital.

## Controles de confidencialidade

Considere estes controles padrão para preservar a confidencialidade. 

- **A criptografia** converte seus dados em um formato que somente alguém com a chave de descriptografia pode entender. 

- **Os controles de acesso** são medidas projetadas para garantir que apenas as pessoas corretas possam consultar, modificar ou compartilhar dados. Se você utilizar proteção por senha, estará utilizando um controle de acesso. Os controles de acesso também incluem dados biométricos, como impressões digitais ou varreduras de retina, que garantem que somente pessoas autorizadas possam acessar os dados. 

- **O gerenciamento de correções** envolve a atualização do software do sistema. A atualização regular do software do sistema corrige possíveis pontos fracos de segurança que os invasores podem explorar.

## Controles de integridade

Considere estes controles padrão para preservar a integridade. 

- **Checksums** são algoritmos matemáticos que geram um valor exclusivo para um conjunto de dados. Se os dados mudarem, a soma de verificação também mudará, alertando sobre a alteração. 

- **Os controles de acesso** e **as permissões de usuário** podem limitar quem pode alterar os dados e quais alterações podem fazer. 

- **Os backups de dados** podem ajudar a restaurar os dados ao seu estado correto se ocorrerem alterações. 

- **As trilhas de auditoria** podem rastrear e registrar todas as alterações feitas nos dados. Elas proporcionam um registro claro de quem fez a alteração e quando a fez.

## Controles de disponibilidade

Considere esses controles padrão para preservar a disponibilidade. 

- **Sistemas redundantes** e **procedimentos de backup de dados** ajudam a proteger contra perda de dados ou falha do sistema. Você pode usar vários servidores ou armazenar dados em vários locais. 

- **Software antimalware** e **firewalls** protegem os sistemas contra ataques que podem interromper os serviços. 

- **Os planos de recuperação de desastres** e **os planos de continuidade de negócios** definem as etapas necessárias para restaurar os serviços com rapidez e eficiência no caso de uma interrupção, minimizando o tempo de inatividade.

---
# Classificação

Na cibersegurança, um **ativo** é algo valioso para o seu proprietário. Os ativos podem ser digitais ou físicos. Por exemplo, um programa ou código é um ativo digital e um servidor é um ativo físico. Informações confidenciais também podem ser chamadas de **ativos de informação**. Por exemplo, os ativos de informação podem ser informações contidas em bases de dados, relatórios de investigação ou registos de saúde. 

Considere sua conta bancária pessoal, biblioteca de fotos, conta de mídia social e telefone celular. **Como a perda de confidencialidade, integridade e disponibilidade afetaria você em cada ativo?** Para responder a esta pergunta, você pode usar a seguinte escala de 1 a 5. 

- **1. Consequência baixa:** A perda não teria impacto perceptível na sua vida cotidiana. 
    
- **3. Consequência média:** A perda teria menor impacto, resultando em algumas horas perdidas. 
    
- **5. Alta consequência:** A perda teria um impacto enorme e transformador que poderia durar meses ou anos. 
ss
## Exemplo

Para saber como aplicar o sistema de classificação, considere o seguinte exemplo de envio de um debate online. 

- A perda de **confidencialidade** para o autor pode ser grave, dependendo do quanto ele valoriza seu anonimato. Suponha que o autor considere a perda de confidencialidade como algo irritante, mas terá apenas um pequeno impacto. Ele tem uma classificação de **2**. 
    
- A perda de **integridade** de outra pessoa que edita o envio pode iniciar uma discussão, levando à perda de tempo fazendo atualizações. Portanto a integridade recebe classificação igual a **3**. 
    
- Uma perda de **disponibilidade**, como o desaparecimento total do comentário online ou a inacessibilidade, pode atrapalhar o fluxo do debate. Portanto a disponibilidade recebe classificação igual a **4**.

![[Imagem do WhatsApp de 2025-06-05 à(s) 15.53.43_a225ea9c.jpg]]

Observe que certos ativos são mais importantes para você do que outros. Esses ativos devem corresponder às **classificações mais altas**. Alguma das suas avaliações de valor surpreende você?

Do ponto de vista da segurança, você deve priorizar suas proteções em torno dos ativos que mais importam para você. Por exemplo, a senha do seu gerenciador de senhas pode ter 20 caracteres ou mais e ser mantida em sigilo, enquanto você pode ocasionalmente compartilhar sua senha de Wi-Fi doméstico com amigos e familiares. 

Na cibersegurança, as organizações tomam essas decisões o tempo todo para priorizar a proteção de ativos.