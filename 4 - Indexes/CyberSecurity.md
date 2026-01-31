#segurança 

## **0. Projetos Práticos**

### 0.1 Simulador de Ataques e Defesas (Mini-lab)

- [[1. Simulador de Ataques e Defesas (Mini-LAB)]]
- [[2. Montando o ambiente do zero]]
- [[3. Instalando Aplicações Vulneráveis]]
- [[4. Ataque de Força Bruta - Hydra]]

### 0.3 Cross-Site Scripting (XSS) - Teoria, Prática e Prevenção
- [[Cross-Site Scripting (XSS) - Teoria, Prática e Prevenção]]


---
## **1. Fundamentos de Cibersegurança**

### **1.1 Fundamentos da Cibersegurança**

#### 1.1.1 Conceitos Básicos

- [[O que é Cibersegurança]]?      
- [[Tríade CIA - Confidencialidade, Integridade e Disponibilidade]]
- [[Principais Elementos da Cibersegurança]]
- [[Gerenciamento de Riscos]]
- [[Conceitos Errôneos Comuns Sobre Cibersegurança]]
- [[Leis e Ética]]
- [[Pontos importantes a serem lembrados - Conceitos Básicos]]
- [[Testes de Penetração (Pentest)]]

#### 1.1.2 Cibersegurança: Na ofensiva

- [[Grupos de Atores de Ameaças]]    
- [[Tipos de ataques cibernéticos]]

	##### 1.1.2.1 Detalhando os tipos de ataque
	- [[Injeção de linguagem de consulta estruturada (SQL Injection)]]
	- [[Cross-Site Scripting (XSS)]]
	- [[Ataques DDoS]]
	- [[Ataques VLAN Hopping]]

- [[IA em Ataques Cibernéticos]]
- [[A estrutura de um ataque cibernético]]
- [[Ecossistema de crime cibernético]]
- [[Engenharia Social]]
- [[Informações de fontes abertas]]
- [[Varredura técnica]]
- [[Estudos de Caso]]
- [[Pontos importantes a serem lembrados - Cibersegurança Na Ofensiva]]

#### 1.1.3 Cibersegurança: Na defesa

- [[Impactos Financeiros]]
- [[Estratégia de Segurança]]
- [[Impedir Ataques]]
- [[Detecção de ataques]]
- [[Resposta a Ataques]]
- [[Introdução à Criptografia]]
- [[Introdução à Inteligência Contra Ameaças]]
- [[Pontos Importantes a serem lembrados - Cibersegurança Na Defesa]]

#### 1.1.4 Panorama do Mercado de Trabalho

- [[O Mercado de Trabalho de Segurança Cibernética]]
- [[Trabalho em Segurança Cibernética]]
- [[O que as empresas estão procurando]]?
- [[Recursos Úteis e Introdução]]
- [[Pontos importantes a serem lembrados - Panorama do Mercado de Trabalho]]

### **1.2 Fundamentos de [[Redes de Computadores]]**

### **1.3 Sistemas Operacionais**

- [[Linux]] (Comandos básicos e avançados, administração)
- [[Windows]] (Active Directory, PowerShell, GPOs)
- Virtualização (VMware, VirtualBox, Docker)

### **1.4 Governança e Segurança da Informação**
- [[Governança & Regulamentação]]

---

## **2. Segurança de Redes**

### **2.1 Fundamentos de Redes em Cibersegurança**

- 2.1.1 Camada de Rede
	- [[Cabeçalhos de Pacotes]]
	- [[Modelo OSI Aplicado à Cibersegurança]]
	- [[Modelo TCP.IP Aplicado à Cibersegurança]]
	- [[Protocolo NAT]]
	- [[Protocolo ARP (Address Resolution Protocol)]]

- 2.1.2 Camada de Transporte
	- [[TCP Flags - Conceitos, Funcionamento e Importância em Cibersegurança]]
	- [[Three-Way Handshake]]
	- [[Protocolo UDP (Used Datagram Protocol)]]

- 2.1.3 Camada de Aplicação
	- [[Protocolo DNS - Domain Name System]]
	- [[Protocolo HTTP - HyperText Transfer Protocol]]
	- [[Protocolo HTTPS - HyperText Transfer Protocol Secure]]
	- [[Protocolo SSH - Secure Shell]]
	- [[Protocolo FTP - File Transfer Protocol]]
	- [[Protocolo SMB - Server Message Block]]

