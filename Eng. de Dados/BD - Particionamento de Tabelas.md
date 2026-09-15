---

tags:

- banco-de-dados
- performance aliases: [Particionamento, Table Partitioning, Partition]

---

# BD - Particionamento de Tabelas

## 📌 Conceito principal

**Particionamento** divide uma tabela logicamente única em várias tabelas físicas menores ("partições"), com base em um critério — mas a aplicação continua enxergando (e consultando) como se fosse uma única tabela. Usado quando uma tabela cresce demais para operações eficientes mesmo com bons índices.

> [!info] Suporte oficial do PostgreSQL A documentação oficial descreve o particionamento declarativo (`PARTITION BY`) como suporte nativo do PostgreSQL desde a versão 10, permitindo dividir uma tabela grande em partes menores e mais gerenciáveis. Fonte: [postgresql.org/docs — Particionamento](https://www.postgresql.org/docs/current/ddl-partitioning.html)

## 📊 Particionamento por Range (intervalo)

O mais comum para dados temporais — cada partição guarda um intervalo de datas.

```sql
CREATE TABLE pedidos (
    id SERIAL,
    cliente_id INT,
    criado_em DATE NOT NULL
) PARTITION BY RANGE (criado_em);

CREATE TABLE pedidos_2025 PARTITION OF pedidos
    FOR VALUES FROM ('2025-01-01') TO ('2026-01-01');

CREATE TABLE pedidos_2026 PARTITION OF pedidos
    FOR VALUES FROM ('2026-01-01') TO ('2027-01-01');
```

Uma consulta filtrando por data recente só precisa varrer a partição correspondente, não a tabela inteira — isso é chamado de **partition pruning**.

```sql
-- O PostgreSQL identifica que só precisa olhar pedidos_2026
SELECT * FROM pedidos WHERE criado_em >= '2026-06-01';
```

## 📋 Particionamento por Lista

Divide com base em valores discretos específicos — útil quando a coluna tem categorias bem definidas.

```sql
CREATE TABLE clientes (
    id SERIAL,
    nome VARCHAR(100),
    regiao VARCHAR(20)
) PARTITION BY LIST (regiao);

CREATE TABLE clientes_sudeste PARTITION OF clientes
    FOR VALUES IN ('SP', 'RJ', 'MG', 'ES');

CREATE TABLE clientes_sul PARTITION OF clientes
    FOR VALUES IN ('PR', 'SC', 'RS');
```

## #️⃣ Particionamento por Hash

Distribui as linhas de forma uniforme entre um número fixo de partições, útil quando não há um critério natural de range/lista, mas se quer distribuir a carga.

```sql
CREATE TABLE eventos (
    id SERIAL,
    payload JSONB
) PARTITION BY HASH (id);

CREATE TABLE eventos_p0 PARTITION OF eventos FOR VALUES WITH (MODULUS 4, REMAINDER 0);
CREATE TABLE eventos_p1 PARTITION OF eventos FOR VALUES WITH (MODULUS 4, REMAINDER 1);
CREATE TABLE eventos_p2 PARTITION OF eventos FOR VALUES WITH (MODULUS 4, REMAINDER 2);
CREATE TABLE eventos_p3 PARTITION OF eventos FOR VALUES WITH (MODULUS 4, REMAINDER 3);
```

## ⚖️ Quando vale a pena particionar

> [!tip] Sinal de que particionar pode ajudar Tabelas na casa de dezenas de milhões de linhas ou mais, onde a maior parte das consultas filtra por um critério previsível (data recente, região) — e onde manutenção (`VACUUM`, backup, exclusão de dados antigos) da tabela inteira já está lenta.

> [!warning] Não particione prematuramente Particionar adiciona complexidade operacional real. Para a maioria dos sistemas, um bom índice B-Tree (ver [[BD - Índices B-Tree]]) resolve o problema de performance muito antes de o particionamento ser necessário. Confirme com [[BD - EXPLAIN e EXPLAIN ANALYZE]] que o problema realmente é volume de dados, não falta de índice.

## 🔗 Notas relacionadas

- [[BD - Índices B-Tree]]
- [[BD - EXPLAIN e EXPLAIN ANALYZE]]
- [[BD - Otimização de Consultas]]
- [[Banco de Dados]]