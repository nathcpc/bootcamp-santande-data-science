# Normalização de Dados e Consultas Avançadas (SQL)

## 🎯 O que eu aprendi

Processo completo de normalização (1FN, 2FN, 3FN, BCNF), junções avançadas (INNER, LEFT, RIGHT, FULL), subconsultas, funções agregadas, GROUP BY/HAVING, otimização com índices (EXPLAIN) e conceitos de ORM para Data Science.

---

## 📊 Normalização de Dados

**Objetivo:** Organizar dados para eliminar redundâncias e anomalias, garantindo consistência e integridade.

**As formas normais são INCREMENTAIS** (cada uma inclui as anteriores).

### **1FN - Primeira Forma Normal (Atomicidade)**

✅ **Cada valor deve ser ATÔMICO** (indivisível, sem listas)

❌ VIOLAÇÃO: endereco = "Rua A, 123, SP"
✅ 1FN: Separar em colunas
rua = "Rua A"
numero = "123"
cidade = "SP"
estado = "SP"

text

**Correção prática:**
ALTER TABLE usuarios
ADD COLUMN rua VARCHAR(100),
ADD COLUMN numero VARCHAR(10),
ADD COLUMN cidade VARCHAR(50),
ADD COLUMN estado VARCHAR(20);

UPDATE usuarios
SET rua = SUBSTRING_INDEX(endereco, ',', 1),
numero = SUBSTRING_INDEX(SUBSTRING_INDEX(endereco, ',', 2), ',', -1),
cidade = SUBSTRING_INDEX(SUBSTRING_INDEX(endereco, ',', 3), ',', -1),
estado = SUBSTRING_INDEX(endereco, ',', -1);

text

### **2FN - Segunda Forma Normal (Dependência Total)**

✅ **Todos atributos NÃO-CHAVE dependem TOTALMENTE da chave primária**

**Aplica-se apenas a chaves primárias COMPOSTAS**

❌ VIOLAÇÃO (chave: pedido_id + produto_id):
desconto → depende APENAS de produto_id (parcial)

✅ 2FN: Separar em tabelas
pedidos_produtos (pedido_id, produto_id, quantidade)
produtos (produto_id, desconto)

text

### **3FN - Terceira Forma Normal (Sem Transitivas)**

✅ **Nenhum atributo NÃO-CHAVE depende de outro NÃO-CHAVE**

❌ VIOLAÇÃO:
estado → cidade → cep (transitiva)

✅ 3FN:
usuarios (id, cidade_id)
cidades (cidade_id, nome, estado_id)
estados (estado_id, nome)

text

### **BCNF (Boyce-Codd) e Além**

| Forma Normal | Requisito |
|--------------|-----------|
| **BCNF** | Todo determinante é chave candidata |
| **4FN** | Elimina dependências multi-valoradas |
| **5FN** | Elimina dependências de JOIN |
| **DK/NF** | Todas restrições seguem domínios/chaves |

**Na prática:** 3FN atende 95% dos casos.

---

## 🔗 Consultas com Junções (JOINs)

Combinam dados de **duas ou mais tabelas** baseadas em condições.

### **Tipos de JOIN**

| JOIN | Retorna | Exemplo |
|------|---------|---------|
| **INNER JOIN** | Apenas correspondências | Clientes COM pedidos |
| **LEFT JOIN** | TODOS da esquerda + correspondentes da direita | TODOS clientes (com/sem pedidos) |
| **RIGHT JOIN** | TODOS da direita + correspondentes da esquerda | TODOS pedidos (com/sem cliente) |
| **FULL JOIN** | TODOS de AMBAS (NULL onde não há match) | União completa |

### **Exemplos Práticos**

-- INNER JOIN (padrão mais usado)
SELECT c.nome, p.valor
FROM clientes c
INNER JOIN pedidos p ON c.id = p.id_cliente;

-- LEFT JOIN (todos clientes)
SELECT c.nome, p.valor
FROM clientes c
LEFT JOIN pedidos p ON c.id = p.id_cliente;

-- RIGHT JOIN (raramente usado)
SELECT c.nome, p.valor
FROM clientes c
RIGHT JOIN pedidos p ON c.id = p.id_cliente;

-- FULL JOIN (pouco suportado)
SELECT c.nome, p.valor
FROM clientes c
FULL JOIN pedidos p ON c.id = p.id_cliente;

text

---

## 🧮 Subconsultas

Usar resultado de UMA consulta como entrada de OUTRA.

-- WHERE (filtro)
SELECT nome
FROM clientes
WHERE id IN (
SELECT id_cliente
FROM pedidos
WHERE valor > 1000
);

-- FROM (tabela derivada)
SELECT AVG(valor)
FROM (
SELECT valor
FROM pedidos
WHERE data >= '2025-01-01'
) AS pedidos_recentes;

