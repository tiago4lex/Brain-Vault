#SQL

---
## 1. INTRODUÇÃO AO SQL

- [[1.1 Linguagem de Consulta Estruturada - História e Evolução do SQL]]
- [[1.2 Banco de Dados - Conceitos Fundamentais]]
	- Dados
	- Sistema de Gerenciamento de Banco de Dados (SGBD)
	- Bancos de Dados Relacional
	- Banco de Dados Estruturado e Não Estruturado

- 1.3 Diferenças entre SQL e NoSQL

## 2. CONCEITOS FUNDAMENTAIS

- 2.1 Bancos de Dados Relacionais
- 2.2 Tabelas, Linhas e Colunas
- 2.3 Chaves Primárias e Estrangeiras
- 2.4 Relacionamentos (1:1, 1:N, N:N)
- 2.5 Normalização de Dados
- 2.6 Integridade Referencial

## 3. COMANDOS SQL


- [[3.1 Data Definition Language (DDL) - Linguagem de Definição de Dados]]
	- CREATE DATABASE
	- CREATE TABLE
	- ALTER TABLE
	- DROP TABLE
	- TRUNCATE TABLE
	- Constraints (PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL, CHECK)

- [[3.2 Data Manipulation Language (DML) - Linguagem de Manipulação de Dados]]
	- SELECT (consultas básicas)
	- INSERT (inserção de dados)
	- UPDATE (atualização de dados)
	- DELETE (exclusão de dados)
	- MERGE/UPSERT

- 3.3 CONSULTAS AVANÇADAS (SELECT)
	- Cláusula WHERE (operadores de comparação)
	- Operadores Lógicos (AND, OR, NOT)
	- Cláusula ORDER BY
	- Cláusula LIMIT/TOP
	- Funções de Agregação (COUNT, SUM, AVG, MAX, MIN)
	- Cláusula GROUP BY
	- Cláusula HAVING    

## 6. JUNÇÕES (JOINS)

- [[JOIN em SQL]]
- 6.1 INNER JOIN
    
- 6.2 LEFT JOIN
    
- 6.3 RIGHT JOIN
    
- 6.4 FULL OUTER JOIN
    
- 6.5 CROSS JOIN
    
- 6.6 SELF JOIN
    
- 6.7 Junções Múltiplas
    

## 7. SUBCONSULTAS (SUBQUERIES)

- 7.1 Subconsultas na Cláusula WHERE
    
- 7.2 Subconsultas na Cláusula FROM
    
- 7.3 Subconsultas na Cláusula SELECT
    
- 7.4 Subconsultas Correlacionadas
    
- 7.5 EXISTS e NOT EXISTS
    
- 7.6 ANY, SOME, ALL
    

## 8. FUNÇÕES DO SQL

- 8.1 Funções de String
    
- 8.2 Funções Numéricas
    
- 8.3 Funções de Data e Hora
    
- 8.4 Funções de Conversão
    
- 8.5 Funções Condicionais (CASE, COALESCE, NULLIF)
    

## 9. CONTROLE DE TRANSAÇÕES (TCL - Transaction Control Language)

- [[9.1 COMMIT e ROLLBACK]]
    
- 9.2 SAVEPOINT
    
- 9.3 Propriedades ACID
    
- 9.4 Isolamento de Transações
    

## 10. CONTROLE DE ACESSO (DCL - Data Control Language)

- 10.1 GRANT
    
- 10.2 REVOKE
    
- 10.3 CREATE USER
    
- 10.4 Permissões e Privilégios
    

## 11. VISÕES (VIEWS)

- 11.1 CREATE VIEW
    
- 11.2 ALTER VIEW
    
- 11.3 DROP VIEW
    
- 11.4 Views Atualizáveis
    
- 11.5 Views Materializadas
    

## 12. ÍNDICES E PERFORMANCE

- 12.1 CREATE INDEX
    
- 12.2 Tipos de Índices (B-tree, Hash, etc.)
    
- 12.3 Índices Únicos e Compostos
    
- 12.4 EXPLAIN e Análise de Query
    
- 12.5 Otimização de Consultas
    

## 13. PROCEDURES E FUNÇÕES ARMAZENADAS

- [[13.1 CREATE PROCEDURES e DELIMITER]]
    
- 13.2 CREATE FUNCTION
    
- 13.3 Parâmetros (IN, OUT, INOUT)
    
- 13.4 Estruturas de Controle (IF, CASE, LOOP)
    
- 13.5 Cursors
    

## 14. TRIGGERS

- 14.1 CREATE TRIGGER
    
- 14.2 Triggers BEFORE e AFTER
    
- 14.3 Triggers para INSERT, UPDATE, DELETE
    
- 14.4 OLD e NEW
    

## 15. TIPOS DE DADOS AVANÇADOS

- 15.1 Tipos JSON/XML
    
- 15.2 Arrays
    
- 15.3 Tipos Espaciais (GIS)
    
- 15.4 Tipos Definidos pelo Usuário
    

## 16. CONSULTAS HIERÁRQUICAS E RECURSIVAS

- 16.1 Common Table Expressions (CTEs)
    
- 16.2 CTEs Recursivas
    
- 16.3 Consultas Hierárquicas (CONNECT BY)
    

## 17. TÓPICOS AVANÇADOS

- 17.1 Full-Text Search
    
- 17.2 Particionamento de Tabelas
    
- 17.3 Replicação e Sharding
    
- 17.4 Backup e Recovery
    
- 17.5 Data Warehousing
    
- 17.6 OLAP vs OLTP
    

## 18. SQL ESPECÍFICO POR SGBD

- 18.1 MySQL/MariaDB
    
- 18.2 PostgreSQL
    
- 18.3 SQL Server
    
- 18.4 Oracle Database
    
- 18.5 SQLite
    

## 19. BOAS PRÁTICAS E PADRÕES

- 19.1 Convenções de Nomenclatura
    
- 19.2 Design de Banco de Dados
    
- 19.3 Segurança em SQL
    
- 19.4 SQL Injection e Prevenção
    
- 19.5 Versionamento de Banco de Dados
    

## 20. FERRAMENTAS E AMBIENTES

- 20.1 IDEs para SQL
    
- 20.2 Ferramentas de Administração
    
- 20.3 Linha de Comando vs Interface Gráfica
    

## 21. PROJETOS PRÁTICOS

- 21.1 Modelagem de Casos Reais
    
- 21.2 Otimização de Bancos Existentes
    
- 21.3 Migração entre SGBDs
    
- 21.4 Documentação de Esquemas