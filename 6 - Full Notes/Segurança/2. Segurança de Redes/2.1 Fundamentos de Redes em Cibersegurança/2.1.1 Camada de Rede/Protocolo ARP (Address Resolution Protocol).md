2025-12-16 09:50

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[ARP]]

----
# Introdução

O **ARP (Address Resolution Protocol)** é um protocolo fundamental das redes TCP/IP, responsável por **associar endereços IP a endereços MAC** dentro de uma rede local (LAN).

Sempre que um dispositivo precisa se comunicar com outro na mesma rede e conhece apenas o IP de destino, o ARP entra em ação para descobrir qual é o endereço físico (MAC) correspondente.

Em cibersegurança, o ARP é extremamente relevante porque **não possui mecanismos de autenticação**, tornando-se um alvo frequente de ataques.

![[Pasted image 20251216065353.png]]

---
# Em qual camada o ARP atua?

- **Modelo OSI:** Camada 2 (Enlace de Dados)
- **Modelo TCP/IP:** Camada de Acesso à Rede

Apesar de lidar com IP (Camada 3), o ARP é considerado um protocolo de enlace, pois opera diretamente com endereços MAC.

---
# Para que serve o ARP?

O ARP serve para:

- resolver endereços IP em endereços MAC;
- permitir comunicação dentro da rede local;
- viabilizar o envio correto de quadros Ethernet.

Sem o ARP, dispositivos não conseguiriam se comunicar em uma LAN.

---
# Como o protocolo ARP funciona?

O funcionamento do ARP ocorre em quatro etapas principais:

![[Pasted image 20251216065344.png]]

## 1. Verificação da Tabela ARP

Antes de enviar uma requisição, o dispositivo verifica sua **tabela ARP (ARP Cache)**.

- Se o IP já estiver mapeado → comunicação ocorre normalmente;
- Se não estiver → inicia o processo ARP.

## 2. ARP Request

O dispositivo envia um **ARP Request** em broadcast:

> “Quem tem o IP 192.168.1.1? Responda para 192.168.1.10”

Características:

- enviado para **FF:FF:FF:FF:FF:FF**;
- todos os dispositivos da rede recebem.

## 3. ARP Reply

O dispositivo que possui o IP solicitado responde com um **ARP Reply** em unicast:

- informa seu endereço MAC;
- apenas o solicitante recebe a resposta.

## 4. Atualização da Tabela ARP

O dispositivo solicitante salva a associação IP ↔ MAC na tabela ARP por um tempo limitado.

---
# Tabela ARP (ARP Cache)

A tabela ARP armazena associações temporárias entre IP e MAC.

## Exemplo de Tabela ARP

| **IP**       | **Endereço MAC**  | **Interface** |
| ------------ | ----------------- | ------------- |
| 192.168.1.1  | 00:11:22:33:44:55 | eht0          |
| 192.168.1.10 | aa:bb:cc:dd:ee:ff | eth0          |

**Comandos comuns:**

- Linux: `arp -a` ou `ip neigh`]
- Windows: `arp -a`

---
# Tipos de Mensagens ARP

## 1. ARP Request

- Broadcast    
- Solicita endereço MAC

## 2. ARP Reply

- Unicast
- Responde com endereço MAC

## 3. Gratuitous ARP

- Enviado sem solicitação prévia
- Usado para:

    - detectar IP duplicado;
    - atualizar caches ARP;
    - failover (ex.: VRRP, HSRP)

---
# Vulnerabilidades do Protocolo ARP

O ARP **não possui autenticação**, o que abre espaço para ataques graves.

## 1. ARP Spoofing / ARP Poisoning

Ataque mais comum envolvendo ARP.

O atacante envia ARP Replies falsos associando:

- IP do gateway → MAC do atacante

Consequências:

- Man-in-the-Middle (MITM);
- interceptação de tráfego;
- modificação de pacotes;
- roubo de credenciais.

## 2. Man-in-the-Middle (MITM)

Explorando o ARP Spoofing, o atacante se posiciona entre duas vítimas.

Impactos:

- espionagem de dados;
- injeção de malware;
- sequestro de sessão.

## 3. DoS via ARP

Envio massivo de respostas ARP falsas pode:

- corromper tabelas ARP;
- causar perda de conectividade.

## 4. ARP Cache Poisoning Persistente

Alguns sistemas mantêm entradas ARP por longos períodos, facilitando ataques prolongados.

---
# ARP em ataques Reais

- Captura de senhas HTTP;
- Downgrade de HTTPS;
- Redirecionamento para páginas falsas;
- Ataques combinados com DNS Spoofing.

---
# Ferramentas para Ataques e Testes ARP

## Ettercap

- MITM baseado em ARP;
- sniffing e modificação de pacotes.

## Bettercap

- Ataques ARP modernos;
- integração com Wi-Fi e BLE.

## Arpspoof (dsniff)

- Simples e eficiente para ARP Poisoning.

## Cain & Abel

- Ferramenta clássica para ARP MITM (Windows).

## Wireshark

- Análise de tráfego ARP;
- detecção de ARP Replies suspeitos;

---
# Detecção de Ataques ARP

Sinais de alerta:

- múltiplos IPs usando o mesmo MAC;
- mudanças frequentes na tabela ARP;
- ARP Replies não solicitados;
- latência ou perda de conexão inesperada.

---
# Mitigação e Boas Práticas de Segurança

## 1. ARP Estático

- Associa IP ↔ MAC manualmente
- Pouco escalável

## 2. Dynamic ARP Inspection (DAI)

- Recurso de switches gerenciáveis;
- valida ARP Replies.

## 3. DHCP Snooping

- Base para DAI;
- impede servidores DHCP falsos.

## 4. Segmentação de Rede

- VLANs reduzem impacto do ataque.

## 5. Ferramentas de Monitoramento

- arpwatch
- IDS/IPS

## 6. Uso de Criptografia

- HTTPS, SSH e VPNs minimizam impacto do MITM.

---
# ARP vs IPv6 (NDP)

No IPv6, o ARP foi substituído pelo **NDP (Neighbor Discovery Protocol)**, que:

- utiliza ICMPv6;
- possui mecanismos de segurança melhores;
- ainda assim pode ser explorado sem proteções adicionais.

---
# Importância do ARP para Cibersegurança

O ARP é simples, essencial e perigoso quando mal protegido. Ele está presente em praticamente todas as redes locais e é frequentemente explorado em ataques internos.

Dominar o funcionamento do ARP permite:

- detectar ataques MITM;
- proteger redes corporativas;
- realizar pentests realistas;
- fortalecer políticas de segurança de camada 2.

---
# Conclusão

O protocolo ARP é um dos pilares da comunicação em redes locais, mas também representa um dos maiores riscos de segurança na camada de enlace.

Por não possuir autenticação nativa, ele depende fortemente de boas práticas, configurações corretas de switches e uso de criptografia para mitigar ataques.

Para profissionais de cibersegurança, compreender profundamente o ARP é indispensável para análise de tráfego, pentest e defesa de redes modernas.