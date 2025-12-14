2025-06-03 06:06

Status: #developed #segurança 

Tags: [[CyberSecurity]]

----
# Introdução

Este plano é dividido em **fases**, desde iniciante até avançado, com sugestão de tempo, recursos e atividades práticas.

---

## **📌 Fase 1: Fundamentos (1-2 meses)**

**Objetivo:** Entender conceitos básicos de segurança, redes e sistemas.

### **📚 Tópicos Principais:**

1. **Introdução à Cibersegurança**
    
    - Princípios da segurança (CID: Confidencialidade, Integridade, Disponibilidade)
        
    - Tipos de ameaças (Malware, Phishing, DDoS, etc.)
        
    - Recursos:
        
        - Livro: _"Cybersecurity for Beginners"_ (Raef Meeuwisse)
            
        - Curso Gratuito:
	        - [Introduction to Cybersecurity (Cisco NetAcad)](https://www.netacad.com/courses/cybersecurity/introduction-cybersecurity)
	        - [Certificado Profissional de Analista de Cibersegurança](https://www.coursera.org/professional-certificates/ibm-cybersecurity-analyst/paidmedia?utm_medium=sem&utm_source=gg&utm_campaign=b2c_latam_ibm-cybersecurity-analyst_ibm_ftcof_professional-certificates_px_dr_bau_gg_sem_pr-bd_s1_en_m_hyb_24-10_x&campaignid=21821169584&adgroupid=169340301095&device=c&keyword=&matchtype=&network=g&devicemodel=&creativeid=717670135571&assetgroupid=&targetid=dsa-2446733152277&extensionid=&placement=&gad_source=1&gad_campaignid=21821169584&gclid=Cj0KCQjwgIXCBhDBARIsAELC9Zjd_JLfymoJ87YVerk9SyGPwCmfKi4jNK1V5qtzhcQCpF37I2JlgNQaAgnEEALw_wcB#outcomes )
            
2. **Redes de Computadores**
    
    - Modelo OSI e TCP/IP
        
    - Protocolos (HTTP, DNS, SSH, VPN)
        
    - Ferramentas: Wireshark (análise de tráfego)
        
    - Recursos:
        
        - Livro: _"Redes de Computadores"_ (Andrew Tanenbaum)
            
        - Curso: [Computer Networking (Coursera - Google)](https://www.coursera.org/learn/computer-networking)
            
3. **Sistemas Operacionais (Linux e Windows)**
    
    - Comandos básicos do Linux (`ls`, `grep`, `chmod`, etc.)
        
    - Active Directory (Windows)
        
    - Recursos:
        
        - Curso: [Linux para Iniciantes (Udemy)](https://www.udemy.com/course/linux-para-iniciantes/)
            
        - Laboratório: Instalar Kali Linux em uma VM
            

### **✅ Atividades Práticas:**

- Criar um laboratório virtual (VirtualBox + Kali Linux)
    
- Analisar tráfego com Wireshark
    
- Configurar uma rede simples e testar conectividade
    

---

## **📌 Fase 2: Segurança Básica (2-3 meses)**

**Objetivo:** Aprender defesas básicas e primeiras ferramentas de segurança.

### **📚 Tópicos Principais:**

1. **Segurança de Redes**
    
    - Firewalls, IDS/IPS (Snort, Suricata)
        
    - VPNs e proxies
        
    - Recursos:
        
        - Curso: [Network Security (Coursera)](https://www.coursera.org/learn/network-security)
            
2. **Segurança em Aplicações Web**
    
    - OWASP Top 10 (SQL Injection, XSS, CSRF)
        
    - Ferramentas: Burp Suite, OWASP ZAP
        
    - Recursos:
        
        - Livro: _"The Web Application Hacker's Handbook"_
            
        - Laboratório: [Web Security Academy (PortSwigger)](https://portswigger.net/web-security)
            
3. **Criptografia Básica**
    
    - Hash (SHA, MD5), Criptografia (AES, RSA)
        
    - Certificados SSL/TLS
        
    - Recursos:
        
        - Curso: [Criptografia Prática (Udemy)](https://www.udemy.com/course/criptografia/)
            

### **✅ Atividades Práticas:**

- Configurar um firewall (pfSense)
    
- Testar vulnerabilidades em um site fictício (DVWA - Damn Vulnerable Web App)
    
- Criar e quebrar hashes com Python
    

---

## **📌 Fase 3: Ethical Hacking e Pentest (3-4 meses)**

**Objetivo:** Aprender técnicas ofensivas e defensivas.

### **📚 Tópicos Principais:**

1. **Metodologias de Pentest**
    
    - Fases (Recon, Scanning, Exploração, Pós-Exploração)
        
    - Frameworks (MITRE ATT&CK, NIST)
        
    - Recursos:
        
        - Livro: _"Penetration Testing: A Hands-On Introduction"_ (Georgia Weidman)
            
2. **Ferramentas de Hacking Ético**
    
    - Kali Linux (Metasploit, Nmap, Hydra)
        
    - Engenharia Social (SEToolkit)
        
    - Recursos:
        
        - Curso: [Ethical Hacking (Udemy - ZSecurity)](https://www.udemy.com/course/learn-ethical-hacking-from-scratch/)
            
3. **Red Team vs. Blue Team**
    
    - Técnicas de ataque e defesa
        
    - SIEM (Splunk, ELK Stack)
        
    - Recursos:
        
        - Laboratório: [TryHackMe](https://tryhackme.com/)
            

### **✅ Atividades Práticas:**

- Realizar um pentest básico em máquina virtual (Metasploitable)
    
- Participar de CTFs (Capture The Flag) no Hack The Box
    
- Simular um ataque e defender uma rede
    

---

## **📌 Fase 4: Avançado e Certificações (4-6 meses)**

**Objetivo:** Especialização e certificações reconhecidas.

### **📚 Tópicos Principais:**

1. **Forense Digital e Resposta a Incidentes**
    
    - Análise de malware (YARA, Volatility)
        
    - Recuperação de dados (Autopsy, FTK)
        
    - Recursos:
        
        - Curso: [Digital Forensics (SANS)](https://www.sans.org/)
            
2. **Segurança em Cloud (AWS, Azure)**
    
    - AWS Security (GuardDuty, IAM, CloudTrail)
        
    - Recursos:
        
        - Curso: [AWS Certified Security - Specialty](https://aws.amazon.com/certification/)
            
3. **Certificações**
    
    - **CompTIA Security+** (Básico)
        
    - **CEH (Certified Ethical Hacker)** (Intermediário)
        
    - **OSCP (Offensive Security)** (Avançado)
        

### **✅ Atividades Práticas:**

- Investigar um caso de forense (usando FTK ou Autopsy)
    
- Configurar segurança em uma instância AWS
    
- Preparar-se para a certificação OSCP
    

---

## **📌 Fase 5: Especialização e Carreira (Contínuo)**

**Objetivo:** Escolher uma área de atuação e aprofundar.

### **🚀 Áreas de Especialização:**

- **Red Team / Pentester** (Foco em ataques simulados)
    
- **Blue Team / SOC Analyst** (Monitoramento e defesa)
    
- **Forense Digital** (Investigação de crimes cibernéticos)
    
- **Governança e Compliance (GRC)** (ISO 27001, LGPD)
    

### **🔗 Recursos Adicionais:**

- **Comunidades:** Reddit (/r/cybersecurity), Discord (Hack The Box)
    
- **Eventos:** Black Hat, DEF CON, BSides
    
- **Networking:** LinkedIn, grupos de hackers éticos
    

---

## **📅 Cronograma Sugerido (12 Meses)**

|Mês|Foco|
|---|---|
|1-2|Fundamentos (Redes, Linux, Segurança Básica)|
|3-5|Ethical Hacking e Pentest|
|6-8|Forense, Cloud e SIEM|
|9-12|Certificações (Security+, CEH, OSCP)|

---

### **🎯 Dicas Finais:**

✅ **Pratique diariamente** (Use Hack The Box, TryHackMe)  
✅ **Documente seu aprendizado** (Crie um blog ou GitHub)  
✅ **Networking** (Participe de eventos e comunidades)