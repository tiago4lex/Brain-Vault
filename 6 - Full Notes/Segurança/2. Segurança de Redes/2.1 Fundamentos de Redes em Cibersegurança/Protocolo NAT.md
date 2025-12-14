2025-12-06 18:45

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[NAT]]

----
# Introdução

O **NAT** *(Network Address Translation)* é um protocolo utilizado para traduzir endereços IP privados para endereços IP públicos (e vice-versa). Ele é amplamente utilizado em redes domésticas, corporativas e de provedores de internet com o objetivo de:

- economizar endereços IPv4 públicos;
- permitir que diversos dispositivos internos compartilhem um único IP público;
- aumentar a segurança ao ocultar a estrutura interna da rede.

O NAT é uma das tecnologias fundamentais na arquitetura moderna da internet e também uma ferramenta importante em cibersegurança.

![[Network_Address_Translation_(NAT).png]]

---
# Por que o NAT existe?

O motivo principal do surgimento do NAT foi a **escassez de endereços IPv4**. Como os endereços públicos são limitados, o NAT permite que redes inteiras operem com apenas um IP público.

Além disso, ele proporciona:

- Isolamento da rede interna;
- Dificuldade para atacantes identificarem dispositivos internos;
- Flexibilidade para reorganizar a rede sem alterar a comunicação externa.

---
# Tipos de NAT

Existem diversos tipos de NAT, cada um com características próprias.

## 1. Static NAT

Associa um **IP privado fixo** a um **IP público fixo**.

**Uso comum:**

- Servidores internos que precisam ser acessados externamente (ex.: servidor web local).

**Vantagem:** acesso externo direto.
**Desvantagem:** não esconde o IP interno completamente.

## 2. Dynamic NAT

Mapeia IPs privados para um grupo de IPs públicos disponíveis, de forma dinâmica.

**Uso comum:**

- empresas com pool de IPs públicos limitado.

**Vantagem:** mais flexível que o static NAT.
**Desvantagem:** conexões podem mudar de IP público.

## 3. PAT *(Port Address Translation)*

Também conhecido como **NAT Overload**, é o tipo mais usado atualmente.

Traduz vários IPs privados para um único IP público, diferenciando sessões por **número de porta**.

**Uso comum:**

- redes domésticas e corporativas.

**Vantagens:**

- economiza IP público;
- aumenta a segurança ao mascarar a rede interna.

## 4. NAT64/ NAT46

Usado para tradução entre IPv6  IPv4.

**Uso comum:**

- transição para IPv6.

**Importância:** essencial para compatibilidade entre sistemas.

---
# Como o NAT funciona?

Quando um dispositivo interno deseja acessar a internet:

1. O pacote sai da rede privada com um IP interno (ex.: 192.168.0.10).
2. O roteador NAT substitui esse IP pelo IP público.
3. O roteador cria uma entrada na **tabela de tradução NAT**.
4. Quando a resposta chega, o roteador consulta a tabela e devolve ao dispositivo correto.

## Tabela NAT (exemplo)


| **IP Privado** | **Porta Privada** | **IP Público** | **Porta Pública** |
| -------------- | ----------------- | -------------- | ----------------- |
| 192.168.0.10   | 54532             | 200.200.50.10  | 40001             |
| 192.168.0.12   | 54533             | 200.200.50.10  | 40002             |

---
# Vantagens do NAT

## 1. Economia de IPv4

Permite que dezenas ou centenas de dispositivos usem um único IP público.

## 2. Ocultação da rede interna *(obfuscation)*

O NAT age como uma forma simples de firewall: conexões não chegam diretamente aos dispositivos internos.

## 3. Flexibilidade

Mudanças internas não afetam a comunicação com a internet.

---
# Limitações do NAT

Apesar das vantagens, o NAT apresenta alguns problemas:

- **Quebra o princípio de fim a fim** da comunicação IP.
- Protocolos que incluem endereços IP no payload podem falhar (FTP antigo, SIP, H.323).
- Algumas aplicações precisam de ajustes (ex.: jogos, VoIP, VPNs).
- NAT pode dificultar auditoria e rastreamento.

