2025-12-30 08:29

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[WAF]]

----
# Introdução

O **WAF (Web Application Firewall)** é um mecanismo de segurança projetado para **proteger aplicações web** contra ataques que exploram vulnerabilidades na **camada de aplicação (Camada 7 do modelo OSI)**.

Diferente de firewalls tradicionais, que analisam principalmente IPs, portas e protocolos, o WAF **inspeciona o conteúdo das requisições HTTP/HTTPS**, entendendo parâmetros, cookies, headers e payloads.

![[Pasted image 20251230083111.png]]

---
# Para que serve um WAF?

O WAF é utilizado para:

- proteger aplicações web públicas;
- bloquear ataques conhecidos e desconhecidos;
- reduzir a superfície de ataque;
- mitigar falhas de desenvolvimento;
- proteger APIs REST e GraphQL;
- auxiliar no cumprimento de requisitos de compliance.

---
# Em qual camada o WAF atua?

- **Modelo OSI:** Camada 7 – Aplicação
- **Modelo TCP/IP:** Aplicação

Protocolos analisados:

- HTTP
- HTTPS
- WebSockets
- APIs REST

---
# Como funciona um WAF?

Fluxo básico:

1. O cliente envia uma requisição HTTP/HTTPS
2. A requisição passa pelo WAF
3. O WAF analisa headers, parâmetros, cookies e corpo
4. As regras são avaliadas
5. A requisição é permitida, bloqueada ou registrada

---
# Modos de Operação do WAF

## 1. WAF Baseado em Assinaturas

- utiliza regras conhecidas;
- rápido e eficaz;
- não detecta zero-day.

## 2. WAF Baseado em Comportamento (Anomalia)

- detecta desvios do padrão normal;
- identifica ataques desconhecidos;
- pode gerar falsos positivos.

## 3. Modelo Híbrido

- combina assinaturas e comportamento;
- mais utilizado em ambientes corporativos.

---
# Tipos de Implementações de WAF

## 1. WAF Baseado em Rede *(Appliance)*

- instalado no perímetro;
- alta performance;
- custo elevado.

## 2. WAF Baseado em Host

- integrado ao servidor web;
- maior controle;
- depende do host.    

## 3. WAF em Cloud

- proteção escalável;    
- fácil implementação;
- ideal para aplicações públicas.

---
# Exemplos de Soluções WAF

## Open Source

- ModSecurity
- NAXSI
- Coraza    

## Comerciais

- Cloudflare WAF
- AWS WAF
- Azure WAF
- Google Cloud Armor
- Imperva
- F5 Advanced WAF

---
# Principais Ataques Mitigados por WAF

- SQL Injection
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Remote Code Execution (RCE)
- File Inclusion (LFI/RFI)
- Command Injection
- Directory Traversal
- Bots e scraping

---
# WAF e OWASP Top 10

O WAF atua diretamente na mitigação de várias categorias do **OWASP Top 10**, como:

- A01 – Broken Access Control
- A03 – Injection
- A07 – Identification and Authentication Failures
- A10 – Server-Side Request Forgery (SSRF)

---
# WAF para APIs

Proteções comuns:

- validação de métodos HTTP;
- controle de rate limit;
- proteção contra abuso;
- inspeção de JSON/XML;
- autenticação e autorização.

---
# Limitações e vulnerabilidades do WAF

## 1. Bypass de WAF

- encoding;
- payload fragmentado;
- evasão por lógica de aplicação.

## 2. Falsos Positivos

- bloqueio de usuários legítimos;
- impacto na experiência.

## 3. Dependência Excessiva

- não substitui código seguro;
- deve ser camada adicional.

---
# Ferramentas para Testar e Avaliar WAF (Pentest)

- Burp Suit    
- OWASP ZAP
- Nikto
- sqlmap
- wfuzz
- nmap (`http-waf-detect`)

---
# Boas Práticas de Configuração de WAF

- usar modo de aprendizado inicial;
- ajustar regras;
- revisar logs;
- integrar com SIEM;
- manter regras atualizadas;
- proteger APIs separadamente.

---
# WAF vs Firewall Tradicional

| **Característica** | **Firewall** | **WAF** |
| ------------------ | ------------ | ------- |
| Camada             | 3-4          | 7       |
| Entende HTTP       | Não          | Sim     |
| Protege aplicações | Parcial      | Sim     |
| Mitiga OWAP Top 10 | Não          | Sim     |

---
# Importância do WAF na Cibersegurança

O WAF é essencial para proteger aplicações web modernas expostas à Internet.

Ele atua como uma **camada de defesa crítica**, especialmente quando falhas no código ainda não foram corrigidas.

---
# Conclusão

O Web Application Firewall é um componente indispensável para a segurança de aplicações web e APIs.

Quando corretamente configurado e monitorado, o WAF reduz significativamente riscos de exploração, vazamento de dados e indisponibilidade, sendo fundamental para arquiteturas modernas de segurança e DevSecOps.