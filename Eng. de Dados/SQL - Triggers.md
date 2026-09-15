---

tags:

- banco-de-dados
- sql aliases: [Trigger, Gatilho]

---

# SQL - Triggers

## 📌 Conceito principal

Uma **trigger** (gatilho) é um bloco de código que o SGBD executa **automaticamente** em resposta a um evento em uma tabela (`INSERT`, `UPDATE`, `DELETE`) — sem que a aplicação precise chamar nada explicitamente.

## ⏱️ Eventos BEFORE e AFTER

```sql
-- BEFORE: executa antes da alteração acontecer (pode inclusive cancelá-la)
-- AFTER: executa depois que a alteração já foi persistida
```

## 💻 Exemplo prático — trigger de auditoria (AFTER)

```sql
CREATE TABLE auditoria_produtos (
    id SERIAL PRIMARY KEY,
    produto_id INT,
    preco_antigo NUMERIC(10,2),
    preco_novo NUMERIC(10,2),
    alterado_em TIMESTAMP DEFAULT NOW()
);

CREATE FUNCTION registrar_alteracao_preco()
RETURNS TRIGGER AS $$
BEGIN
    IF OLD.preco IS DISTINCT FROM NEW.preco THEN
        INSERT INTO auditoria_produtos (produto_id, preco_antigo, preco_novo)
        VALUES (OLD.id, OLD.preco, NEW.preco);
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_auditoria_preco
AFTER UPDATE ON produtos
FOR EACH ROW
EXECUTE FUNCTION registrar_alteracao_preco();
```

> [!note] OLD e NEW Dentro de uma trigger, `OLD` representa o valor da linha **antes** da alteração e `NEW` o valor **depois**. Em triggers de `DELETE`, só `OLD` existe; em `INSERT`, só `NEW` existe.

## 🛡️ Exemplo prático — validação com BEFORE (pode bloquear a operação)

```sql
CREATE FUNCTION impedir_preco_negativo()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.preco < 0 THEN
        RAISE EXCEPTION 'Preço não pode ser negativo';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_valida_preco
BEFORE INSERT OR UPDATE ON produtos
FOR EACH ROW
EXECUTE FUNCTION impedir_preco_negativo();
```

## ✅ Casos de uso legítimos

- Auditoria de alterações (histórico de mudanças, ver [[Recipe - Auditoria de Alterações]])
- Manutenção de colunas derivadas/desnormalizadas (ver [[BD - Desnormalização Consciente]])
- Validações de regra de negócio que precisam valer **sempre**, independente de qual aplicação insere os dados

## ⚠️ Riscos de triggers

> [!warning] "Lógica invisível" é o maior risco Triggers rodam silenciosamente, sem aparecer no código da aplicação — um desenvolvedor lendo a query de `INSERT` não vê que uma trigger está fazendo outras alterações por trás. Isso torna o sistema mais difícil de depurar e de entender por completo. Use triggers com moderação, e sempre documente sua existência de forma visível (nesta mesma nota do vault, por exemplo).

> [!warning] Cadeia de triggers Uma trigger pode disparar uma alteração que aciona outra trigger, e assim por diante — cadeias longas e difíceis de rastrear são uma fonte clássica de bugs sutis em bancos de produção.

## 🔗 Notas relacionadas

- [[SQL - Stored Procedures e Functions]]
- [[Recipe - Auditoria de Alterações]]
- [[BD - Desnormalização Consciente]]
- [[Banco de Dados]]