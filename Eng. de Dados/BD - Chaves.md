---

tags:

- banco-de-dados
- modelagem aliases: [Chave Primária, Chave Estrangeira, Primary Key, Foreign Key]

---

# BD - Chaves

## 📌 Conceito principal

**Chaves** são os atributos (ou conjuntos de atributos) usados para identificar e conectar registros de forma única e confiável dentro de um banco relacional. Sem chaves bem definidas, não existe integridade referencial garantida pelo SGBD.

## 🔑 Tipos de chave

### Chave candidata

Qualquer atributo (ou conjunto de atributos) que **poderia** identificar unicamente um registro. Uma tabela pode ter várias chaves candidatas (ex.: `id` e `email` podem ambos identificar um cliente unicamente).

### Chave primária (Primary Key)

A chave candidata **escolhida** para identificar oficialmente cada registro da tabela. Não pode ser nula e deve ser única.

```sql
CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,   -- chave primária
    email VARCHAR(100) UNIQUE -- chave candidata não escolhida como PK
);
```

### Chave estrangeira (Foreign Key)

Um atributo que referencia a chave primária de **outra** tabela, criando o vínculo entre elas e garantindo **integridade referencial** — o SGBD impede inserir uma referência para um registro que não existe.

```sql
CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(id) -- chave estrangeira
);
```

### Chave composta

Uma chave primária (ou estrangeira) formada por mais de uma coluna — comum em tabelas associativas de relacionamentos N:N.

```sql
CREATE TABLE itens_pedido (
    pedido_id INT REFERENCES pedidos(id),
    produto_id INT REFERENCES produtos(id),
    PRIMARY KEY (pedido_id, produto_id) -- chave primária composta
);
```

## ⚠️ Comportamento de integridade referencial

Ao definir uma chave estrangeira, é possível (e recomendado) especificar o que acontece quando o registro referenciado é apagado ou atualizado:

```sql
CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(id)
        ON DELETE CASCADE   -- apaga os pedidos se o cliente for apagado
        ON UPDATE CASCADE   -- atualiza o cliente_id se o id do cliente mudar
);
```

|Opção|Comportamento|
|---|---|
|`CASCADE`|Propaga a alteração/exclusão para os registros dependentes|
|`RESTRICT` / `NO ACTION`|Impede a exclusão/alteração se houver dependentes (padrão mais seguro)|
|`SET NULL`|Define a coluna como nula quando o registro pai é apagado|
|`SET DEFAULT`|Define a coluna para seu valor padrão|

> [!warning] Cuidado com `ON DELETE CASCADE` em produção É conveniente, mas perigoso: um `DELETE` acidental na tabela pai pode apagar silenciosamente uma cadeia inteira de registros relacionados. Muitas equipes preferem `RESTRICT` como padrão e cascatas explícitas só onde o negócio realmente exige (ex.: apagar itens de um pedido quando o pedido é cancelado).

## 🔗 Notas relacionadas

- [[BD - Modelo Entidade-Relacionamento (MER)]]
- [[BD - Cardinalidades e Relacionamentos]]
- [[BD - Modelo Físico]]
- [[SQL - DDL]]
- [[Banco de Dados]]