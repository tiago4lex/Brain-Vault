2025-12-29 13:12

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Redes de Computadores]] | [[Redes]] | [[FTP]]

----
# Introdução

O **FTP *(File Transfer Protocol)*** é um protocolo clássico utilizado para **transferência de arquivos** entre um cliente e um servidor em redes TCP/IP. Criado antes da popularização da segurança na internet, o FTP **não possui criptografia nativa**, o que o torna um protocolo de alto risco quando exposto.

Em cibersegurança, o FTP é relevante por dois motivos principais:

- ainda é encontrado em ambientes legados e dispositivos;
- é frequentemente explorado por atacantes quando mal configurado.

![[Pasted image 20251229131717.png]]

---
# Em qual camada o FTP atua?

- **Modelo OSI:** Camada 7 - Aplicação
- **Modelo TCP/IP:** Camada de Aplicação

Portas padrão:

- **21/TCP** - canal de controle
- **20/TCP** - canal de dados (modo ativo)

---
# Para que serve o FTP?

O FTP é usado para:

- upload e download de arquivos;
- publicação de sites antigos;
- backup e sincronização de dadoos;
- administração de sistemas legados.

>[!warning] Atenção:
>Hoje, seu uso é **desencorajado em ambientes expostos**, sendo substituído por protocolos seguros.

---
# Como o FTP funciona?

O FTP utiliza **dois canais separados:**

- **Canal de Controle:** autenticação e comandos
- **Canal de Dados:** transferência de arquivos

![[Pasted image 20251229131823.png]]

Fluxo básico:

1. Cliente conecta ao servidor (porta 21)
2. Usuário se autentica
3. Um canal de dados é criado
4. Arquivos são transferidos

---
# Modos de operação do FTP

## 1. Modo Ativo

- cliente abre porta aleatória;
- servidor conecta ao cliente (porta 20);
- problemas com firewall/NAT.

## 2. Modo Passivo (PASV)

- servidor abre porta aleatória;
- cliente inicia a conexão;
- mais compatível com firewalls.

---
# Autenticação no FTP

## 1. Autenticação por Usuário e Senha

- transmitida em texto puro;
- facilmente interceptável.

## 2. FTP Anônimo

- acesso sem credenciais;
- alto risco de exposição de dados.

---
# Comandos FTP mais comuns

| **Comando** | **Função**      |
| ----------- | --------------- |
| USER        | Usuário         |
| PASS        | Senha           |
| LIST        | Listar arquivos |
| RETR        | Download        |
| STOR        | Upload          |
| DELE        | Excluir         |
| QUIT        | Encerrar sessão |

---
# Principais vulnerabilidades do FTP

## 1. Transmissão em Texto Claro

- captura de credenciais via sniffing;
- exposição de dados sensíveis.

## 2. Brute Force e Credential Stuffing

- serviços FTP são alvos comuns;
- falta de rate limiting.

## 3. FTP Bounce Attack

Explora o modo ativo para realizar conexões não autorizadas.

## 4. Anonymous FTP mal configurado

- upload/download irrestrito;
- distribuição de malware;
- vazamento de dados.

## 5. Directory Traversal

- acesso a arquivos fora do diretório permitido.

## 6. Exploração de Software FTP vulneráveis

- versões antigas (vsftpd, ProFTPD);
- backdoors e CVEs conhecidos.

---
# Ataques reais envolvendo FTP

- vazamento de backups corporativos;
- hospedagem de malware;
- pivoting em redes internas;
- comprometimento de servidores.

---
# Ferramentas pra testes de segurança FTP

## Enumeração e Pentest

- Nmap (`ftp-anon`, `ftp-brute`, `ftp-bounce`)    
- Hydra
- Medusa
- Metasploit

## Análise de Tráfego

- Wireshark    
- tcpdump

## Clientes FTP

- ftp (CLI)    
- FileZilla
- lftp

---
# Mitigações e Boas Práticas de segurança FTP

## 1. Evitar uso de FTP em produção

Preferir protocolos seguros.

## 2. Uso de FTPS

- FTP sobre TLS;
- criptografia do canal de controle de dados.

## 3. Substituir por SFTP

- baseado em SSH;
- canal único e criptografado.

## 4. Hardening do Servidor FTP

- desativar FTP anônimo;
- limitar usuários;
- definir chroot;
- usar portas não padrão.

## 5. Firewall e IDS/IPS

- restringir IPs;
- monitorar tentativas suspeitas.

## 6. Monitoramento e Logs

- auditoria de acessos;
- alertas de brute force.

---
# FTP vs FTPS vs SFTP

| **Protocolo** | **Segurança** | Porta | **Observação**        |
| ------------- | ------------- | ----- | --------------------- |
| FTP           | Nenhuma       | 21    | Inseguro              |
| FTPS          | TLS           | 21    | Configuração complexa |
| SFTP          | SSH           | 22    | Recomendado           |

---
# FTP em Ambientes Corporativos

Ainda encontrado em:

- sistemas legados;
- equipamentos industriais;
- dispositivos embarcados.

Boas práticas:

- isolar em VLAN;
- restringir acesso;
- planejar migração.

---
# Importância do FTP para Cibersegurança

Estudar FTP permite:

- identificar riscos legados;
- realizar pentests realistas;
- detectar vazamentos de dados;
- fortalecer políticas de segurança.

---
# Conclusão

O protocolo FTP foi essencial no início da internet, mas hoje representa um **alto risco de segurança** quando utilizado sem proteção.

Em ambientes modernos, seu uso deve ser **evitado ou rigidamente controlado**, com preferência por **SFTP ou FTPS**.

Para profissionais de cibersegurança, compreender o FTP é fundamental para identificar falhas legadas, conduzir testes de intrusão e planejar migrações seguras.