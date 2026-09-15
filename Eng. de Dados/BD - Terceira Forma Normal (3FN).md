---

tags:

- banco-de-dados
- normalizacao aliases: [3FN, Third Normal Form, 3NF]

---

# BD - Terceira Forma Normal (3FN)

## 📌 Conceito principal

Uma tabela está na **Terceira Forma Normal (3FN)** quando, além de estar na [[BD - Segunda Forma Normal (2FN)]], **nenhum atributo não-chave depende de outro atributo não-chave** — apenas da chave primária. Ou seja, elimina-se toda **dependência transitiva**.

## ❌ Exemplo de violação da 3FN

```
produtos(id, nome, categoria_id, nome_categoria)
```

Dependências:

- `id → nome` ✅ correto (depende da chave)
- `id → categoria_id` ✅ correto
- `categoria_id → nome_categoria` — e portanto `id → nome_categoria` de forma **transitiva** (via `categoria_id`, não diretamente da chave) ❌

O problema prático: se o nome de uma categoria mudar (ex.: "Eletrônicos" → "Eletrônicos e Informática"), seria preciso atualizar essa string em **todo produto** daquela categoria — redundância e risco de inconsistência (dois produtos da mesma categoria com nomes de categoria diferentes por erro de atualização).

## ✅ Correção — extraindo a dependência transitiva

```sql
CREATE TABLE categorias (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100)
);

CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    categoria_id INT REFERENCES categorias(id)
);
```

Agora o nome da categoria existe em um único lugar, e uma consulta com JOIN recupera a informação sem redundância:

```sql
SELECT p.nome, c.nome AS categoria
FROM produtos p
JOIN categorias c ON c.id = p.categoria_id;
```

> [!tip] Regra de bolso para lembrar 1FN → 2FN → 3FN
> 
> - **1FN**: cada célula tem um valor só (atomicidade)
> - **2FN**: cada coluna depende da chave **inteira** (relevante só com chave composta)
> - **3FN**: cada coluna depende **só** da chave, e de mais nada além dela (sem dependências transitivas)

## ⚖️ Até onde normalizar na prática

A maioria dos sistemas transacionais reais para na 3FN — é o ponto de equilíbrio entre eliminar redundância e manter as consultas razoavelmente simples (sem JOINs excessivos). Ir além (BCNF) só costuma ser necessário em casos específicos com múltiplas chaves candidatas sobrepostas — ver [[BD - Forma Normal de Boyce-Codd (BCNF)]].

## 🔗 Notas relacionadas

- [[BD - Segunda Forma Normal (2FN)]]
- [[BD - Forma Normal de Boyce-Codd (BCNF)]]
- [[BD - Desnormalização Consciente]]
- [[Banco de Dados]]