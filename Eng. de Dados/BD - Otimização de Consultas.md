---

tags:

- banco-de-dados
- performance aliases: [Otimização de Query, Query Tuning]

---

# BD - Otimização de Consultas

## 📌 Conceito principal

Otimizar uma consulta é reescrevê-la (ou apoiá-la com índices/estrutura) para que o SGBD consiga o mesmo resultado gastando menos tempo e recursos. A ferramenta de diagnóstico é sempre o [[BD - EXPLAIN e EXPLAIN ANALYZE]] — otimizar "no escuro", sem medir, costuma ser perda de tempo.

## ❌ Evite SELECT *

```sql
-- Ruim: traz todas as colunas, mesmo as que não serão usadas
SELECT * FROM produtos WHERE categoria_id = 3;

-- Melhor: traz só o necessário, reduz tráfego de rede e uso de memória
SELECT id, nome, preco FROM produtos WHERE categoria_id = 3;
```

## 🔁 Problema N+1

O erro de performance mais comum em aplicações que usam ORM (ver [[BD - O que é um ORM]]): buscar uma lista, e depois fazer **uma consulta separada para cada item** da lista.

```python
# N+1: 1 query para pedidos + N queries (uma por pedido) para buscar o cliente
pedidos = Pedido.objects.all()
for pedido in pedidos:
    print(pedido.cliente.nome)  # dispara uma query nova a cada iteração
```

```python
# Corrigido: 1 única query com JOIN (select_related, no caso do Django ORM)
pedidos = Pedido.objects.select_related('cliente').all()
for pedido in pedidos:
    print(pedido.cliente.nome)  # já veio junto, sem query extra
```

```sql
-- O equivalente em SQL puro seria simplesmente:
SELECT p.*, c.nome AS cliente_nome
FROM pedidos p
JOIN clientes c ON c.id = p.cliente_id;
```

## 📉 Reescrevendo subqueries lentas

```sql
-- Pode ser lento: subquery correlacionada roda "para cada linha"
SELECT nome FROM clientes c
WHERE (SELECT COUNT(*) FROM pedidos p WHERE p.cliente_id = c.id) > 5;

-- Geralmente mais eficiente: JOIN + GROUP BY + HAVING
SELECT c.nome
FROM clientes c
JOIN pedidos p ON p.cliente_id = c.id
GROUP BY c.nome
HAVING COUNT(*) > 5;
```

## 🎯 Filtre o quanto antes possível

```sql
-- Menos eficiente: filtra depois de juntar tudo
SELECT c.nome, p.id
FROM clientes c
JOIN pedidos p ON p.cliente_id = c.id
WHERE p.criado_em > '2026-01-01' AND c.cidade = 'Itabira';

-- O otimizador do PostgreSQL geralmente já reordena isso sozinho,
-- mas em consultas muito complexas (várias CTEs/subqueries), filtrar
-- o quanto antes na própria CTE evita processar dados desnecessários:
WITH pedidos_recentes AS (
    SELECT * FROM pedidos WHERE criado_em > '2026-01-01'
)
SELECT c.nome, pr.id
FROM clientes c
JOIN pedidos_recentes pr ON pr.cliente_id = c.id
WHERE c.cidade = 'Itabira';
```

## 🧭 Checklist rápido de otimização

1. Rode `EXPLAIN ANALYZE` antes de qualquer alteração — meça primeiro.
2. Existe `Seq Scan` em tabela grande onde deveria haver índice?
3. A consulta traz colunas/linhas que não são realmente necessárias?
4. Existe N+1 escondido em algum loop da aplicação?
5. As estatísticas da tabela estão atualizadas (`ANALYZE tabela;`)?
6. Depois de otimizar, meça de novo — confirme que realmente melhorou.

## 🔗 Notas relacionadas

- [[BD - EXPLAIN e EXPLAIN ANALYZE]]
- [[BD - Índices B-Tree]]
- [[BD - O que é um ORM]]
- [[Banco de Dados]]