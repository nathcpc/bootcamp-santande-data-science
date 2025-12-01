# Introdução a Bancos de Dados Relacionais (SQL)

## 🎯 O que eu aprendi

Conceitos fundamentais de bancos relacionais, modelagem de dados (MER/DER), operações CRUD, chaves primárias/estrangeiras, normalização e consultas avançadas essenciais para Data Science.

---

## 🗄️ Tipos de Bancos de Dados

| Tipo | Características | Exemplos | Uso em Data Science |
|------|-----------------|----------|---------------------|
| **Relacional (SQL)** | Tabelas, relacionamentos, SQL padronizado | PostgreSQL, MySQL, SQLite | Análise estruturada, BI, relatórios |
| **Não Relacional (NoSQL)** | Documentos, grafos, chave-valor | MongoDB, Cassandra | Big Data, dados não estruturados |
| **Orientado a Objetos** | Armazena objetos complexos | db4o | Aplicações OOP avançadas |
| **Hierárquico** | Estrutura árvore | IBM IMS | Sistemas legados |

**SGBD (Sistema Gerenciador de Banco de Dados):** Software que gerencia o BD (PostgreSQL, MySQL, SQLite).

---

## 🔑 Estrutura do Banco Relacional

**Características principais:**
- **Relacionamentos entre tabelas** via chaves estrangeiras  
- **SQL** (Structured Query Language) padronizada  
- **Integridade referencial** (evita dados órfãos)  
- **Normalização** (evita redundância)  
- **Transações ACID** (Atomicidade, Consistência, Isolamento, Durabilidade)  

**ACID explicado:**
ATOMICIDADE: Tudo ou nada (se erro, desfaz)
CONSISTÊNCIA: Sai de estado válido para válido
ISOLAMENTO: Transações não interferem
DURABILIDADE: Dados salvos permanentemente

text

---

## 🗣️ Organização da SQL

| Categoria | Comandos | Função |
|-----------|----------|--------|
| **DQL** | `SELECT` | Consultar/Recuperar dados |
| **DML** | `INSERT`, `UPDATE`, `DELETE` | Manipular dados |
| **DDL** | `CREATE`, `ALTER`, `DROP` | Definir estrutura |
| **DCL** | `GRANT`, `REVOKE` | Controle de acesso |
| **DTL** | `BEGIN`, `COMMIT`, `ROLLBACK` | Gerenciar transações |

**Convenções de nomenclatura:**
- Começa com letra ou `_`  
- Apenas letras, números e `_`  
- Case-sensitive em alguns SGBDs  

---

## 📐 Modelagem: MER e DER

### MER (Modelo Entidade-Relacionamento)

Modelo **conceitual** que define:
- **Entidades** (retângulo) → Tabelas  
- **Atributos** (elipse/lista) → Colunas  
- **Relacionamentos** (losango) → Ligações  

### DER (Diagrama Entidade-Relacionamento)

Representação gráfica do MER.

**Cardinalidades:**
1:1 → Um cliente, um endereço
1:N → Um cliente, vários pedidos
N:N → Pedidos com vários produtos (tabela intermediária)

text

**Ferramentas recomendadas:**
- https://dbdiagram.io  
- https://app.quickdatabasediagrams.com  

---

## 🛠️ Tabelas, Colunas e Registros

- **Tabela** → Container organizado (nome único)  
- **Coluna** → Atributo específico (nome + tipo de dado)  
- **Registro** → Linha completa (tupla)  

### Tipos de Dados Comuns

| Tipo | Exemplo | Uso |
|------|---------|-----|
| `INT` | `42` | IDs, contadores |
| `DECIMAL(10,2)` | `1234.56` | Valores monetários |
| `VARCHAR(50)` | `"João Silva"` | Nomes, emails |
| `DATE` | `2025-11-28` | Datas |
| `BOOLEAN` | `TRUE` | Sim/Não |
| `TEXT` | (texto longo) | Descrições |

---

## ⚙️ Operações CRUD

### CREATE (Criar)

CREATE TABLE clientes (
id INT PRIMARY KEY AUTO_INCREMENT,
nome VARCHAR(100) NOT NULL,
email VARCHAR(100) UNIQUE,
data_cadastro DATE DEFAULT CURRENT_DATE
);

text

### READ (Ler)

-- Simples
SELECT * FROM clientes;

-- Específico com filtro
SELECT nome, email
FROM clientes
WHERE data_cadastro >= '2025-01-01'
AND id IN (1, 2, 3);

text

Principais operadores para `WHERE`:

= igual
<> ou != diferente

