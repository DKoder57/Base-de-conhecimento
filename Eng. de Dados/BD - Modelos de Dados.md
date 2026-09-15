---

tags:

- banco-de-dados
- fundamentos aliases: [Modelos de Banco de Dados]

---

# BD - Modelos de Dados

## 📌 Conceito principal

Um **modelo de dados** define como a informação é logicamente organizada dentro de um SGBD. A escolha do modelo influencia diretamente como você modela, consulta e escala o sistema.

## 🗂️ Principais modelos

### 1. Relacional

Dados organizados em **tabelas** (relações), com linhas (tuplas) e colunas (atributos), conectadas por chaves. É o modelo mais usado no mercado — PostgreSQL, MySQL, SQL Server, Oracle.

```sql
CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    cidade VARCHAR(50)
);
```

### 2. Hierárquico

Dados organizados como uma árvore — cada registro tem um único "pai". Muito usado historicamente (ex.: sistemas de arquivos, XML). Pouco usado hoje como SGBD de propósito geral, mas o conceito sobrevive em estruturas como árvores de categorias.

### 3. Em rede

Evolução do modelo hierárquico, permitindo que um registro tenha múltiplos "pais" — mais flexível, mas mais complexo de navegar. Praticamente extinto como produto comercial, mas historicamente relevante (CODASYL).

### 4. Orientado a documentos (NoSQL)

Dados armazenados como documentos semiestruturados (geralmente JSON/BSON), sem exigir um schema fixo. Exemplo: MongoDB.

```json
{
  "_id": "123",
  "nome": "João",
  "enderecos": [
    { "cidade": "Itabira", "tipo": "residencial" }
  ]
}
```

> [!note] Onde entram outros modelos NoSQL Chave-valor (Redis), colunar (Cassandra) e grafos (Neo4j) são variações do "não-relacional" com propósitos específicos — cobertos em detalhe no [[NoSQL - Documentos (MongoDB)|Nível 10 da matriz de Banco de Dados]].

## ⚖️ Comparativo rápido

|Modelo|Estrutura|Flexibilidade de schema|Uso típico hoje|
|---|---|---|---|
|Relacional|Tabelas com relações|Rígida (schema definido)|Sistemas transacionais, ERPs, e-commerce|
|Hierárquico|Árvore|Rígida|Legado, sistemas de arquivos|
|Em rede|Grafo com múltiplos pais|Rígida|Praticamente extinto|
|Documentos|Documentos aninhados|Flexível|Catálogos de produtos, CMS, dados variáveis|

> [!tip] Como escolher Comece assumindo relacional — é o padrão mais testado, com garantias fortes de integridade (ver [[BD - ACID]]). Migre partes específicas para NoSQL apenas quando um problema real de escala, flexibilidade de schema, ou performance justificar — nunca ao contrário.

## 🔗 Notas relacionadas

- [[BD - Relacional vs NoSQL]]
- [[BD - O que é um SGBD]]
- [[BD - Modelo Conceitual]]
- [[Banco de Dados]]