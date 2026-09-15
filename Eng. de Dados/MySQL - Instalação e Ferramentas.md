---

tags:

- banco-de-dados
- mysql aliases: [MySQL Workbench, Instalação MySQL]

---

# MySQL - Instalação e Ferramentas

## 📌 Conceito principal

Assim como o PostgreSQL tem o `psql`, o MySQL tem seu próprio cliente oficial de linha de comando (`mysql`) e uma ferramenta gráfica oficial (**MySQL Workbench**).

> [!tip] Estudo via Docker Da mesma forma que o Postgres, a forma mais prática de estudar MySQL sem "sujar" o sistema é via container — ver [[Docker - MySQL em Container]].

## 💻 Cliente mysql — linha de comando

```bash
mysql -h localhost -u root -p
```

### Comandos úteis dentro do cliente mysql

```
SHOW DATABASES;              -- listar bancos de dados
USE nome_banco;              -- selecionar um banco
SHOW TABLES;                 -- listar tabelas do banco atual
DESCRIBE nome_tabela;         -- ver estrutura de uma tabela
SHOW CREATE TABLE nome_tabela; -- ver o script DDL exato da tabela
EXIT;                        -- sair
```

> [!note] Fonte oficial A documentação oficial do MySQL (MySQL Reference Manual, mantida pela Oracle) cobre o cliente `mysql`, todos os comandos `SHOW`, e opções de configuração do servidor. Fonte: [dev.mysql.com/doc/refman](https://dev.mysql.com/doc/refman/en/)

## 🖥️ MySQL Workbench

Ferramenta gráfica oficial, com:

- Editor de SQL com autocomplete
- Modelagem visual de ER (Entity-Relationship) que gera DDL automaticamente
- Ferramentas de administração (usuários, backup, monitoramento)

> [!tip] Diferencial do Workbench A modelagem visual do Workbench é um dos motivos pelos quais ele ainda é muito usado em cursos e times que fazem modelagem MER diretamente na ferramenta antes de gerar o script DDL — uma aplicação direta do fluxo Conceitual → Lógico → Físico visto em [[BD - Modelo Físico]].

## 💻 Exemplo prático — primeiro acesso via Docker

```bash
docker run --name meu-mysql -e MYSQL_ROOT_PASSWORD=senha123 -p 3306:3306 -d mysql:8.4

# Conectar de dentro do container
docker exec -it meu-mysql mysql -u root -p

# Conectar do host, usando cliente mysql instalado localmente
mysql -h 127.0.0.1 -P 3306 -u root -p
```

## 🔗 Notas relacionadas

- [[Docker - MySQL em Container]]
- [[MySQL - Storage Engines]]
- [[MySQL - Particularidades de Sintaxe]]
- [[Banco de Dados]]