---
tags:
  - banco-de-dados
  - sql
  - postgresql
  - mysql
  - nosql
  - matriz
---
# 🗄️ Banco de Dados — Matriz da Trilha

> Construir conhecimento reutilizável, não apenas concluir cursos.

---

> [!info] O que cobre esta trilha **Banco de Dados** aqui cobre modelagem relacional, SQL (básico ao avançado), normalização, transações, performance/índices, administração, e uma introdução a NoSQL — com foco nos dois motores mais relevantes hoje para novos projetos: **PostgreSQL** (padrão de mercado para projetos novos) e **MySQL** (ainda dominante em stacks legadas e PHP/WordPress).

> [!abstract] Objetivo desta trilha Organizar o estudo de banco de dados de forma progressiva, transformando documentação oficial, laboratórios e projetos em base de conhecimento reutilizável — priorizando a capacidade de modelar, escrever SQL de qualidade e diagnosticar performance, não só decorar sintaxe.

---

## 🧠 Como usar esta matriz

Cada nota é uma unidade independente de conhecimento. Fluxo recomendado:

**Teoria → Exemplo → Laboratório → Projeto → Documentação própria**

Uma nota só é considerada concluída depois de aplicada em projeto ou laboratório real.

```text
Fundamentos → Modelagem → SQL Básico → Normalização → SQL Avançado
→ Transações e Concorrência → Índices e Performance → PostgreSQL
→ MySQL → NoSQL → ORMs → Administração e Segurança
→ Laboratórios → Receitas → Projetos
```

---

## 📚 Resumo da matriz

|Nível|Área|Resumo|
|:--|:--|:--|
|🌱 1|Fundamentos de Banco de Dados|Conceitos de dado, informação, SGBD, modelos de dados, arquitetura cliente-servidor|
|🌿 2|Modelagem de Dados|Modelo conceitual, entidade-relacionamento, cardinalidades, modelo lógico e físico|
|🌿 3|SQL Básico|DDL, DML, DQL, filtros, ordenação, agregações|
|🌿 4|Normalização|1FN, 2FN, 3FN, BCNF, desnormalização consciente|
|🌳 5|SQL Avançado|JOINs, subqueries, CTEs, window functions, views|
|🌳 6|Transações e Concorrência|ACID, isolamento, locks, deadlocks, controle de concorrência|
|🌳 7|Índices e Performance|Índices B-Tree/Hash/GIN, EXPLAIN, otimização de consultas|
|🌳 8|PostgreSQL|Tipos avançados, JSONB, extensões, funções e triggers|
|🌳 9|MySQL|Engines de armazenamento, particularidades de sintaxe, replicação|
|🌳 10|NoSQL|Documentos, chave-valor, colunar, grafos — quando fugir do relacional|
|🏆 11|ORMs e Integração|SQLAlchemy, Prisma, Sequelize — mapeamento objeto-relacional|
|🏆 12|Administração e Segurança|Backup, restore, usuários, permissões, criptografia|
|🔬 13|Laboratórios|Experimentação prática isolada|
|📖 14|Receitas|Implementações reutilizáveis de consulta rápida|
|🚀 15|Projetos|Modelagem e implementação de bancos completos|

---

# 🌱 NÍVEL 1 — FUNDAMENTOS DE BANCO DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|1.1|[[BD - Dado, Informação e Conhecimento]]|Diferenças conceituais, ciclo de vida do dado|
|1.2|[[BD - O que é um SGBD]]|Sistema de Gerenciamento de Banco de Dados, funções, exemplos de mercado|
|1.3|[[BD - Modelos de Dados]]|Relacional, hierárquico, em rede, orientado a documentos|
|1.4|[[BD - Arquitetura Cliente-Servidor]]|Conexões, drivers, portas padrão, arquitetura em camadas|
|1.5|[[BD - Relacional vs NoSQL]]|Quando usar cada abordagem, trade-offs|

---

# 🌿 NÍVEL 2 — MODELAGEM DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|2.1|[[BD - Modelo Conceitual]]|Entidades, atributos, levantamento de requisitos|
|2.2|[[BD - Modelo Entidade-Relacionamento (MER)]]|Diagrama ER, notação Peter Chen / Crow's Foot|
|2.3|[[BD - Cardinalidades e Relacionamentos]]|1:1, 1:N, N:N, relacionamentos ternários|
|2.4|[[BD - Chaves]]|Chave primária, estrangeira, candidata, composta|
|2.5|[[BD - Modelo Lógico]]|Conversão de MER para tabelas relacionais|
|2.6|[[BD - Modelo Físico]]|Tipos de dados por SGBD, constraints, scripts DDL|

---

# 🌿 NÍVEL 3 — SQL BÁSICO

