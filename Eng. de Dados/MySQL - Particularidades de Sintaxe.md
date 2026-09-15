---

tags:

- banco-de-dados
- mysql aliases: [MySQL vs PostgreSQL, Diferenças de Sintaxe SQL]

---

# MySQL - Particularidades de Sintaxe

## 📌 Conceito principal

Embora ambos falem "SQL", MySQL e PostgreSQL têm diferenças reais de sintaxe, tipos e comportamento — importantes de conhecer ao migrar entre os dois ou trabalhar em stacks que usam MySQL.

## 🔢 Autoincremento

```sql
-- PostgreSQL
id SERIAL PRIMARY KEY

-- MySQL
id INT AUTO_INCREMENT PRIMARY KEY
```

## ✅ Booleano

```sql
-- PostgreSQL: tipo nativo
ativo BOOLEAN DEFAULT true

-- MySQL: não existe BOOLEAN nativo, é apelido de TINYINT(1)
ativo TINYINT(1) DEFAULT 1
```

## 📄 Texto: LIMIT vs. TOP e paginação

```sql
-- Ambos suportam LIMIT/OFFSET da mesma forma
SELECT * FROM produtos ORDER BY id LIMIT 10 OFFSET 20;

-- MySQL aceita a forma abreviada:
SELECT * FROM produtos LIMIT 20, 10; -- OFFSET 20, LIMIT 10 (ordem invertida, cuidado!)
```

> [!warning] Cuidado com a forma abreviada do LIMIT no MySQL `LIMIT 20, 10` no MySQL significa "pule 20, traga 10" — a ordem dos números é o oposto do que a leitura sugere à primeira vista. Prefira a forma explícita `LIMIT 10 OFFSET 20`, suportada em ambos os SGBDs, para evitar erro de leitura.

## 🔤 Aspas e identificadores

```sql
-- PostgreSQL: identificadores com aspas duplas, strings com aspas simples
SELECT "coluna com espaço" FROM tabela WHERE nome = 'João';

-- MySQL: aceita crase para identificadores (não é padrão SQL)
SELECT `coluna com espaço` FROM tabela WHERE nome = 'João';
```

## 🧩 JSON

```sql
-- PostgreSQL tem JSON e JSONB (binário, indexável — ver PostgreSQL - JSONB na Prática)
-- MySQL tem apenas JSON (armazenado de forma otimizada internamente, mas sem a distinção JSONB)

-- Sintaxe de consulta é parecida, mas com funções próprias:
SELECT JSON_EXTRACT(atributos, '$.cor') FROM produtos; -- MySQL
SELECT atributos -> 'cor' FROM produtos;                -- PostgreSQL
```

## 🔁 UPSERT (inserir ou atualizar)

```sql
-- PostgreSQL
INSERT INTO produtos (id, nome, preco) VALUES (1, 'Caneta', 2.50)
ON CONFLICT (id) DO UPDATE SET preco = EXCLUDED.preco;

-- MySQL
INSERT INTO produtos (id, nome, preco) VALUES (1, 'Caneta', 2.50)
ON DUPLICATE KEY UPDATE preco = VALUES(preco);
```

## 📆 Funções de data comuns que diferem

|Função|PostgreSQL|MySQL|
|---|---|---|
|Data/hora atual|`NOW()`|`NOW()` (ambos suportam)|
|Extrair parte da data|`EXTRACT(YEAR FROM data)`|`YEAR(data)`|
|Concatenar strings|`\|` ou `CONCAT()`|`CONCAT()` (não suporta `\|` por padrão)|

> [!tip] Ao migrar entre os dois motores A maior parte do SQL "core" (SELECT, WHERE, JOIN, GROUP BY) é idêntica — as diferenças concentram-se em: tipos de dado avançados, funções específicas de data/JSON, e sintaxe de UPSERT. Ver também o guia de migração em [[Cloud para Dados - Matriz da Trilha]] (Nível 11 — Multi-Cloud e Portabilidade).

## 🔗 Notas relacionadas

- [[SQL - Tipos de Dados]]
- [[MySQL - Storage Engines]]
- [[BD - Relacional vs NoSQL]]
- [[Banco de Dados]]