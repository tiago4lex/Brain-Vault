2026-01-25 16:37

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wireshark]]

----
# Dissecção do Pacote

A dissecção de pacotes também é conhecida como dissecção de protocolo, que investiga detalhes de pacotes decodificando protocolos e campos disponíveis. O Wireshark suporta uma longa lista de protocolos para dissecção, e você também pode escrever seus scripts de dissecção. Você pode encontrar mais detalhes sobre dissecação [**aqui**](https://github.com/boundary/wireshark/blob/master/doc/README.dissector).

**Nota:** Esta seção cobre como o Wireshark usa camadas OSI para quebrar pacotes e como usar essas camadas para análise.Espera-se que você já tenha conhecimento de fundo do modelo OSI e como ele funciona.

---
## Detalhes do pacote

Você pode clicar em um pacote no painel da lista de pacotes para abrir seus detalhes (o duplo clique abrirá detalhes em uma nova janela). Os pacotes consistem em 5 a 7 camadas com base no modelo OSI. Vamos analisar todos eles em um pacote HTTP a partir de uma captura de amostra. A imagem abaixo mostra a visualização do número 27 do pacote.

![Wireshark - detalhes do pacote](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761041216054.svg)

Cada vez que você clicar em um detalhe, ele irá destacar a parte correspondente no painel de bytes do pacote.

![Wireshark - bytes de pacote](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761041609772.svg)

Vamos ter uma visão mais próxima do painel de detalhes.

![Wireshark - detalhes do pacote](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761041779487.png)

Podemos ver sete camadas distintas no pacote: `frame/packet`,`source [MAC]`,`source [IP]`,`protocol`,`protocol errors`, `application protocol`, e `application data`. Abaixo vamos passar por cima das camadas com mais detalhes.

**O quadro (camada 1):** Isso mostrará qual quadro / pacote você está olhando e detalhes específicos para a camada física do modelo OSI.

![Wireshark - camada 1](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761041779538.png)

**Fonte MAC (Camada 2**): Isso mostrará os Endereços MAC de origem e destino; a partir da camada de Data Link do modelo OSI.

![Wireshark - camada 2](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042014059.png)

**Fonte IP (Camada 3):** Isso mostrará os Endereços IPv4 de origem e destino; da camada de Rede do modelo OSI.

![Wireshark - camada 3](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042013990.png) 

**Protocolo (Camada 4):** Isso mostrará detalhes do protocolo usado (UDP / TCP) e portos de origem e destino; da camada de transporte do modelo OSI.

![Wireshark - camada 4](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042014024.png)

**Erros de** Protocolo: Esta continuação da 4a camada mostra segmentos específicos do TCP que precisavam ser remontados.

![Wireshark - erro de protocolo](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042204301.png)

**Application Protocol (Layer 5):** Isso mostrará detalhes específicos para o protocolo usado, como HTTP, FTP e SMB. Da camada Aplicação do modelo OSI.

![Wireshark - camada 5](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042014014.png)

**Dados** de **aplicação:** Esta extensão da 5a camada pode mostrar os dados específicos do aplicativo.

![Wireshark - dados da aplicação](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761042014019.png)

---
# Navegação de Pacotes
## Números do pacote

O Wireshark calcula o número de pacotes investigados e atribui um número exclusivo para cada pacote. Isso ajuda o processo de análise para grandes capturas e facilita a volta a um ponto específico de um evento.

![Wireshark - números de pacotes](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116217726.svg)

## Go

Os números do pacote não ajudam apenas a contar o número total de pacotes ou facilitam a localização/investigação de pacotes específicos. Esse recurso não apenas navega entre pacotes para cima e para baixo; ele também fornece rastreamento de pacotes no quadro e encontra o próximo pacote na parte específica da conversa. Você pode usar o menu e a barra de ferramentas **"Go"** para visualizar pacotes específicos.

![Wireshark - vá para pacote](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433008.gif)

## Encontre Pacotes

Além do número do pacote, o Wireshark pode encontrar pacotes por conteúdo de pacote. Você pode usar o menu **"Editar --> Localizar Pacote"** para fazer uma pesquisa dentro dos pacotes para um evento específico de interesse. Isso ajuda analistas e administradores a encontrar padrões de intrusão ou traços de falha específicos.

Há dois pontos cruciais para encontrar pacotes. O primeiro é conhecer o tipo de entrada. Esta funcionalidade aceita quatro tipos de entradas (filtro de exibição, Hex, String e Regex). As buscas de string e regex são os tipos de pesquisa mais usados. As pesquisas são insensíveis ao caso, mas você pode definir a sensibilidade do caso em sua pesquisa clicando no botão de rádio.

O segundo ponto é escolher o campo de busca. Você pode realizar pesquisas nos três painéis (lista de pacotes, detalhes do pacote e bytes de pacotes), e é importante saber as informações disponíveis em cada painel para encontrar o evento de interesse. Por exemplo, se você tentar encontrar as informações disponíveis no painel de detalhes do pacote e realizar a pesquisa no painel da lista de pacotes, o Wireshark não a encontrará mesmo que exista.

![Wireshark - encontrar pacotes](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433011.gif)

## Marcar Pacotes

Marcar pacotes é outra funcionalidade útil para analistas. Você pode encontrar/apontar para um pacote específico para uma investigação mais aprofundada, marcando-o. Isso ajuda os analistas a apontar para um evento de interesse ou exportar pacotes específicos da captura. Você pode usar o menu **"Editar"** ou **"clicar com o botão direito do mouse"** para marcar/desmarcar pacotes.

Pacotes marcados serão mostrados em preto, independentemente da cor original que representa o tipo de conexão. Observe que as informações de pacotes marcados são renovadas a cada sessão de arquivo, portanto, os pacotes marcados serão perdidos após o fechamento do arquivo de captura.

![Wireshark - marcar pacotes](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433047.gif)

## Comentários de Pacotes

Semelhante à marcação de pacotes, comentar é outro recurso útil para analistas. Você pode adicionar comentários para pacotes específicos que ajudarão a investigação adicional ou lembrar e apontar pontos importantes / suspeitos para outros analistas de camada. Ao contrário da marcação de pacotes, os comentários podem ficar dentro do arquivo de captura até que o operador os remova.

![Wireshark - comentários de pacotes](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1763530577252.gif)

## Exportar Pacotes

Os arquivos de captura podem conter milhares de pacotes em um único arquivo. Como mencionado anteriormente, o Wireshark não é um IDS, portanto, às vezes, é necessário separar pacotes específicos do arquivo e se aprofundar para resolver um incidente. Essa funcionalidade ajuda os analistas a compartilhar os únicos pacotes suspeitos (escopo decidido). Assim, informações redundantes não estão incluídas no processo de análise. Você pode usar o menu **"Arquivo"** para exportar pacotes.

![Wireshark - pacotes de exportação](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433024.gif)

## Objetos de exportação (arquivos)

O Wireshark pode extrair arquivos transferidos através do fio. Para um analista de segurança, é vital descobrir arquivos compartilhados e salvá-los para uma investigação mais aprofundada. A exportação de objetos está disponível apenas para fluxos de protocolo selecionados (DICOM, HTTP, FMI, SMB e TFTP).

![Wireshark - objetos de exportação](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433258.gif)

## Formato de exibição de tempo

O Wireshark lista os pacotes à medida que são capturados, portanto, investigar o fluxo padrão nem sempre é a melhor opção. Por padrão, o Wireshark mostra o tempo em "Segundos Desde o Início da Captura", o uso comum está usando o formato de exibição de tempo UTC para uma melhor visualização. Você pode usar o menu **"Exibir -->** formato de exibição de **tempo"** para alterar o formato **de exibição** de tempo.

![Wireshark - Editar formato de exibição de tempo](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1761116433016.gif)

![Wireshark - formato de exibição de tempo](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d2333318ff4df99df252c6ee1c236619.png)

## Informações Especializadas *(Expert Info)*

O Wireshark também detecta estados específicos de protocolos para ajudar os analistas a detectar facilmente possíveis anomalias e problemas. Note que estas são apenas sugestões, e há sempre uma chance de ter falsos positivos / negativos. Informações especializadas podem fornecer um grupo de categorias em três diferentes gravidades. Os detalhes são mostrados na tabela abaixo.

| **Severidade** | **Cor**      | **Informação**                                                    |
| -------------- | ------------ | ----------------------------------------------------------------- |
| **Bate-papo**  | **Azul**     | Informações sobre o fluxo de trabalho habitual.                   |
| **Nota**       | **Cyan**     | Eventos notáveis como códigos de erro de aplicação.               |
| **Avisar**     | **Amarelo**  | Avisos como códigos de erro incomuns ou declarações de problemas. |
| **Erro**       | **Vermelho** | Problemas como pacotes malformados.                               |

Grupos de informações frequentemente encontrados estão listados na tabela abaixo. Você pode consultar a [documentação oficial](https://www.wireshark.org/docs/) do Wireshark para obter mais informações sobre as entradas de informações de especialistas.

| **Grupo**               | **Informação**                   | **Grupo**      | **Informação**                  |
| ----------------------- | -------------------------------- | -------------- | ------------------------------- |
| **Soma de verificação** | Erros de soma de verificação     | **Depreciado** | Uso de protocolo obsoleto       |
| **Comentário**          | Detecção de comentário de pacote | **Malformado** | Detecção de pacotes malformados |

Você pode usar a **"seção inferior inferior esquerda"** na barra de status ou no menu **"Analise --> Expert Information"** para visualizar todas as entradas de informações disponíveis por meio de uma caixa de diálogo. Ele mostrará o número do pacote, resumo, protocolo de grupo e ocorrência total.

![Wireshark - informações de especialistas](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31917b6f1e846d3383218cabf1c07caf.png)

---
# Filtragem de Pacotes

O Wireshark tem um poderoso motor de filtro que ajuda os analistas a reduzir o tráfego e se concentrar no evento de interesse. O Wireshark possui dois tipos de abordagens de filtragem: filtros de captura e exibição. Os filtros de captura são usados para **"capturar"** apenas os pacotes válidos para o filtro usado. Filtros de exibição são usados para **"visualização"** dos pacotes válidos para o filtro usado. Vamos discutir as diferenças desses filtros e uso avançado na próxima sala. Agora vamos nos concentrar no uso básico dos filtros de exibição, o que ajudará os analistas em primeiro lugar.

Filtros são consultas específicas projetadas para protocolos disponíveis na referência oficial do protocolo do Wireshark. Embora os filtros sejam apenas a opção de investigar o evento de interesse, existem duas maneiras diferentes de filtrar o tráfego e remover o ruído do arquivo de captura. A primeira usa consultas e a segunda usa o menu do botão direito do mouse. O Wireshark fornece uma interface gráfica poderosa, e há uma regra de ouro para analistas que não querem escrever consultas para tarefas básicas: **"Se você pode clicar nela, você pode filtrá-la e copiá-la"**

## Aplicar como Filtro

Esta é a forma mais básica de filtrar o tráfego. Ao investigar um arquivo de captura, você pode clicar no campo que deseja filtrar e usar o menu "clique com o botão direito do mouse" ou **"Analise** para filtrar o valor específico. Observe que o número de pacotes totais e exibidos são sempre mostrados na barra de status.

![Wireshark - aplicar como filtro](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124912.gif)

## Filtro de conversa

Quando você usa a opção "Aplicar como filtro", você filtrará apenas uma única entidade do pacote. Esta opção é uma boa maneira de investigar um valor particular em pacotes. No entanto, suponha que você queira investigar um número de pacote específico e todos os pacotes vinculados, concentrando-se em endereços IP e números de porta. Nesse caso, a opção "Filtro de Conversação" ajuda você a visualizar apenas os pacotes relacionados e ocultar o resto dos pacotes facilmente. Você pode usar o menu "clique com o botão direito do mouse" ou **"Analise --> Conversation** Filter" menu para filtrar conversas.

![Wireshark - filtro de conversa](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124660.gif)

## Conversa Colorida

Esta opção é semelhante ao "Filtramento de Conversação" com uma diferença. Ele destaca os pacotes vinculados sem aplicar um filtro de exibição e diminuir o número de pacotes visualizados. Esta opção funciona com a opção "Regras de colorir" o anúncio altera as cores do pacote sem considerar a regra de cores aplicada anteriormente. Você pode usar o menu "clicar com o botão direito do mouse" ou **"Exibir --> Conversa Colorise"** para colorir um pacote vinculado em um único clique. Observe que você pode usar o menu **"Exibir --> Conversa Colorise --> Redefinir** colorização" para desfazer essa operação.

![Wireshark - colorir conversa](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124692.gif)

## Preparar como filtro

Semelhante ao "Aplicar como Filtro", esta opção ajuda os analistas a criar filtros de exibição usando o menu "clique com o botão direito do mouse". No entanto, ao contrário do anterior, este modelo não aplica os filtros após a escolha. Ele adiciona a consulta necessária ao painel e aguarda o comando de execução (inserir) ou outra opção de filtragem escolhida usando **o ".. e/ou..."** no "menu do botão direito do mouse".

![Wireshark - prepare-se como filtro](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124871.gif)

## Aplicar como Coluna

Por padrão, o painel de lista de pacotes fornece informações básicas sobre cada pacote. Você pode usar o menu "clicar com o botão direito do mouse" ou **"Analisar --> Aplicar como coluna** " para adicionar colunas ao painel da lista de pacotes. Depois de clicar em um valor e aplicá-lo como uma coluna, ele estará visível no painel da lista de pacotes. Essa função ajuda os analistas a examinar a aparência de um valor/campo específico nos pacotes disponíveis no arquivo de captura. Você pode ativar/desativar as colunas mostradas no painel de lista de pacotes clicando na parte superior do painel de lista de pacotes.

![Wireshark - aplicar como coluna](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124914.gif)

## Follow Stream (Seguir fluxo de pacotes)

O Wireshark exibe tudo no tamanho da porção do pacote. No entanto, é possível reconstruir os fluxos e visualizar o tráfego bruto como é apresentado no nível da aplicação. Seguindo o protocolo, os streams ajudam os analistas a recriar os dados em nível de aplicativo e entender o evento de interesse. Também é possível visualizar os dados de protocolo não criptografados, como nomes de usuário, senhas e outros dados transferidos.

Você pode usar o **TCPUDPHTTP**menu "clique com o botão direito do mouse" ou **"Analise** **--> Follow TCP / UDP / HTTP Stream"** para seguir os fluxos de tráfego. Os fluxos são mostrados em uma caixa de diálogo separada; pacotes originários do servidor são destacados com azul, e aqueles originários do cliente são destacados com vermelho.

![Wireshark - siga o fluxo](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124617.gif)

Depois de seguir um fluxo, o Wireshark cria e aplica automaticamente o filtro necessário para visualizar o fluxo específico. Lembre-se, uma vez que um filtro é aplicado, o número dos pacotes visualizados será alterado. Você precisará usar o botão " **X** **button**" localizado no lado superior direito da barra de filtro de exibição para remover o filtro de exibição e visualizar todos os pacotes disponíveis no arquivo de captura.

## Consultas de filtro de exibição simples

A maneira mais fácil de filtrar rapidamente a enorme quantidade de pacotes, é aplicando um filtro de exibição usando a barra "Aplicar um filtro de exibição" mostrado na imagem abaixo.

![Filtro de exibição](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124666.png)

Existem muitas consultas de filtro disponíveis e cada uma delas pode ser extensivamente ajustada para mostrar resultados muito específicos. Abaixo estão alguns filtros simples para começar.

**Filtrar por nome do protocolo ou porta**  
Existem duas maneiras básicas de filtrar com base em um protocolo específico: por nome do protocolo e por número de porta do protocolo.

Para filtrar por **nome** do **protocolo**, basta digitar o nome do protocolo e clicar em entrar ou clicar no botão de seta no lado direito da barra de filtro de exibição. O GIF abaixo mostra um exemplo de como filtrar o tráfego http. Você pode também filtrar outros protocolos usando palavras-chave como `arp`, `dhcp`, `ftp`, `smtp`, `pop`, `imap`, e mais.

![Filtro de exibição: Nome do protocolo](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404126755.gif)

Para filtrar por **número de porta de protocolo**, você pode usar a estrutura " tcp.port == <número de porta>" ou " udp.port == <número de porta>". Por exemplo, se você quiser ver apenas pacotes http, você usaria o filtro " tcp.port == 80" e, em seguida, digitar. O GIF abaixo mostra um exemplo do filtro de porta http.

![Filtro de exibição: Número da porta](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404126766.gif)

**Filtrar por IP**  
Ao analisar uma captura de pacote, muitas vezes há a necessidade de filtrar um IP específico. Para filtrar um IP específico, você pode usar a estrutura "ip.addr == <endereço IP>". Então, se você precisar procurar o IP 192.168.1.2, seu filtro seria "ip.addr == 192.168.1.2". O GIF abaixo mostra um exemplo do filtro IP.

![Filtro de exibição: IP](https://tryhackme-images.s3.amazonaws.com/user-uploads/66c44fd9733427ea1181ad58/room-content/66c44fd9733427ea1181ad58-1768404124724.gif)

