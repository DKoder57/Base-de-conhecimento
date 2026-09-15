---

tags:

- banco-de-dados
- performance aliases: [Índice B-Tree, B-Tree Index]

---

# BD - Índices B-Tree

## 📌 Conceito principal

Um **índice** é uma estrutura de dados auxiliar que permite ao SGBD localizar linhas sem precisar ler a tabela inteira (_sequential scan_). O **B-Tree** (árvore balanceada) é o tipo de índice padrão e mais usado — otimizado para igualdade e comparações de ordem (`=`, `<`, `>`, `BETWEEN`, `ORDER BY`).

> [!info] Padrão da indústria A documentação oficial do PostgreSQL descreve o B-Tree como o método de índice padrão, adequado para os casos de uso mais comuns de indexação, e é o tipo criado automaticamente quando nenhum outro é especificado. Fonte: [postgresql.org/docs — Índices B-Tree](https://www.postgresql.org/docs/current/indexes-types.html)

## 🧱 Como funciona (intuição)

Um B-Tree organiza os valores indexados de forma hierárquica e ordenada, permitindo que o SGBD "pule" diretamente para a região relevante dos dados em vez de varrer tudo — de forma parecida com procurar uma palavra em um dicionário físico usando as letras de guia, em vez de ler página por página.

## 🔑 Criando um índice

```sql
CREATE INDEX idx_clientes_email ON clientes(email);

-- Índice único (também garante ausência de duplicatas)
CREATE UNIQUE INDEX idx_clientes_email_unico ON clientes(email);

-- Índice composto (mais de uma coluna)
CREATE INDEX idx_pedidos_cliente_status ON pedidos(cliente_id, status);
```

> [!warning] Chave primária já cria índice automaticamente Ao definir `PRIMARY KEY`, o SGBD cria um índice único automaticamente sobre essa coluna — não é necessário (nem recomendado) criar outro índice manual sobre a mesma coluna.

## 🎯 Quando um índice B-Tree é usado

```sql
-- Usa o índice em idx_clientes_email:
SELECT * FROM clientes WHERE email = 'joao@email.com';

-- Índice composto (cliente_id, status) é usado eficientemente aqui,
-- pois a consulta usa a PRIMEIRA coluna do índice:
SELECT * FROM pedidos WHERE cliente_id = 42;
SELECT * FROM pedidos WHERE cliente_id = 42 AND status = 'concluido';

-- Mas NÃO é usado eficientemente aqui, pois pula a primeira coluna do índice composto:
SELECT * FROM pedidos WHERE status = 'concluido';
```

> [!tip] Ordem importa em índices compostos Um índice composto `(a, b)` funciona como um índice em `a` sozinho, ou em `(a, b)` juntos — mas não ajuda diretamente uma consulta que filtra só por `b`. Ao criar índices compostos, coloque primeiro a coluna mais seletiva ou mais usada isoladamente.

## ⚖️ Custo de ter um índice

Índices aceleram leitura, mas têm custo:

- Ocupam espaço em disco
- Toda escrita (`INSERT`/`UPDATE`/`DELETE`) precisa também atualizar os índices da tabela, tornando escritas mais lentas

> [!warning] Não crie índice em toda coluna "por garantia" Índices em excesso deixam `INSERT`/`UPDATE` mais lentos sem necessariamente ajudar consultas reais. Crie índices baseado em consultas que você sabe que são frequentes e lentas — idealmente confirmadas com [[BD - EXPLAIN e EXPLAIN ANALYZE]], não por suposição.

## 🔗 Notas relacionadas

- [[BD - Índices Hash, GIN e GiST]]
- [[BD - EXPLAIN e EXPLAIN ANALYZE]]
- [[BD - Otimização de Consultas]]
- [[Banco de Dados]]