---

tags:

- banco-de-dados
- fundamentos aliases: [SQL vs NoSQL, Relacional vs Não-Relacional]

---

# BD - Relacional vs NoSQL

## 📌 Conceito principal

Não existe "melhor" entre relacional e NoSQL — existe o mais adequado para o problema. A decisão certa depende de estrutura dos dados, necessidade de consistência forte, e padrão de acesso (leitura vs. escrita, consultas complexas vs. simples).

## ⚖️ Comparação direta

|Critério|Relacional (SQL)|NoSQL|
|---|---|---|
|Schema|Rígido, definido antecipadamente|Flexível, pode variar por registro|
|Consistência|Forte (ACID) por padrão|Geralmente eventual (dependendo do produto)|
|Relacionamentos|Nativo via JOINs e chaves estrangeiras|Geralmente desnormalizado/embutido|
|Escalabilidade|Vertical, historicamente|Horizontal (sharding nativo na maioria)|
|Linguagem de consulta|SQL padronizado|Varia por produto (query própria)|
|Exemplos|PostgreSQL, MySQL, SQL Server|MongoDB, Redis, Cassandra, Neo4j|

## 🧭 Quando usar cada abordagem

> [!tip] Use relacional quando:
> 
> - Os dados têm relacionamentos claros e consultáveis (pedidos ↔ clientes ↔ produtos)
> - Integridade forte é crítica (sistema financeiro, estoque, cadastros)
> - Você precisa de consultas ad-hoc complexas (JOINs, agregações)

> [!tip] Considere NoSQL quando:
> 
> - O schema muda com frequência ou varia muito entre registros
> - O padrão de acesso é simples (buscar por chave) e precisa de altíssima performance/escala horizontal
> - Os dados já são naturalmente hierárquicos/aninhados (perfil de usuário com preferências variáveis, catálogo de produtos com atributos diferentes por categoria)

> [!warning] Erro comum Escolher NoSQL só porque "escala mais" sem ter um problema real de escala, e depois recriar JOINs manualmente na aplicação — isso costuma ser pior do que ter ficado no relacional desde o início.

## 🔀 Abordagem híbrida (a mais comum na prática)

Muitos sistemas reais usam os dois ao mesmo tempo:

- **PostgreSQL** como fonte de verdade transacional
- **Redis** como cache de leituras frequentes
- **MongoDB** (ou o próprio JSONB do Postgres — ver [[PostgreSQL - JSONB na Prática]]) para dados variáveis dentro de um sistema majoritariamente relacional

## 💻 Exemplo prático — mesmo dado, duas abordagens

```sql
-- Abordagem relacional: pedido e itens em tabelas separadas
CREATE TABLE pedidos (id SERIAL PRIMARY KEY, cliente_id INT, criado_em TIMESTAMP);
CREATE TABLE itens_pedido (id SERIAL PRIMARY KEY, pedido_id INT REFERENCES pedidos(id), produto VARCHAR(100), quantidade INT);
```

```json
// Abordagem documento (NoSQL): pedido e itens no mesmo documento
{
  "pedido_id": 1,
  "cliente_id": 42,
  "itens": [
    { "produto": "Teclado", "quantidade": 1 },
    { "produto": "Mouse", "quantidade": 2 }
  ]
}
```

## 🔗 Notas relacionadas

- [[BD - Modelos de Dados]]
- [[NoSQL - Teorema CAP]]
- [[PostgreSQL - JSONB na Prática]]
- [[Banco de Dados]]