2025-06-10 21:56

Status: #developed  #segurança 

Tags: [[CyberSecurity]]

----
# Introdução

Mesmo as melhores defesas não podem impedir e detectar todos os ataques. Todas as organizações devem responder a um ataque cibernético em algum momento. Uma parte vital do planejamento de segurança é preprar-se para um incidente e estabelecer planos para o que fazer quando ocorrer.

---
# Resposta a incidentes

O [SANS Institute](https://www.sans.org/) oferece muitos cursos educacionais, eventos e recursos online relacionados à segurança cibernética, incluindo uma estrutura padrão do setor para resposta a incidentes.

### **Fase 1:** Preparação

- Na primeira fase, a preparação, uma organização começa a planejar o que fará quando ocorrer um incidente. As etapas típicas são a preparação de recursos e procedimentos de teste.

### **Fase 2:** Identificação

- Na segunda fase, a equipe de segurança detecta o evento de segurança. Em seguida, a equipe inicia o protocolo de resposta a incidentes para investigar mais a fundo e confirma que o evento é um incidente de segurança real, não um alarme falso.

### **Fase 3:** Contenção

- Na terceira fase, a equipe de segurança trabalha para evitar que a situação piore. As etapas típicas incluem segregar redes e desativar rotas de acesso ou determinados sistemas.

### **Fase 4:** Erradicação

- Na quarte fase, erradicação, a equipe de segurança trabalha para remover completamente a presença e o impacto do malware ou dos invasores. Por exemplo, a equipe pode limpar dispositivos ou restaurá-los para estados seguros. A erradicação incompleta muitas vezes resulta em ressurgimento de malware, de modo que os esforços de erradicação devem ser completos.

### **Fase 5:** Recuperação

- Na quinta fase, recuperação, a organização retorna à operação padrão. As etapas típicas incluem remover correções temporárias e restaurar determinados serviços.

### **Fase 6:** Reflexão

- Na sexta fase, reflexão, a equipe de segurança e as partes relevantes refletem sobre a causa do incidente e a eficácia da resposta. Algumas estruturas de resposta a incidentes são mencionadas nessa fase como fase de lições aprendidas. No entanto, a fase de lições *identificadas* pode ser um título melhor se a organização não fizer alterações.


## Exemplo

Essa estrutura de resposta a incidentes apresenta uma linha de base sólida sobre a qual você se pode basear. Alguns tipos de ataques ou incidentes exigem a expansão de determinados estágios. Por exemplo, considere um evento de violação de dados causado por um dispositivo de armazenamento perdido. A fase de erradicação pode ser curta e simples, mas a fase de recuperação pode ser mais longe e envolver mais participantes.

### **Introdução**

- Considere um cenário em que a HealthyOnline, um provedor de serviços de saúde online, enfrenta uma violação de dados.

### **Fase 1: Preparação**

Antes da violação, a HealthyOnline realizou regularmente testes de penetração para identificar possíveis vulnerabilidades. Eles também preparam um plano detalhado de resposta a incidentes, fizeram backup de todos os dados críticos e treinaram todos os membros da equipe sobre suas funções e responsabilidades em relação à resposta a incidentes.

### **Fase 2: Identificação**

A equipe de segurança percebe uma quantidade incomum de tráfego de dados do servidor para um endereço IP desconhecido. O HealthyOnline inicia o protocolo de resposta a incidentes rapidamente e confirma uma possível violação de dados.

### **Fase 3: Contenção**

A equipe de segurança inicia imediatamente os procedimentos de contenção. Eles isolam o servidor comprometido da rede para evitar que a violação se espalhe mais. Ao mesmo tempo, desconectam sessões ativas do usuário para minimizar o risco.

### **Fase 4: Erradicação** 

A equipe de segurança identifica o *malware* responsável pela violação e o remove completamente do sistema. A equipe substitui o servidor comprometido por um backup limpo e fortalece as regras de firewall relevantes para evitar a recorrência.

### **Fase 5: Recuperação**

Depois de assegurar-se remoção completa de ameaça, a equipe de segurança reconecta o servidor à rede. A organização gradualmente retomará as operações, começando com os serviços mais importantes. A equipe de segurança redefine todas as senhas de funcionários. A organização informa os clientes sobre o incidente e recomenda que os clientes também atualizem suas senhas.

### **Fase 6: Reflexão**

Após o retorno das operações ao normal, a HealthyOnline reflete sobre o incidente e a resposta, resumindo suas conclusões em um relatório. O relatório observa que uma correção de software recomendada não foi aplicada a tempo, deixando uma vulnerabilidade que foi explorada por um atacante. Em resposta a este incidente, a organização decidiu automatizar o processo de correção para evitar falhas semelhantes no futuro.

### **Conclusão**

A HealthyOnline concluiu todas as seis fases da estrutura de resposta a incidentes, resolvendo o incidente de forma rápida e eficaz. E com a implantação das mudanças com base nas lições aprendidas, a organização fica mais resiliente a ataques futuros.

---
# Preparação para incidentes

Como parte das atividades comerciais padrão, muitas organizações Passarão por várias atividades simuladas para testar seu nível de preparação: testes baseados em papel, exercícios teóricos e testes em tempo real.

## Testes baseados em papel

Em um teste em papel, as equipes de segurança respondem a pesquisas sobre seu nível de preparação. Eles podem ter que identificar o pessoal-chave, explicar como criar backups adequados e explicar como produzir documentos de processo mediante solicitação.

## Testes Teóricos

Um teste teórico é um formato de teste mais envolvido. Nesse teste, os principais funcionários se reúnem para simular o processo de resposta a incidentes de ponta a ponta. Um benefício desse teste é que as equipes podem interagir umas com as outras e ver como o cenário mais amplo se desenvolveria.

## Testes em tempo real

Testes em tempo real, ou testes em sistemas ativos, são a forma mais realista de testes. As organizações podem desligar sistemas críticos para testar várias falhas e como suas equipes respondem.

---
# Continuidade dos negócios e recuperação após desastres

## Continuidade dos negócios

**Continuidade dos negócios** refere-se à capacidade de uma organização continuar operando apesar de um incidente. Por exemplo, uma organização pode ter sites de backup para assumir a entrega de serviços ou uma tecnologia de backup para assumir o controle caso algum deles falhe.

## Recuperação após desastre

A **recuperação de desastres** refere-se à capacidade de uma organização se recuperar de um desastre. Por exemplo, imagine que um desastre desative todos os computadores de uma organização ou exclua bancos de dados inteiros. Nesse processo de planejamento de recuperação, as organizações devem estar preparadas para começar com praticamente nada.

## Conclusão

O planejamento de continuidade e a recuperação de desastres têm altos níveis de sobreposição com outras funções de segurança. As preocupações costumavam estar relacionadas principalmente a desastres naturais, como enchentes, terremotos ou incêndios. Agora, os ataques cibernéticos podem ser tão ou mais perturbadores do que seus equivalentes naturais. Por exemplo, é extremamente improvável que um corte de energia elétrica atinja todos os sites de uma organização multinacional simultaneamente, no entanto um ataque cibernético que desligue os principais serviços globais, como compartilhamentos de arquivos organizacionais ou sistemas de gerenciamento de domínios, é muito mais plausível.

---
# Benefício das equipes de reposta a incidentes

As organizações se beneficiam de ter equipes de resposta a incidentes. Os planos de resposta podem economizar dinheiro.

Por exemplo, considere as descobertas no [relatório de custo de uma violação de dados de 2023](https://www.ibm.com/security/data-breach). Em organizações _com_ capacidade de resposta a incidentes, o custo médio de uma violação foi de USD 3,62 milhões em 2023. Em organizações _sem_ recursos de resposta a incidentes, o custo médio de uma violação foi de USD 5,11 milhões. Esse custo médio foi uma diferença de USD 1,49 milhão, ou 34%.