|#|Nota|Tópicos|
|:--|:--|:--|
|3.1|[[SQL - DDL]]|`CREATE`, `ALTER`, `DROP`, constraints|
|3.2|[[SQL - DML]]|`INSERT`, `UPDATE`, `DELETE`|
|3.3|[[SQL - DQL e SELECT]]|`SELECT`, `WHERE`, `ORDER BY`, `LIMIT`|
|3.4|[[SQL - Operadores e Filtros]]|`BETWEEN`, `IN`, `LIKE`, `IS NULL`, operadores lógicos|
|3.5|[[SQL - Funções de Agregação]]|`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY`, `HAVING`|
|3.6|[[SQL - Tipos de Dados]]|Numéricos, texto, data/hora, booleano por SGBD|

---

# 🌿 NÍVEL 4 — NORMALIZAÇÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|4.1|[[BD - Dependência Funcional]]|Conceito, notação, dependências parciais e transitivas|
|4.2|[[BD - Primeira Forma Normal (1FN)]]|Atomicidade dos valores|
|4.3|[[BD - Segunda Forma Normal (2FN)]]|Eliminação de dependências parciais|
|4.4|[[BD - Terceira Forma Normal (3FN)]]|Eliminação de dependências transitivas|
|4.5|[[BD - Forma Normal de Boyce-Codd (BCNF)]]|Casos em que 3FN não é suficiente|
|4.6|[[BD - Desnormalização Consciente]]|Quando e por que desnormalizar por performance|

---

# 🌳 NÍVEL 5 — SQL AVANÇADO

