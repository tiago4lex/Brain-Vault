2025-11-25 14:21

Status: #developed #SQL 

Tags:

----
# Conteúdos:

1. **Apelidos (Aliases)**    
2. **Subquery**
3. **JOIN**
4. **Transações**
5. **Procedimentos (Stored Procedures)**
6. **Funções (Stored Functions)**
7. **Controle de Acesso**
8. **Visões (Views)**

----
# APELIDOS (ALIASES)

## Definição

Apelidos permitem renomear colunas ou tabelas temporariamente durante uma consulta. Melhora a legibilidade e ajudam em consultas complexas.

## Sintaxe

```sql
SELECT coluna AS apelido
FROM tabela as t;
```

## Exemplos usando o banco

### 1. Renomeando colunas

```sql
SELECT nome AS Funcionário, nascimento AS Data_Nascimento
FROM pessoa;
```

###  2. Renomeando tabelas

```sql
SELECT p.nome, f.id
FROM pessoa AS p
JOIN funcionarios AS f ON p.cpf = f.pessoa;
```

### 3. Apelidos úteis em cálculos

```sql
SELECT nome, salario * 1.10 AS Salario_Reajustado
FROM cargo;
```

---
# SUBQUERY (Subconsultas)

## Definição

Uma **subquery** é uma consulta dentro de outra consulta. Pode retornar **um único valor, uma linha,** ou **um conjunto de registros**.

## Tipos

- **Subquery escalar** → retorna um valor
- **Subquery de linha** → retorna uma linha
- **Subquery de tabela** → retorna uma tabela inteira
- **Subquery correlacionado** → depende da query externa

## Exemplos

### 1. Subquery escalar
Encontrar o salário mais alto:

```sql
SELECT nome, salario
FROM cargo
WHERE salario = (SELECT MAX(salario) FROM cargo);
```

### 2. Subquery retornando lista (IN)
Funcionários do departamento supervisionado por "Érica":

```sql
SELECT p.nome
FROM pessoa p
WHERE p.cpf IN (
	SELECT f.pessoa
	FROM funcionario f
	JOIN departamento d ON f.departamento = d.id
	WHERE d.supervisor = (
		SELECT id FROM funcionario WHERE pessoa = "00000000007"
	)
);
```

### 3. Subquery correlacionada
Lista funcionários que ganham acima da média de seu próprio cargo:

```sql
SELECT p.nome, c.salario
FROM funcionario f
JOIN pessoa p ON f.pessoa = p.cpf
JOIN cargo ON f.cargo = c.id
WHERE c.salario > (
	SELECT AVG(salario) FROM cargo
);
```

---
# JOIN

## Definição
JOIN é usado para combinar linhas de tabelas diferentes com base em relacionamentos definidos (chaves estrangeiras).

## Tipos principais

- **INNER JOIN** - retorna registros que existem nas duas tabelas.
- **LEFT JOIN** - retorna todos da esquerda + correspondentes da direita.
- **RIHGT JOIN** - inverso do LEFT JOIN.
- **FULL JOIN** - MySQL não tem nativamente (simulado com UNION).

## Exemplos

### 1. INNER JOIN - listar funcionários com seus nomes e cargos

```sql
SELECT p.nome, c.nome AS cargo
FROM funcionario f
JOIN pessoa p on f.pessoa = p.cpf
JOIN cargo c on f.cargo = c.id;
```

### 2. LEFT JOIN - máquinas e seus responsáveis (incluindo máquinas sem responsável)

```sql
SELECT m.modelo, p.nome AS responsavel
FROM maquina m
LEFT JOIN funcionario f ON m.responsavel = f.id
LEFT JOIN pessoa p ON f.pessoa = p.cpf;
```

### 3. Join múltiplo com departamentos

```sql
SELECT p.nome AS funcionario, d.nome AS departamento, p2.nome AS supervisor
FROM funcionario f
JOIN pessoa p ON f.pessoa = p.cpf
JOIN departamento d ON f.departamento = d.id
LEFT JOIN funcionario fs ON d.supervisor = fs.id
LEFT JOIN pessoa p2 ON fs.pessoa = p2.cpf;
```

---
# TRANSAÇÕES

## Definição
Uma **transição** é um conjunto de operações que devem ser executadas como uma unidade.
Usa os princípios ACID (Atomicidade, Consistência, Isolamento e Durabilidade).

