---

tags:

- banco-de-dados
- sql aliases: [Stored Procedure, Function, PL/pgSQL, Procedimento Armazenado]

---

# SQL - Stored Procedures e Functions

## 📌 Conceito principal

**Functions** e **stored procedures** permitem colocar lógica de negócio **dentro do banco de dados**, executada com uma chamada simples, em vez de repetir a mesma lógica em SQL solto ou em código de aplicação.

## 🔧 Function (PostgreSQL, PL/pgSQL)

Uma function sempre **retorna um valor** e pode ser usada dentro de um `SELECT`.

```sql
CREATE FUNCTION calcular_desconto(preco NUMERIC, percentual NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
    RETURN preco - (preco * percentual / 100);
END;
$$ LANGUAGE plpgsql;

-- Uso
SELECT nome, calcular_desconto(preco, 10) AS preco_com_desconto
FROM produtos;
```

## ⚙️ Procedure (PostgreSQL 11+)

Uma procedure **não retorna valor** diretamente e pode controlar suas próprias transações (`COMMIT`/`ROLLBACK` internos) — algo que uma function não pode fazer.

```sql
CREATE PROCEDURE aplicar_desconto_categoria(cat_id INT, percentual NUMERIC)
LANGUAGE plpgsql AS $$
BEGIN
    UPDATE produtos
    SET preco = preco - (preco * percentual / 100)
    WHERE categoria_id = cat_id;

    COMMIT;
END;
$$;

-- Uso
CALL aplicar_desconto_categoria(3, 15);
```

|Critério|Function|Procedure|
|---|---|---|
|Retorna valor|Sim|Não (ou via parâmetros `OUT`)|
|Pode usar `COMMIT`/`ROLLBACK` interno|Não|Sim|
|Chamada|Dentro de `SELECT`|Via `CALL`|
|Uso típico|Cálculos reutilizáveis|Rotinas de manutenção/batch|

## ⚠️ Quando vale (e quando não vale) colocar lógica no banco

> [!tip] Bons casos de uso
> 
> - Validações complexas que precisam ser garantidas independentemente de qual aplicação acessa o banco
> - Rotinas de manutenção pesadas que evitam trafegar grandes volumes de dados entre banco e aplicação
> - Cálculos usados por várias aplicações diferentes que acessam o mesmo banco

> [!warning] Riscos de abusar de lógica no banco
> 
> - Fica mais difícil de testar, versionar e revisar em code review comparado a código na aplicação
> - Cria acoplamento forte a um SGBD específico (PL/pgSQL não roda em MySQL)
> - Dificulta escalar a camada de aplicação horizontalmente sem sobrecarregar o banco

Muitos times modernos preferem manter lógica de negócio na aplicação e reservar functions/procedures para casos onde a proximidade com o dado realmente compensa (validações críticas, triggers de auditoria).

## 🔗 Notas relacionadas

- [[SQL - Triggers]]
- [[BD - Transações (BEGIN, COMMIT, ROLLBACK)]]
- [[PostgreSQL - Funções e Triggers em PL/pgSQL]]
- [[Banco de Dados]]