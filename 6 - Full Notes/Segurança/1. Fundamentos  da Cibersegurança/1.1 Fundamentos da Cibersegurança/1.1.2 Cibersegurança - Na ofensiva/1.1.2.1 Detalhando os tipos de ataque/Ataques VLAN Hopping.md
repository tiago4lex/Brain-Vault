2025-06-04 13:01

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[VLAN]]

----
# Introdução

## 1. Definição

VLAN Hopping é um ataque de rede que permite a um invasor **escapar da segmentação de VLAN** e acessar tráfego de outras VLANS não autorizadas, violando a segurança da arquitetura de redes comutadas.

## 2. Porque é Perigoso?

- Permite **acesso lateral** entre VLANs (ex: um invasor na VLAN de visitante acessar a VLAN administrativa).
- Viola o princípio de **isolamento de redes**.
- Pode levar a roubo de dados, interceptação de tráfego ou ataques MITM *(Man-In-The-Middle)*.

----
# Como Funciona o VLAN Hopping?

## 1. Switch Spoofing (Falsificação de Switch)

- **Objetivo:** Enganar o switch para que ele trate o host do atacante como outro switch.
- **Mecanismo:**
	- O atacante configura sua interface de rede para emular um trunk (802.1Q).
	- Se o switch estivar mal configurada (auto-negociação de trunk ativada), ele pode aceitar a conexão como trunk.
	- **Resultado:** O atacante recebe tráfego de todas as VLANs.

## 2. Double Tagging *(VLAN Double Encapsulation)*

- **Objetivo:** Enviar quadros com **dois tags VLAN** para bypassar restrições.
- **Mecanismo:**
	1. O atacante envia um pacote com:
		- **Tag 1:** VLAN nativa do trunk (ex: VLAN 1, que muitas vezes não é filtrada).
		- **Tag 2:** VLAN alvo (ex: VLAN 100, a ser atacada).
	2. O primeiro switch remove a Tag 1 (pois é a VLAN nativa) e encaminha o quadro.
	3. O segundo switch processa apenas a Tag 2 enviando o tráfego para a VLAN alvo.
- **Requisitos:**
	- O atacante deve estar conectado a uma porta na **VLAN nativa**.
	- O switch não deve filtrar quadros com múltiplas tags.

---
# Ferramentas Usadas em VLAN Hopping

| **Ferramenta** | **Descrição**                                                   | **Uso em VLAN Hopping**                                |
| -------------- | --------------------------------------------------------------- | ------------------------------------------------------ |
| Yersinia       | Framework para ataques em protocolos de rede (incluindo 802.1Q) | Gera quadros maliciosos para Switch Spoofing           |
| Scapy (Python) | Biblioteca para manipulação de pacotes                          | Cria pacotes com double tagging                        |
| Wireshark      | Analisador de tráfego                                           | Identifica VLANs e verifica tags                       |
| Macof          | Flood de endereços MAC                                          | Usada para forçar um switch a entrar em modo promíscuo |

---
# Exemplos Práticos

## Exemplo 1: Switch Spoofing com Yersinia

```bash
yersinia -G # Abre a interface gráfica
```

1. Selecione o ataque "802.1Q"
2. Configure a interface de rede (ex: `eh0`)
3. Defina a VLAN alvo (ex: VLAN 100)
4. Inicie o ataque para negociar um trunk não autorizado

**Resultado:** O atacante recebe tráfego da VLAN 100.

## Exemplo 2: Double Tagging com Scapy (Python)

```python
from scapy.all import *
pacote = Ether (dst="00:11:22:33:44:55") / Dot1Q(vlan=1) / Dot1Q(vlan=100) / IP(dst="10.0.100.5") / ICMP()

sendp(pacote, iface="eth0")
```

**Funcionamento:**

- O primeiro switch remove a tag da VLAN 1 (nativa)
- O segundo switch encaminha o pacote para a VLAN 100

---
# Como se proteger?

## 1. Boas Práticas para Mitigação

- **Desative VLAN nativa em trunks:**

```cisco
switchport trunk native vlan 999 # Usar uma VLAN não utilizada
```

- **Desative auto-negociação de trunk:**

```cisco
show vlan brief
show interfaces trunk
```

- **Monitorar tentativas de VLAN Hopping:**

```cisco
show port-security
```

---
# Conclusão

VLAN Hopping é uma técnica crítica em ataques de rede que explora más configurações em switches. **Redes corporativas devem implementar hardening de VLANs** para evitar violações.
