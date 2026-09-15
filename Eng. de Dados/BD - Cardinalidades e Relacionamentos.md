---

tags:

- banco-de-dados
- modelagem aliases: [Cardinalidade, Relacionamentos 1:1 1:N N:N]

---

# BD - Cardinalidades e Relacionamentos

## 📌 Conceito principal

**Cardinalidade** define quantas instâncias de uma entidade podem se relacionar com quantas instâncias de outra entidade. É o detalhe que determina como o relacionamento será implementado fisicamente no banco.

## 🔢 Os três tipos de cardinalidade

### 1:1 (um para um)

Cada registro de A se relaciona com no máximo um registro de B, e vice-versa.

**Exemplo**: Pessoa ↔ Passaporte (uma pessoa tem um passaporte; um passaporte pertence a uma pessoa).

**Implementação**: a chave estrangeira pode ficar em qualquer uma das duas tabelas, geralmente na que "depende" conceitualmente da outra.

### 1:N (um para muitos)

Um registro de A pode se relacionar com vários registros de B, mas cada registro de B se relaciona com apenas um de A.

**Exemplo**: Cliente ↔ Pedido (um cliente faz vários pedidos; um pedido pertence a um único cliente).

**Implementação**: a chave estrangeira fica sempre do lado "muitos" (na tabela Pedido, uma coluna `cliente_id`).

### N:N (muitos para muitos)

Vários registros de A se relacionam com vários registros de B.

**Exemplo**: Pedido ↔ Produto (um pedido tem vários produtos; um produto aparece em vários pedidos).

**Implementação**: exige uma **tabela associativa** (também chamada tabela de junção/pivô) com chaves estrangeiras para ambas as tabelas.

> [!warning] N:N nunca se implementa direto Não existe forma de representar N:N com uma única chave estrangeira — é sempre necessária uma terceira tabela intermediária.

## 💻 Exemplo prático — implementando N:N

```sql
CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(id)
);

CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100)
);

-- Tabela associativa que resolve o N:N
CREATE TABLE itens_pedido (
    pedido_id INT REFERENCES pedidos(id),
    produto_id INT REFERENCES produtos(id),
    quantidade INT NOT NULL DEFAULT 1,
    PRIMARY KEY (pedido_id, produto_id)
);
```

## 🔺 Relacionamentos ternários

Envolvem três entidades ao mesmo tempo, não apenas duas relações binárias separadas.

**Exemplo**: Médico atende Paciente em determinada Data — o relacionamento "atendimento" só faz sentido conectando as três entidades simultaneamente, não apenas Médico↔Paciente e Paciente↔Data isoladamente.

```sql
CREATE TABLE atendimentos (
    medico_id INT REFERENCES medicos(id),
    paciente_id INT REFERENCES pacientes(id),
    data_hora TIMESTAMP NOT NULL,
    PRIMARY KEY (medico_id, paciente_id, data_hora)
);
```

## 🔗 Notas relacionadas

- [[BD - Modelo Entidade-Relacionamento (MER)]]
- [[BD - Chaves]]
- [[BD - Modelo Lógico]]
- [[SQL - JOINs]]
- [[Banco de Dados]]