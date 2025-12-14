2025-06-30 18:46

Status: #developed #Windows 

Tags: [[Windows]]

----
# Introdução

As contas de usuário podem ser de dois tipos em um sistema Windows local típico: **Administrador** e **Usuário Padrão**.

O tipo de conta de usuário determinará quais ações o usuário pode executar naquele sistema Windows específico.

- Um Administrador pode fazer alterações no sistema: adicionar usuários, excluir usuários, modificar grupos, modificar configurações do sistema, etc.

- Um Usuário Padrão só pode fazer alterações em pastas/arquivos atribuídos ao usuário e não pode realizar alterações no nível do sistema, como instalar programas.

Existem várias maneiras de determinar quais contas de usuário existem no sistema. Uma maneira é clicar no `Menu Iniciar` e digitar `Outro Usuário`. Um atalho para `Configurações do Sistema > Outros usuários` deverá aparecer.

![[Pasted image 20250630184908.png]]

Quando clicado, uma janela de configurações deve aparecer

![[Pasted image 20250630184937.png]]

Quando se é p Administrador, haverá a opção **Adicionar outra pessoa a este PC**.

>[!note] Observação:
>Um Usuário Padrão não verá esta opção.

Clicando na conta de usuário local. Mais opções deverão aparecer: **Alterar tipo de conta** e **Remover**.

![[Pasted image 20250630185100.png]]

Em Alterar tipo de conta. O valor na caixa suspensa (ou o valor destacado se você clicar na lista suspensa) é o tipo de conta atual.

![[Pasted image 20250630185117.png]]

Quando uma conta de usuário é criada, um perfil é criado para o usuário. O local para cada pasta de perfil de usuário será C:\Usuários.

Por exemplo, a pasta de perfil de usuário para a conta de usuário Max será C:\Usuários\Max.

A criação do perfil do usuário é feita no login inicial. Quando uma nova conta de usuário efetua login em um sistema local pela primeira vez, ela verá várias mensagens na tela de login. Uma das mensagens, "Serviço de Perfil de Usuário", permanece na tela de login por um tempo, enquanto cria o perfil do usuário.

![[Pasted image 20250630185204.png]]

Após o login, o usuário verá uma caixa de diálogo semelhante à abaixo (novamente), indicando que o perfil está em criação.

![[Pasted image 20250630185215.png]]

Cada perfil de usuário terá as mesmas pastas; algumas delas são:

- Área de Trabalho
- Documentos
- Downloads
- Música
- Imagens

Outra maneira de acessar essas informações, e mais algumas, é usando o **Gerenciamento de Usuários e Grupos Locais**.

Clique com o botão direito do mouse no Menu Iniciar e clique em Executar. Digite `lusrmgr.msc`.

![[win-lusrmgr.gif]]

> [!note] Observação:
> A caixa de diálogo Executar permite abrir itens rapidamente.

De volta ao `lusrmgr`, você verá duas pastas: **Usuários** e **Grupos**.

Se clicar em Grupos, verá todos os nomes dos grupos locais, juntamente com uma breve descrição de cada grupo.

Cada grupo possui permissões definidas, e os usuários são atribuídos/adicionados a grupos pelo Administrador. Quando um usuário é atribuído a um grupo, ele herda as permissões desse grupo. Um usuário pode ser atribuído a vários grupos.

>[!note] Observação:
>Se você clicar em Adicionar outra pessoa a este PC em Outros usuários, a opção Usuários e Gerenciamento Locais será aberta.

---
# Controle de contas de usuários

A grande maioria dos usuários domésticos está conectada aos seus sistemas Windows como administradores locais. Qualquer usuário com o tipo de conta "administrador" pode fazer alterações no sistema.

Um usuário não precisa executar tarefas com privilégios altos (elevados) no sistema, como navegar na Internet, trabalhar em um documento do Word, etc. Esse privilégio elevado aumenta o risco de comprometimento do sistema, pois facilita a infecção por malware. Consequentemente, como a conta do usuário pode fazer alterações no sistema, o malware seria executado no contexto do usuário conectado.

Para proteger o usuário local com esses privilégios, a Microsoft introduziu o Controle de Conta de Usuário (UAC). Esse conceito foi introduzido pela primeira vez com o breve [Windows Vista](https://en.wikipedia.org/wiki/Windows_Vista) e continuou nas versões subsequentes do Windows.

>[!note] Observação:
>O UAC (por padrão) não se aplica à conta de administrador local integrada.

Como funciona o UAC? ​​Quando um usuário com o tipo de conta "administrador" efetua login em um sistema, a sessão atual não é executada com permissões elevadas. Quando uma operação que requer privilégios de nível superior precisar ser executada, o usuário será solicitado a confirmar se permite a execução da operação.

Vejamos o programa na conta em que você está conectado, a conta de administrador integrada — clique com o botão direito do mouse para visualizar suas Propriedades.

Na aba Segurança, podemos ver os usuários/grupos e suas permissões para este arquivo. Observe que o usuário padrão não está listado.

![[Pasted image 20250630190724.png]]

Efetuando o login como usuário padrão e tente instalar este programa. Para isso, você pode acessar a área de trabalho remota da máquina com a conta de usuário padrão.

>[!note] Observação:
>Você tem o nome de usuário e a senha do usuário padrão. Eles estão visíveis em `lusrmgr.msc`.

Antes de instalar o programa, observe o ícone. Você vê a diferença? Quando você está logado como usuário padrão, o ícone de escudo aparece no ícone padrão do programa. Veja abaixo.

![[Pasted image 20250630190853.png]]

Este ícone de escudo indica que o UAC solicitará privilégios de nível superior para instalar o programa.

![[Pasted image 20250630190941.png]]

Clicando duas vezes no programa irá aparecer o prompt do UAC. Observe que a conta do administrador integrado já está definida como nome de usuário e solicita a senha da conta. Veja abaixo.

![[Pasted image 20250630191004.png]]

Após algum tempo, se uma senha não for inserida, o prompt do UAC desaparece e o programa não é instalado.

Esse recurso reduz a probabilidade de malware comprometer seu sistema. Você pode ler mais sobre o [UAC](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works) aqui.