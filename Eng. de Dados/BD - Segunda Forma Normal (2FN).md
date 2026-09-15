---

tags:

- banco-de-dados
- normalizacao aliases: [2FN, Second Normal Form, 2NF]

---

# BD - Segunda Forma Normal (2FN)

## 📌 Conceito principal

Uma tabela está na **Segunda Forma Normal (2FN)** quando, além de estar na [[BD - Primeira Forma Normal (1FN)]], **todos os atributos não-chave dependem da chave primária inteira** — não apenas de parte dela.

> [!note] Quando essa regra se aplica A 2FN só é relevante em tabelas com **chave primária composta** (mais de uma coluna). Se a chave primária é uma única coluna, a tabela automaticamente satisfaz a 2FN.

## ❌ Exemplo de violação da 2FN

```
itens_pedido(pedido_id, produto_id, nome_produto, preco_produto, quantidade)
Chave primária composta: (pedido_id, produto_id)
```

Dependências identificadas:

- `(pedido_id, produto_id) → quantidade` ✅ depende da chave inteira — correto
- `produto_id → nome_produto` ❌ depende só de parte da chave — **dependência parcial**
- `produto_id → preco_produto` ❌ dependência parcial

Isso causa **redundância**: o nome e o preço do produto se repetem em toda linha de `itens_pedido` que referencia aquele produto — e se o preço mudar, seria preciso atualizar várias linhas ao mesmo tempo (risco de inconsistência).

## ✅ Correção — extraindo o que depende só de parte da chave

```sql
CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    preco NUMERIC(10,2)
);

CREATE TABLE itens_pedido (
    pedido_id INT REFERENCES pedidos(id),
    produto_id INT REFERENCES produtos(id),
    quantidade INT NOT NULL,
    PRIMARY KEY (pedido_id, produto_id)
);
```

Agora `nome` e `preco` vivem uma única vez em `produtos`, e `itens_pedido` guarda apenas o que realmente depende da combinação `(pedido_id, produto_id)`.

> [!tip] Detalhe importante sobre preço histórico Ao mover `preco` para a tabela `produtos`, perde-se o preço **no momento da compra** — se o preço do produto mudar depois, pedidos antigos "mudariam de valor" retroativamente ao consultar via JOIN. Na prática, sistemas de e-commerce guardam intencionalmente uma cópia do preço em `itens_pedido` (`preco_unitario_na_compra`) — isso não é um erro de normalização, é uma decisão consciente de negócio (registro histórico), diferente da redundância acidental que a 2FN evita.

## 🔗 Notas relacionadas

- [[BD - Dependência Funcional]]
- [[BD - Primeira Forma Normal (1FN)]]
- [[BD - Terceira Forma Normal (3FN)]]
- [[Banco de Dados]]