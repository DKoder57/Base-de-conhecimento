---

tags:

- banco-de-dados
- fundamentos aliases: [Cliente-Servidor, Arquitetura de BD]

---

# BD - Arquitetura Cliente-Servidor

## 📌 Conceito principal

A maioria dos SGBDs relacionais (PostgreSQL, MySQL) segue o modelo **cliente-servidor**: um processo servidor (o próprio SGBD) fica em execução esperando conexões, e clientes (aplicações, ferramentas administrativas, outros serviços) se conectam a ele através da rede — mesmo quando "rede" significa apenas `localhost`.

> [!info] Como a documentação oficial descreve A documentação do PostgreSQL descreve explicitamente esse modelo: um processo servidor que gerencia os arquivos do banco, aceita conexões de aplicações clientes e realiza ações no banco em nome dos clientes. Os programas clientes podem ser bem variados — desde ferramentas de texto até aplicações web complexas. Fonte: [postgresql.org/docs](https://www.postgresql.org/docs/current/tutorial-arch.html)

## 🔌 Componentes da arquitetura

1. **Servidor (backend)**: processo do SGBD que escuta em uma porta específica, gerencia arquivos de dados, executa consultas e devolve resultados.
2. **Cliente (frontend)**: qualquer programa que se conecta ao servidor — pode ser um cliente de linha de comando (`psql`, `mysql`), uma ferramenta gráfica (DBeaver, pgAdmin) ou a própria aplicação via **driver**.
3. **Driver/conector**: biblioteca que implementa o protocolo de comunicação entre a linguagem da aplicação e o SGBD (ex.: `psycopg2`/`asyncpg` para Python + Postgres, `mysql-connector` para Python + MySQL).

## 🔢 Portas padrão dos principais SGBDs

|SGBD|Porta padrão|
|---|---|
|PostgreSQL|5432|
|MySQL|3306|
|SQL Server|1433|
|MongoDB|27017|
|Redis|6379|

> [!tip] Por que isso importa na prática Ao configurar um container Docker (ver [[Docker - PostgreSQL em Container]]) ou uma conexão de aplicação, é a combinação **host + porta + usuário + senha + banco** que define a conexão cliente-servidor. Erros de conexão em ~90% dos casos são porta errada, serviço não exposto, ou firewall bloqueando a comunicação.

## 🏗️ Arquitetura em camadas (aplicação real)

Num sistema real, o cliente do SGBD geralmente não é o usuário final, mas sim a camada de aplicação:

```
Usuário → Frontend (navegador/app) → Backend (API) → Driver/ORM → SGBD (servidor)
```

O SGBD nunca "sabe" que existe um usuário do outro lado — ele só enxerga a conexão vinda do backend.

## 💻 Exemplo prático

```python
# Exemplo de conexão cliente-servidor em Python com psycopg2
import psycopg2

conexao = psycopg2.connect(
    host="localhost",   # onde o servidor está escutando
    port=5432,           # porta padrão do PostgreSQL
    dbname="meu_banco",
    user="postgres",
    password="senha"
)
cursor = conexao.cursor()
cursor.execute("SELECT 1;")
print(cursor.fetchone())
```

## 🔗 Notas relacionadas

- [[BD - O que é um SGBD]]
- [[Docker - PostgreSQL em Container]]
- [[BD - Connection Pooling]]
- [[Banco de Dados]]