maior que
< menor que
= maior ou igual
<= menor ou igual
LIKE '%joao%' padrão
BETWEEN 100 AND 200 intervalo
IN (1,2,3) lista
AND / OR lógicos

text

### UPDATE (Atualizar)

UPDATE clientes
SET email = 'novo@email.com'
WHERE id = 1;

text

⚠️ Sempre usar `WHERE` para não atualizar tudo sem querer.

### DELETE (Excluir)

DELETE FROM clientes
WHERE id = 1;

text

---

## 🔐 Chaves Primárias e Estrangeiras

### Chave Primária (PK)

- Identifica **exclusivamente** cada registro  
- **Única** e **não nula**  
- Geralmente `AUTO_INCREMENT`  

CREATE TABLE pedidos (
id_pedido INT PRIMARY KEY AUTO_INCREMENT,
id_cliente INT,
valor DECIMAL(10,2)
);

text

### Chave Estrangeira (FK)

CREATE TABLE pedidos (
id_pedido INT PRIMARY KEY AUTO_INCREMENT,
id_cliente INT,
valor DECIMAL(10,2),
FOREIGN KEY (id_cliente) REFERENCES clientes(id)
);

text

Restrições comuns em FK:

ON DELETE CASCADE → Deleta filhos se pai for deletado
ON DELETE SET NULL → Define NULL nos filhos
ON UPDATE CASCADE → Propaga updates do pai

text

---

## 🔄 DDL: ALTER e DROP

-- Adicionar coluna
ALTER TABLE clientes
ADD COLUMN telefone VARCHAR(20);

-- Modificar coluna
ALTER TABLE clientes
MODIFY COLUMN nome VARCHAR(150);

-- Remover coluna
ALTER TABLE clientes
DROP COLUMN telefone;

-- Remover tabela (permanente)
DROP TABLE clientes;

text

---

## 📊 Normalização de Dados

Objetivo: eliminar redundância e anomalias de inserção, atualização e exclusão.

### 1NF (Primeira Forma Normal)

- Valores **atômicos** (uma informação por célula)
- Sem listas dentro de uma mesma coluna

❌ ANTES: nome_cliente = "João, Maria"
✅ DEPOIS: separar em tabela de clientes

text

### 2NF (Segunda Forma Normal)

- Estar em 1NF  
- Não ter **dependência parcial** em chave primária composta  
  (nenhuma coluna depende só de parte da chave composta)

### 3NF (Terceira Forma Normal)

- Estar em 2NF  
- Não ter **dependência transitiva**  
  (coluna não pode depender de outra coluna, apenas da chave)

---

## 🚀 Consultas Avançadas (Data Science)

### Funções Agregadas + GROUP BY

-- Vendas por cliente
SELECT
c.nome,
COUNT(p.id_pedido) AS total_pedidos,
SUM(p.valor) AS total_gasto,
AVG(p.valor) AS ticket_medio
FROM clientes c
JOIN pedidos p
ON c.id = p.id_cliente
GROUP BY c.id, c.nome
HAVING total_gasto > 1000
ORDER BY total_gasto DESC;

text

### JUNÇÕES (JOINs)

-- INNER JOIN: apenas registros com correspondência nas duas tabelas
SELECT c.nome, p.valor
FROM clientes c
INNER JOIN pedidos p
ON c.id = p.id_cliente;

-- LEFT JOIN: todos os clientes, mesmo sem pedidos
SELECT c.nome, p.valor
FROM clientes c
LEFT JOIN pedidos p
ON c.id = p.id_cliente;

text

---

## 💡 SQL para Data Science

Por que SQL é essencial:

1. Grande parte dos dados corporativos está em bancos relacionais  
2. Integração direta com Python (por exemplo, `pandas.read_sql`)  
3. Uso em ferramentas de BI (Power BI, Tableau, Looker, etc.)  
4. Construção de pipelines ETL (Extrair → Transformar → Carregar)  

Exemplo de query de KPIs:

-- KPIs de negócio em uma query
SELECT
DATE(p.data) AS dia,
COUNT(*) AS pedidos,
SUM(p.valor) AS receita,
AVG(p.valor) AS ticket_medio,
COUNT(DISTINCT p.id_cliente) AS clientes_unicos
FROM pedidos p
WHERE p.data >= CURRENT_DATE - INTERVAL 30 DAY
GROUP BY DATE(p.data)
ORDER BY dia;

text

---

## 🔗 Recursos Recomendados

- https://www.sqltutorial.org/  
- https://dbdiagram.io  
- https://www.postgresql.org/  
- https://clients.cloudclusters.io/  

---

[⬅️ Voltar ao Índice do Módulo](README.md)