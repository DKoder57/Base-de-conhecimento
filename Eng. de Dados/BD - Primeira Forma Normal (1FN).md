---

tags:

- banco-de-dados
- normalizacao aliases: [1FN, First Normal Form, 1NF]

---

# BD - Primeira Forma Normal (1FN)

## 📌 Conceito principal

Uma tabela está na **Primeira Forma Normal (1FN)** quando todos os seus atributos contêm apenas **valores atômicos** (indivisíveis) — ou seja, nenhuma coluna guarda múltiplos valores, listas ou estruturas aninhadas.

## ❌ Exemplo de violação da 1FN

```
clientes(id, nome, telefones)

id | nome  | telefones
1  | João  | "31999990000, 31988887777"
```

A coluna `telefones` guarda mais de um valor na mesma célula — isso viola a atomicidade exigida pela 1FN. Buscar "quem tem o telefone 31988887777" exigiria manipulação de texto em vez de uma consulta relacional simples.

## ✅ Correção — separando em uma tabela relacionada

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

Agora cada telefone é uma linha própria, atômica, e pode ser consultada normalmente:

```sql
SELECT c.nome, t.numero
FROM clientes c
JOIN telefones_cliente t ON t.cliente_id = c.id
WHERE t.numero = '31988887777';
```

## 🔍 Outras violações comuns da 1FN

- Colunas repetidas para representar uma lista: `telefone1`, `telefone2`, `telefone3`
- Um campo de texto com valores separados por vírgula (`"tag1, tag2, tag3"`)
- Colunas que misturam tipos diferentes de informação em um único campo (`"João - 28 anos - Itabira"`)

> [!warning] Colunas telefone1/telefone2/telefone3 Esse padrão parece resolver o problema, mas na verdade só disfarça a violação: e se um cliente tiver 4 telefones? A estrutura não escala e ainda gera colunas vazias (`NULL`) para quem tem menos telefones. A solução correta é sempre uma tabela relacionada 1:N.

> [!tip] Exceção consciente: JSONB Bancos modernos como o PostgreSQL permitem guardar listas em colunas `JSONB` de forma deliberada, quando o caso de uso realmente pede flexibilidade de schema (ver [[PostgreSQL - JSONB na Prática]]). Isso é diferente de "violar a 1FN por descuido" — é uma escolha consciente de desnormalização, tratada em [[BD - Desnormalização Consciente]].

## 🔗 Notas relacionadas

- [[BD - Dependência Funcional]]
- [[BD - Segunda Forma Normal (2FN)]]
- [[PostgreSQL - JSONB na Prática]]
- [[Banco de Dados]]