## Comandos principais

| Comando             | Função               |
| ------------------- | -------------------- |
| `START TRANSACTION` | inicia uma transação |
| `COMMIT`            | aplica as mudanças   |
| `ROLLBACK`          | desfaz as mudanças   |

## Exemplo

```sql
START TRANSACTION;

UPDATE departamento
SET supervisor = 2
WHERE id = 4;

UPDATE departamento
SET supervisor = NULL
WHERE id = 1;

COMMIT;
```

## Exemplo com erro → usando ROLLBACK

```sql
START TRANSACTION;

UPDATE funcionario SET cargo = 99 WHERE id = 1;

ROLLBACK; -- desfaz porque o cargo 99 não existe
```

---
# PROCEDIMENTOS (Stored Procedures)

## Definição
Bloco de código SQL salvo no servidor que pode ser executado quando necessário.

## Estrutura

```sql
DELIMITER $$

CREATE PROCEDURE nome_procedimento(parametros)
BEGIN
	comandos...
END $$

DELIMITER ;
```

## Exemplos

### 1. Lista funcionários por departamento

```sql
DELIMITER $$

CREATE PROCEDURE listar_funcionarios_por_departamento(IN dep_id INT)
BEGIN
	SELECT p.nome, c.nome AS cargo
	FROM funcionario f
	JOIN pessoa p ON f.pessoa = p.cpf
	JOIN cargo c on f.cargo = c.id
	WHERE f.departamento = dep_id;
END $$

DELIMITER ;
```

Chamar procedimento

```sql
CALL listar_funcionarios_por_departamento
```

---
# FUNÇÕES (Stored Functions)

## Definição
Funções retornam um **valor único** e podem ser usadas dentro de SELECTs.

## Estrutura

```sql
DELIMITER $$

CREATE FUNCTION nome_funcao(parametros)
RETURNS tipo
DETERMINISTIC
BEGIN
    DECLARE resultado tipo;
    ...
    RETURN resultado;
END $$

DELIMITER ;
```

## Exemplo: Calcular o tempo de empresa (em anos) na data de nascimento

```sql
DELIMITER $$

CREATE FUNCTION idade(data_nasc DATE)
RETURNS INT
DETERMINISTIC
BEGIN
	RETURN TIMESTAMPDIFF(YEAR, data_nasc, CURDATE());
END $$

DELIMITER ;
```

Uso:

```sql
SELECT nome, idade(nascimento) AS idade
FROM pessoa;
```

---
# ACESSO (GRANT, REVOKE)

## Definição
Controle de acesso define permissões que usuários possuem no banco.

## Criar usuário

```sql
CREATE USER 'estagioario'@'localhost' IDENTIFIED BY '1234';
```

## Permissões

#### Dar permissão de SELECT

```sql
GRANT SELECT ON industria.* TO 'estagiario'@'localhost';
```

## Dar permissão de INSERT em uma tabela

```sql
GRANT INSERT ON industria.funcionario TO 'estagioario'@'localhost';
```

## Revogar permissão

```sql
REVOKE INSERT ON industria.funcionario FROM 'estagiario'@'localhost';
```

---
# VISÕES (Views)

## Definição
Uma **view** é uma tabela virtual baseada em uma query.
Facilita consultas complexas e melhora segurança.

## Sintaxe

```sql
CREATE VIEW nome_view AS
SELECT ...
FROM ...
```

## Exemplos

### 1. View de funcionários com detalhes completos

```sql
CREATE VIEW vw_funcionarios AS
SELECT f.id, p.nome, d.nome AS departamento, c.nome AS cargo, c.salario
FROM funcionario f
JOIN pessoa p ON f.pessoa = p.cpf
JOIN departamento d ON f.departamento = d.id
JOIN cargo c ON f.cargo = c.id;
```

Consulta:

```sql
SELECT * FROM vw_funcionarios;
```

### 2. View de máquinas e responsáveis

```sql
CREATE VIEW vw_maquinas AS
SELECT m.modelo, m.fabricante, p.nome AS responsavel
FROM maquina ,
LEFT JOIN funcionario f ON m.responsavel = f.id
LEFT JOIN pessoa p ON f.pessoa = p.cpf;
```