### **2.2 Proteção de Infraestrutura**

- [[Telnet - Telecommunication Network]]
- [[FTP, SFTP e seu Uso em Cibersegurança]]
- [[SMB - Server Message Block]]
- [[Firewall - Fundamentos, Funcionamento e Aplicações]]
- [[IDS e IPS - Sistemas de Detecção e Prevenção de Intrusões]]
- [[WAF - Web Application Firewall]]
- [[ACL - Access Control List]]
- [[Proxies]]
- [[VPN - Virtual Private Network]]
- SIEM (Splunk, ELK Stack, IBM QRadar)
- Honeypots e Honeynets
- [[Segmentação de Redes]]
	- [[5.1 Redes Locais Virtuais (VLAN)]]
	- Microsegmentação

### **2.3 Análise de Tráfego e Packet Sniffing**

- [[Análise de Tráfego de Rede]]
- [[Wireshark]]
- [[Análise de Pacotes com Wireshark]]
- Tcpdump
- [[Análise de Logs de Rede]]
- [[Detecção de Anomalias e Tráfego Suspeito em Redes]]
- [[Sniffing de Tráfego de Rede]]
- [[Mapeamento de Redes WiFi sem Autenticação]]
  
### **2.4 Redes Sem Fio e Segurança**

- 2.4.1 Wi-Fi (WEP, WPA, WPA2, WPA3)
	- [[Segurança em Redes Wi-Fi - Fundamentos, Ataques e Defesas]]
	- [[Testes de Penetração em Redes Wi-Fi]]
	- [[Reconhecimento e Enumeração em Redes Wi-Fi]]

- 2.4.2 Ataques a redes Wi-Fi (Evil Twin, KRACK, Deauthentication)
	- [[Quebra de Autenticação em Redes Wi-Fi]]
	- [[Ataques de Ponto de Acesso Falso (Evil Twin)]]

- 2.4.3 Ferramentas (Aircrack-ng, Kismet)
	- [[AIRCRACK-NG - Suite Completa de Auditoria Wireless]]
	- [[AIRCRACK-NG - Necessidade de Dispositivos Conectados para Ataques Wireless]]
	- [[WIFIPHISHER - Framework de Ataque de Falsa Autenticação Wi-Fi]]

---

## **3. Segurança de Sistemas e Aplicações**

### **3.1 Hardening de Sistemas**

- [[Medidas de Segurança e Limpeza Automática no Linux]]
    
- Gerenciamento de patches e atualizações
    
- Controle de acesso (RBAC, Least Privilege)
    

### **3.2 Segurança em Aplicações Web**

- OWASP Top 10 (SQL Injection, XSS, CSRF, etc.)
    
- Ferramentas de teste (Burp Suite, OWASP ZAP, Nikto)
    
- Secure Coding (Práticas de desenvolvimento seguro)
- [[Vazamento de DNS]]
- [[AnonSurf - Ferramenta de Redirecionamento de Tráfego]]

### **3.3 Segurança em Cloud Computing**

- Modelos de serviço (IaaS, PaaS, SaaS)
    
- AWS, Azure e Google Cloud Security
    
- Ferramentas (CloudTrail, AWS GuardDuty, Azure Security Center)

---

## **4. Ethical Hacking e Pentest**

### **4.1 Metodologias de Teste de Invasão**

- 4.1.1 Fases do Pentest (Reconhecimento, Scanning, Exploração, Pós-Exploração, Relatório)
	- [[Google Dorks - Técnicas de Busca Avançada]]
	- [[Web Crawler - Web Spider Bot]]
	- [[Cross-Site Scripting (XSS) - Cheat Sheet]]

- 4.1.2 Frameworks (PTES, MITRE ATT&CK, NIST)
	- [[PTES (Penetration Testing Execution Standard)]]

### **4.2 Ferramentas de Pentest**

- Kali Linux (Metasploit, Nmap, John the Ripper, Hydra)
- Engenharia reversa (Ghidra, IDA Pro)

- 4.2.1 Exploração de vulnerabilidades
	- [[Cross-Site Request Forgery (CSRF)]]
	- [[Server-Side Request Forgery (SSRF)]]
	- [[Local File Inclusion (LFI)]]
	- [[Remote File Inclusion (RFI)]]
	- [[Redeemer Write-up - Redis]]
	- [[Unified Write-Up - Nagios]]
	- [[Appointment Write-up]]
	- [[CORS - Cross-Origin Resource Sharing]]

