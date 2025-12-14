2025-08-28 10:13

Status: #developed #segurança 

Tags: [[CyberSecurity]] | [[Web Scraper]]

----
## 📋 Índice

1. [Visão Geral](#-visão-geral)
2. [Funcionalidades](#-funcionalidades)
3. [Tecnologias Utilizadas](#-tecnologias-utilizadas)
4. [Estrutura do Projeto](#-estrutura-do-projeto)
5. [Configuração do Ambiente](#-configuração-do-ambiente)
6. [Explicação Detalhada do Código](#-explicação-detalhada-do-código)
7. [Estrutura do Banco de Dados](#-estrutura-do-banco-de-dados)
8. [Como Executar](#-como-executar)
9. [Exemplos de Uso](#-exemplos-de-uso)
10. [Boas Práticas](#-boas-práticas)

---
## 🌟 Visão Geral

Este é um programa completo de web scraping desenvolvido em Python para extrair dados do site [Books to Scrape](https://books.toscrape.com/) e armazená-los em um banco de dados MySQL. O sistema coleta informações detalhadas de todos os livros disponíveis no site e as armazena de forma estruturada para análise e consulta.

---
## 🚀 Funcionalidades

- **✅ Scraping Completo**: Coleta dados de todas as páginas do catálogo
- **✅ Armazenamento MySQL**: Armazena dados em banco relacional com relacionamentos
- **✅ Dados Detalhados**: Extrai mais de 15 campos de informação por livro
- **✅ Paginação Automática**: Navega automaticamente por todas as páginas
- **✅ Inserção em Lote**: Inserção eficiente de múltiplos registros
- **✅ Tratamento de Erros**: Robustez contra falhas de conexão
- **✅ Análise de Dados**: Gera estatísticas e insights dos dados coletados
- **✅ Respeito ao Servidor**: Implementa delays e headers apropriados

---
## 🛠 Tecnologias Utilizadas

| Biblioteca               | Versão | Propósito                              |
| ------------------------ | ------ | -------------------------------------- |
| `requests`               | 2.31.0 | Requisições HTTP para acessar páginas  |
| `beautifulsoup4`         | 4.12.2 | Parseamento e extração de dados HTML   |
| `mysql-connector-python` | 8.1.0  | Conexão e operações com MySQL          |
| `python-dotenv`          | 1.0.0  | Gerenciamento de variáveis de ambiente |
| `pandas`                 | 2.0.3  | Manipulação de dados e backup CSV      |
| `urllib`                 | 3.11.0 | Manipulação de URLs                    |

---
## 📁 Estrutura do Projeto

```txt
books_scraper_mysql.py
├── DatabaseManager Class          # Gerenciador do banco de dados
│   ├── create_connection_pool()   # Cria pool de conexões
│   ├── initialize_database()      # Cria tabelas no MySQL
│   ├── insert_or_update_books()   # Insere dados em lote
│   └── get_book_stats()           # Obtém estatísticas
├── scrape_books_toscrape()        # Função principal de scraping
├── extract_book_data()            # Extrai dados básicos do livro
├── scrape_book_details()          # Raspa página individual
├── save_to_csv()                  # Backup em CSV
├── analyze_data()                 # Análise básica
└── main()                         # Função principal
```

---
## ⚙️ Configuração do Ambiente

### Instalação de Dependências

```bash
pip install requests beautifulsoup4 mysql-connector-python python-dotenv pandas
```

---
## 📊 Configuração do MySQL

### 1. Instalação do MySQL

```bash
# Ubuntu/Debian
sudo apt-get install mysql-server

# Windows
# Download do MySQL Installer: https://dev.mysql.com/downloads/installer/

# macOS
brew install mysql
```

### 2. Configuração do Banco de Dados

```sql
-- Conectar ao MySQL
mysql -u root -p

-- Criar banco de dados
CREATE DATABASE books_scraper CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Criar usuário dedicado
CREATE USER 'scraper_user'@'localhost' IDENTIFIED BY 'sua_senha_segura';
GRANT ALL PRIVILEGES ON books_scraper.* TO 'scraper_user'@'localhost';
FLUSH PRIVILEGES;
```

### 3. Arquivo de Configuração (.env)

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=books_scraper
DB_USER=scraper_user
DB_PASSWORD=sua_senha_segura
DB_CHARSET=utf8mb4
```

---
## 🔍 Explicação Detalhada do Código

### 1. Classe `DatabaseManager`

```python
class DatabaseManager:
    """Gerencia todas as operações com o banco de dados MySQL"""
    
    def __init__(self):
        self.connection_pool = self.create_connection_pool()
```

**Propósito**: Centraliza todas as operações de banco de dados usando pool de conexões para melhor performance.

### 2. Pool de Conexões

```python
def create_connection_pool(self) -> pooling.MySQLConnectionPool:
    """Cria um pool de conexões com configurações do .env"""
    return pooling.MySQLConnectionPool(
        pool_name="scraper_pool",
        pool_size=5,  # 5 conexões simultâneas
        host=os.getenv('DB_HOST', 'localhost'),
        database=os.getenv('DB_NAME', 'books_scraper'),
        user=os.getenv('DB_USER', 'root'),
        password=os.getenv('DB_PASSWORD', ''),
        charset=os.getenv('DB_CHARSET', 'utf8mb4')
    )
```

**Vantagens**: Reutiliza conexões, melhorando performance e reduzindo overhead.

### 3. Inicialização do Banco

```python
def initialize_database(self):
    """Cria as tabelas se não existirem"""
    create_tables_sql = [
        """
        CREATE TABLE IF NOT EXISTS categories (
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100) NOT NULL UNIQUE,
            created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        )
        """,
        # ... outras tabelas
    ]
```

**Funcionamento:** Executa DDL statements para criar a estrutura do banco de dados.

### 4. Inserção em Lote

```python
def insert_or_update_books(self, books_data: List[Dict]):
    """Insere múltiplos livros de uma vez usando executemany"""
    books_to_insert = []
    for book in books_data:
        # Preprocessa dados
        price = self._convert_price(book.get('Preço', ''))
        # ... outros campos
        
        books_to_insert.append((
            book.get('UPC'), book.get('Título'), price, # ... 
        ))
    
    cursor.executemany(insert_sql, books_to_insert)
```

**Performance**: Inserção em lote é muito mais rápida que inserções individuais.

### 5. Função Principal: `scrap_books_toscrap()`

```python
def scrape_books_toscrape():
    """Coordena o scraping de todas as páginas"""
    base_url = "https://books.toscrape.com/"
    all_books = []
    page = 1
    
    while True:  # Loop até não encontrar mais páginas
        url = f"{base_url}catalogue/page-{page}.html" if page > 1 else base_url
        response = requests.get(url, headers=headers)
        soup = BeautifulSoup(response.content, 'html.parser')
        
        # Encontrar livros na página
        books = soup.find_all('article', class_='product_pod')
```

**Como funciona a paginação:**

- O site usa URLs sequenciais: `/catalogue/page-2.html`, `/catalogue/page-3.html`, etc.
- A primeira página é a URL base, as demais seguem o padrão acima.
- O loop continua até encontrar a mensagem *"No results found."* ou até que não haja mais livros.

### 6. Estrutura HTML do Site e Seletores

**HTML Típico de um Livro:**

```html
<article class="product_pod">
    <div class="image_container">
        <a href="catalogue/a-light-in-the-attic_1000/index.html">
            <img src="media/cache/2c/da/2cdad67c44b002e7ead0cc35693c0e8b.jpg" 
                 alt="A Light in the Attic" class="thumbnail">
        </a>
    </div>
    <p class="star-rating Three">  <!-- 3 estrelas -->
        <i class="icon-star"></i>
        <i class="icon-star"></i>
        <i class="icon-star"></i>
        <i class="icon-star"></i>
        <i class="icon-star"></i>
    </p>
    <h3><a href="catalogue/a-light-in-the-attic_1000/index.html" 
           title="A Light in the Attic">A Light in the Attic</a></h3>
    <div class="product_price">
        <p class="price_color">£51.77</p>
        <p class="instock availability">
            <i class="icon-ok"></i> In stock
        </p>
        <form>
            <button type="submit" class="btn btn-primary btn-block">Add to basket</button>
        </form>
    </div>
</article>
```

### 7. Extraindo Dados Básicos: `extract_book_data()`

```python
def extract_book_data(book, base_url):
    """Extrai dados de um elemento livro"""
    title = book.h3.a['title']  # Título do atributo title
    price = book.find('p', class_='price_color').get_text(strip=True)
    availability = book.find('p', class_='instock availability').get_text(strip=True)
    
    # Sistema de avaliação por estrelas
    rating_class = book.find('p', class_='star-rating')['class'][1]
    rating_map = {'One': '1 estrela', 'Two': '2 estrelas', ...}
    rating = rating_map.get(rating_class, 'Não avaliado')
```

**Seletores CSS utilizados:**

- `.product_pod` → Container do livro
- `.price_color` → Preço
- `.star-rating` → Avaliação
- `.instock.availability` → Disponibilidade

### 8. Sistema de Avaliação por Estrelas

```python
# As avaliações são representadas por classes CSS:
rating_class = book.find('p', class_='star-rating')['class'][1]
rating_map = {
    'One': '1 estrela',      # Classe: "star-rating One"
    'Two': '2 estrelas',     # Classe: "star-rating Two"
    'Three': '3 estrelas',   # Classe: "star-rating Three"
    'Four': '4 estrelas',    # Classe: "star-rating Four"
    'Five': '5 estrelas'     # Classe: "star-rating Five"
}
rating = rating_map.get(rating_class, 'Não avaliado')
```

### 9. Scraping de Páginas Individuais: `scrap_book_details()`

Para obter informações detalhadas, o programa visita a página individual de cada livro:

```python
def scrape_book_details(book_url):
    """Raspa detalhes da página individual do livro"""
    response = requests.get(book_url)
    soup = BeautifulSoup(response.content, 'html.parser')
    
    # Meta description
    description = soup.find('meta', attrs={'name': 'description'})['content']
    
    # Tabela de metadados
    product_info = {}
    table = soup.find('table', class_='table table-striped')
    for row in table.find_all('tr'):
        header = row.find('th').get_text(strip=True)  # Ex: "UPC"
        value = row.find('td').get_text(strip=True)   # Ex: "a897fe39b1053632"
        product_info[header] = value
```

**Estrutura da Tabela de Metadados**

```html
<table class="table table-striped">
    <tr>
        <th>UPC</th>
        <td>a897fe39b1053632</td>
    </tr>
    <tr>
        <th>Product Type</th>
        <td>Books</td>
    </tr>
    <tr>
        <th>Price (excl. tax)</th>
        <td>£51.77</td>
    </tr>
    <!-- ... mais linhas ... -->
</table>
```

### 10. Conversão de Preços

```python
def _convert_price(self, price_str: str) -> Optional[float]:
    """Converte '£51.77' para 51.77"""
    if not price_str or price_str == 'N/A':
        return None
    try:
        return float(price_str.replace('£', '').strip())
    except ValueError:
        return None
```

### 11. Navegação no Breadcrumb para Categoria

```python
# O breadcrumb mostra a hierarquia de navegação
# Exemplo: Home > Books > Poetry
category = ""
breadcrumb = soup.find('ul', class_='breadcrumb')
if breadcrumb:
	breadcrumb_items = breadcrumb.find_all('li')
	if len(breadcrumb_items) >= 3:
		category = breadcrumb_items[2].get_text(strip=True)
```

**Estrutura do Breadcrumb:**

```html
<ul class="breadcrumb">
    <li><a href="index.html">Home</a></li>
    <li><a href="catalogue/category/books_1/index.html">Books</a></li>
    <li><a href="catalogue/category/books/poetry_23/index.html">Poetry</a></li>
</ul>
```

### 12. Tratamento de URLs Relativas

```python
# Converte URLs relativas para absolutas
from urllib.parse import urljoin

relative_link = book.h3.a['href']  # Ex: "catalogue/book-name/index.html"
book_link = urljoin(base_url, relative_link)  # Ex: "https://books.toscrape.com/catalogue/book-name/index.html"

image_url = soup.find('img')['src']  # Ex: "../../media/cache/image.jpg"
full_image_url = urljoin(book_url, image_url)  # URL absoluta completa
```

### 13. Gerenciamento de Erros e Robustez

```python
try:
    response = requests.get(url, headers=headers)
    response.raise_for_status()  # Levanta exceção para status 4xx/5xx
    
except requests.RequestException as e:
    print(f"Erro na requisição: {e}")
    # Continua para a próxima página em vez de quebrar o programa

# Fallbacks para seletores que podem falhar
title = book.h3.a['title'] if book.h3 and book.h3.a else 'Título não disponível'
```

### 14. Exportação para CSV com Pandas

```python
def save_to_csv(books_data, filename='books_toscrape.csv'):
    """
    Converte lista de dicionários para DataFrame e exporta para CSV
    """
    df = pd.DataFrame(books_data)  # Cria DataFrame from list of dicts
    
    # Cria diretório se não existir
    os.makedirs('dados', exist_ok=True)
    filepath = os.path.join('dados', filename)
    
    # Exporta com encoding UTF-8 para suportar caracteres especiais
    df.to_csv(filepath, index=False, encoding='utf-8')
```

### 15. Análise e Estatísticas dos Dados

```python
 # Obter estatísticas do banco
stats = db_manager.get_book_stats()
print("\n=== 📊 ESTATÍSTICAS DO BANCO ===")
print(f"📚 Total de livros: {stats.get('total_books', 0)}")
print(f"💰 Preço médio: £{stats.get('avg_price', 0):.2f}")
print(f"🏷️ Categorias únicas: {stats.get('unique_categories', 0)}")

if stats.get('top_categories'):
	print("\n🏆 Top 5 categorias:")
	for category in stats['top_categories']:
		print(f"  {category['name']}: {category['book_count']}
```

---
## 🗃️ Estrutura do Banco de Dados

### Diagrama do Schema

```text
books_scraper
├── categories
│   ├── id (PK)
│   ├── name (UNIQUE)
│   └── created_at
│
└── books
    ├── id (PK)
    ├── upc (UNIQUE)
    ├── title
    ├── price (DECIMAL)
    ├── category_id (FK → categories.id)
    ├── rating
    ├── description (TEXT)
    └── scraped_at
```

### Script de Criação das Tabelas

```sql
USE books_scraper;

CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE books (
    id INT AUTO_INCREMENT PRIMARY KEY,
    upc VARCHAR(50) UNIQUE,
    title VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2),
    price_excl_tax DECIMAL(10, 2),
    price_incl_tax DECIMAL(10, 2),
    tax DECIMAL(10, 2),
    availability VARCHAR(100),
    rating VARCHAR(20),
    category_id INT,
    product_type VARCHAR(100),
    description TEXT,
    number_of_reviews INT DEFAULT 0,
    image_url VARCHAR(500),
    book_url VARCHAR(500),
    scraped_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL,
    INDEX idx_books_title (title),
    INDEX idx_books_price (price),
    INDEX idx_books_category (category_id),
    INDEX idx_books_upc (upc)
);
```

---
## 🚀 Como Executar

### 1. Arquivo de Requisitos (`requirements.txt`)

```txt
requests==2.31.0
beautifulsoup4==4.12.2
pandas==2.0.3
mysql-connector-python==8.1.0
python-dotenv==1.0.0
urllib==3.11.0
```

### 2. Preparação do Ambiente

```bash
# Instalar dependências
pip install -r requirements.txt

# Configurar arquivo .env
echo "DB_HOST=localhost" > .env
echo "DB_PORT=3306" >> .env
echo "DB_NAME=books_scraper" >> .env
echo "DB_USER=scraper_user" >> .env
echo "DB_PASSWORD=sua_senha_segura" >> .env
```

### 3. Execução

```bash
python books_scraper_mysql.py
```

### 4. Verificação dos Dados

```bash
# Acessar MySQL
mysql -u scraper_user -p books_scraper

-- Verificar dados
SELECT COUNT(*) as total_livros FROM books;
SELECT title, price, rating FROM books LIMIT 10;
```

### Saída Esperada

```text
=== WEB SCRAPING - BOOKS TO SCRAPE COM MYSQL ===
✅ Banco de dados inicializado com sucesso!
🔄 Iniciando scraping...
📚 Iniciando scraping do Books to Scrape...
📄 Raspando página 1: https://books.toscrape.com/
✅ Encontrados 20 livros na página 1
📄 Raspando página 2: https://books.toscrape.com/catalogue/page-2.html
✅ Encontrados 20 livros na página 2
📄 Raspando página 3: https://books.toscrape.com/catalogue/page-3.html
...
✅ Não há mais páginas. Finalizando...
💾 Salvando dados no MySQL...
✅ Inseridos/Atualizados 980 livros no banco de dados
✅ Backup salvo em: dados\books_toscrape.csv
📊 Total de livros no backup: 1000

=== 📊 ESTATÍSTICAS DO BANCO ===
📚 Total de livros: 1001
💰 Preço médio: £35.05
🏷️ Categorias únicas: 51

🏆 Top 5 categorias:
  Default: 152 livros
  Nonfiction: 110 livros
  Sequential Art: 75 livros
  Add a comment: 67 livros
  Fiction: 65 livros
```

### Banco de Dados

![[Pasted image 20250828145844.png]]

### Programa em Ação

![[Pasted image 20250828150503.png]]

### Resultados

![[Pasted image 20250828151742.png]]

---
## 📊 Exemplos de Uso

### Consultas SQL Úteis

```sql
-- Livros por categoria
SELECT c.name as categoria, COUNT(b.id) as total
FROM books b
JOIN categories c ON b.category_id = c.id
GROUP BY c.name
ORDER BY total DESC;

-- Preço médio por categoria
SELECT c.name, AVG(b.price) as preco_medio
FROM books b
JOIN categories c ON b.category_id = c.id
GROUP BY c.name
ORDER BY preco_medio DESC;

-- Top 10 livros mais caros
SELECT title, price, rating, availability
FROM books
ORDER BY price DESC
LIMIT 10;
```

### Análise com Python

```python
# Após o scraping, analyze os dados
stats = db_manager.get_book_stats()
print(f"Total de livros: {stats['total_books']}")
print(f"Preço médio: £{stats['avg_price']:.2f}")
print(f"Categoria com mais livros: {stats['top_categories'][0]['name']}")
```

---
## ⚡ Boas Práticas de Web Scraping Implementadas

### 1. Gestão de Conexões

```python
# Uso de connection pool
with connection_pool.get_connection() as conn:
    with conn.cursor() as cursor:
        cursor.execute(...)
```

### 2. Tratamento de Erros

```python
try:
    # Operação de banco
except mysql.connector.Error as e:
    print(f"Erro MySQL: {e}")
    if connection:
        connection.rollback()
```

### 3. Prevenção de SQL Injection

```python
# Uso de parâmetros seguros
cursor.execute("INSERT INTO books (title, price) VALUES (%s, %s)", 
               (title, price))
```

### 4. Respeito ao Servidor

```python
# Delay entre requisições
time.sleep(1)  # 1 segundo entre páginas

# Headers realistas
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36',
    'Accept-Language': 'pt-BR,pt;q=0.9,en;q=0.8'
}
```

### 5. Backup e Resilência

```python
# Backup em CSV além do MySQL
def save_to_csv(books_data):
    df = pd.DataFrame(books_data)
    df.to_csv('backup_books.csv', index=False, encoding='utf-8')
```

---
## 🐛 Possíveis Problemas e Soluções

### 1. Erro de Conexão MySQL

```bash
# Verificar se MySQL está rodando
sudo service mysql start

# Verificar credenciais no .env
```

### 2. Erro de Permissões

```sql
-- Conceder permissões
GRANT ALL PRIVILEGES ON books_scraper.* TO 'scraper_user'@'localhost';
FLUSH PRIVILEGES;
```

### 3. Timeout de Conexão

```python
# Aumentar timeout
response = requests.get(url, timeout=30)
```

---
## 📈 Próximos Passos e Melhorias Possíveis

1. **🔄 Scraping Incremental**: Atualizar apenas dados modificados
2. **📊 Dashboard Web**: Interface visual para os dados
3. **🔍 Busca Avançada**: Funcionalidade de search no banco
4. **📱 API REST**: Endpoints para acesso programático
5. **🤖 Automação**: Agendamento de scraping periódico

---
## 📝 Licença e Considerações Éticas

Este projeto é para fins educacionais. O site Books to Scrape foi criado especificamente para praticar web scraping. Ao fazer scraping de sites reais:

- ✅ Verifique o `robots.txt`
- ✅ Respeite os termos de serviço
- ✅ Use delays apropriados
- ✅ Não sobrecarregue os servidores
- ✅ Use os dados coletados de forma ética