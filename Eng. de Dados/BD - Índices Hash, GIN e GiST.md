---

tags:

- banco-de-dados
- performance
- postgresql aliases: [Índice Hash, GIN, GiST, Índices Especiais]

---

# BD - Índices Hash, GIN e GiST

## 📌 Conceito principal

Nem todo tipo de consulta se beneficia de um índice B-Tree (ver [[BD - Índices B-Tree]]). PostgreSQL oferece métodos de índice especializados para casos específicos: igualdade pura, busca em texto/JSON, e dados geoespaciais/intervalos.

> [!info] Métodos de índice do PostgreSQL A documentação oficial do PostgreSQL lista B-Tree, Hash, GiST, SP-GiST, GIN e BRIN como os métodos de índice disponíveis, cada um usando um algoritmo diferente, mais adequado a tipos distintos de consulta. Fonte: [postgresql.org/docs — Tipos de Índice](https://www.postgresql.org/docs/current/indexes-types.html)

## #️⃣ Índice Hash

Otimizado **exclusivamente** para igualdade (`=`) — não serve para `<`, `>`, `BETWEEN` ou `ORDER BY`.

```sql
CREATE INDEX idx_produtos_codigo_hash ON produtos USING HASH (codigo_barras);

SELECT * FROM produtos WHERE codigo_barras = '7891000100103'; -- usa o índice
SELECT * FROM produtos WHERE codigo_barras > '7891000100103'; -- NÃO usa (hash não ordena)
```

> [!tip] Hash vs. B-Tree para igualdade Na prática, B-Tree já é eficiente o suficiente para igualdade na maioria dos casos, e ainda serve para comparações de ordem — por isso o índice Hash é usado com pouca frequência hoje; B-Tree costuma ser o padrão até para buscas só por igualdade.

## 🧩 GIN (Generalized Inverted Index)

Ideal para dados que contêm **múltiplos valores em uma única linha** — arrays, `JSONB`, e busca de texto completo (full-text search).

```sql
-- Índice sobre uma coluna JSONB inteira
CREATE INDEX idx_produtos_metadados ON produtos USING GIN (metadados);

-- Consulta que se beneficia do índice
SELECT * FROM produtos WHERE metadados @> '{"cor": "azul"}';

-- Índice para full-text search
CREATE INDEX idx_produtos_busca ON produtos USING GIN (to_tsvector('portuguese', descricao));
```

Ver também [[PostgreSQL - JSONB na Prática]] e [[Recipe - Busca Full-Text]].

## 🌐 GiST (Generalized Search Tree)

Estrutura flexível usada para dados que não têm uma ordem linear simples — dados geoespaciais (via extensão **PostGIS**), intervalos de tempo/número, e busca por similaridade de texto (via extensão `pg_trgm`).

```sql
-- Índice geoespacial (requer extensão PostGIS)
CREATE INDEX idx_lojas_localizacao ON lojas USING GIST (localizacao);

-- Índice para busca por similaridade de texto (requer extensão pg_trgm)
CREATE INDEX idx_produtos_nome_trgm ON produtos USING GIST (nome gist_trgm_ops);
SELECT * FROM produtos WHERE nome % 'notbook'; -- encontra "notebook" mesmo com erro de digitação
```

## ⚖️ Quando usar cada um

|Método|Melhor para|
|---|---|
|B-Tree|Igualdade e comparações de ordem (caso geral, padrão)|
|Hash|Só igualdade — raro na prática moderna|
|GIN|Arrays, JSONB, full-text search|
|GiST|Dados geoespaciais, intervalos, busca por similaridade|

## 🔗 Notas relacionadas

- [[BD - Índices B-Tree]]
- [[PostgreSQL - JSONB na Prática]]
- [[PostgreSQL - Extensões]]
- [[Recipe - Busca Full-Text]]
- [[Banco de Dados]]