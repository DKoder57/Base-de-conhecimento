---

tags:

- banco-de-dados
- normalizacao aliases: [Desnormalização, Denormalization]

---

# BD - Desnormalização Consciente

## 📌 Conceito principal

**Desnormalizar** é introduzir redundância de propósito — de forma controlada e documentada — para ganhar performance de leitura, abrindo mão de parte da pureza normalizada (2FN/3FN). Diferente da redundância acidental que a normalização evita, essa é uma **decisão de arquitetura**, tomada depois de entender o custo.

> [!warning] Desnormalizar não é "esquecer" a normalização A ordem correta é: modelar normalizado (até 3FN) primeiro, medir performance real, e só então desnormalizar pontos específicos com um motivo claro e documentado — nunca pular a normalização "para ser mais rápido" desde o início.

## 🎯 Quando desnormalizar costuma valer a pena

- **Leitura muito mais frequente que escrita**: dashboards e relatórios que rodam a cada segundo, mas os dados de origem mudam raramente.
- **JOINs caros e repetitivos**: consultas que sempre juntam as mesmas 4-5 tabelas para exibir um relatório.
- **Preço/dado histórico**: registrar o valor **no momento da transação**, mesmo que ele já exista "normalizado" em outra tabela (ver nota em [[BD - Segunda Forma Normal (2FN)]] sobre `preco_unitario_na_compra`).
- **Relatórios analíticos (OLAP)**: modelagem dimensional (Star Schema) é deliberadamente desnormalizada — é o padrão em Data Warehouses.

## 🛠️ Técnicas comuns de desnormalização

### Coluna calculada/duplicada

```sql
-- Em vez de sempre calcular via JOIN + SUM:
ALTER TABLE pedidos ADD COLUMN total_itens INT;
-- Atualizado via trigger ou na própria aplicação sempre que um item muda
```

### Tabela agregada/resumo

```sql
CREATE TABLE resumo_vendas_diarias (
    data DATE PRIMARY KEY,
    total_pedidos INT,
    receita_total NUMERIC(12,2)
);
-- Populada periodicamente, evita recalcular agregações pesadas a cada consulta
```

### Views materializadas

A forma mais "segura" de desnormalizar — o SGBD gerencia a cópia dos dados por você (ver [[SQL - Views e Views Materializadas]]).

```sql
CREATE MATERIALIZED VIEW vw_resumo_vendas AS
SELECT categoria_id, COUNT(*) AS total, SUM(preco) AS receita
FROM produtos
GROUP BY categoria_id;

REFRESH MATERIALIZED VIEW vw_resumo_vendas;
```

## ⚖️ Trade-off que você está assumindo

|Ganho|Custo|
|---|---|
|Leitura mais rápida (menos JOINs)|Escrita mais complexa (precisa manter os dois lugares sincronizados)|
|Menos carga no banco em relatórios pesados|Risco de inconsistência se a sincronização falhar|
|Consultas mais simples de escrever|Mais lógica de aplicação/trigger para manter consistência|

> [!tip] Regra prática Nunca desnormalize "por precaução". Desnormalize quando um `EXPLAIN ANALYZE` (ver [[BD - EXPLAIN e EXPLAIN ANALYZE]]) mostrar que uma consulta normalizada está genuinamente lenta em produção, e documente o porquê da redundância na própria migration/nota da tabela.

## 🔗 Notas relacionadas

- [[BD - Terceira Forma Normal (3FN)]]
- [[SQL - Views e Views Materializadas]]
- [[BD - EXPLAIN e EXPLAIN ANALYZE]]
- [[Banco de Dados]]