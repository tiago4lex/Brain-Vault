#python

---
## 🔹 1. Fundamentos da Programação com Python (Iniciante)

### 1.1 Introdução ao Python

- O que é Python
- História e filosofia (Zen of Python)
- Onde Python é usado
- Vantagens e desvantagens
- Python 2 vs Python 3

### 1.2 Instalação e Ambiente

- Instalação do Python
- Interpretador Python
- VS Code / PyCharm
- Terminal e execução de scripts
- REPL
- Ambientes virtuais (`venv`)
- `pip` e gerenciamento de pacotes

### 1.3 Sintaxe Básica

- Estrutura de um programa Python
- Indentação
- Comentários
- Palavras reservadas
- Boas práticas de escrita

### 1.4 Variáveis e Tipos de Dados

- Variáveis
- Tipagem dinâmica
- Tipos primitivos:
    - `int`
    - `float`
    - `bool`        
    - `str`

- Conversão de tipos (`cast`)

- `type()`

### 1.5 Operadores

- Operadores aritméticos
- Operadores relacionais
- Operadores lógicos
- Operadores de atribuição
- Operadores de identidade (`is`)
- Operadores de associação (`in`)

---

## 🔹 2. Controle de Fluxo

- [[2.1 Estruturas Condicionais]]
	- `if`    
	- `elif`
	- `else`
	- Condições aninhadas
	- Operador ternário

- [[2.2 Estruturas de Repetição]]
	- `while`    
	- `for`
	- `range()`
	- `break`
	- `continue`
	- `pass`

---

## 🔹 3. Estruturas de Dados

- [[3.1 Listas (list)]]
	- Criação e acesso
	- Métodos principais
	- List comprehension
	- Listas aninhadas

- [[3.2 Tuplas (tuple)]]
	- Imutabilidade    
	- Desempacotamento
	- Casos de uso

-  [[3.3 Conjuntos (set)]]
	- Operações matemáticas
	- Diferenças entre set e list
	- Casos de uso

- [[3.4 Dicionários (dict)]]
	- Chave e valor
	- Métodos principais
	- Iteração em dicionários
	- Casos de uso práticos

---

## 🔹 4. Strings e Manipulação de Texto

- [[4.1 Indexação e Slicing]]
- [[4.2 Métodos de String]]
	- `upper()`, `lower()`, `capitalize()`, `title()`
	- `strip()`, `lstrip()`, `rstrip()`
	- `find()`, `count()`, `startswith()`, `endswith()`
	- `replace()`
	- `split()`, `join()`
	- `isdigit()`, `isalpha()`, `isalnum()` `isspace()`
	- `format()`, f-strings

- [[4.3 Expressões Regulares]]
- [[4.4 Strings Multilinha]]

---

## 🔹 5. Funções

- [[5.1 Funções Básicas]]
	- Definição de funções    
	- Parâmetros e retorno
	- Escopo de variáveis
	- Docstrings

### 5.2 Tipos de Parâmetros

- Parâmetros posicionais
- Parâmetros nomeados
- Valores padrão
- `*args`
- `**kwargs`

### 5.3 Funções Avançadas

- Funções lambda
- Funções como objetos
- Funções aninhadas
- Closures

---

## 🔹 6. Módulos e Pacotes

- Importação (`import`, `from`)
- Criando módulos próprios
- Estrutura de pacotes
- `__name__ == "__main__"`

- Bibliotecas padrão importantes:    
    - `os`
    - `sys`
    - `math`        
    - `random`
    - `datetime`

---

## 🔹 7. Manipulação de Arquivos

- Leitura e escrita de arquivos
- Modos (`r`, `w`, `a`)
- Arquivos `.txt`
- CSV (`csv`)
- JSON (`json`)
- Manipulação de diretórios

---

## 🔹 8. Tratamento de Erros

- Exceções
- `try`, `except`
- `else`
- `finally`
- Criando exceções personalizadas
- Boas práticas de tratamento de erros

---

## 🔹 9. Programação Orientada a Objetos (POO)

### 9.1 Conceitos Fundamentais

- Classes e objetos    
- Atributos
- Métodos
- `__init__`

### 9.2 Pilares da POO

- Encapsulamento
- Herança
- Polimorfismo
- Abstração

### 9.3 POO Avançada

- Métodos mágicos (`__str__`, `__repr__`)
- Classes abstratas (`abc`)
- Composição
- `@staticmethod` e `@classmethod`

---

## 🔹 10. Python Intermediário

- Compreensões:
    
    - list
    - dict
    - set

- `map()`, `filter()`, `reduce()`    
- Iteradores e geradores
- `yield`
- `enumerate()`
- `zip()`

---

## 🔹 11. Testes e Qualidade de Código

- Testes unitários (`unittest`)
- `pytest`
- Testes automatizados
- Debugging
- Logging (`logging`)
- PEP 8
- Type hints (`typing`)

---

## 🔹 12. Python Avançado

- Decorators
- Metaclasses
- Context managers (`with`)
- Programação funcional
- Imutabilidade
- `dataclasses`

---

## 🔹 13. Concorrência e Paralelismo

- Threads (`threading`)
    
- Processos (`multiprocessing`)
    
- GIL
    
- Async:
    
    - `async`
        
    - `await`
        
    - `asyncio`
        

---

## 🔹 14. Bibliotecas Importantes

### 14.1 Manipulação de Dados

- `numpy`
    
- `pandas`
    

### 14.2 Visualização

- `matplotlib`
    
- `seaborn`
    

### 14.3 Web

- `requests`
    
- `BeautifulSoup`
    
- `Flask`
    
- `Django`
    

---

## 🔹 15. Python para Segurança e Automação 🚨

_(Muito alinhado com teu foco em cibersegurança)_

- Automação de tarefas
    
- Scripts de rede
    
- Sockets
    
- Scanner de portas
    
- Manipulação de pacotes
    
- `scapy`
    
- `paramiko`
    
- `subprocess`
    
- Criação de ferramentas próprias
    

---

## 🔹 16. Python para DevOps e Sistemas

- Scripts para Linux
    
- Automação com Bash + Python
    
- Manipulação de processos
    
- Docker com Python
    
- APIs REST
    

---

## 🔹 17. Boas Práticas Profissionais

- Estrutura de projetos Python
    
- Versionamento com Git
    
- Documentação
    
- Clean Code
    
- Design Patterns em Python
    

---

## 🔹 18. Projetos Práticos (Muito Importante)

- Projetos iniciante
    
- Projetos intermediários
    
- Projetos avançados
    
- Scripts úteis
    
- Projetos voltados à cibersegurança
    

---

## 🔹 19. Preparação para Mercado de Trabalho

- Python para entrevistas
    
- Desafios técnicos
    
- Portfólio
    
- GitHub bem estruturado
    
- Integração com LinkedIn
    

---
