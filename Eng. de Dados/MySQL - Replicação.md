---

tags:

- banco-de-dados
- mysql aliases: [Replicação MySQL, Master-Replica, Binlog]

---

# MySQL - Replicação

## 📌 Conceito principal

**Replicação** copia os dados de um servidor MySQL (origem/master) para um ou mais servidores secundários (réplicas), mantendo-os sincronizados — usada para escalar leituras, ter backup "quente" e melhorar disponibilidade.

> [!info] Fonte oficial A documentação oficial do MySQL descreve a replicação baseada em binlog (binary log), onde o servidor origem registra todas as alterações de dados em um log binário, que as réplicas leem e reaplicam para se manterem sincronizadas. Fonte: [dev.mysql.com/doc/refman — Replication](https://dev.mysql.com/doc/refman/en/replication.html)

## 🔁 Como funciona (visão geral)

1. O servidor **origem** registra toda alteração de dados no **binlog** (binary log).
2. Cada servidor **réplica** se conecta à origem e recebe uma cópia contínua desse log.
3. A réplica reaplica as mesmas alterações localmente, mantendo seus dados sincronizados (com uma pequena defasagem, chamada _replication lag_).

```
┌──────────┐   binlog   ┌───────────┐
│  Origem  │ ─────────> │  Réplica  │
│ (escrita)│            │ (leitura) │
└──────────┘            └───────────┘
```

## 🎯 Casos de uso

### Escalonamento de leitura

A aplicação direciona escritas para a origem e leituras (relatórios, consultas pesadas) para as réplicas, distribuindo a carga.

```
Aplicação --escreve--> Origem
Aplicação --lê--------> Réplica 1
Aplicação --lê--------> Réplica 2
```

### Alta disponibilidade

Se a origem falhar, uma réplica pode ser promovida a novo servidor principal (failover), reduzindo o tempo de indisponibilidade.

### Backup sem impactar produção

Rodar `mysqldump` ou outra rotina pesada de backup contra uma réplica, sem consumir recursos do servidor que atende a aplicação em produção.

## ⚠️ Replication lag (atraso de replicação)

> [!warning] Réplicas não são instantâneas Existe sempre um pequeno atraso entre uma escrita na origem e ela aparecer na réplica. Se a aplicação escreve um dado e imediatamente tenta lê-lo de uma réplica, pode não encontrá-lo ainda — um padrão de bug clássico em arquiteturas com réplicas de leitura. A solução geralmente é ler dados recém-escritos diretamente da origem por um curto período, ou aceitar consistência eventual para esse caso específico.

## 💻 Verificando o status de uma réplica

```sql
-- Rodado na réplica
SHOW REPLICA STATUS\G

-- Verificar se há atraso significativo (Seconds_Behind_Source)
```

> [!tip] Equivalente no PostgreSQL O PostgreSQL tem seu próprio mecanismo de replicação baseado em WAL (Write-Ahead Log) — o conceito de origem/réplica e o problema de replication lag são praticamente os mesmos entre os dois SGBDs, mudando apenas a terminologia e os comandos específicos.

## 🔗 Notas relacionadas

- [[MySQL - Storage Engines]]
- [[BD - Backup e Restore]]
- [[BD - MVCC]]
- [[Banco de Dados]]