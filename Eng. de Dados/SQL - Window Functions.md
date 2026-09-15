---

tags:

- banco-de-dados
- sql aliases: [Window Functions, Funções de Janela, OVER, PARTITION BY]

---

# SQL - Window Functions

## 📌 Conceito principal

**Window functions** (funções de janela) calculam um valor para cada linha **considerando um conjunto de linhas relacionadas** ("janela"), sem colapsar o resultado em uma única linha por grupo — diferente do [[SQL - Funções de Agregação|GROUP BY]], que reduz várias linhas a uma só.

> [!note] Diferença chave para GROUP BY `GROUP BY` retorna **uma linha por grupo**. Window functions retornam **uma linha por linha original**, com um valor calculado "ao lado" considerando o grupo — por isso é possível ver o detalhe e o agregado lado a lado na mesma consulta.

## 🪟 Sintaxe básica: OVER e PARTITION BY

```sql
SELECT nome, categoria_id, preco,
       AVG(preco) OVER (PARTITION BY categoria_id) AS media_categoria
FROM produtos;
-- Cada produto aparece com seu preço E a média da categoria dele, sem perder o detalhe
```

`PARTITION BY` divide as linhas em grupos (janelas) — como um `GROUP BY`, mas sem colapsar o resultado.

## 🔢 ROW_NUMBER — numerando linhas

```sql
SELECT nome, preco,
       ROW_NUMBER() OVER (ORDER BY preco DESC) AS posicao
FROM produtos;
-- Numera cada produto do mais caro (1) ao mais barato
```

## 🏆 RANK e DENSE_RANK — ranqueamento com empates

```sql
SELECT nome, categoria_id, preco,
       RANK() OVER (PARTITION BY categoria_id ORDER BY preco DESC) AS posicao_na_categoria
FROM produtos;
```

|Função|Comportamento com empate|
|---|---|
|`ROW_NUMBER()`|Sempre numera sequencialmente, sem empate (1, 2, 3, 4)|
|`RANK()`|Empates recebem o mesmo número, e pula o próximo (1, 2, 2, 4)|
|`DENSE_RANK()`|Empates recebem o mesmo número, sem pular (1, 2, 2, 3)|

## 💻 Exemplo prático — top N por grupo (caso de uso clássico)

```sql
WITH produtos_ranqueados AS (
    SELECT nome, categoria_id, preco,
           ROW_NUMBER() OVER (PARTITION BY categoria_id ORDER BY preco DESC) AS rn
    FROM produtos
)
SELECT nome, categoria_id, preco
FROM produtos_ranqueados
WHERE rn <= 3;
-- "Os 3 produtos mais caros DE CADA categoria"
```

> [!tip] Por que essa consulta não daria certo só com LIMIT `LIMIT 3` sozinho traria os 3 produtos mais caros **no geral**, não os 3 mais caros **de cada categoria**. Esse é exatamente o tipo de problema que window functions resolvem e um `GROUP BY` simples não consegue.

## 📈 Outras funções de janela úteis

```sql
-- Comparar com a linha anterior/seguinte
SELECT nome, preco,
       LAG(preco) OVER (ORDER BY id) AS preco_anterior,
       LEAD(preco) OVER (ORDER BY id) AS preco_seguinte
FROM produtos;

-- Soma acumulada
SELECT data, valor,
       SUM(valor) OVER (ORDER BY data) AS acumulado
FROM vendas;
```

## 🔗 Notas relacionadas

- [[SQL - Funções de Agregação]]
- [[SQL - CTEs (Common Table Expressions)]]
- [[SQL - Subqueries]]
- [[Banco de Dados]]