-- HAVING
SELECT cliente_id, SUM(valor) as total
FROM pedidos
GROUP BY cliente_id
HAVING total > (
SELECT AVG(total)
FROM (SELECT SUM(valor) as total FROM pedidos GROUP BY cliente_id) t
);

text

---

## ⚙️ Funções Agregadas

Realizam cálculos em conjuntos de dados.

| Função | Descrição | Exemplo |
|--------|-----------|---------|
| `COUNT(*)` | Conta registros | `COUNT(*) AS total_usuarios` |
| `SUM(coluna)` | Soma valores | `SUM(valor) AS receita_total` |
| `AVG(coluna)` | Média | `AVG(idade) AS idade_media` |
| `MIN(coluna)` | Mínimo | `MIN(data) AS primeiro_pedido` |
| `MAX(coluna)` | Máximo | `MAX(valor) AS maior_venda` |

**Exemplos:**
-- Contar usuários com reservas
SELECT COUNT(*) AS usuarios_com_reserva
FROM usuarios u
INNER JOIN reservas r ON u.id = r.id_usuario;

-- Idade máxima
SELECT MAX(TIMESTAMPDIFF(YEAR, data_nascimento, CURRENT_DATE())) AS maior_idade
FROM usuarios;

text

**Apelidos (ALIAS):**
SELECT COUNT(*) AS total, AVG(valor) AS ticket_medio
FROM pedidos;

text

---

## 📈 GROUP BY + HAVING + ORDER BY

### **Estrutura Completa**

SELECT coluna, agregacao
FROM tabelas
JOIN condições
WHERE filtros
GROUP BY coluna
HAVING filtro_agregado
ORDER BY coluna ASC|DESC;

text

**Exemplo Data Science:**
SELECT
DATE(p.data) AS dia,
COUNT(*) AS pedidos,
SUM(p.valor) AS receita,
COUNT(DISTINCT p.id_cliente) AS clientes_unicos
FROM pedidos p
WHERE p.data >= '2025-11-01'
GROUP BY DATE(p.data)
HAVING receita > 10000
ORDER BY receita DESC;

text

---

## 🚀 Otimização com Índices

**Índices aceleram buscas** (como índice remissivo de livro).

### **Criar Índice**

-- Índice simples
CREATE INDEX idx_nome ON usuarios(nome);

-- Índice composto
CREATE INDEX idx_data_valor ON pedidos(data, valor);

-- Índice único (evita duplicatas)
CREATE UNIQUE INDEX idx_email ON usuarios(email);

text

### **EXPLAIN - Análise de Performance**

EXPLAIN SELECT * FROM usuarios WHERE email = 'teste@teste.com';

text

**Campos importantes:**
| Campo | Significado |
|-------|-------------|
| `type` | ALL=varre tudo, INDEX=usa índice |
| `key` | Nome do índice usado |
| `rows` | Linhas processadas |
| `possible_keys` | Índices disponíveis |

**Exemplo prático:**
-- ❌ SEM ÍNDICE (type: ALL, rows: 1000000)
EXPLAIN SELECT * FROM usuarios WHERE nome = 'João';

-- ✅ COM ÍNDICE (type: ref, rows: 1)
CREATE INDEX idx_nome ON usuarios(nome);
EXPLAIN SELECT * FROM usuarios WHERE nome = 'João';

text

---

## 🔄 ORM (Object-Relational Mapping)

**Tradutor** entre código (Python, JS) e SQL.

**Como funciona:**
Código Python → ORM → SQL
SELECT * FROM usuarios → ORM → objetos Python

text

**Vantagens:**
- ✅ Código mais legível
- ✅ Menos SQL manual
- ✅ Portabilidade entre SGBDs
- ✅ Segurança (evita SQL injection)

**Exemplos populares:**
SQLAlchemy (Python)
usuario = Usuario.query.filter_by(email="teste@teste.com").first()

Django ORM (Python)
usuarios = Usuario.objects.filter(idade__gt=18)

Sequelize (Node.js)
const usuarios = await Usuario.findAll({ where: { idade: { [Op.gt]: 18 } } });

text

---

## 💡 Dicas para Data Science

1. **Sempre use EXPLAIN** antes de queries em produção
2. **Crie índices em colunas WHERE/JOIN/GROUP BY**
3. **Evite SELECT *** (especifique colunas)
4. **Use 3FN** como padrão (desnormalizar só com motivo)
5. **JOINs > Subconsultas** para performance

---

## 🔗 Recursos Recomendados

- [MariaDB - CREATE INDEX](https://mariadb.com/docs/server/reference/sql-statements/data-definition/alter/alter-table#add-index)
- [DataCamp - SQL Indexes](https://www.datacamp.com/pt/tutorial/sql-server-index)
- [DataCamp - Normalização](https://www.datacamp.com/pt/tutorial/normalization-in-dbms)
- [Alura - ORM](https://www.alura.com.br/artigos/orm)

---

[⬅️ Voltar ao Índice do Módulo](README.md)