---

tags:

- banco-de-dados
- modelagem aliases: [MER, Diagrama ER, Entity-Relationship Model, DER]

---

# BD - Modelo Entidade-Relacionamento (MER)

## 📌 Conceito principal

O **Modelo Entidade-Relacionamento (MER)**, proposto por Peter Chen em 1976, é a forma padrão de representar visualmente entidades, atributos e relacionamentos identificados no [[BD - Modelo Conceitual]], através de um diagrama (DER — Diagrama Entidade-Relacionamento).

## 🎨 Notações mais usadas

### Notação de Peter Chen (clássica)

- **Retângulos** representam entidades
- **Elipses** representam atributos
- **Losangos** representam relacionamentos
- Linhas conectam entidades aos relacionamentos, com a cardinalidade escrita ao lado

### Notação Crow's Foot ("pé de galinha")

- Mais usada em ferramentas modernas (dbdiagram.io, MySQL Workbench, DBeaver)
- Entidades são retângulos com os atributos listados dentro
- Relacionamentos são linhas diretas entre entidades
- A cardinalidade é representada por símbolos no final da linha (um traço = "um", um "pé de galinha" = "muitos")

> [!tip] Qual notação usar Peter Chen é ótima para ensinar o conceito (mais explícita), mas Crow's Foot é o padrão de fato nas ferramentas de mercado — vale se acostumar com ela para ler diagramas de ferramentas reais.

## 🧩 Elementos de uma entidade no diagrama

- **Entidade forte**: existe por si só (Cliente, Produto)
- **Entidade fraca**: depende da existência de outra entidade (Item_Pedido não existe sem Pedido)
- **Atributo simples**: não pode ser dividido (idade)
- **Atributo composto**: pode ser dividido em partes (endereço → rua, número, cidade)
- **Atributo multivalorado**: pode ter mais de um valor (telefones de um cliente)
- **Atributo derivado**: calculado a partir de outro (idade derivada da data de nascimento)

## 💻 Exemplo prático — MER em notação Crow's Foot (texto)

```
┌─────────────┐        ┌──────────────┐        ┌─────────────┐
│   CLIENTE   │        │    PEDIDO    │        │   PRODUTO   │
├─────────────┤   1  N ├──────────────┤ N    N ├─────────────┤
│ id (PK)     │───────<│ id (PK)      │>──────<│ id (PK)     │
│ nome        │        │ cliente_id   │        │ nome        │
│ email       │        │ data         │        │ preco       │
└─────────────┘        │ status       │        └─────────────┘
                        └──────────────┘
```

Esse relacionamento N:N entre Pedido e Produto exige uma **tabela associativa** (ver [[BD - Cardinalidades e Relacionamentos]]) quando for convertido para o [[BD - Modelo Lógico]].

## 🔗 Notas relacionadas

- [[BD - Modelo Conceitual]]
- [[BD - Cardinalidades e Relacionamentos]]
- [[BD - Chaves]]
- [[BD - Modelo Lógico]]
- [[Banco de Dados]]