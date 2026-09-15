---

tags:

- banco-de-dados
- transacoes aliases: [BEGIN, COMMIT, ROLLBACK, Transação, SAVEPOINT]

---

# BD - Transações (BEGIN, COMMIT, ROLLBACK)

## 📌 Conceito principal

Uma **transação** é um bloco de uma ou mais operações SQL tratadas como uma única unidade — controlada explicitamente com `BEGIN` (início), `COMMIT` (confirma tudo) ou `ROLLBACK` (desfaz tudo). É o mecanismo prático que entrega a garantia de [[BD - ACID]].

## ▶️ BEGIN — iniciando uma transação

```sql
BEGIN;
-- todas as operações a partir daqui fazem parte da mesma transação
```

> [!note] Fora de uma transação explícita Por padrão, a maioria dos SGBDs roda cada comando isoladamente em **auto-commit** — cada `INSERT`/`UPDATE`/`DELETE` já é confirmado sozinho assim que executa. `BEGIN` desliga esse comportamento até o próximo `COMMIT` ou `ROLLBACK`.

## ✅ COMMIT — confirmando a transação

```sql
BEGIN;
UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;
COMMIT;
-- As duas alterações são persistidas de forma permanente e definitiva
```

## ↩️ ROLLBACK — desfazendo a transação

```sql
BEGIN;
UPDATE contas SET saldo = saldo - 100 WHERE id = 1;
UPDATE contas SET saldo = saldo + 100 WHERE id = 2;

-- Algo deu errado ou uma verificação falhou:
ROLLBACK;
-- Nenhuma das duas alterações é aplicada, como se a transação nunca tivesse existido
```

## 🎯 SAVEPOINT — pontos de retorno parciais

Permite desfazer só uma parte de uma transação longa, sem cancelar tudo.

```sql
BEGIN;

UPDATE produtos SET preco = preco * 1.1 WHERE categoria_id = 1;
SAVEPOINT antes_categoria_2;

UPDATE produtos SET preco = preco * 1.1 WHERE categoria_id = 2;
-- Percebe que esse segundo update estava errado:
ROLLBACK TO SAVEPOINT antes_categoria_2;

-- A alteração da categoria 1 continua válida; só a da categoria 2 foi desfeita
COMMIT;
```

## 💻 Exemplo prático — padrão seguro para alterações críticas

```sql
BEGIN;

UPDATE estoque SET quantidade = quantidade - 5 WHERE produto_id = 10;

-- Verificação de segurança antes de confirmar
SELECT quantidade FROM estoque WHERE produto_id = 10;
-- Se quantidade < 0, a lógica da aplicação decide fazer ROLLBACK

COMMIT; -- ou ROLLBACK; dependendo da checagem acima
```

> [!tip] Transações e conexões `BEGIN`, `COMMIT` e `ROLLBACK` só fazem sentido dentro da **mesma conexão** com o banco — não é possível iniciar uma transação em uma conexão e confirmá-la em outra. Isso é especialmente relevante ao usar pools de conexão (ver [[BD - Connection Pooling]]).

## 🔗 Notas relacionadas

- [[BD - ACID]]
- [[BD - Níveis de Isolamento]]
- [[BD - Locks e Deadlocks]]
- [[SQL - DML]]
- [[Banco de Dados]]