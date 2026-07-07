---
tags: [cyber, writeup, dvwa, modelo]
área: Cibersegurança / Prática (nota avulsa)
status: draft
oculta_da_matriz: true

---

# 📝 Writeup Exemplo — DVWA: SQL Injection (Nível Low)

> [!quote] Princípio Um bom writeup não é sobre "quebrar o sistema" — é sobre documentar raciocínio de forma que outra pessoa (ou você mesmo, 6 meses depois) entenda o processo.

> [!NOTE] Nota fora da matriz principal Esta nota não está listada em `[[Cybersecurity]]`. Acesse-a via [[Cyber - Ambientes de Prática Legal]]. Ambiente: **DVWA rodando localmente via Docker**, de propósito vulnerável para fins didáticos.

---

## 🎯 Objetivo

Demonstrar o formato padrão de writeup, usando o módulo de **SQL Injection** do DVWA em nível de segurança **Low** como exemplo — o cenário clássico de introdução ao tópico.

---

## 1️⃣ Reconhecimento

O DVWA, após login, expõe um módulo "SQL Injection" com um campo de busca por **User ID**, que consulta um banco de dados de usuários.

```
URL: http://localhost/vulnerabilities/sqli/?id=1&Submit=Submit#
```

Testando o campo com um valor simples (`1`) retorna os dados de um usuário — indicando que o parâmetro `id` provavelmente é usado diretamente em uma consulta SQL no back-end.

---

## 2️⃣ Vulnerabilidade Identificada

Testando o campo com uma aspa simples (`'`) no lugar de um ID válido, a aplicação retorna um erro de sintaxe SQL — sinal clássico de que a entrada não está sendo tratada com consulta parametrizada (o mesmo conceito visto em [[Cyber - Ataques em Aplicações Web]]).

---

## 3️⃣ Exploração (ambiente autorizado)

Usando `' OR '1'='1` no campo, a condição da cláusula `WHERE` se torna sempre verdadeira, retornando todos os registros da tabela em vez de apenas um usuário:

```
id: ' OR '1'='1
```

> [!NOTE] Por que isso funciona A aplicação (nível Low, sem nenhum tratamento) provavelmente monta a query como: `SELECT * FROM users WHERE user_id = '` + entrada + `'` Ao inserir `' OR '1'='1`, a consulta final vira `WHERE user_id = '' OR '1'='1'`, que é sempre verdadeira para qualquer linha da tabela.

---

## 4️⃣ Pós-exploração (nesse contexto de laboratório)

Nesse módulo específico do DVWA, a "pós-exploração" natural é demonstrar extração de mais dados usando `UNION SELECT`, técnica amplamente documentada nos próprios materiais oficiais do DVWA e no PortSwigger Web Security Academy — recomendo seguir esses dois recursos para o passo a passo completo dessa técnica, já que são a referência oficial e mantêm o conteúdo atualizado.

---

## 5️⃣ Lições Aprendidas / Como se Defenderia

- A causa raiz é **concatenação direta de entrada do usuário em SQL**
- A correção correta é usar **consultas parametrizadas** (prepared statements) — nunca sanitização manual de aspas como única defesa
- Um **WAF** (Web Application Firewall) reduziria o risco, mas não substitui a correção no código
- Testar o nível "Medium" e "High" do próprio DVWA depois é um ótimo exercício, pois cada nível implementa uma defesa incremental diferente — vendo como cada uma pode ou não ser contornada

---

## 🔗 Notas Relacionadas

- [[Cyber - Ambientes de Prática Legal]]
- [[Cyber - Ataques em Aplicações Web]]
- [[Cyber - Criptografia e Senhas]]