Por isso, muitos serviços usam **NAT Traversal**, com STUN, TURN e ICE.

---
# NAT e VPNs

VPNs e NAT podem entrar em conflito.

## Problemas Comuns

- VPNs site-to-site podem falhar se NAT não permitir IPsec;
- IPsec ESP não funciona bem com PAT, exigindo **NAT-T**;
- Portas UDP 500 e 4500 precisam ser abertas.

## Solução

- habilitar NAT-T (NAT Traversal) nos dois lados.

---
# NAT e Firewalls: Diferenças e Complementos

NAT não é um firewall, mas possui um efeito de segurança semelhante.

## NAT oferece

- mascaramento do IP interno.
- criação de estado de conexões (para PAT);
- redução da exposição externa.

## Firewalls oferecem

- regras de bloqueio;
- inspeção profunda de pacotes (DPI);
- proteção contra ataques.

Em cibersegurança, NAT e firewall são complementares.

---
# Aplicações do NAT em Cibersegurança

## 1. Redução da superfície de ataque

Com NAT, dispositivos internos **não são diretamente acessíveis de fora**.

## 2. Prevenção contra varreduras externas.

Um atacante não consegue identificar hosts internos através de scans simples.

## 3. Contenção de ameaças internas

Ataques internos têm mais dificuldades para sair da rede sem passar pelo NAT.

## 4. Logs centralizados de tráfego

O NAT registra conexões, facilitando análises em:

- investigações forenses;
- auditorias;
- detecção de comportamentos anômalos.

## 5. Suporte à segmentação de redes

Cada segmento pode usar seu próprio NAT.

## 6. Proteção de servidores via DNAT/Port Forwarding

Permite expor serviços de forma controlada.

**Exemplo:**

- redirecionar porta 443 externa para um servidor interno específico.

---
# Tipos de NAT em Cibersegurança

## 1. SNAT (Source Network Address Translation)

Altera o endereço de **origem**.
**Uso:** saída de dispositivos internos.

## 2. DNAT (Destination Network Address Translation)

Altera o endereço de **destino**.
**Uso:** publicar serviços internos.

## 3. Masquerade

Semelhante ao SNAT, mas usado quando o IP público muda (ex.: links dinâmicos).

## 4. Hairpin NAT

Permite que dispositivos internos acessem o IP público da rede para chegar a outro dispositivo interno.

---
# NAT e Ataques comuns

## 1. Bypass NAT

Técnicas usadas por malware para furar redes NAT.
Exemplos:

- tunelamento em DNS;
- UPnP abusado para abrir portas automaticamente.

## 2. Port Scanning de serviços redirecionados

Serviços expostos via NAT podem ser escaneados. A proteção depende do firewall.

## 3. Evasão de detecção

Malwares usam pedidos longos e diversas portas para driblar tabelas NAT.

## 4. NAT Slipstreaming

Atacante induz navegadores a abrirem portas internas, atravessando o NAT.
Mitigações:

- bloquear protocolos inseguros;
- usar firewalls modernos;
- desativar ALG inseguro.

---
# Boas Práticas para segurança com NAT

- utilizar firewalls em conjunto com NAT;
- desabilitar UPnP em roteadores;
- manter NAT estáticos apenas quando necessário;
- limitar portas expostas via DNAT;
- monitorar tabelas NAT em ambientes corporativos;
- preferir IPv6 quando possível para reduzir o uso excessivo de NAT.

---
# Conclusão

O NAT é essencial para redes modernas, tanto pela questão de economia de endereços IPv4 quanto por sua importância em **cibersegurança**, oferecendo ocultação, segmentação e proteção adicional.

Mesmo com a evolução para IPv6, o NAT continuará sendo usado por muitos anos, especialmente por seu papel estratégico em firewalls, roteadores e ambientes complexos.

Compreender profundamente o funcionamento do NAT é indispensável para profissionais de segurança que desejam configurar, proteger e monitorar redes corporativas de forma eficiente.