- 4.2.2 Ferramentas de Exploração e Pós-Exploração
	- [[Metasploit Framework]]
	
		- 4.2.2.1 Ferramentas Web
		- [[Gobuster - Ferramenta para Pentest Web]]
		- [[Wapiti - Ferramenta de testes de invasão]]
		- [[Comando cURL]]
		- [[Hydra Login Cracker]]
		
		- 4.2.2.2 SQL Injection
			- [[SQL Injection - Usando na prática]]
			- [[SQLmap - Ferramenta automática de injeção de SQL]]
			- [[Tipos de SQL Injection e Uso no SQLmap]]
		
		- 4.2.2.3 Burp Suite
			- [[Burp Suite - Guia Completo de Funcionalidades]]
			- [[Burp Suite - Interceptação de Requisições]]
			- [[Força Bruta com CSRF Token usando Burp Suite]]
		
		- 4.2.2.4 Nuclei
			- [[Nuclei - Vulnerability Scanner]]
			- [[Templates do Nuclei - Como escolher e Usar]]
		
		- 4.2.2.5 Metasploit
			- [[Metasploit Framework]]

- 4.2.3 Ferramentas para DDoS
	- [[Hping3 em Linux]]
	- [[Slowloris]]

- 4.2.4 Ferramentas de Rede
	- [[Nmap (Network Mapper)]]
	- [[Pixie-Dust - Ataque de WPS]]
	- [[BetterCap - O Swiss Army Knife de Segurança de Redes]]
	- [[Ataque ARP Spoofing + MITM com BetterCap]]

- 4.2.5 Ferramentas de Comunicação
	- [[BitchX e IRC (Internet Relay Chat)]]
	- [[WeeChat - Cliente IRC em Terminal]]

- 4.2.6 Ferramentas de Engenharia Social
	- [[Social-Engineer Toolkit (SET)]]
	- [[Phishing por SMS com SET e Gerenciadores de SMS]]
	- [[Evilginx - Ferramenta de Phishing]]

- 4.2.7 TOR - *The Onion Router*
	- [[Rede TOR (The Onion Router)]]
	- [[Abrindo um Navegador TOR pelo terminal]]
	- [[Usando o TOR como Proxy em Ferramentas de Pentest (SQLmap, Hydra, Gobuster, etc.)]]

- 4.2.8 Outras Ferramentas
	- [[CanSniffer - CAN (Controller Area Network)]]
	- [[John The Ripper]]

### **4.3 Red Team vs. Blue Team**

- 4.3.1 Técnicas de Red Team (Ataques avançados, Persistência)
	- [[Red Team]]
	- [[Escalamento de Privilégios em Sistemas Linux]]
	- [[Python para Pentesters]]

- 4.3.2 Técnicas de Blue Team (Detecção, Resposta a Incidentes)
	- [[Segurança Defensiva, SOC e Blue Team]]

---

## **5. Forense Digital e Resposta a Incidentes**

### **5.1 Fundamentos de Forense**

- Coleta e preservação de evidências
    
- Análise de discos (Autopsy, FTK, EnCase)
    
- Análise de memória RAM (Volatility)
    

### **5.2 Resposta a Incidentes (IR)**

- Ciclo de vida de um incidente (NIST SP 800-61)
    
- Ferramentas (Splunk, LogRhythm, TheHive)
    
- Análise de malware (Sandboxing, YARA Rules)
    

---

## **6. Criptografia e Segurança de Dados**

### **6.1 Fundamentos de Criptografia**

- [[Noções Básicas de Criptografia]]
- Criptografia simétrica e assimétrica (AES, RSA)
    
- Hashing (SHA, MD5)
    
- Certificados digitais e PKI
    

### **6.2 Proteção de Dados**

- GDPR, LGPD e outras regulamentações
	- [[Computação em Nuvem e LGPD - Análise de Risos e Conformidade]]
    
- DLP (Data Loss Prevention)
    
- Backup e recuperação de desastres
    

---

## **7. Certificações em Cibersegurança**

### **7.1 Certificações Iniciantes**

