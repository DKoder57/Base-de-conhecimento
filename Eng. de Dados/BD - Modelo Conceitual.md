---

tags:

- banco-de-dados
- modelagem aliases: [Modelagem Conceitual]

---

# BD - Modelo Conceitual

## 📌 Conceito principal

O **modelo conceitual** é a primeira etapa da modelagem de dados: uma representação abstrata e independente de tecnologia do que precisa ser armazenado, focada em **entender o domínio do problema** — não em como isso vai virar tabelas.

> [!note] Ordem correta da modelagem Modelo **Conceitual** (o quê existe) → Modelo **Lógico** (como se relaciona, ainda sem SGBD específico) → Modelo **Físico** (SQL de fato, com tipos e constraints do SGBD escolhido). Pular direto para SQL sem passar pelo conceitual é a causa mais comum de modelagem ruim.

## 🧩 Elementos do modelo conceitual

- **Entidades**: "coisas" do domínio que precisam ser armazenadas (Cliente, Pedido, Produto).
- **Atributos**: características de uma entidade (Cliente tem nome, e-mail, data de cadastro).
- **Relacionamentos**: como as entidades se conectam (Cliente **faz** Pedido).

## 🔍 Levantamento de requisitos

Antes de desenhar qualquer diagrama, é preciso responder:

1. Quais são as principais "coisas" que o sistema precisa lembrar?
2. Quais informações sobre cada uma delas são realmente necessárias?
3. Como essas coisas se relacionam entre si?
4. Quais regras de negócio afetam esses relacionamentos? (Ex.: "um pedido não pode existir sem cliente", "um produto pode estar em vários pedidos")

> [!tip] Técnica prática Liste substantivos do problema (viram entidades ou atributos) e verbos que conectam esses substantivos (viram relacionamentos). "Um **cliente** **faz** um **pedido** que **contém** vários **produtos**" já revela 3 entidades e 2 relacionamentos.

## 💻 Exemplo prático — de requisito a modelo conceitual

**Requisito**: "Precisamos de um sistema onde clientes fazem pedidos, e cada pedido pode ter vários produtos, com a quantidade de cada um."

**Entidades identificadas**: Cliente, Pedido, Produto **Atributos identificados**:

- Cliente: nome, e-mail
- Pedido: data, status
- Produto: nome, preço

**Relacionamentos identificados**:

- Cliente → faz → Pedido (1:N)
- Pedido → contém → Produto (N:N, com atributo "quantidade" no relacionamento)

Esse texto já é suficiente para avançar para o [[BD - Modelo Entidade-Relacionamento (MER)]], onde isso vira um diagrama formal.

## 🔗 Notas relacionadas

- [[BD - Modelo Entidade-Relacionamento (MER)]]
- [[BD - Cardinalidades e Relacionamentos]]
- [[BD - Modelo Lógico]]
- [[Banco de Dados]]