| #   | Nota                                      | Tópicos                                                     |
| :-- | :---------------------------------------- | :---------------------------------------------------------- |
| 5.1 | [[SQL - JOINs]]                           | `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, `CROSS JOIN`        |
| 5.2 | [[SQL - Subqueries]]                      | Subconsultas correlacionadas e não correlacionadas          |
| 5.3 | [[SQL - CTEs (Common Table Expressions)]] | `WITH`, CTEs recursivas                                     |
| 5.4 | [[SQL - Window Functions]]                | `ROW_NUMBER`, `RANK`, `PARTITION BY`, `OVER`                |
| 5.5 | [[SQL - Views e Views Materializadas]]    | Abstração de consultas, atualização de dados materializados |
| 5.6 | [[SQL - Stored Procedures e Functions]]   | Lógica no banco, parâmetros, retorno                        |
| 5.7 | [[SQL - Triggers]]                        | Eventos `BEFORE`/`AFTER`, casos de uso e riscos             |

---

# 🌳 NÍVEL 6 — TRANSAÇÕES E CONCORRÊNCIA

|#|Nota|Tópicos|
|:--|:--|:--|
|6.1|[[BD - ACID]]|Atomicidade, Consistência, Isolamento, Durabilidade|
|6.2|[[BD - Transações (BEGIN, COMMIT, ROLLBACK)]]|Controle transacional explícito|
|6.3|[[BD - Níveis de Isolamento]]|Read Uncommitted, Read Committed, Repeatable Read, Serializable|
|6.4|[[BD - Locks e Deadlocks]]|Locks otimistas/pessimistas, detecção e prevenção de deadlocks|
|6.5|[[BD - MVCC]]|Multiversion Concurrency Control (usado no PostgreSQL)|

---

# 🌳 NÍVEL 7 — ÍNDICES E PERFORMANCE

|#|Nota|Tópicos|
|:--|:--|:--|
|7.1|[[BD - Índices B-Tree]]|Estrutura padrão de índice, quando usar|
|7.2|[[BD - Índices Hash, GIN e GiST]]|Casos específicos (JSONB, full-text search, dados geoespaciais)|
|7.3|[[BD - EXPLAIN e EXPLAIN ANALYZE]]|Leitura de planos de execução|
|7.4|[[BD - Otimização de Consultas]]|Reescrita de queries, evitar `SELECT *`, N+1|
|7.5|[[BD - Particionamento de Tabelas]]|Particionamento por range, lista e hash|

---

# 🌳 NÍVEL 8 — POSTGRESQL

|#|Nota|Tópicos|
|:--|:--|:--|
|8.1|[[PostgreSQL - Instalação e Ferramentas]]|`psql`, pgAdmin, configuração inicial|
|8.2|[[PostgreSQL - Tipos Avançados]]|`JSONB`, `ARRAY`, `UUID`, `ENUM`, tipos de intervalo|
|8.3|[[PostgreSQL - JSONB na Prática]]|Consultas e índices sobre dados semiestruturados|
|8.4|[[PostgreSQL - Extensões]]|`pgcrypto`, `pg_trgm`, `PostGIS`, `pgvector`|
|8.5|[[PostgreSQL - Funções e Triggers em PL/pgSQL]]|Linguagem procedural nativa|

---

# 🌳 NÍVEL 9 — MYSQL

|#|Nota|Tópicos|
|:--|:--|:--|
|9.1|[[MySQL - Instalação e Ferramentas]]|MySQL Workbench, `mysql` CLI|
|9.2|[[MySQL - Storage Engines]]|InnoDB vs MyISAM, quando cada um é usado|
|9.3|[[MySQL - Particularidades de Sintaxe]]|Diferenças de tipos, funções e comportamento vs. padrão SQL|
|9.4|[[MySQL - Replicação]]|Replicação master-replica, casos de uso|

---

# 🌳 NÍVEL 10 — NOSQL

|#|Nota|Tópicos|
|:--|:--|:--|
|10.1|[[NoSQL - Documentos (MongoDB)]]|Coleções, documentos BSON, consultas|
|10.2|[[NoSQL - Chave-Valor (Redis)]]|Cache, estruturas de dados, expiração (TTL)|
|10.3|[[NoSQL - Colunar (Cassandra)]]|Escrita distribuída, particionamento|
|10.4|[[NoSQL - Grafos (Neo4j)]]|Nós, relacionamentos, Cypher|
|10.5|[[NoSQL - Teorema CAP]]|Consistência, Disponibilidade, Tolerância a Partição|

---

# 🏆 NÍVEL 11 — ORMS E INTEGRAÇÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|11.1|[[BD - O que é um ORM]]|Vantagens, desvantagens, quando evitar|
|11.2|[[ORM - SQLAlchemy (Python)]]|Core vs ORM, sessões, migrations com Alembic|
|11.3|[[ORM - Prisma (Node/TS)]]|Schema, migrations, Prisma Client|
|11.4|[[BD - Migrations]]|Versionamento de schema, rollback seguro|
|11.5|[[BD - Connection Pooling]]|Pool de conexões, `pgbouncer`, limites de conexão|

---

# 🏆 NÍVEL 12 — ADMINISTRAÇÃO E SEGURANÇA

|#|Nota|Tópicos|
|:--|:--|:--|
|12.1|[[BD - Backup e Restore]]|`pg_dump`/`pg_restore`, `mysqldump`, estratégias de backup|
|12.2|[[BD - Usuários e Permissões]]|`GRANT`, `REVOKE`, papéis (roles), princípio do menor privilégio|
|12.3|[[BD - Criptografia de Dados]]|Dados em repouso e em trânsito, SSL/TLS|
|12.4|[[BD - Prevenção de SQL Injection]]|Prepared statements, sanitização, boas práticas|
|12.5|[[BD - Monitoramento e Logs]]|Slow query log, métricas de performance|

---

# 🔬 NÍVEL 13 — LABORATÓRIOS

|#|Nota|Tópicos|
|:--|:--|:--|
|13.1|[[Lab - Modelagem ER]]|Modelagem de um domínio real do zero|
|13.2|[[Lab - SQL Avançado]]|Exercícios com JOINs, CTEs e window functions|
|13.3|[[Lab - Otimização de Query Lenta]]|Diagnóstico com `EXPLAIN ANALYZE` e correção|
|13.4|[[Lab - PostgreSQL com JSONB]]|Modelagem híbrida relacional + semiestruturada|
|13.5|[[Lab - Redis como Cache]]|Cache de consultas frequentes|
|13.6|[[Lab - Migrations com Alembic/Prisma]]|Evolução de schema em ambiente real|

---

# 📖 NÍVEL 14 — RECEITAS

|#|Nota|Tópicos|
|:--|:--|:--|
|14.1|[[Recipe - CRUD Completo em SQL]]|Create, Read, Update, Delete com boas práticas|
|14.2|[[Recipe - Paginação Eficiente]]|`LIMIT/OFFSET` vs. keyset pagination|
|14.3|[[Recipe - Busca Full-Text]]|`tsvector`/`tsquery` (Postgres) ou `FULLTEXT` (MySQL)|
|14.4|[[Recipe - Soft Delete]]|Exclusão lógica vs. física|
|14.5|[[Recipe - Auditoria de Alterações]]|Tabelas de histórico, triggers de auditoria|
|14.6|[[Recipe - Script de Backup Automatizado]]|Agendamento e rotação de backups|

---

# 🚀 NÍVEL 15 — PROJETOS

|#|Nota|Tópicos|
|:--|:--|:--|
|15.1|[[Projeto - Modelagem de E-commerce]]|Produtos, pedidos, estoque, clientes|
|15.2|[[Projeto - Sistema de Reservas]]|Concorrência, locks, disponibilidade|
|15.3|[[Projeto - Dashboard Analítico]]|Consultas agregadas, views materializadas|
|15.4|[[Projeto - API com Cache Redis]]|Integração relacional + cache|
|15.5|[[Projeto - Migração MySQL → PostgreSQL]]|Diferenças práticas de migração entre motores|

---

# 📈 Roadmap profissional

|Etapa|Objetivo|Conhecimentos|
|:--|:--|:--|
|🌱 Fundamentos|Entender o que é e para que serve um SGBD|Conceitos, modelos de dados, arquitetura|
|🌿 Modelagem e SQL|Modelar e consultar dados corretamente|MER, chaves, normalização, SQL básico|
|🌳 SQL Intermediário/Avançado|Escrever consultas complexas e eficientes|JOINs, CTEs, window functions, transações|
|🌳 Performance|Diagnosticar e corrigir gargalos|Índices, EXPLAIN, particionamento|
|🏆 Especialização por motor|Dominar PostgreSQL e/ou MySQL na prática|Tipos avançados, extensões, replicação|
|🚀 Integração e Escala|Integrar com aplicações reais|ORMs, migrations, connection pooling, NoSQL|
|👑 Administração|Operar bancos em produção com segurança|Backup, permissões, criptografia, monitoramento|

---

# 🎯 Critérios de conclusão

|Critério|Descrição|
|:--|:--|
|Conhecimento|Consigo explicar o conceito sem consulta|
|Implementação|Consigo implementar do zero|
|Depuração|Consigo identificar e corrigir erros comuns|
|Aplicação|Já utilizei em projeto real|
|Documentação|Possuo nota própria documentada|
|Exemplo|Tenho exemplo funcional salvo|
|Reutilização|Tenho receita pronta para consulta futura|

---

# 📊 Matriz de proficiência

|Status|Significado|
|:--|:--|
|⬜ Não Estudado|Conteúdo ainda não iniciado|
|🟦 Em Estudo|Teoria em andamento|
|🟨 Praticando|Exercícios e laboratórios|
|🟩 Aplicado|Utilizado em projeto real|
|🟪 Dominado|Capaz de ensinar e implementar sem consulta|

---

# 📚 Fontes

## Oficiais

- [PostgreSQL — Documentação oficial](https://www.postgresql.org/docs/) — considerada uma das melhores documentações técnicas de todo o open source; comece pelo [tutorial oficial](https://www.postgresql.org/docs/current/tutorial.html)
- [MySQL — Reference Manual (oficial)](https://dev.mysql.com/doc/refman/en/) — documentação oficial da Oracle/MySQL
- [SQLite — Documentação oficial](https://www.sqlite.org/docs.html) — ótimo para laboratórios locais e entender internals de forma simples
- [MongoDB — Documentação oficial](https://www.mongodb.com/docs/)
- [Redis — Documentação oficial](https://redis.io/docs/latest/)
- [Neo4j — Documentação oficial](https://neo4j.com/docs/)
- [SQLAlchemy — Documentação oficial](https://docs.sqlalchemy.org/)
- [Prisma — Documentação oficial](https://www.prisma.io/docs)

## Referências técnicas e prática

- [Use The Index, Luke!](https://use-the-index-luke.com/) — a melhor referência independente sobre índices e performance de SQL, agnóstica de SGBD
- [PostgreSQL Exercises](https://pgexercises.com/) — exercícios práticos de SQL direto no navegador, focado em Postgres
- [Mode SQL Tutorial](https://mode.com/sql-tutorial/) — tutorial prático de SQL orientado a análise de dados
- [Planet PostgreSQL](https://planet.postgresql.org/) — agregador de blogs oficiais e da comunidade PostgreSQL

## Livros

- _SQL Antipatterns_ (Bill Karwin)
- _Designing Data-Intensive Applications_ (Martin Kleppmann) — referência avançada para quem quer entender os fundamentos por trás de todo SGBD e sistema distribuído
- _Database Design for Mere Mortals_ (Michael J. Hernandez)

> [!note] Nota de mercado (2026) PostgreSQL ultrapassou o MySQL como o banco relacional mais usado entre desenvolvedores profissionais e é hoje a escolha padrão para projetos novos, graças à maior aderência ao padrão SQL, tipos avançados (JSONB, arrays) e ecossistema de extensões. MySQL continua dominante em stacks legadas e no ecossistema PHP/WordPress. Por isso esta trilha trata SQL Avançado (Nível 5) e Transações (Nível 6) de forma agnóstica, e reserva níveis específicos (8 e 9) para as particularidades de cada motor.

> [!note] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → `[!NOTE]` / `[!TIP]` → exemplos de código → links relacionados.