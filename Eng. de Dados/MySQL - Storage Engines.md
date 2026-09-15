---

tags:

- banco-de-dados
- mysql aliases: [InnoDB, MyISAM, Storage Engine, Mecanismo de Armazenamento]

---

# MySQL - Storage Engines

## 📌 Conceito principal

Diferente do PostgreSQL (que tem um único motor de armazenamento interno), o MySQL permite escolher o **storage engine** por tabela — o componente que efetivamente controla como os dados são gravados, indexados e recuperados em disco.

> [!info] Fonte oficial A documentação oficial do MySQL (MySQL Reference Manual) descreve o InnoDB como o storage engine padrão desde o MySQL 5.5, recomendado para a maioria dos casos de uso por oferecer conformidade com ACID e suporte a chaves estrangeiras. Fonte: [dev.mysql.com/doc/refman — InnoDB](https://dev.mysql.com/doc/refman/en/innodb-storage-engine.html)

## 🏆 InnoDB — o padrão atual

- Suporta **transações** completas ([[BD - ACID]])
- Suporta **chaves estrangeiras** com integridade referencial
- Usa **locking a nível de linha** (não trava a tabela inteira em escritas concorrentes)
- É o engine padrão desde o MySQL 5.5 — praticamente toda tabela nova deveria usar InnoDB

```sql
CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
) ENGINE=InnoDB;
```

## 📜 MyISAM — motor legado

- **Não suporta transações** nem chaves estrangeiras
- Usa locking a nível de **tabela inteira** (pior para concorrência de escrita)
- Historicamente mais rápido em leituras simples e full-text search antigo, mas essa vantagem praticamente desapareceu com as versões modernas do InnoDB

```sql
CREATE TABLE logs_legado (
    id INT AUTO_INCREMENT PRIMARY KEY,
    mensagem TEXT
) ENGINE=MyISAM;
```

> [!warning] Quando encontrar MyISAM na prática Praticamente só em sistemas legados antigos, muitas vezes ligados a instalações antigas de WordPress ou aplicações PHP mais antigas. Para qualquer projeto novo, não há motivo para escolher MyISAM sobre InnoDB.

## ⚖️ Comparativo direto

|Critério|InnoDB|MyISAM|
|---|---|---|
|Transações (ACID)|Sim|Não|
|Chaves estrangeiras|Sim|Não|
|Locking|Nível de linha|Nível de tabela|
|Recomendado para projetos novos|Sim|Não|

## 🔍 Verificando o engine de uma tabela existente

```sql
SHOW TABLE STATUS WHERE Name = 'pedidos';

-- Ou consultando diretamente o catálogo do sistema
SELECT table_name, engine
FROM information_schema.tables
WHERE table_schema = 'meu_banco';
```

## 🔗 Notas relacionadas

- [[BD - ACID]]
- [[MySQL - Particularidades de Sintaxe]]
- [[MySQL - Replicação]]
- [[Banco de Dados]]