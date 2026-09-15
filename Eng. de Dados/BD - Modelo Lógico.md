---

tags:

- banco-de-dados
- modelagem aliases: [Modelagem Lógica, Modelo Relacional Lógico]

---

# BD - Modelo Lógico

## 📌 Conceito principal

O **modelo lógico** é a etapa intermediária entre o [[BD - Modelo Entidade-Relacionamento (MER)]] (conceitual, abstrato) e o [[BD - Modelo Físico]] (SQL real, específico do SGBD). Aqui, entidades viram **tabelas**, atributos viram **colunas**, e relacionamentos viram **chaves estrangeiras** — mas ainda sem se prender a tipos de dados específicos de um SGBD.

## 🔄 Regras de conversão MER → Modelo Lógico

### Entidade → Tabela

Cada entidade forte vira uma tabela, com seus atributos como colunas.

### Relacionamento 1:N → Chave estrangeira

A chave primária do lado "1" vira uma chave estrangeira na tabela do lado "N".

```
Cliente (1) ── faz ──> (N) Pedido
```

vira:

```
pedidos.cliente_id → clientes.id
```

### Relacionamento N:N → Nova tabela associativa

Como não existe forma direta de representar N:N com uma coluna só, cria-se uma tabela nova, cuja chave primária é a combinação das chaves estrangeiras das duas entidades originais (ver [[BD - Cardinalidades e Relacionamentos]]).

### Atributo multivalorado → Nova tabela

Um atributo que pode ter múltiplos valores (ex.: telefones de um cliente) não cabe em uma única coluna relacional — vira uma tabela própria com relacionamento 1:N para a entidade original.

```sql
CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100)
);

CREATE TABLE telefones_cliente (
    id SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(id),
    numero VARCHAR(20)
);
```

### Relacionamento ternário → Tabela com três chaves estrangeiras

Como visto em [[BD - Cardinalidades e Relacionamentos]], vira uma tabela com uma FK para cada uma das três entidades envolvidas.

## 💻 Exemplo prático completo

**MER**: Cliente (1:N) Pedido (N:N) Produto

**Modelo lógico resultante**:

```
clientes(id, nome, email)
pedidos(id, cliente_id → clientes.id, data, status)
produtos(id, nome, preco)
itens_pedido(pedido_id → pedidos.id, produto_id → produtos.id, quantidade)
```

> [!tip] Ainda não é o modelo físico Repare que não há tipos de dado específicos do PostgreSQL (`SERIAL`, `TIMESTAMP`) nem constraints detalhadas — isso só entra no [[BD - Modelo Físico]], quando o SGBD já foi escolhido.

## 🔗 Notas relacionadas

- [[BD - Modelo Entidade-Relacionamento (MER)]]
- [[BD - Cardinalidades e Relacionamentos]]
- [[BD - Chaves]]
- [[BD - Modelo Físico]]
- [[Banco de Dados]]