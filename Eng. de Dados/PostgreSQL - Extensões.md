---

tags:

- banco-de-dados
- postgresql aliases: [Extensões PostgreSQL, pgcrypto, pg_trgm, PostGIS, pgvector]

---

# PostgreSQL - Extensões

## 📌 Conceito principal

**Extensões** ampliam as funcionalidades nativas do PostgreSQL sem precisar de outro SGBD — desde criptografia até dados geoespaciais e busca vetorial para IA. É um dos maiores diferenciais competitivos do PostgreSQL frente a outros bancos relacionais.

> [!info] Fonte oficial A documentação do PostgreSQL mantém um catálogo (`pg_available_extensions`) e explica o mecanismo de `CREATE EXTENSION`, que empacota funcionalidades adicionais de forma gerenciada pelo próprio SGBD. Fonte: [postgresql.org/docs — Extensões](https://www.postgresql.org/docs/current/external-extensions.html)

## 🔧 Como habilitar uma extensão

```sql
CREATE EXTENSION IF NOT EXISTS nome_da_extensao;

-- Ver extensões disponíveis no servidor
SELECT * FROM pg_available_extensions;

-- Ver extensões já habilitadas no banco atual
SELECT * FROM pg_extension;
```

## 🔐 pgcrypto — criptografia

```sql
CREATE EXTENSION IF NOT EXISTS pgcrypto;

-- Gerar UUID (ver PostgreSQL - Tipos Avançados)
SELECT gen_random_uuid();

-- Hash de senha (nunca armazene senha em texto puro)
SELECT crypt('minha_senha', gen_salt('bf'));

-- Verificar senha no login
SELECT (senha_hash = crypt('senha_digitada', senha_hash)) AS senha_correta
FROM usuarios WHERE email = 'joao@email.com';
```

## 🔤 pg_trgm — busca por similaridade de texto

```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;

SELECT nome, similarity(nome, 'notbook') AS score
FROM produtos
WHERE nome % 'notbook'  -- encontra "notebook" mesmo com erro de digitação
ORDER BY score DESC;
```

Útil para busca tolerante a erros de digitação, complementando o full-text search tradicional (ver [[Recipe - Busca Full-Text]]).

## 🗺️ PostGIS — dados geoespaciais

```sql
CREATE EXTENSION IF NOT EXISTS postgis;

CREATE TABLE lojas (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    localizacao GEOGRAPHY(POINT)
);

-- Lojas num raio de 5km de um ponto
SELECT nome FROM lojas
WHERE ST_DWithin(localizacao, ST_MakePoint(-43.22, -19.62)::geography, 5000);
```

> [!note] PostGIS é o padrão de mercado para dados geoespaciais É usado tanto em sistemas de logística/delivery quanto em SIGs (Sistemas de Informação Geográfica) profissionais — extremamente maduro e bem documentado.

## 🧠 pgvector — busca vetorial (embeddings de IA)

```sql
CREATE EXTENSION IF NOT EXISTS vector;

CREATE TABLE documentos (
    id SERIAL PRIMARY KEY,
    conteudo TEXT,
    embedding VECTOR(1536) -- dimensão depende do modelo de embedding usado
);

-- Busca por similaridade (distância de cosseno)
SELECT conteudo FROM documentos
ORDER BY embedding <=> '[0.1, 0.2, ...]'
LIMIT 5;
```

> [!tip] Por que isso importa hoje `pgvector` permite usar o PostgreSQL como banco vetorial para aplicações de IA (busca semântica, RAG), evitando a necessidade de um banco vetorial dedicado separado para muitos casos de uso.

## 🔗 Notas relacionadas

- [[PostgreSQL - Tipos Avançados]]
- [[BD - Índices Hash, GIN e GiST]]
- [[Recipe - Busca Full-Text]]
- [[Banco de Dados]]