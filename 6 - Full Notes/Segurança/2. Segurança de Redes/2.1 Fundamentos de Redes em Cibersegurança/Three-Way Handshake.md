2025-12-06 22:44

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[Wireshark]] | [[Nmap]]

----
# Introdução

O ***Three-Way Handshake*** é o processo usado pelo protocolo TCP *(Transmission Control Protocol)* para estabelecer uma conexão confiável entre cliente e servidor. 

Ele garante que ambas as partes estejam prontas para comunicar sincronizem números de sequência e confirmem a recepção das mensagens iniciais.

O handshake é fundamental para o funcionamento de serviços como:

- HTTP/HTTPS
- FTP
- SSH
- SMTP

Por ser um componente crítico, ele também é alvo de ataques que exploram falhas no gerenciamento de conexões.

![[what-is-a-tcp-3-way-handshake-process-three-way-handshaking-establishing-connection-6a724e77ba96e241.jpg]]

---
# O que é o Three-Way Handshake?

É o processo de **três passos** usado para iniciar uma conexão TCP. O seu objetivo é:

- sincronizar números de sequência (SEQ);
- confirmar a recepção de pacotes;
- estabelecer uma conexão confiável antes da transmissão de dados.

Os três passos são:

1. **SYN** - Cliente pede conexão.
2. **SYN/ACK** - Servidor aceita e responde.
3. **ACK** - Cliente confirma e a conexão é estabelecida.

---
# Como o Three-Way Handshake funciona?

## Etapa 1: Cliente → Servidor (SYN)

O cliente envia um pacote com o bit **SYN = 1** para solicitar uma conexão.

- Define um valor de número de sequência inicial (ISN - *Initial Sequence Number*)
- Exemplo: `SEQ = 1000`

## Etapa 2: Servidor → Cliente (SYN/ACK)

O servidor responde confirmando o SYN do cliente e envia seu próprio número de sequência.

- Exemplo: `SEQ = 3000` e `ACK = 1001`
- Aqui o ACK confirma que o servidor recebeu o valor `1000` e espera o próximo (`1001`)

## Etapa 3: Cliente → Servidor (ACK)

O cliente confirma a resposta do servidor.

- Exemplo: `ACK = 3001`.
- Agora a conexão está estabelecida.

## Representação Visual

```
CLIENTE SERVIDOR

| ----------- SYN (SEQ=1000) -----------> |
| <------ SYN/ACK (SEQ=3000, ACK=1001) -- |
| ----------- ACK (ACK=3001) -----------> |
```

Após isso, começa a troca de dados.

---
# Por que o Handshake é importante?

- Cria uma conexão confiável;
- Sincroniza números de sequência;
- Evita perda de pacotes;
- Permite retransmissão corretas;
- Impede que dados sejam enviados para hosts que não esperam a comunicação.

Em cibersegurança, o entendimento desse processo é vital para:

- detecção de ataques de rede;
- análise de tráfego com ferramentas como Wireshark;
- testes de pentest e hardening de firewalls.

---
# Vulnerabilidades do Three-Way Handshake

Embora confiável, o protocolo TCP apresenta vulnerabilidades que atacantes podem explorar.

## 1. SYN Flood Attack

Um dos ataques mais conhecidos.

O atacante envia milhares de pacotes **SYN falsos** ao servidor e **não envia ACK** final.

Consequência:

- Tabelas de conexão do servidor ficam cheias;
- Recursos são consumidos;
- Servidores legítimos não conseguem estabelecer novas conexões.

É uma forma de DDoS na camada de transporte.

## 2. IP Spoofing

O atacante falsifica IPs de origem nos pacotes SYN.

Impactos:

- dificulta rastreamento;
- facilita ataques de SYN Flood;
- pode confundir logs.

## 3. Session Hijacking

Se o atacante adivinhar ou interceptar números de sequência, pode assumir conexões válidas.

## 4. Reset Injection (TCP RST Attack)

Atacantes podem enviar pacotes **RST falsos** para encerrar conexões legítimas.

## 5. ACK Scan

Técnica usada para identificar portas filtradas de firewalls.

## 6. Half-Open Connections

Se o handshake não se completa, muitas conexões "semiabertas" podem sobrecarregar o servidor.

---
# Mitigações de Ataques ao Three-Way Handshake

## 1. SYN Cookies

Forma moderna e eficiente de mitigar SYN Flood.

## 2. Firewalls Statefull

Monitoramento estado das conexões e bloqueiam comportamentos suspeitos.

## 3. Rate Limiting

Limita tentativas de conexão por IP.

## 4. TCP Intercept

Firewall intercepta handshakes e age como intermediário.

## 5. Filtragem de IP Spoofing

- BCP 38

## 6. Proteções contra Session Hijacking

- TLS/SSH
- ISN imprevisível
- Criptografia forte

---
# Ferramentas para testar vulnerabilidades no Three-Way Handshake

## 1. Wireshark

- captura e analisa pacotes TCP;
- permite ver o handshake em detalhe;
- útil para auditorias de rede.

## 2. Nmap

Testa portas e verifica como o TCP responde.
Modos úteis:

- `-sS` (SYN Scan)
- `-sA` (ACK Scan)
- `-sN` (Null Scan)

## 3. Hping3

Ferramenta avançada para criação de pacotes TCP personalizados

**Exemplos:**

- simular SYN Flood;
- testar spoofing;
- investigar respostas irregulares do servidor.

## 4. Metasploit

Possui módulos para explorar falhas de gerenciamento TCP.

## 5. Scapy

Framework Python para criar pacotes TCP customizados.

Útil para:

- testar ISN previsível.
- simular ataques de hijacking.

## LOIC/HOIC (DDoS Tools)

Usadas apenas em laboratórios controlados.

---
# Visualizando Handshake com Wireshark

Exemplo de filtros úteis:

- `tcp.flags.syn == 1`
- `tcp.flags.syn == 1 && tcp.flags.ack == 0` → SYN
- `tcp.flags.syn == 1 && tcp.flags.ack == 1` → SYN/ACK
- `tcp.flags.ack == 1 && tcp.flags.syn == 0` → ACK

---
# Importância para Cibersegurança

O entendimento do Three-Way Handshake é essencial para:

- análise de logs e incidentes;
- defesa contra DoS/DDoS;
- configuração de firewalls;
- detecção de tráfego malicioso;
- pentests de rede;
- engenharia reversa de malwares que usam sockets.

Profissionais que dominam a dinâmica do handshake conseguem identificar:

- conexões inválidas;
- padrões de ataque;
- anomalias em tráfego legítimo.

---
# Conclusão

O Three-Way Handshake é um dos pilares da comunicação segura e confiável na internet. No entanto, também pode ser alvo de ataques que exploram o gerenciamento de conexões TCP.

Entender profundamente seu funcionamento, suas vulnerabilidades e as ferramentas que permitem analisá-lo é indispensável para qualquer profissional de cibersegurança, especialmente nas áreas de pentest, SOC e engenharia de redes.