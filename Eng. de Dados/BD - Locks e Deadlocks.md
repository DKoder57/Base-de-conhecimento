---

tags:

- banco-de-dados
- transacoes aliases: [Lock, Deadlock, Locks Otimistas, Locks Pessimistas]

---

# BD - Locks e Deadlocks

## 📌 Conceito principal

Um **lock** (trava) impede que duas transações modifiquem o mesmo dado de forma conflitante ao mesmo tempo. Um **deadlock** acontece quando duas (ou mais) transações ficam esperando locks uma da outra indefinidamente, sem nenhuma conseguir prosseguir.

## 🔒 Lock pessimista

Assume que conflitos **vão** acontecer, então trava o dado assim que ele é lido para alteração, bloqueando outras transações até o fim da atual.

```sql
BEGIN;
SELECT * FROM estoque WHERE produto_id = 10 FOR UPDATE;
-- Essa linha fica travada; outra transação que tente o mesmo SELECT FOR UPDATE
-- espera até esta transação terminar (COMMIT ou ROLLBACK)
UPDATE estoque SET quantidade = quantidade - 1 WHERE produto_id = 10;
COMMIT;
```

> [!tip] Quando usar FOR UPDATE Ideal para operações onde o conflito é **esperado e frequente** — como decrementar estoque em um sistema de alta concorrência de vendas. Garante que ninguém mais leia (para alterar) aquela linha até você terminar.

## 🔓 Lock otimista

Assume que conflitos são **raros**. Em vez de travar o dado, a transação lê um valor (geralmente uma coluna de versão), faz seu trabalho, e só na hora de salvar verifica se o valor ainda é o mesmo — se outra transação alterou no meio tempo, a operação é rejeitada e precisa ser repetida.

```sql
-- Tabela com coluna de controle de versão
ALTER TABLE produtos ADD COLUMN versao INT DEFAULT 1;

-- Leitura, sem lock
SELECT preco, versao FROM produtos WHERE id = 10; -- retorna preco=100, versao=3

-- Ao salvar, verifica se a versão ainda é a mesma
UPDATE produtos
SET preco = 90, versao = versao + 1
WHERE id = 10 AND versao = 3;
-- Se 0 linhas forem afetadas, outra transação alterou no meio tempo — trate esse caso na aplicação
```

> [!tip] Quando usar lock otimista Melhor para cenários onde conflitos são raros e o custo de manter um lock pessimista (bloqueando outras transações) seria maior que o custo ocasional de repetir uma operação — comum em aplicações web com baixa concorrência por registro.

## 💥 Deadlock — quando dois locks se travam mutuamente

```sql
-- Transação A:
BEGIN;
UPDATE contas SET saldo = saldo - 100 WHERE id = 1; -- trava a linha 1
-- ... espera para travar a linha 2

-- Transação B (rodando ao mesmo tempo):
BEGIN;
UPDATE contas SET saldo = saldo - 50 WHERE id = 2;  -- trava a linha 2
-- ... espera para travar a linha 1

-- A espera a linha 2 (travada por B), B espera a linha 1 (travada por A) — deadlock
```

O SGBD detecta esse ciclo e **cancela automaticamente uma das duas transações** (com um erro específico de deadlock), permitindo que a outra prossiga.

> [!warning] Como evitar deadlocks na prática A causa mais comum é acessar as mesmas tabelas **em ordens diferentes** em transações concorrentes. A prevenção mais simples e eficaz: sempre acessar/atualizar tabelas (e linhas) **na mesma ordem** em toda a aplicação — por exemplo, sempre pela ordem crescente de `id`.

## 🔗 Notas relacionadas

- [[BD - ACID]]
- [[BD - Níveis de Isolamento]]
- [[BD - MVCC]]
- [[Banco de Dados]]