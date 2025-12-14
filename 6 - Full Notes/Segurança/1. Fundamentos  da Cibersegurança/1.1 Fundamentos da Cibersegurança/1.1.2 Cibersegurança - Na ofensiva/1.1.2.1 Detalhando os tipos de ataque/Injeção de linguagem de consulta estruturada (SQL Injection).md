2025-05-23 06:25

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[3 - Tags/Segurança/SQL]] | [[SQL Injection]] 

----
# 1. Oque é SQL Injection?

- **SQL Injection** é um vulnerabilidade de segurança que permite a um atacante interferir nas consultas feitas a um banco de dados por uma aplicação. Em termos simples, é quando dados inseridos por um usuário malicioso são interpretados como comandos SQL pelo servidor, permitindo acesso não autorizado a informações ou até mesmo controle total sobre o banco de dados.
- Essa falha ocorre principalmente quando a aplicação não valida ou sanitiza corretamente os dados de entrada antes de incluí-los em comandos SQL.

# 2. Como funciona o SQL Injection?

- O ataque acontece quando comandos SQL maliciosos são inseridos em campos de entrada, como formulários de login, campos de busca ou parâmetros de URL. O bando de dados interpreta esses dados como parte da consulta, comprometendo a integridade, confidencialidade e disponibilidade das informações.

**Exemplo de consulta vulnerável:**

```sql
SELECT * FROM users WHERE name = 'admin' AND password = '1234';
```

Se o sistema não tratar corretamente os dados inseridos, um atacante pode inserir:
- **Nome:** `admin' --`
- **Senha:** (deixando em branco)

A consulta resultante será:

```sql
SELECT * FROM users WHERE name = 'admin' --' AND password = '';
```

O `--` comenta o restante da linha, ignorando a verificação da senha. Resultado: login sem autenticação adequada.

# 3. Tipos de SQL Injection

## a. Injeção Clássica (ou *In-band*)

- O atacante manipula diretamente os dados de entrada e visualiza os resultados no próprio site.

## b. *Blind* SQL Injection

- Quando a aplicação não retorna diretamente os erros, mas o atacante consegue inferir o comportamento do banco por meio de respostas verdadeiras ou falsas: (ex: tempo de resposta, mensagens genéricas).

## *Out-of-Band* SQL Injection

- Ocorre quando o atacante não consegue ver a resposta diretamente, mas usa canais externos (como DNS ou HTTP) para coletar dados.

# 4. Exemplos práticos

## **Exemplo 1: Login Bypass**

**Consulta original:**

```sql
SELECT * FROM users WHERE user = '$user' AND password = '$password';
```

Entrada maliciosa:

- Usuário: `' OR '1'='1`
- Senha: `' OR '1'='1`

Resultado:

```sql
SELECT * FROM users WHERE user = '' OR '1'='1' AND password = '' or '1'='1';
```

Isso sempre retorna verdadeiro, permitindo o login sem autenticação.

## **Exemplo 2: Exfiltração de dados**

**Entrada em campo de busca:**

```sql
' UNION SELECT name, password FROM users --
```

Consulta final:

```sql
SELECT * FROM products WHERE name = '' UNION SELECT name, password FROM users --';
```

Essa instrução retorna a lista de usuários e senhas do banco.

# 5. Como prevenir SQL Injection

- **Prepared Statements** (Consultas parametrizadas): Exemplo em PHP (PDO):
```php
$stmt = $pdo->prepare('SELECT * FROM usuarios WHERE nome = ? AND senha = ?');
$stmt->execute([$usuario, $senha]); 
```

- **ORMs** *(Object-Relational Mappers)* que abstraem consultas SQL.
- Validação e sanitização de entradas.
- **Princípio do menor privilégio:** o usuário da aplicação no banco de dados deve ter acesso apenas ao necessário.
- **Firewall de aplicação web (WAF)* e escaneamentos periódicos.

# 6. Conclusão

-  SQL Injection é uma das vulnerabilidades mais conhecidas e perigosas da web, frequentemente explorada por cibercriminosos devido à simplicidade de execução e impacto potencial. Desenvolvedores devem estar atentos às boas práticas de codificação e segurança para proteger suas aplicações e os dados dos usuários.

----

# Referências
