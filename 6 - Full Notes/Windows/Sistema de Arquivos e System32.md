2025-06-23 21:54

Status: #developed #Windows 

Tags: [[Windows]]

----
# Sistema de Arquivos

O sistema de arquivos usado nas versões modernas do Windows é o ***New Technology File System*** ou simplesmente [NTFS](https://learn.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview).

Antes do NTFS, havia o **FAT16/FAT32** *(File Allocation Table)* e o HPFS *(High Performance File System)*.

Partições FAT ainda estão em uso hoje. Por exemplo, normalmente é possível encontrar partições FAT em dispositivos USB, cartões MicroSD, etc., mas tradicionalmente não em computadores/laptops pessoais com Windows ou servidores Windows.

O NTFS é conhecido como um sistema de arquivos com registro em diário. Em caso de falha, o sistema de arquivos pode reparar automaticamente as pastas/arquivos no disco usando as informações armazenadas em um arquivo de log. Essa função não é possível com o FAT.

O NTFS aborda muitas das limitações dos sistemas de arquivos anteriores, como:

- Suporta arquivos maiores que 4 GB
- Definir permissões específicas para pastas e arquivos
- Compactação de pastas e arquivos
- Criptografia (*[Encryption File System](https://learn.microsoft.com/en-us/windows/win32/fileio/file-encryption)* ou **EFS**)

É possível verificar as Propriedades (clicando com o botão direito) da unidade na qual seu sistema operacional está instalado, normalmente a unidade C (C:\).

![[win-file-system.gif]]

>[!note] Nota
>É possível ler a documentação oficial da Microsoft sobre FAT, HPFS e NTFS [aqui](https://learn.microsoft.com/en-us/troubleshoot/windows-client/backup-and-storage/fat-hpfs-and-ntfs-file-systems).

Em volumes NTFS, é possível definir permissões que concedem ou negam acesso a arquivos e pastas.

As permissões são:

- **Controle total**
- **Modificar**
- **Ler e executar**
- **Listar o conteúdo da pasta**
- **Ler**
- **Gravar**

A imagem abaixo lista o significado de cada permissão e como ela se aplica a um arquivo e uma pasta.

![[Pasted image 20250623220310.png]]

Como visualizar as permissões de um arquivo ou pasta?

- Clique com o botão direito do mouse no arquivo ou pasta cujas permissões deseja verificar.
- No menu de contexto, selecione `Propriedades`.
- Em Propriedades, clique na aba `Segurança`.
- Na lista `Nomes de grupo` ou `Usuário`, selecione o usuário, computador ou grupo cujas permissões deseja visualizar.

Na imagem abaixo, as permissões do grupo Usuários para a pasta Windows.

![[Pasted image 20250623220514.png]]

Outro recurso do NTFS são os **Fluxos de Dados Alternativos** (ADS).

**Fluxos de Dados Alternativos** (ADS) são um atributo de arquivo específico do Windows NTFS *(New Technology File System)*.

Cada arquivo possui pelo menos um fluxo de dados (`$DATA`), e o ADS permite que os arquivos contenham mais de um fluxo de dados. Nativamente, o [Windows Explorer](https://support.microsoft.com/en-us/windows/file-explorer-in-windows-ef370130-1cca-9dc5-e0df-2f7416fe1cb1) não exibe o ADS para o usuário. Existem executáveis ​​de terceiros que podem ser usados ​​para visualizar esses dados, mas o [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.5&viewFallbackFrom=powershell-7.1) oferece a capacidade de visualizar o ADS para arquivos.

Do ponto de vista da segurança, criadores de malware têm usado o ADS para ocultar dados.

Nem todos os seus usos são maliciosos. Por exemplo, quando se baixa um arquivo da Internet, há identificadores gravados no ADS para identificar que o arquivo foi baixado da Internet.

Para saber mais sobre o ADS, é possível consulta o site da MalwareBytes [aqui](https://www.malwarebytes.com/blog/101/2015/07/introduction-to-alternate-data-streams).

---
# `C:\Windows\System32`

A pasta Windows (`C:\Windows`) é tradicionalmente conhecida como a pasta que contém o sistema operacional Windows.

A pasta não precisa necessariamente residir na unidade C. Ela pode residir em qualquer outra unidade e, tecnicamente, pode residir em uma pasta diferente.

É aqui que as variáveis ​​de ambiente, mais especificamente as variáveis ​​de ambiente do sistema, entram em ação. Embora ainda não tenha sido discutida, a variável de ambiente do sistema para o diretório Windows é `%windir%`.

>[!quote] De acordo com a Microsoft
>"Variáveis ​​de ambiente armazenam informações sobre o ambiente do sistema operacional. Essas informações incluem detalhes como o caminho do sistema operacional, o número de processadores usados ​​pelo sistema operacional e a localização das pastas temporárias".

Existem muitas pastas dentro da pasta "Windows".

![[Pasted image 20250623221237.png]]

Uma destas pastas é chamada `System32`

![[Pasted image 20250623221307.png]]

A pasta System32 contém os arquivos importantes para o sistema operacional.

É necessário ter extremo cuidado ao interagir com esta pasta. A exclusão acidental de arquivos ou pastas dentro do System32 pode tornar o sistema operacional Windows inoperante. Saiba mais sobre esta ação [aqui](https://www.howtogeek.com/346997/what-is-the-system32-directory-and-why-you-shouldnt-delete-it/).

>[!note] Observação:
>Muitas das ferramentas que serão abordadas na série Fundamentos do Windows residem na pasta System32.