- #### **🔐 CompTIA Security+**
	- **Nível:** Iniciante a intermediário  
	- **Indicado para:** Quem está começando na área de segurança da informação.

	-  📚 Conteúdo principal:
		- Fundamentos de segurança da informação
		- Gestão de riscos
		- Arquitetura de segurança (rede, dispositivos e aplicativos)
		- Criptografia e PKI
		- Resposta a incidentes
		- Controle de acesso, autenticação e identidade
		- Governança, políticas e conformidades

	- 💰 Custo:
		- **Exame:** US$ 392 (~R$ 2.100,00)
		- **Cursos preparatórios (opcional):** Gratuitos até mais de R$ 1.000, dependendo da plataforma (Udemy, CompTIA, Coursera, etc.)

	- ⏱️ Duração do exame:
		- 90 questões (escolha múltipla e questões práticas)
		- 90 minutos

	- 📝 Pré-requisitos:
		- Nenhum obrigatório, mas é recomendado ter:
		    - Certificação **CompTIA Network+**
		    - 1 a 2 anos de experiência em segurança de redes

- #### **🧑‍💻 CEH (Certified Ethical Hacker)**
	- **Nível:** Intermediário a avançado  
	- **Indicado para:** Quem quer se tornar **penetration tester** ou trabalhar com **red teaming**.

	- 📚 Conteúdo principal:
		- Reconhecimento e footprinting
		- Scanning de redes e enumeração
		- Gaining Access (ataques em sistemas, redes e aplicações)
		- Sniffing, phishing e engenharia social
		- Ataques web (XSS, SQLi, etc.)
		- Criptografia e segurança de nuvem
		- Malware, DoS e ataques em IoT

	- 💰 Custo:
		- **Exame oficial:** US$ 1.199 (~R$ 6.500)
		- **Curso oficial (opcional):** US$ 850 a US$ 2.000
		- **Re-teste (se necessário):** ~US$ 100

	 - ⏱️ Duração do exame:
		- 125 questões
		- 4 horas

	- 📝 Pré-requisitos:
		- 2 anos de experiência em segurança da informação **OU**
		- Curso oficial de treinamento (EC-Council)

- #### **🧠 CISSP Associate**
	- **Nível:** Avançado  
	- **Indicado para:** Profissionais que visam cargos de **analista sênior, gerente de segurança, CISO**.

	- 📚 Conteúdo (8 domínios CBK):
		1. Segurança e gestão de riscos
		2. Segurança de ativos
		3. Segurança em engenharia
		4. Comunicação e redes
		5. Gestão de identidade e controle de acesso
		6. Avaliação e teste de segurança
		7. Operações de segurança
		8. Segurança no desenvolvimento de software

	- 💰 Custo:
		- **Exame:** US$ 749 (~R$ 4.000)
		- **Curso preparatório:** Pode variar de US$ 500 a US$ 3.000 (Coursera, bootcamps, etc.)

	- ⏱️ Duração do exame:
		- 100 a 150 questões (formato adaptativo)
		- 3 horas

	- 📝 Pré-requisitos:
		- Para ser **CISSP completo**: 5 anos de experiência em 2 ou mais dos domínios.
		- Para ser **CISSP Associate**: **Sem experiência exigida**, mas você terá 6 anos para adquirir a experiência e validar a certificação completa.

### **7.2 Certificações Intermediárias/Avançadas**

- **OSCP (Offensive Security Certified Professional)**
    
- **CISSP (Certified Information Systems Security Professional)**
    
- **CISM (Certified Information Security Manager)**
    
- **CCSP (Certified Cloud Security Professional)**
    

### **7.3 Certificações Específicas**

- **SANS GIAC (GCIH, GPEN, GCFA)**
    
- **AWS Certified Security – Specialty**
    
- **Azure Security Engineer**
    

---

## **8. Habilidades Complementares**

- Programação (Python, Bash, PowerShell)
    
- Automação em segurança (Ansible, Terraform)
    
- Gestão de projetos (ITIL, Scrum)
    
- Inglês técnico (Leitura de documentações)
    

---

## **9. Áreas de Especialização**

- **Segurança Ofensiva (Pentester, Red Team)**
    
- [[Segurança Defensiva, SOC e Blue Team]]
    
- **Forense Digital e Resposta a Incidentes**
    
- **Governança, Risco e Compliance (GRC)**
    
- **Segurança em Cloud e DevOps (DevSecOps)**
    

---

## **10. Prática e Networking**

- Laboratórios práticos (Hack The Box, TryHackMe, VulnHub)
    
- Participação em CTFs (Capture The Flag)
    
- Comunidades (Reddit, Discord, grupos de hackers éticos)
    
- Eventos e conferências (Black Hat, DEF CON, BSides)