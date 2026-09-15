---

tags:

- banco-de-dados
- modelagem aliases: [Modelagem Física, Script DDL]

---

# BD - Modelo Físico

## 📌 Conceito principal

O **modelo físico** é a implementação real do [[BD - Modelo Lógico]] em um SGBD específico — aqui entram tipos de dados concretos, constraints, índices e o script DDL que efetivamente cria as tabelas no banco.

> [!note] Última etapa da modelagem Conceitual (o quê) → Lógico (como se relaciona) → **Físico (SQL de verdade, específico do PostgreSQL/MySQL/etc.)**. É só aqui que a modelagem "vira banco de dados" de fato.

## 🧱 Tipos de dados por SGBD

Cada SGBD tem seu próprio catálogo de tipos — a mesma coluna "lógica" pode virar tipos diferentes dependendo de onde é implementada.

|Conceito lógico|PostgreSQL|MySQL|
|---|---|---|
|Identificador auto-incremento|`SERIAL` / `GENERATED ALWAYS AS IDENTITY`|`INT AUTO_INCREMENT`|
|Texto curto|`VARCHAR(n)`|`VARCHAR(n)`|
|Texto longo|`TEXT`|`TEXT`|
|Data e hora|`TIMESTAMP` / `TIMESTAMPTZ`|`DATETIME`|
|Verdadeiro/falso|`BOOLEAN`|`TINYINT(1)` (não há `BOOLEAN` nativo)|
|Dado semiestruturado|`JSONB`|`JSON`|
|Dinheiro/decimal exato|`NUMERIC(p,s)`|`DECIMAL(p,s)`|

> [!warning] Particularidade do MySQL O MySQL não tem um tipo `BOOLEAN` verdadeiro — ele é apenas um apelido para `TINYINT(1)`. Isso é uma das diferenças de sintaxe entre os motores tratadas no [[MySQL - Particularidades de Sintaxe]].

## 🔒 Constraints no modelo físico

```sql
CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    idade INT CHECK (idade >= 0),
    criado_em TIMESTAMP DEFAULT NOW()
);
```

|Constraint|Função|
|---|---|
|`PRIMARY KEY`|Identifica unicamente cada linha|
|`NOT NULL`|Impede valores nulos na coluna|
|`UNIQUE`|Impede valores duplicados|
|`CHECK`|Valida uma regra de negócio na própria coluna|
|`DEFAULT`|Define valor padrão quando nenhum é informado|
|`FOREIGN KEY` / `REFERENCES`|Garante integridade referencial (ver [[BD - Chaves]])|

## 💻 Exemplo prático — do modelo lógico ao script DDL completo

```sql
CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL
);

CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco NUMERIC(10,2) NOT NULL CHECK (preco >= 0)
);

CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    cliente_id INT NOT NULL REFERENCES clientes(id),
    status VARCHAR(20) NOT NULL DEFAULT 'pendente',
    criado_em TIMESTAMP NOT NULL DEFAULT NOW()
);

CREATE TABLE itens_pedido (
    pedido_id INT REFERENCES pedidos(id),
    produto_id INT REFERENCES produtos(id),
    quantidade INT NOT NULL DEFAULT 1 CHECK (quantidade > 0),
    PRIMARY KEY (pedido_id, produto_id)
);
```

> [!tip] Próximo passo natural Depois de rodar esse script, o próximo movimento é aprender a consultar esses dados — que é exatamente o Nível 3 desta trilha, começando por [[SQL - DDL]] e [[SQL - DQL e SELECT]].

## 🔗 Notas relacionadas

- [[BD - Modelo Lógico]]
- [[BD - Chaves]]
- [[SQL - DDL]]
- [[SQL - Tipos de Dados]]
- [[Banco de Dados]]