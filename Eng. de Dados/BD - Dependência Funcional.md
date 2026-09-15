---

tags:

- banco-de-dados
- normalizacao aliases: [Dependência Funcional, Functional Dependency]

---

# BD - Dependência Funcional

## 📌 Conceito principal

Uma **dependência funcional** existe quando o valor de um atributo (ou conjunto de atributos) determina univocamente o valor de outro atributo. É a base matemática sobre a qual toda a teoria de normalização (1FN, 2FN, 3FN, BCNF) é construída.

## 📝 Notação

Se o atributo **A** determina o atributo **B**, escreve-se:

```
A → B
```

Lê-se: "B depende funcionalmente de A" ou "A determina B".

**Exemplo**: em uma tabela de pedidos, `pedido_id → cliente_id` — dado um `pedido_id`, o `cliente_id` correspondente é sempre o mesmo (um pedido pertence a um único cliente).

## 🔀 Tipos de dependência

### Dependência total

`B` depende do **conjunto completo** de atributos da chave, não de uma parte dela.

### Dependência parcial

`B` depende de **apenas parte** de uma chave composta — só existe quando a chave primária tem mais de uma coluna.

```
Chave composta: (pedido_id, produto_id)
nome_produto depende apenas de produto_id (dependência parcial — viola a 2FN)
```

### Dependência transitiva

`A → B` e `B → C`, portanto `A → C` indiretamente — mas `C` não depende diretamente de `A`.

```
produto_id → categoria_id → nome_categoria
-- nome_categoria depende de produto_id apenas de forma transitiva (via categoria_id)
```

> [!note] Por que isso importa Dependências parciais violam a [[BD - Segunda Forma Normal (2FN)]] e dependências transitivas violam a [[BD - Terceira Forma Normal (3FN)]]. Identificar essas dependências é o primeiro passo prático antes de normalizar qualquer tabela.

## 💻 Exemplo prático — identificando dependências em uma tabela mal projetada

```
itens_pedido(pedido_id, produto_id, nome_produto, preco_produto, quantidade, nome_categoria)
```

Dependências identificadas:

- `(pedido_id, produto_id) → quantidade` — dependência total (correta, depende da chave inteira)
- `produto_id → nome_produto` — dependência parcial (viola 2FN, pois `nome_produto` só depende de parte da chave)
- `produto_id → preco_produto` — dependência parcial
- `produto_id → categoria_id → nome_categoria` — dependência transitiva (viola 3FN)

Essas dependências mal resolvidas geram os problemas clássicos de redundância e anomalias tratados nas próximas notas: [[BD - Segunda Forma Normal (2FN)]] e [[BD - Terceira Forma Normal (3FN)]].

## 🔗 Notas relacionadas

- [[BD - Primeira Forma Normal (1FN)]]
- [[BD - Segunda Forma Normal (2FN)]]
- [[BD - Terceira Forma Normal (3FN)]]
- [[Banco de Dados]]