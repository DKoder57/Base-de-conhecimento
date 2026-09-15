---

tags:

- banco-de-dados
- normalizacao aliases: [BCNF, Boyce-Codd Normal Form]

---

# BD - Forma Normal de Boyce-Codd (BCNF)

## 📌 Conceito principal

A **BCNF** é uma versão mais rigorosa da [[BD - Terceira Forma Normal (3FN)]]. Uma tabela pode satisfazer a 3FN e ainda assim ter anomalias — isso acontece quando existem **múltiplas chaves candidatas que se sobrepõem**. A BCNF exige que, para toda dependência funcional `A → B`, `A` seja uma **superchave** (um conjunto de atributos que determina unicamente toda a tabela).

> [!note] Regra da BCNF Uma tabela está em BCNF quando, para toda dependência funcional não trivial `X → Y`, `X` é uma superchave. Em outras palavras: nada pode determinar outra coisa a menos que esse "nada" já seja (ou contenha) uma chave.

## ❌ Exemplo clássico de violação (3FN satisfeita, mas BCNF não)

```
aulas(aluno_id, disciplina, professor)
```

Regras do domínio:

- Cada professor leciona apenas uma disciplina
- Uma disciplina pode ter vários professores diferentes (turmas diferentes)
- Um aluno pode cursar a mesma disciplina com professores diferentes em turmas diferentes

Dependências funcionais:

- `(aluno_id, disciplina) → professor` (chave candidata)
- `professor → disciplina` (mas `professor` **não é** uma superchave — não determina `aluno_id`)

A tabela está em 3FN (não há dependência transitiva entre atributos não-chave), mas viola BCNF porque `professor → disciplina` tem do lado esquerdo um atributo que não é superchave.

**Problema prático**: se um professor mudar de disciplina, é preciso atualizar todas as linhas dele — redundância que a 3FN não capturou, mas a BCNF captura.

## ✅ Correção — decompondo em duas tabelas

```sql
CREATE TABLE professores (
    professor VARCHAR(100) PRIMARY KEY,
    disciplina VARCHAR(100)
);

CREATE TABLE matriculas (
    aluno_id INT,
    professor VARCHAR(100) REFERENCES professores(professor),
    PRIMARY KEY (aluno_id, professor)
);
```

Agora `professor → disciplina` vive isolado em uma tabela onde `professor` é a própria chave — satisfazendo BCNF.

> [!warning] BCNF é raro na prática do dia a dia A maioria dos sistemas transacionais comerciais para na 3FN, que já resolve praticamente todas as anomalias de redundância do cotidiano. BCNF costuma aparecer em casos acadêmicos ou domínios muito específicos com múltiplas chaves candidatas sobrepostas — vale conhecer o conceito, mas não é necessário perseguir BCNF como meta padrão de todo projeto.

## 🔗 Notas relacionadas

- [[BD - Terceira Forma Normal (3FN)]]
- [[BD - Dependência Funcional]]
- [[BD - Desnormalização Consciente]]
- [[Banco de Dados]]