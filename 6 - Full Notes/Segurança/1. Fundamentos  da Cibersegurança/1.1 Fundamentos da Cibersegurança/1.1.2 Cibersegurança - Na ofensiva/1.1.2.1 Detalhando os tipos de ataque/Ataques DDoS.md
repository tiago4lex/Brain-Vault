2025-06-01 23:34

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[DDoS]] | [[Pentest]]

----
# Introdução

Ataques **DDoS *(Distributed Denial of Service)*** são uma das ameaças mais comuns na segurança cibernética. <span style="background:#fff88f">Eles visam tornar um serviço, servidor ou rede indisponível, sobrecarregando-o com um grande volume de tráfego.</span>

Este documento abordará:

- O que são ataques DDoS
- Como eles funcionam
- Métodos de execução
- Ferramentas para testes de penetração *(pentest)*
- Como usar essas ferramentas

---
# O que é um Ataque DDoS?

Um ataque DDoS <span style="background:#fff88f">é uma tentativa maliciosa de interromper o tráfego normal de um servidor, serviço ou rede, sobreacrregando-o com uma inundação de solicitações de múltiplas fontes</span> (geralmente dispositivos infectados, chamados de ***botnet***).

## Diferença entre DoS e DDoS

- **DoS *(Denial of Service)*:** Vem de uma única fonte
- **DDoS *(Distributed Denial of Service)*:** Vem de múltiplas fontes distribuídas, tornando-o mais difícil de mitigar.

---
# Como Funcionam os Ataques DDoS?

Os ataques DDoS exploram protocolos de rede e vulnerabilidades para sobrecarregar o alvo. Eles podem ser categorizados em três tipos principais:

## 1. Ataques de Camada de Aplicação (Layer 7)

- **Alvo:** Serviços web (HTTP/HTTPS)
- **Exemplo:** Envio massivo de requisições a uma página web até que o servidor fique indisponível.
- **Ferramentas:** Slowloris, HTTP Flood.

## 2. Ataques de Protocolo (Layer 3/4)

- **Alvo:** Infraestrutura de rede (roteadores, firewalls).
- **Exemplos:**
	- **SYN Flood:** Explora o handshake TCP, deixando conexões em estado "SYN_RECEIVED".
	- **UDP Flood:** Inunda a vítima com pacotes UDP.
	- **ICMP Flood *(Ping Flood)*:** Envia muitos pacotes ICMP *(ping)*.

## 3. Ataques Volumétricos

- **Alvo:** Largura de banda do alvo.
- **Exemplo:** DNS Amplification (usa servidores DNS públicos para amplificar o tráfego).

---
# Como são realizados Ataques DDoS?

1. **Criação de uma Botnet:**
	- Dispositivos infectados (IoT, servidores, PCs) são controlados por um atacante.
	- Malwares como **Mirai** são usados para criar botnets.

2. **Identificação do Alvo:**
	- Um servidor, site ou serviço específico é escolhido

3. **Início do Ataque:**
	- O atacante  comanda a botnet para enviar tráfego massivo ao alvo.

---
# Ferramentas para Testar Ataques DDoS em Pentest

## 1. LOIC (Low Orbit Ion Cannon)

- **Função:** Realiza ataques Dos/UDP Flood.
- **Como usar:**

```bash
# Baixar e executar (Windows/Linux com Wine)
java -jar LOIC.jar
```

- Definir IP e porta do alvo.
- Configurar threads e intensidade.

## 2. Hping3

- **Função:** Ataques SYN Flood, ICMP Flood.
- **Como Usar:**

```bash
hping3 -S -p 80 --flood [IP-alvo]
```

- `-S` = SYN Flood
- `--flood` = Modo de inundação

## 3. [[Slowloris - Ferramenta de DDoS]]

- **Função:** Ataque Layer 7 (HTTP)
- **Como usar (Python):**

```bash
python slowloris.py [IP-alvo] -p 80
```

## 4. GoldenEye

- **Função:** HTTP Flood.
- **Como usar:**

```bash
python goldeneye.py http://site-avlo -w 100 -s 1000
```

## 5. Xerxes

- **Função:** Ataque DoS em camada de aplicação.
- **Como usar:**

```bash
./xerxes [IP] 80
```

---
# Como se Proteger de Ataques DDoS?

- **Mitigação em Nuvem:** Usar Cloudflare, Akamai ou AWS Shield.
- **Firewalls e IPS:** Configurar regras para filtrar tráfego malicioso.
- **Rate Limiting:** Limitar requisições por IP.
- **Anycast DNS:** Distribuir tráfego em vários servidores.

---
# Conclusão

Ataques DDoS são uma ameaça significativa, mas entender seu funcionamento e ferramentas ajuda na prevenção e testes de segurança.

---
# Referências

- [OWASP DDoS Protection](https://owasp.org/)
- [Cloudflare DDoS Guide](https://www.cloudflare.com/learning/ddos/)

**Aviso Legal**: O uso indevido dessas informações pode ser crime. Utilize apenas em ambientes autorizados.