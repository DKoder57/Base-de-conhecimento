---

tags:

- banco-de-dados
- sql aliases: [CTE, WITH, Common Table Expression, CTE Recursiva]

---

# SQL - CTEs (Common Table Expressions)

## 📌 Conceito principal

Uma **CTE (Common Table Expression)**, criada com `WITH`, define uma consulta nomeada e temporária que existe apenas durante a execução da query principal. Funciona como uma [[SQL - Subqueries|subquery]] mais legível — dá nome a um resultado intermediário e permite reutilizá-lo.

## 📝 CTE básica

```sql
WITH vendas_por_categoria AS (
    SELECT categoria_id, SUM(preco * quantidade) AS total_vendido
    FROM itens_pedido ip
    JOIN produtos p ON p.id = ip.produto_id
    GROUP BY categoria_id
)
SELECT c.nome, v.total_vendido
FROM vendas_por_categoria v
JOIN categorias c ON c.id = v.categoria_id
ORDER BY v.total_vendido DESC;
```

> [!tip] CTE vs. Subquery no FROM Fazem exatamente a mesma coisa em termos de resultado — a diferença é legibilidade. CTEs permitem nomear e até encadear várias etapas (`WITH a AS (...), b AS (...)`), deixando consultas complexas muito mais fáceis de ler que subqueries aninhadas.

## 🔗 Múltiplas CTEs encadeadas

```sql
WITH pedidos_concluidos AS (
    SELECT * FROM pedidos WHERE status = 'concluido'
),
resumo_cliente AS (
    SELECT cliente_id, COUNT(*) AS total_pedidos, SUM(valor_total) AS receita
    FROM pedidos_concluidos
    GROUP BY cliente_id
)
SELECT c.nome, r.total_pedidos, r.receita
FROM resumo_cliente r
JOIN clientes c ON c.id = r.cliente_id
WHERE r.total_pedidos >= 3;
```

## 🔁 CTE recursiva

Usada para percorrer estruturas hierárquicas (árvores de categorias, organogramas, listas de materiais) que uma consulta comum não conseguiria navegar sem saber a profundidade de antemão.

```sql
WITH RECURSIVE subordinados AS (
    -- Caso base: o funcionário inicial
    SELECT id, nome, gerente_id
    FROM funcionarios
    WHERE id = 1

    UNION ALL

    -- Passo recursivo: busca quem tem como gerente alguém já encontrado
    SELECT f.id, f.nome, f.gerente_id
    FROM funcionarios f
    JOIN subordinados s ON f.gerente_id = s.id
)
SELECT * FROM subordinados;
-- "Todos os subordinados diretos e indiretos do funcionário 1"
```

> [!note] Anatomia de uma CTE recursiva Toda CTE recursiva tem duas partes unidas por `UNION ALL`: o **caso base** (ponto de partida) e o **passo recursivo** (que referencia a própria CTE). O SGBD repete o passo recursivo até que ele não retorne mais linhas novas.

## 🔗 Notas relacionadas

- [[SQL - Subqueries]]
- [[SQL - Window Functions]]
- [[SQL - Views e Views Materializadas]]
- [[Banco de Dados]]