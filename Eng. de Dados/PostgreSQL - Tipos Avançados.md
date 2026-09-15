---

tags:

- banco-de-dados
- postgresql aliases: [JSONB, UUID, ENUM, ARRAY, Tipos Avançados Postgres]

---

# PostgreSQL - Tipos Avançados

## 📌 Conceito principal

Além dos tipos padrão do SQL (ver [[SQL - Tipos de Dados]]), o PostgreSQL oferece tipos avançados que outros SGBDs relacionais (como o MySQL) não têm de forma nativa — são um dos motivos que fazem do PostgreSQL a escolha padrão para projetos novos em 2026.

> [!info] Fonte oficial A documentação do PostgreSQL detalha o catálogo completo de tipos suportados, incluindo os tipos avançados citados abaixo. Fonte: [postgresql.org/docs — Tipos de Dados](https://www.postgresql.org/docs/current/datatype.html)

## 🧩 JSONB — dados semiestruturados indexáveis

```sql
CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    atributos JSONB
);

INSERT INTO produtos (nome, atributos) VALUES
    ('Camiseta', '{"cor": "azul", "tamanho": "M"}');

SELECT nome FROM produtos WHERE atributos @> '{"cor": "azul"}';
```

Ver aprofundamento em [[PostgreSQL - JSONB na Prática]].

## 🆔 UUID — identificador único universal

```sql
CREATE EXTENSION IF NOT EXISTS "pgcrypto"; -- necessário para gen_random_uuid()

CREATE TABLE sessoes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    usuario_id INT
);
```

> [!tip] UUID vs. SERIAL como chave primária `UUID` evita que IDs sejam previsíveis/sequenciais (útil em APIs públicas) e permite gerar o identificador **antes** de inserir no banco (útil em sistemas distribuídos). Em troca, ocupa mais espaço (16 bytes vs. 4/8 de um inteiro) e pode ser levemente mais lento em índices B-Tree por não ser sequencial.

## 🏷️ ENUM — conjunto fixo de valores

```sql
CREATE TYPE status_pedido AS ENUM ('pendente', 'processando', 'concluido', 'cancelado');

CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    status status_pedido NOT NULL DEFAULT 'pendente'
);

-- O banco rejeita valores fora do conjunto definido:
INSERT INTO pedidos (status) VALUES ('invalido'); -- ERRO
```

> [!tip] ENUM vs. CHECK vs. tabela de referência `ENUM` é rápido e garante integridade no schema, mas alterar a lista de valores depois exige `ALTER TYPE` (uma operação um pouco mais delicada). Para listas que mudam com frequência, uma tabela de referência com chave estrangeira costuma ser mais flexível a longo prazo.

## 📚 ARRAY — lista de valores em uma coluna

```sql
CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    tags TEXT[]
);

INSERT INTO produtos (tags) VALUES (ARRAY['promocao', 'novidade']);

SELECT * FROM produtos WHERE 'promocao' = ANY(tags);
```

> [!warning] Array não substitui uma tabela relacionada Um `ARRAY` é conveniente para listas simples e pequenas, mas viola a atomicidade da [[BD - Primeira Forma Normal (1FN)]] no sentido estrito. Para listas que precisam de metadados próprios (data de associação, quem adicionou) ou que crescem muito, uma tabela relacionada 1:N continua sendo a escolha mais robusta.

## ⏳ Tipos de intervalo (Range Types)

```sql
CREATE TABLE reservas (
    id SERIAL PRIMARY KEY,
    periodo TSRANGE
);

INSERT INTO reservas (periodo) VALUES ('[2026-08-01, 2026-08-10)');

-- Verifica sobreposição de intervalos diretamente no SQL
SELECT * FROM reservas WHERE periodo && '[2026-08-05, 2026-08-15)';
```

## 🔗 Notas relacionadas

- [[SQL - Tipos de Dados]]
- [[PostgreSQL - JSONB na Prática]]
- [[PostgreSQL - Extensões]]
- [[Banco de Dados]]