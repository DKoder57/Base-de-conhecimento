---

tags:

- banco-de-dados
- sql aliases: [View, Views Materializadas, Materialized View]

---

# SQL - Views e Views Materializadas

## 📌 Conceito principal

Uma **view** é uma consulta salva com um nome — funciona como uma "tabela virtual" que não armazena dados próprios, apenas executa a query definida toda vez que é consultada. Uma **view materializada** vai além: guarda fisicamente o resultado, funcionando como um cache de consulta.

## 👁️ View comum

```sql
CREATE VIEW vw_clientes_ativos AS
SELECT id, nome, email
FROM clientes
WHERE ativo = true;

-- Consultar a view é igual a consultar uma tabela
SELECT * FROM vw_clientes_ativos WHERE nome LIKE 'João%';
```

> [!note] View não guarda dados Toda vez que `vw_clientes_ativos` é consultada, o SGBD executa a query original por trás — sempre reflete o estado atual das tabelas. Não há ganho de performance, só de **abstração** (esconder a complexidade de um JOIN grande atrás de um nome simples).

### Quando usar view comum

- Simplificar consultas repetidas e complexas (esconder JOINs grandes)
- Restringir acesso a colunas sensíveis (dar acesso só à view, não à tabela original)
- Manter compatibilidade quando a estrutura de tabelas muda, sem quebrar consultas antigas

## 🗄️ View materializada

```sql
CREATE MATERIALIZED VIEW vw_vendas_por_categoria AS
SELECT categoria_id, SUM(preco * quantidade) AS total_vendido
FROM itens_pedido ip
JOIN produtos p ON p.id = ip.produto_id
GROUP BY categoria_id;

-- Consulta é instantânea, pois lê dados já calculados
SELECT * FROM vw_vendas_por_categoria;
```

> [!warning] View materializada não se atualiza sozinha É preciso rodar `REFRESH` manualmente (ou via job agendado) para atualizar os dados:
> 
> ```sql
> REFRESH MATERIALIZED VIEW vw_vendas_por_categoria;
> -- Bloqueia leituras durante o refresh, por padrão
> 
> REFRESH MATERIALIZED VIEW CONCURRENTLY vw_vendas_por_categoria;
> -- Permite leituras durante o refresh, mas exige um índice único na view
> ```

## ⚖️ View vs. View Materializada

|Critério|View comum|View materializada|
|---|---|---|
|Armazena dados|Não|Sim|
|Sempre atualizada|Sim (automaticamente)|Não (precisa de `REFRESH`)|
|Performance de leitura|Igual à query original|Muito mais rápida|
|Caso de uso típico|Abstração e segurança|Relatórios pesados, dashboards|

> [!tip] Conexão com desnormalização Views materializadas são a forma mais segura de fazer [[BD - Desnormalização Consciente]] — o SGBD cuida de manter a cópia dos dados, sem você precisar escrever lógica manual de sincronização.

## 🔗 Notas relacionadas

- [[BD - Desnormalização Consciente]]
- [[SQL - CTEs (Common Table Expressions)]]
- [[Recipe - Paginação Eficiente]]
- [[Banco de Dados]]