---

tags:

- banco-de-dados
- transacoes aliases: [Isolation Levels, Read Committed, Serializable, Repeatable Read]

---

# BD - Níveis de Isolamento

## 📌 Conceito principal

O **isolamento** (o "I" de [[BD - ACID]]) não é binário — é ajustável em **níveis**, definindo o quanto uma transação pode "ver" de outras transações rodando ao mesmo tempo. Níveis mais rígidos dão mais segurança, mas custam mais performance/concorrência.

## 🐛 Os três problemas que os níveis de isolamento evitam

|Problema|Descrição|
|---|---|
|**Dirty Read** (leitura suja)|Ler um dado que outra transação alterou, mas ainda não confirmou (`COMMIT`)|
|**Non-Repeatable Read** (leitura não repetível)|Ler o mesmo registro duas vezes na mesma transação e obter valores diferentes, porque outra transação alterou e confirmou no meio tempo|
|**Phantom Read** (leitura fantasma)|Rodar a mesma consulta com filtro duas vezes e obter um **conjunto diferente de linhas**, porque outra transação inseriu/removeu linhas que casam com o filtro|

## 🔢 Os quatro níveis (padrão SQL)

### 1. Read Uncommitted

Permite dirty read. Praticamente não implementado de forma real no PostgreSQL (que trata como Read Committed internamente) — existe mais por compatibilidade com o padrão SQL.

### 2. Read Committed (padrão do PostgreSQL e do MySQL/InnoDB em algumas configurações)

Evita dirty read: uma transação só enxerga dados já confirmados por outras. Ainda pode sofrer non-repeatable read e phantom read.

```sql
BEGIN ISOLATION LEVEL READ COMMITTED;
SELECT saldo FROM contas WHERE id = 1; -- pode retornar valores diferentes se repetido
```

### 3. Repeatable Read (padrão do MySQL/InnoDB)

Garante que, dentro da mesma transação, ler o mesmo registro sempre retorna o mesmo valor. No PostgreSQL, esse nível também evita phantom read na prática (graças ao [[BD - MVCC]]).

```sql
BEGIN ISOLATION LEVEL REPEATABLE READ;
```

### 4. Serializable

O nível mais rígido: garante que o resultado de transações concorrentes seja **equivalente a rodá-las uma de cada vez, em alguma ordem** — elimina todos os três problemas, mas com maior custo de performance e maior chance de a transação precisar ser reiniciada por conflito.

```sql
BEGIN ISOLATION LEVEL SERIALIZABLE;
```

## ⚖️ Comparativo

|Nível|Dirty Read|Non-Repeatable Read|Phantom Read|
|---|:-:|:-:|:-:|
|Read Uncommitted|Possível|Possível|Possível|
|Read Committed|❌ Evitado|Possível|Possível|
|Repeatable Read|❌ Evitado|❌ Evitado|Possível (padrão SQL) / evitado na prática no Postgres|
|Serializable|❌ Evitado|❌ Evitado|❌ Evitado|

> [!tip] Qual usar na prática `Read Committed` (o padrão do PostgreSQL) é suficiente para a esmagadora maioria das aplicações. Reserve `Serializable` para operações realmente críticas onde qualquer inconsistência é inaceitável (ex.: reservas de assento, controle de estoque com alta concorrência) — e esteja preparado para tratar erros de serialização, que exigem repetir a transação.

## 🔗 Notas relacionadas

- [[BD - ACID]]
- [[BD - Locks e Deadlocks]]
- [[BD - MVCC]]
- [[Banco de Dados]]