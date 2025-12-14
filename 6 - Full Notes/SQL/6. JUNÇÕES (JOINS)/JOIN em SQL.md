2025-11-25 19:20

Status:

Tags:

----
# Introdução

O comando **JOIN** permite combinar linhas de duas ou mais tabelas com uma condição lógica — normalmente, uma **chave estrangeira** que relaciona tabelas.

No banco *industria*, temos vários relacionamentos:

- `funcionario.pessoa` → `pessoa.cpf`
- `funcionario.depertamento` → `departamento.id`
- `funcionario.cargo` → `cargo.id`
- `maquina.responsval` → `funcionario.id`
- `departamento.supervisor` → `funcionario.id`

Isso faz com que JOINs sejam essenciais para consultar informações completas.

---
# Tipos de JOIN

1. **INNER JOIN**
2. **LEFT JOIN**
3. **RIGHT JOIN**
4. **FULL JOIN** (MySQL não tem nativo, mas mostramos como simular)
5. **CROSS JOIN**

---
# INNER JOIN

## O que é?
Retorna apenas os registros que possuem **correspondência nas duas tabelas**.

## Exemplo: listar os funcionários e seus respectivos nomes

```sql
SELECT f.id, p.nome, f.departamento, f.cargo
FROM funcionario f
INNER JOIN pessoa p ON f.pessoa = p.cpf;
```

## Resultado

| id  | nome      | departamento | cargo |
| --- | --------- | ------------ | ----- |
| 1   | Mariana   | 1            | 2     |
| 2   | Érica     | 1            | 4     |
| 3   | Mauricio  | 4            | 1     |
| 4   | Moises    | 4            | 4     |
| 5   | Tiago     | 5            | 3     |
| 6   | Cristiano | 5            | 4     |

## Exemplo: funcionário + nome do departamento

```sql
SELECT p.nome AS funcionario, d.nome AS departamento
FROM funcionario f
INNER JOIN pessoa p ON p.cpf = f.pessoa
INNER JOIN departamento d ON d.id = f.departamento;
```

## Resultado

|funcionario|departamento|
|---|---|
|Mariana|RH|
|Érica|RH|
|Mauricio|Montagem|
|Moises|Montagem|
|Tiago|Pintura|
|Cristiano|Pintura|

---
# LEFT JOIN
## O que é?

Retorna:
- **todos os registros da tabela da esquerda**
- apenas os correspondentes da tabela da direta

Se não houve correspondência, valores da direita ficam **NULL**.

## Exemplo: listar todas as máquinas e seus responsáveis (mesmo as sem responsável)

```sql
SELECT m.modelo, p.nome AS responsavel
FROM maquina m
LEFT JOIN funcionario f ON m.responsavel = f.id
LEFT JOIN pessoa p ON f.pessoa = p.cpf;
```

## Resultado

|modelo|responsavel|
|---|---|
|Maquina de Solda X255|Mauricio|
|Pistola de tinta fixo S752|Tiago|
|Parafusadeira Y2525|NULL|

Observe que a última máquina **não tem responsável**, e por isso o resultado mostra **NULL**.

---
# RIGHT JOIN

## O que é?

Retorna:

- todos os registros da tabela da direita,
- apenas correspondentes da esquerda.

Como RIGHT JOIN é pouco usado, um exemplo claro:

## Exemplo: listar todos os departamentos e seus supervisores

```sql
SELECT d.nome AS departamento, p.nome AS supervisor
FROM funcionario f
RIGHT JOIN departamento d ON d.supervisor = f.id
LEFT JOIN pessoa p ON f.pessoa = p.cpf;
```

## Resultado

| departamento  | supervisor |
| ------------- | ---------- |
| RH            | Érica      |
| Contabilidade | NULL       |
| Logistica     | NULL       |
| Montagem      | Moises     |
| Pintura       | Cristiano  |

(repare que departamentos sem supervisor aparecem com **NULL**)

---
# FULL JOIN (SIMULADO)

MySQL não possui `FULL OUTER JOIN` nativo.
Mas é possível simular com:

```sql
SELECT ...
FROM A
LEFT JOIN B ON ...
UNION
SELECT ...
FROM A
RIGHT JOIN B ON ...
```

## Exemplo: listar funcionários e máquinas que eles operam, mesmo que uns não tenham máquinas e máquinas não tenham responsável

```sql
SELECT p.nome AS funcionario, m.modelo
FROM funcionario f
LEFT JOIN pessoa p ON f.pessoa = p.cpf
LEFT JOIN maquina m ON m.responsavel = f.id

UNION

SELECT p.nome AS funcionario, m.modelo
FROM funcionario f
RIGHT JOIN pessoa p ON f.pessoa = p.cpf
RIGHT JOIN maquina m ON m.responsavel = f.id;
```

---
# CROSS JOIN

## O que é?
Produz o **produto cartesiano** entre duas tabelas.  
Ou seja: combina **todas as linhas da primeira** com **todas as linhas da segunda**.

Exemplo:

```sql
SELECT p.nome, c.nome
FROM pessoa p
CROSS JOIN cargo c;
```

Se houver:
- 8 pessoas
- 5 cargos

Resultado → 40 linhas

---
# JOIN com múltiplas tabelas - exemplo mais completo

## Objetivo: listar funcionários, cargo, salário e departamento

```sql
SELECT
	p.nome AS funcionario,
	c.nome AS cargo,
	c.salario,
	d.nome AS departamento
FROM funcionario f
INNER JOIN pessoa p ON p.cpf = f.pessoa
INNER JOIN cargo c ON c.id = f.cargo
INNER JOIN departamento d ON d.id = f.departamento;
```

## Resultado

|funcionario|cargo|salario|departamento|
|---|---|---|---|
|Mariana|Aux. RH|2900.00|RH|
|Érica|Supervisor|5500.00|RH|
|Mauricio|Aux. Montagem|2100.00|Montagem|
|Moises|Supervisor|5500.00|Montagem|
|Tiago|Aux. Pintura|2300.00|Pintura|
|Cristiano|Supervisor|5500.00|Pintura|

---
# Resumo dos JOINs

|Tipo de JOIN|O que retorna?|
|---|---|
|**INNER JOIN**|Apenas correspondências|
|**LEFT JOIN**|Tudo da esquerda + correspondências da direita|
|**RIGHT JOIN**|Tudo da direita + correspondências da esquerda|
|**FULL JOIN**|Tudo de ambas, com NULL onde não houver correspondência|
|**CROSS JOIN**|Combinação total entre as tabelas|