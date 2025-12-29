2025-12-28 21:25

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[HTTPS]]

----
# Introdução

O **HTTPS *(HyperText Transfer Protocol Secure)*** é a versão segura do HTTP. Ele combina o protocolo HTTP com **TLS *(Transport Layer Security)*** para fornecer **confidencialidade, integridade e autenticação** na comunicação entre clientes e servidores web.

Atualmente, o HTTPS é o padrão da internet moderna e um **requisito básico de segurança**, especialmente para aplicações web, APIs, e-commerce e sistemas corporativos.

![[Pasted image 20251228212731.png]]

---
# Diferença entre HTTP e HTTPS


| **Características**    | **HTTP** | **HTTPS** |
| ---------------------- | -------- | --------- |
| Criptografia           | Não      | Sim (TLS) |
| Porta padrão           | 80       | 443       |
| Proteção contra MITM   | Não      | Sim       |
| Integridade dos dados  | Não      | Sim       |
| Confiança do navegador | Não      | Sim       |

O HTTPS protege os dados mesmo que o tráfego seja interceptado.

---
# Em qual camada o HTTPS atua?

- **Modelo OSI:**
    - HTTP: Camada 7 – Aplicação        
    - TLS: Entre Camada 6 (Apresentação) e 7

- **Modelo TCP/IP:**
    - Camada de Aplicação

O TLS funciona como uma camada de segurança entre o HTTP e o TCP.

---
# Para que serve o HTTPS?

o HTTPS serve para:

- proteger credenciais e dados sensíveis;
- evitar interceptação e espionagem;
- impedir alteração de dados em trânsito.
- autenticar o servidor;
- garantir confiança ao usuário.

---
# Como o HTTPS funciona?

O HTTPS utiliza **criptografia assimétrica e simétrica**.

## 1. Criptografia Assimétrica

- usa chave pública e privada;
- utilizado no início da conexão;
- permite troca segura de chaves.

## 2. Criptografia Simétrica

- usada após o handshake;
- mais rápida;
- mesma chave para cifrar e decifrar.

---
# TLS Handshake (Passo Passo)

![[Pasted image 20251228213142.png]]

1. Cliente envia `ClientHello`
2. Servidor responde com `ServerHello`
3. Servidor envia o **certificado digital**
4. Cliente valida o certificado
5. Troca segura de chaves
6. Comunicação criptografada estabelecida

---
# Certificados Digitais

## 1. O que é um Certificado Digital?

Documento eletrônico que associa um domínio a uma chave pública.

## 2. Autoridades Certificadoras (CA)

Entidades confiáveis que emitem certificados.

**Exemplos:**

- Let's Encrypt
- DigiCert
- GlobalSign

![[Pasted image 20251228213345.png]]

## 3. Tipos de Certificados

| **Tipo** | **Descrição**            |
| -------- | ------------------------ |
| DV       | Validação de domínio     |
| OV       | Validação organizacional |
| EV       | Validação estendida      |
| Wildcard | Subdomínios              |
| SAN      | Múltiplos domínios       |

---
# Versões do TLS

| **Versão**    | **Status**           |
| ------------- | -------------------- |
| SSL 2.0 / 3.0 | Inseguro (obsoleto)  |
| TLS 1.0       | Inseguro             |
| TLS 1.1       | Inseguro             |
| TLS 1.2       | Seguro               |
| TLS 1.3       | Mais seguro e rápido |

---
# Vulnerabilidades relacionadas ao HTTPS

## 1. Certificados Inválidos ou Expirados

- permitem MITM;
- quebram confiança.

## 2. Configuração TLS fraca

- cifras fracas;
- protocolos obsoletos.

## 3. SSL Stripping

Ataque que força downgrade para HTTP.

## 4. MITM com certificados falsos

Exploração de CAs comprometidas ou usuários desatentos.

## 5. Falhas em Implementações

- Heartbleed;
- BEAST;
- POODLE;
- CRIME;
- BREACH.

---
# Ferramentas para testes de segurança HTTPS

### Análise de Certificados

- SSL Labs (Qualys)
- OpenSSL

### Pentest

- Nmap (`ssl-enum-ciphers`)
- testssl.sh
- Burp Suite
- OWASP ZAP

### Monitoramento

- Wireshark
- tcpdump

---
# Mitigações e Boas Práticas HTTPS

## 1. Uso de TLS 1.2 ou 1.3

Desabilitar versões antigas.

## 2. Configuração Segura de Cifras

- AES-GCM;
- ChaCha20;
- ECDHE.

## 3. HSTS (HTTP Strict Transport Security)

Força uso de HTTPS.

## 4. Certificados Válidos e Atualizados

- renovar antes do vencimento;
- usar CAs confiáveis.

## 5. Redirecionamento HTTP → HTTPS

Evita downgrade.

## 6. Monitoramento Contínuo

- alertas de expiração;
- análise de logs.

---
# HTTPS e APIs

APIs modernas exigem HTTPS.

Boas práticas:

- autenticação via token;
- TLS mútuo (mTLS);
- rate limiting.

---
# Importância do HTTPS para Cibersegurança

Compreender HTTPS permite:

- proteger dados sensíveis;
- detectar ataques MITM;
- auditar configurações TLS;
- realizar pentests web;
- garantir conformidade (LGPD, PCI-DSS).

---
# Conclusão

O HTTPS é um pilar fundamental da segurança na web moderna. Ele transforma o HTTP inseguro em um canal confiável, protegendo usuários e aplicações.

Configurações inadequadas, no entanto, podem comprometer essa segurança. Por isso, além de usar HTTPS, é essencial **configurá-lo corretamente**, manter certificados válidos e monitorar continuamente.

Para profissionais de cibersegurança, o domínio do HTTPS e TLS é indispensável para atuar em **AppSec, Blue Team, Red Team e SOC**.