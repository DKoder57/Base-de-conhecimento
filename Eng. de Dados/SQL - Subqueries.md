---

tags:

- banco-de-dados
- sql aliases: [Subquery, Subconsulta, Nested Query]

---

# SQL - Subqueries

## 📌 Conceito principal

Uma **subquery** (subconsulta) é um `SELECT` dentro de outro `SELECT`, `INSERT`, `UPDATE` ou `DELETE`. Permite resolver perguntas que dependem de um resultado intermediário antes da consulta principal.

## 🔹 Subquery não correlacionada

Executa de forma independente — o SGBD roda a subquery uma vez, e o resultado é usado na consulta externa.

```sql
SELECT nome FROM produtos
WHERE preco > (SELECT AVG(preco) FROM produtos);
-- "Produtos com preço acima da média geral"
```

```sql
SELECT nome FROM clientes
WHERE id IN (SELECT cliente_id FROM pedidos WHERE status = 'concluido');
-- "Clientes que têm pelo menos um pedido concluído"
```

## 🔸 Subquery correlacionada

Faz referência a uma coluna da consulta externa — por isso é executada (conceitualmente) uma vez **para cada linha** da consulta externa.

```sql
SELECT p.nome, p.preco
FROM produtos p
WHERE p.preco > (
    SELECT AVG(p2.preco)
    FROM produtos p2
    WHERE p2.categoria_id = p.categoria_id
);
-- "Produtos com preço acima da média DA SUA PRÓPRIA categoria"
```

> [!warning] Performance de subqueries correlacionadas Por rodar (logicamente) uma vez por linha externa, subqueries correlacionadas podem ficar lentas em tabelas grandes. Muitas vezes o mesmo resultado pode ser obtido com [[SQL - Window Functions]] (`AVG() OVER (PARTITION BY ...)`), que costuma ser mais eficiente no plano de execução.

## 🔍 EXISTS e NOT EXISTS

```sql
SELECT nome FROM clientes c
WHERE EXISTS (
    SELECT 1 FROM pedidos p WHERE p.cliente_id = c.id
);
-- "Clientes que têm pelo menos um pedido" (equivalente ao IN, mas geralmente mais eficiente)

SELECT nome FROM clientes c
WHERE NOT EXISTS (
    SELECT 1 FROM pedidos p WHERE p.cliente_id = c.id
);
-- "Clientes que NUNCA fizeram pedido"
```

> [!tip] EXISTS/NOT EXISTS vs. IN/NOT IN `EXISTS` para no primeiro registro encontrado (não precisa contar todos), e principalmente: `NOT EXISTS` não sofre da armadilha de `NULL` que `NOT IN` tem (ver [[SQL - Operadores e Filtros]]). Para checagem de existência, `EXISTS`/`NOT EXISTS` costuma ser a escolha mais segura e eficiente.

## 📦 Subquery no FROM (tabela derivada)

```sql
SELECT categoria_id, total
FROM (
    SELECT categoria_id, COUNT(*) AS total
    FROM produtos
    GROUP BY categoria_id
) AS resumo
WHERE total > 5;
```

## 🔗 Notas relacionadas

- [[SQL - JOINs]]
- [[SQL - CTEs (Common Table Expressions)]]
- [[SQL - Window Functions]]
- [[Banco de Dados]]