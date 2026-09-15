---
Tags

banco-de-dados,fundamentos

Aliases

SGBD,DBMS,Sistema Gerenciador de Banco de Dados
---
# BD - O que é um SGBD

## 📌 Conceito principal

Um **SGBD (Sistema de Gerenciamento de Banco de Dados)** — em inglês _DBMS (Database Management System)_ — é o software responsável por armazenar, organizar, proteger e permitir a consulta de dados de forma estruturada, sem que a aplicação precise lidar diretamente com arquivos brutos em disco.

> [!info] Definição oficial (PostgreSQL Docs) A documentação oficial do PostgreSQL descreve o produto como um sistema de banco de dados objeto-relacional, derivado do POSTGRES da Universidade de Berkeley, com mais de 35 anos de desenvolvimento ativo — um exemplo direto de SGBD maduro em produção. Fonte: [postgresql.org/docs](https://www.postgresql.org/docs/current/intro-whatis.html)

## ⚙️ Principais funções de um SGBD

- **Persistência**: garantir que os dados sobrevivam a reinicializações e falhas.
- **Definição de estrutura**: permitir criar tabelas, tipos, constraints (DDL).
- **Manipulação de dados**: inserir, atualizar, remover e consultar (DML/DQL).
- **Controle de concorrência**: permitir múltiplos usuários acessando o mesmo dado sem corrupção (ver [[BD - MVCC]] e [[BD - Locks e Deadlocks]]).
- **Controle de transações**: garantir atomicidade e consistência (ver [[BD - ACID]]).
- **Segurança**: gerenciar usuários, papéis e permissões (ver [[BD - Usuários e Permissões]]).
- **Backup e recuperação**: proteger contra perda de dados (ver [[BD - Backup e Restore]]).

## 🏛️ Exemplos de SGBDs no mercado

|SGBD|Tipo|Observação|
|---|---|---|
|PostgreSQL|Relacional (objeto-relacional)|Padrão de mercado para projetos novos em 2026|
|MySQL|Relacional|Ainda dominante em stacks legadas e PHP/WordPress|
|SQLite|Relacional (embarcado)|Sem servidor, arquivo único — ótimo para estudo e apps locais|
|MongoDB|NoSQL (documentos)|Dados semiestruturados, sem schema rígido|
|Redis|NoSQL (chave-valor)|Extremamente rápido, usado como cache|

> [!tip] Diferença chave: SGBD vs. banco de dados "Banco de dados" é o conjunto organizado de dados em si. "SGBD" é o software que gerencia esse conjunto. Coloquialmente as pessoas usam os termos como sinônimos, mas tecnicamente o SGBD é a ferramenta e o banco de dados é o que ela gerencia.

## 💻 Exemplo prático

```bash
# Conectando a um SGBD PostgreSQL via cliente oficial
psql -h localhost -U postgres -d meu_banco

# Dentro do psql, o SGBD expõe metadados sobre si mesmo:
meu_banco=# SELECT version();
--                            version
-- ----------------------------------------------------------
-- PostgreSQL 17.x on x86_64-pc-linux-gnu, compiled by gcc...
```

## 🔗 Notas relacionadas

- [[BD - Dado, Informação e Conhecimento]]
- [[BD - Modelos de Dados]]
- [[BD - Arquitetura Cliente-Servidor]]
- [[Banco de Dados]]