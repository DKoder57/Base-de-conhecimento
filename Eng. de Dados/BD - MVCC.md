---

tags:

- banco-de-dados
- transacoes
- postgresql aliases: [MVCC, Multiversion Concurrency Control]

---

# BD - MVCC

## 📌 Conceito principal

**MVCC (Multiversion Concurrency Control)** é a técnica que o PostgreSQL (e vários outros SGBDs modernos) usa para permitir que leitores e escritores trabalhem ao mesmo tempo **sem se bloquearem mutuamente** — cada transação enxerga uma "fotografia" consistente dos dados, mesmo que outras transações estejam alterando as mesmas linhas simultaneamente.

> [!info] Como a documentação oficial descreve A documentação do PostgreSQL explica que o modelo de controle de concorrência do banco evita bloquear leitores contra escritores, mantendo cada transação vendo uma "snapshot" consistente dos dados — cada consulta enxerga os dados como estavam em um determinado instante, não afetados por atualizações concorrentes não confirmadas. Fonte: [postgresql.org/docs — MVCC](https://www.postgresql.org/docs/current/mvcc-intro.html)

## ⚙️ Como funciona, na prática

Em vez de sobrescrever uma linha ao atualizá-la, o PostgreSQL cria uma **nova versão** da linha, mantendo a versão antiga visível para transações que já haviam começado a lê-la:

1. Transação A começa e lê a linha X (versão 1).
2. Transação B começa, atualiza a linha X (cria a versão 2) e confirma (`COMMIT`).
3. Transação A, que ainda está em andamento, continua enxergando a versão 1 (a que existia quando ela começou) — sem qualquer lock ter sido necessário para isso.
4. Depois que A e B terminam, o processo de **VACUUM** do PostgreSQL remove a versão 1, que não é mais necessária.

> [!note] Por isso o PostgreSQL precisa de VACUUM Como cada `UPDATE`/`DELETE` gera uma nova versão de linha em vez de sobrescrever, versões antigas ("tuplas mortas") se acumulam com o tempo. O processo `VACUUM` (manual ou automático via `autovacuum`) limpa essas versões antigas — negligenciar isso é uma das causas mais comuns de degradação de performance em bancos PostgreSQL em produção.

## 🆚 MVCC vs. locks tradicionais

|Abordagem|Leitores bloqueiam escritores?|Escritores bloqueiam leitores?|
|---|:-:|:-:|
|Locking tradicional (sem MVCC)|Sim|Sim|
|MVCC (PostgreSQL)|Não|Não (leitores nunca esperam por escritores)|

Isso não elimina a necessidade de locks completamente — dois `UPDATE`s tentando alterar a **mesma linha** ao mesmo tempo ainda precisam de coordenação (ver [[BD - Locks e Deadlocks]]), mas leituras concorrentes com escritas se tornam muito mais fluidas.

## 💻 Exemplo prático — dois clientes psql simultâneos

```sql
-- Sessão 1:
BEGIN;
SELECT saldo FROM contas WHERE id = 1; -- retorna 100

-- Sessão 2 (enquanto a Sessão 1 ainda está aberta):
BEGIN;
UPDATE contas SET saldo = 200 WHERE id = 1;
COMMIT;

-- De volta à Sessão 1 (mesma transação, mesmo isolamento padrão Read Committed):
SELECT saldo FROM contas WHERE id = 1; -- pode retornar 200, pois cada SELECT em Read Committed pega um novo snapshot
COMMIT;
```

> [!tip] Conexão com Níveis de Isolamento O comportamento exato de "quando" uma transação vê as mudanças de outra depende do nível de isolamento configurado — em `Repeatable Read`, a Sessão 1 do exemplo acima continuaria vendo 100 mesmo depois do commit da Sessão 2, pois o snapshot é fixado no início da transação, não a cada consulta. Ver [[BD - Níveis de Isolamento]].

## 🔗 Notas relacionadas

- [[BD - ACID]]
- [[BD - Níveis de Isolamento]]
- [[BD - Locks e Deadlocks]]
- [[Banco de Dados]]