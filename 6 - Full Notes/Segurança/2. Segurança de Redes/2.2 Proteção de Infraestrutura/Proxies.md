2026-01-02 12:29

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]]

----
# Introdução

## O que é um Proxy?

Um **proxy** é um intermediário entre um cliente (usuário ou aplicação) e um servidor de destino. Em vez de o cliente se conectar diretamente ao servidor final, a comunicação passa primeiro pelo proxy, que pode **inspecionar, registrar, filtrar modificar ou bloquear tráfego**.

Fluxo simplificado:

```text
Cliente → Proxy → Servidor → Proxy → Cliente
```

Na prática, o proxy atua como um **representante** do cliente ou do servidor dependendo do tipo de proxy.

![[Pasted image 20260102123134.png]]

---
# Como um Proxy funciona

1. O cliente envia uma requisição ao proxy.
2. O proxy analisa a requisição (URL, método, headers, IP, etc.).
3. O proxy decide:
	- permitir,
	- negar,
	- modificar,
	- registrar (logar).
4. Se permitido, o proxy encaminha a requisição ao servidor final.
5. A resposta retorna passando novamente pelo proxy.

Em proxies HTTP, pode haver **interceptação TLS** (SSL/TLS inspection), quando configurado.

---
# Tipos de Proxy

## 1. Proxy Forward (Proxy Tradicional)

- Fica entre o cliente e a internet
- Muito usado em empresas
- Controla o que os usuários acessam

**Exemplo:**

> Usuário acessa um site → proxy verifica política → libera ou bloqueia

![[Pasted image 20260102123415.png]]

## 2. Proxy Reverse

- Fica entre a internet e o servidor
- Protege servidores internos
- Muito usado em aplicações web

**Funções comuns:**

- Balanceamento de carga
- Proteção contra ataques
- Ocultação do servidor real

**Exemplos:** Nginx, HAProxy, Apache

![[Pasted image 20260102123531.png]]

## 3. Proxy Transparente

- Usuário não sabe que está usando proxy
- Muito usado por ISPs e redes corporativas
- Não requer configuração no cliente

![[Pasted image 20260102123700.png]]

## 4. Proxy Anônimo e Elite

- Proxy anônimo: oculta IP do cliente
- Proxy elite: oculta IP e o uso de proxy

Muito usados para privacidade e testes.

## 5. Proxy SOCKS

- Trabalha em nível mais baixo
- Suporta TCP e UDP
- Não entende protocolos de aplicação (HTTP, FTP, etc.)

Muito usado com ferramentas de pentest e Tor.

![[Pasted image 20260102123941.png]]

---
# Proxies e Camadas de Rede

- Proxy HTTP/HTTPS → Camada 7 (Aplicação)
- Proxy SOCKS → Camada 5/4
- Reverse Proxy + WAF → Camada 7

---
# Exemplos de Uso de Proxy

## 1. Configurar Proxy no Linux

```bash
export http_proxy=http://192.168.1.10:3128
export https_proxy=http://192.168.1.10:3128
```

## 2. Usar Proxy com `curl`

```bash
curl -x http://127.0.0.1:8080 http://exemplo.com
```

## 3. Usar Proxy SOCKS com `proxychains`

```bash
proxychains nmap -sT exemplo.com
```


---
# Ferramentas de Proxy mais utilizadas

## Burp Suite

- Proxy HTTP/HTTPS
- Intercepta requisições
- Muito usado em pentest web

Uso típico:

- Analisar parâmetros
- Modificar requisições
- Testar vulnerabilidades

## OWASP ZAP

- Proxy open source
- Focado em segurança web
- Ideal para iniciantes

## Squid

- Proxy corporativo
- Cache e controle de acesso
- Muito usado em empresas

## Tor

- Proxy em múltiplos saltos
- Focado em anonimato
- Usa SOCKS5

---
# Uso de Proxies em Cibersegurança

## Pentest Web

- Interceptar login
- Modificar cookies
- Testar SQL Injection, XSS, CSRF

## Monitoramento e Defesa

- Analisar tráfego suspeito
- Detectar malware
- Bloquear domínios maliciosos

## Anonimização de Atacantes e Defensores

- Red Team: ocultar origem
- Blue Team: investigar tráfego

---
# Vulnerabilidades e Riscos de Proxies

- Proxy mal configurado
- Exposição de dados sensíveis
- SSL stripping
- Confiança excessiva em proxy anônimo

---
# Proxy vs VPN vs Firewall

| **Tecnologia** | **Função Principal**       |
| -------------- | -------------------------- |
| Proxy          | Intermediário de aplicação |
| VPN            | Tunelamento criptografado  |
| Firewall       | Filtragem de tráfego       |

---
# Boas práticas de segurança

- Usar autenticação no proxy
- Registrar logs
- Atualizar ferramentas
- Integrar com IDS/IPS e WAF

---
# Conclusão

Proxies são componentes essenciais em ambientes seguros, atuando tanto na **defesa** quanto no **ataque controlado**. Entender proxies é fundamental para quem trabalha com **pentest, SOC, redes e segurança web**.