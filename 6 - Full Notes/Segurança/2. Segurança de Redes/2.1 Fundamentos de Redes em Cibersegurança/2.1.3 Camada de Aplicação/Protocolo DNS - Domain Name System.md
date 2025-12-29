2025-12-16 16:04

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[DNS]]

----
# Introdução

O **DNS *(Domain Name System)*** é um dos protocolos mais críticos da internet. Ele é responsável por **traduzir nomes de domínios legíveis** por humanos (como `www.exemplo.com`) em **endereços IP** que os computadores utilizam para se comunicar.

Sem o DNS, os usuários precisariam memorizar endereços IP numéricos, tornando a navegação impraticável. Em cibersegurança, o DNS é extremamente sensível, pois **controla o direcionamento do tráfego**, sendo alvo frequente de ataques.

![[Pasted image 20251216161258.png]]

---
# Em qual camada o DNS atua?

- **Modelo OSI**: Camada 7 → Aplicação.
- **Modelo TCP/IP:** Camada de Aplicação.

O DNS normalmente utiliza **UDP** na porta 53, mas pode usar TCP em casos específicos, como:

- transferências de zona (AXFR);
- respostas grandes;
- DNSSEC.

---
# Para que serve o DNS?

O DNS serve para:

- resolver nomes de domínio em endereços IP;
- localizar servidores de e-mail;
- permitir balanceamento de carga;
- facilitar a navegação na internet;
- suportar diversos serviços críticos.

---
# Como o DNS funciona?

O processo de resolução de nomes ocorre em etapas.

![[Pasted image 20251216160925.png]]

## 1. Tipos de Servidores DNS

- **DNS Resolver (Recursivo):** recebe a requisição do cliente.
- **Servidor Root:** aponta para servidores TLD.
- **Servidor TLD:** aponta para servidores autoritativos.
- **Servidor Autoritativo:** responde com o IP final.

## 2. Processo de Resolução DNS

1. O cliente consulta o **resolver DNS**.
2. O resolver pergunta a um **Root Server**.
3. O Root indica o TLD (.com, .org, .br).
4. O TLD indica o **Servidor Autoritativo**.
5. O servidor autoritativo retorna o IP.
6. O resolver entrega a resposta ao cliente.

---
# Tipos de consultas DNS

- **Consulta Recursiva:** o resolver faz todo o trabalho.
- **Consulta Interativa:** o servidor responde parcialmente.
- **Consulta Reversa:** IP → nome (PTR)

---
# Registros DNS

| **Tipo** | **Função**             |
| -------- | ---------------------- |
| A        | Nome → IPv4            |
| AAAA     | Nome → IPv6            |
| CNAME    | Alias                  |
| MX       | Servidor de e-mail     |
| NS       | Servidor autoritativo  |
| TXT      | Informações adicionais |
| PTR      | Resolução reserva      |
| SRV      | Serviços específicos   |

---
# Vulnerabilidades do Protocolo DNS

O DNS foi criado sem foco em segurança, o que gera diversas vulnerabilidades.

## 1. DNS Spoofing / Cache Poisoning

O atacante injeta respostas falsas no cache DNS.

**Consequências:**

- redirecionamento para sites maliciosos;
- roubo de credenciais;
- ataques MITM.

![[Pasted image 20251216161904.png]]

## 2. DNS Hijacking

Modificação do servidor DNS usado pela vítima.

Pode ocorrer via:

- malware;
- roteadores comprometidos;
- ataques a ISPs.

![[Pasted image 20251216162000.png]]

## 3. DNS Amplifications (DDoS)

Explora o DNS via UDP.

- pequenas requisições geram grandes respostas;
- IP de origem é falsificado;
- tráfego massivo é direcionado à vítima.

![[Pasted image 20251216162032.png]]

## 4. Zone Transfer Inseguro (AXFR)

Permite copiar todos os registros DNS.

**Impacto:**

- mapeamento completo da infraestrutura;
- facilita ataques direcionados.

## 5. Subdomain Takeover

Ocorre quando um subdomínio aponta para um serviço inexistente.

**Impacto:**

- controle de subdomínios;
- phishing;
- comprometimento de reputação.

![[Pasted image 20251216162313.png]]

## 6. DNS Tunneling

Uso do DNS para exfiltração de dados.

**Usado por:**

- malware;
- bypass de firewalls.

![[Pasted image 20251216162443.png]]

---
# Ataques reais envolvendo DNS

- Campanhas de phishing em larga escala;
- Botnets usando DNS como C2;
- DDoS por amplificação;
- Redirecionamento de tráfego corporativo.

---
# Ferramentas para testes e análise de DNS

## Ferramentas de Consulta

- dig
- nslookup
- host

## Enumeração e Pentest

- DNSenum
- DNSrecon
- Fierce
- Amass

## Ataques e Análise Avançada

- Metasploit
- dnsspoof
- Responder
- Bettercap

## Monitoramento

- Wireshark
- tcpdump

---
# Mitigações e Boas Práticas de Segurança DNS

## 1. DNSSEC

- assina respostas DNS;
- impede spoofing e poisoning.

## 2. Restringir Transferências de Zona

- permitir AXFR apenas para IPs autorizados.

## 3. Hardening de Servidores DNS

- ocultar versão do servidor;
- atualizar software;
- separar DNS recursivo e autoritativo.

## 4. Proteção contra DDoS

- rate limiting;
- Anycast;
- firewalls;
- serviços anti-DDoS.

## 5. Monitoramento e Logs


- detectar consultas anômalas;
- identificar tunneling.

## 6. Uso de DNS Seguro para Clientes

- DNS over HTTPS (DoH);
- DNS over TLS (DoT).

---
# DNS over HTTPS (DoH) e DNS over TLS (DoT)

Essas tecnologias criptografam consultas DNS.

**Vantagens:**

- privacidade;
- proteção contra interceptação.

**Desafios:**

- dificulta inspeção por IDS;
- pode ocultar malware.

---
# Importância do DNS para Cibersegurança

O DNS é um dos principais alvos de ataque porque controla o fluxo de comunicação.

Dominar DNS permite:

- detectar phishing;    
- bloquear domínios maliciosos;
- responder a incidentes;
- realizar pentests eficientes;
- proteger infraestruturas críticas.

---
# Conclusão

O protocolo DNS é essencial para o funcionamento da internet, mas também representa um grande risco de segurança se mal configurado.

Por não possuir segurança nativa, ele depende de mecanismos adicionais, monitoramento constante e boas práticas para mitigar ataques.

Para profissionais de cibersegurança, compreender profundamente o DNS é indispensável para atuar em defesa de redes, SOC, pentest e resposta a incidentes.