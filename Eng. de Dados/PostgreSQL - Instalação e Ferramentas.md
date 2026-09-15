---

tags:

- banco-de-dados
- postgresql aliases: [psql, pgAdmin, Instalação PostgreSQL]

---

# PostgreSQL - Instalação e Ferramentas

## 📌 Conceito principal

Antes de usar o PostgreSQL na prática, é preciso conhecer as duas formas principais de interagir com ele: o cliente de linha de comando oficial (`psql`) e ferramentas gráficas de administração.

> [!tip] Forma recomendada para estudo Em vez de instalar o PostgreSQL diretamente no sistema operacional, rodar via Docker (ver [[Docker - PostgreSQL em Container]]) evita conflitos de versão e permite destruir/recriar o ambiente facilmente — abordagem já coberta na matriz de [[Ferramentas e DevOps para Dados - Matriz da Trilha|Ferramentas e DevOps]].

## 💻 psql — cliente oficial de linha de comando

```bash
# Conectar a um banco local
psql -h localhost -U postgres -d meu_banco

# Conectar informando a porta explicitamente (padrão é 5432)
psql -h localhost -p 5432 -U postgres -d meu_banco
```

### Comandos úteis dentro do psql

```
\l              -- listar todos os bancos de dados
\c nome_banco   -- conectar a outro banco
\dt             -- listar tabelas do banco atual
\d nome_tabela  -- descrever a estrutura de uma tabela (colunas, tipos, índices)
\du             -- listar usuários/roles
\q              -- sair do psql
```

> [!note] Fonte oficial A documentação do PostgreSQL cobre o `psql` em detalhe, incluindo todos os comandos de barra invertida (`\d`, `\l`, etc.) e opções de linha de comando. Fonte: [postgresql.org/docs — psql](https://www.postgresql.org/docs/current/app-psql.html)

## 🖥️ Ferramentas gráficas

|Ferramenta|Característica|
|---|---|
|**pgAdmin**|Ferramenta oficial da comunidade PostgreSQL, roda no navegador ou como app desktop|
|**DBeaver**|Cliente universal (funciona com vários SGBDs), gratuito, boa opção multiplataforma|
|**Adminer**|Ferramenta leve, single-file, ótima para rodar junto de um container Docker|

## 💻 Exemplo prático — primeiro acesso após instalação via Docker

```bash
docker run --name meu-postgres -e POSTGRES_PASSWORD=senha123 -p 5432:5432 -d postgres:17

# Conectar de dentro do próprio container
docker exec -it meu-postgres psql -U postgres

# Ou conectar do host, usando o cliente psql instalado localmente
psql -h localhost -p 5432 -U postgres
```

## 🔗 Notas relacionadas

- [[Docker - PostgreSQL em Container]]
- [[BD - Arquitetura Cliente-Servidor]]
- [[PostgreSQL - Tipos Avançados]]
- [[Banco de Dados]]