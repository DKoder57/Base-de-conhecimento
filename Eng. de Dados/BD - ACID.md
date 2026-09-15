---

tags:

- banco-de-dados
- transacoes aliases: [ACID, Atomicidade Consistência Isolamento Durabilidade]

---

# BD - ACID

## 📌 Conceito principal

**ACID** é o conjunto de quatro garantias que um SGBD transacional promete sobre cada transação — é o que diferencia um banco de dados sério de simplesmente escrever bytes em um arquivo.

## 🅰️ Atomicidade

Uma transação é **tudo ou nada** — ou todas as suas operações são aplicadas, ou nenhuma é.

```sql
BEGIN;
UPDATE contas SET saldo = saldo - 100 WHERE id = 1; -- débito
UPDATE contas SET saldo = saldo + 100 WHERE id = 2; -- crédito
COMMIT;
-- Se qualquer uma das duas linhas falhar, NENHUMA das duas é aplicada
```

Sem atomicidade, uma falha no meio dessa transferência poderia debitar de uma conta sem creditar na outra — dinheiro simplesmente desapareceria.

## 🅲 Consistência

A transação leva o banco de um **estado válido para outro estado válido**, respeitando todas as constraints, checks e regras definidas (ver [[BD - Chaves]] e [[SQL - DDL]]).

```sql
-- Se existe CHECK (saldo >= 0), uma transação que deixaria o saldo negativo
-- é rejeitada inteira, preservando a consistência do banco
```

## 🅸 Isolamento

Transações concorrentes não devem "enxergar" o estado intermediário umas das outras — cada uma se comporta como se fosse a única rodando no banco naquele momento (o nível exato disso é ajustável, ver [[BD - Níveis de Isolamento]]).

## 🅳 Durabilidade

Uma vez que uma transação recebe `COMMIT`, seus efeitos **sobrevivem** a qualquer falha subsequente (queda de energia, crash do processo) — geralmente garantido através de logs de escrita antecipada (WAL — Write-Ahead Logging).

> [!note] Referência técnica A documentação oficial do PostgreSQL descreve o WAL (Write-Ahead Log) como a técnica padrão da indústria para garantir integridade de dados: mudanças são gravadas em log antes de serem aplicadas, garantindo que a durabilidade se mantenha mesmo após uma queda do sistema. Fonte: [postgresql.org/docs — WAL](https://www.postgresql.org/docs/current/wal-intro.html)

## 💻 Exemplo prático — as 4 garantias juntas

```sql
BEGIN;

UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;

COMMIT;
-- Atomicidade: as duas linhas foram alteradas juntas, ou nenhuma foi
-- Consistência: se houver CHECK(saldo >= 0), a transferência não deixa saldo negativo
-- Isolamento: outra transação lendo a conta 1 não vê um estado "no meio" da transferência
-- Durabilidade: após o COMMIT, mesmo uma queda de energia não desfaz a transferência
```

## 🔗 Notas relacionadas

- [[BD - Transações (BEGIN, COMMIT, ROLLBACK)]]
- [[BD - Níveis de Isolamento]]
- [[BD - Locks e Deadlocks]]
- [[Banco de Dados]]