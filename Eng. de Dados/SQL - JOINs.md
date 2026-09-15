---

tags:

- banco-de-dados
- sql aliases: [JOIN, INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN]

---

# SQL - JOINs

## 📌 Conceito principal

**JOIN** combina linhas de duas (ou mais) tabelas com base em uma condição de relacionamento — geralmente uma chave estrangeira. É o mecanismo que torna possível reconstruir informações espalhadas por tabelas normalizadas (ver [[BD - Terceira Forma Normal (3FN)]]).

## 🔗 INNER JOIN — apenas o que casa nos dois lados

```sql
SELECT c.nome, p.id AS pedido_id
FROM clientes c
INNER JOIN pedidos p ON p.cliente_id = c.id;
-- Retorna apenas clientes que têm pelo menos um pedido
```

## ⬅️ LEFT JOIN — tudo da esquerda, casando quando possível

```sql
SELECT c.nome, p.id AS pedido_id
FROM clientes c
LEFT JOIN pedidos p ON p.cliente_id = c.id;
-- Retorna TODOS os clientes, mesmo os sem pedido (pedido_id vem NULL nesse caso)
```

> [!tip] Uso mais comum de LEFT JOIN "Quais clientes **nunca** fizeram pedido?" é uma pergunta clássica de LEFT JOIN:
> 
> ```sql
> SELECT c.nome FROM clientes c
> LEFT JOIN pedidos p ON p.cliente_id = c.id
> WHERE p.id IS NULL;
> ```

## ➡️ RIGHT JOIN — tudo da direita, casando quando possível

```sql
SELECT c.nome, p.id AS pedido_id
FROM clientes c
RIGHT JOIN pedidos p ON p.cliente_id = c.id;
-- Retorna todos os pedidos, mesmo que (por algum motivo) o cliente não exista mais
```

> [!note] RIGHT JOIN na prática É pouco usado — qualquer `RIGHT JOIN` pode ser reescrito como `LEFT JOIN` só invertendo a ordem das tabelas no `FROM`. A maioria dos times padroniza em usar sempre `LEFT JOIN` por consistência de leitura.

## ↔️ FULL OUTER JOIN — tudo dos dois lados

```sql
SELECT c.nome, p.id AS pedido_id
FROM clientes c
FULL OUTER JOIN pedidos p ON p.cliente_id = c.id;
-- Clientes sem pedido E pedidos "órfãos" (se existirem), tudo junto
```

> [!warning] MySQL não suporta FULL OUTER JOIN nativamente É preciso simular com `UNION` de um `LEFT JOIN` e um `RIGHT JOIN`. O PostgreSQL suporta `FULL OUTER JOIN` diretamente.

## ✖️ CROSS JOIN — produto cartesiano

```sql
SELECT c.nome, t.tamanho
FROM cores c
CROSS JOIN tamanhos t;
-- Toda combinação possível entre cores e tamanhos (útil para gerar variações de produto)
```

## 💻 Exemplo prático combinando múltiplos JOINs

```sql
SELECT cl.nome, pe.id AS pedido, pr.nome AS produto, ip.quantidade
FROM clientes cl
JOIN pedidos pe ON pe.cliente_id = cl.id
JOIN itens_pedido ip ON ip.pedido_id = pe.id
JOIN produtos pr ON pr.id = ip.produto_id
WHERE pe.status = 'concluido';
```

## 🔗 Notas relacionadas

- [[BD - Cardinalidades e Relacionamentos]]
- [[SQL - Subqueries]]
- [[SQL - Funções de Agregação]]
- [[Banco de Dados]]