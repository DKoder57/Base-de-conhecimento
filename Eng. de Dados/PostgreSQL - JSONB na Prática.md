---

tags:

- banco-de-dados
- postgresql aliases: [JSONB na Prática, Consultas JSONB]

---

# PostgreSQL - JSONB na Prática

## 📌 Conceito principal

`JSONB` armazena dados JSON em formato **binário decomposto**, permitindo consultas eficientes e indexação — diferente do tipo `JSON` (texto puro, reprocessado a cada leitura). Na prática, `JSONB` é quase sempre a escolha certa sobre `JSON` no PostgreSQL.

> [!info] JSON vs. JSONB A documentação oficial do PostgreSQL recomenda `JSONB` para a maioria das aplicações, a menos que seja necessário preservar a formatação exata do texto original (espaços, ordem de chaves) — algo que o `JSONB` não mantém, por reorganizar os dados internamente. Fonte: [postgresql.org/docs — Tipos JSON](https://www.postgresql.org/docs/current/datatype-json.html)

## 🔍 Operadores de consulta

```sql
CREATE TABLE produtos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100),
    atributos JSONB
);

INSERT INTO produtos (nome, atributos) VALUES
    ('Tênis', '{"cor": "preto", "tamanho": 42, "marca": "XYZ"}');
```

```sql
-- Acessar uma chave (retorna JSONB)
SELECT atributos -> 'cor' FROM produtos;

-- Acessar uma chave e converter para texto
SELECT atributos ->> 'cor' FROM produtos;

-- Verificar se contém um valor específico
SELECT * FROM produtos WHERE atributos @> '{"cor": "preto"}';

-- Verificar se uma chave existe
SELECT * FROM produtos WHERE atributos ? 'marca';

-- Acessar caminho aninhado
SELECT atributos #> '{especificacoes,peso}' FROM produtos;
```

## ⚡ Indexando JSONB

```sql
-- Índice GIN indexa TODAS as chaves/valores do documento
CREATE INDEX idx_produtos_atributos ON produtos USING GIN (atributos);

-- Índice em um caminho específico (mais leve, se só um campo é consultado com frequência)
CREATE INDEX idx_produtos_cor ON produtos ((atributos ->> 'cor'));
```

Ver contexto mais amplo sobre esse tipo de índice em [[BD - Índices Hash, GIN e GiST]].

## ✏️ Atualizando dados dentro de um JSONB

```sql
-- Atualizar/adicionar uma chave específica sem reescrever o documento inteiro
UPDATE produtos
SET atributos = jsonb_set(atributos, '{cor}', '"azul"')
WHERE id = 1;

-- Remover uma chave
UPDATE produtos
SET atributos = atributos - 'marca'
WHERE id = 1;
```

## ⚖️ Quando usar JSONB (e quando não usar)

> [!tip] Bons casos de uso
> 
> - Atributos de produto que variam por categoria (roupa tem "tamanho", eletrônico tem "voltagem")
> - Metadados de configuração de um usuário/aplicação
> - Payloads de eventos/webhooks recebidos de sistemas externos

> [!warning] Não use JSONB para modelar seu domínio principal Se um "atributo" precisa ser consultado, relacionado ou validado como uma entidade própria (ex.: categoria de produto com nome e regras), ele deveria ser uma tabela relacional normal, não uma chave dentro de um JSONB — ver [[BD - Relacional vs NoSQL]]. JSONB é ótimo para o que é genuinamente variável, não para fugir de modelar direito.

## 🔗 Notas relacionadas

- [[PostgreSQL - Tipos Avançados]]
- [[BD - Índices Hash, GIN e GiST]]
- [[BD - Relacional vs NoSQL]]
- [[Banco de Dados]]