---
---
---
tags:

- banco-de-dados
- fundamentos aliases: Dado Informação Conhecimento, DIKW

---

# BD - Dado, Informação e Conhecimento

## 📌 Conceito principal

Antes de falar em banco de dados, é preciso distinguir três níveis que costumam ser confundidos:

- **Dado**: um registro bruto, sem contexto. Ex.: `28`, `"João"`, `2026-07-20`.
- **Informação**: dado com contexto e significado. Ex.: "João tem 28 anos e fez seu cadastro em 20/07/2026".
- **Conhecimento**: informação combinada com experiência/análise, usada para tomar decisão. Ex.: "clientes na faixa de 25-30 anos compram mais no fim de semana, então vale reforçar campanhas de sexta a domingo".

Isso é frequentemente representado pela **pirâmide DIKW** (Data → Information → Knowledge → Wisdom).

> [!note] Por que isso importa para banco de dados Um SGBD armazena e organiza **dados**. Cabe à modelagem, às consultas (SQL) e às ferramentas de análise transformar esses dados em **informação**. O **conhecimento** normalmente vem de fora do banco — de quem interpreta os relatórios e toma decisões com base neles.

## 🔄 Ciclo de vida do dado

Todo dado, dentro de um sistema, passa por fases previsíveis:

1. **Coleta** — o dado entra no sistema (formulário, API, sensor, importação).
2. **Armazenamento** — é persistido em um SGBD ou arquivo.
3. **Processamento** — é transformado, agregado, cruzado com outros dados.
4. **Uso/Distribuição** — é consumido por relatórios, dashboards, outras aplicações.
5. **Arquivamento ou descarte** — dados antigos são movidos para armazenamento frio ou apagados (retenção, LGPD/GDPR).

> [!tip] Aplicação prática Ao modelar um banco, pense em qual fase do ciclo de vida cada tabela representa. Dados "quentes" (muito acessados) merecem índices e otimização; dados "frios" (histórico raramente consultado) podem ir para armazenamento mais barato — isso conecta diretamente com o Nível 7 (Índices e Performance) e com [[Cloud para Dados - Matriz da Trilha]].

## 💻 Exemplo prático

```sql
-- Dado bruto (uma linha na tabela)
SELECT * FROM clientes WHERE id = 42;
-- id | nome | idade | cidade
-- 42 | João | 28    | Itabira

-- Informação (dado com contexto agregado)
SELECT cidade, AVG(idade) AS idade_media
FROM clientes
GROUP BY cidade;
-- cidade    | idade_media
-- Itabira   | 27.4

-- "Conhecimento" viria da análise humana desse resultado:
-- "clientes de Itabira são, em média, mais jovens que os de outras cidades —
--  vale ajustar a comunicação de marketing para esse público."
```

## 🔗 Notas relacionadas

- [[BD - O que é um SGBD]]
- [[BD - Modelos de Dados]]
- [[Banco de Dados]]