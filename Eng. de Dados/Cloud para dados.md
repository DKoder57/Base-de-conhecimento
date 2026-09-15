---
tags:
  - cloud
  - engenharia-de-dados
  - aws
  - gcp
  - azure
  - matriz
---
# ☁️ Cloud para Dados 

> Construir conhecimento reutilizável, não apenas concluir cursos.

---

> [!info] O que cobre esta trilha **Cloud para Dados** cobre os serviços de armazenamento, processamento, orquestração e governança de dados nos três grandes provedores — **AWS**, **GCP** e **Azure** — com foco no que é comum entre eles (conceitos de object storage, data warehouse, lake, streaming) e no que é específico de cada um (S3/Redshift, BigQuery/Cloud Storage, Synapse/Data Lake Storage).

> [!abstract] Objetivo desta trilha Organizar o estudo de serviços de dados em nuvem de forma progressiva, priorizando entender o problema que cada categoria de serviço resolve — antes de decorar nomes de produtos — e aplicar isso em laboratórios reais nas contas gratuitas de cada provedor.

---

## 🧠 Como usar esta matriz

Cada nota é uma unidade independente de conhecimento. Fluxo recomendado:

**Teoria → Exemplo → Laboratório (free tier) → Projeto → Documentação própria**

Uma nota só é considerada concluída depois de aplicada em laboratório ou projeto real — cloud é uma área onde ler documentação sem colocar a mão em um console/CLI rende pouco.

```text
Fundamentos de Cloud → IAM e Segurança → Armazenamento (Object Storage)
→ Processamento Distribuído → Data Warehouse → Data Lake e Lakehouse
→ Orquestração e ETL → Streaming → Governança e Custos (FinOps)
→ Multi-Cloud → Laboratórios → Receitas → Projetos
```

---

## 📚 Resumo da matriz

|Nível|Área|Resumo|
|:--|:--|:--|
|🌱 1|Fundamentos de Cloud|Modelos de serviço (IaaS/PaaS/SaaS), regiões, zonas, custos sob demanda|
|🌿 2|IAM e Segurança|Identidade, papéis, políticas, princípio do menor privilégio|
|🌿 3|Armazenamento (Object Storage)|S3, Cloud Storage, Blob Storage — classes de armazenamento, ciclo de vida|
|🌳 4|Processamento Distribuído|EMR, Dataproc, HDInsight, Spark gerenciado|
|🌳 5|Data Warehouse na Nuvem|Redshift, BigQuery, Synapse Analytics, Snowflake|
|🌳 6|Data Lake e Lakehouse|Data Lake, Delta Lake, Iceberg, catálogo de dados|
|🌳 7|Orquestração e ETL Gerenciado|Glue, Data Factory, Dataflow, Cloud Composer/MWAA|
|🌳 8|Streaming na Nuvem|Kinesis, Pub/Sub, Event Hubs|
|🏆 9|Governança e Qualidade de Dados|Catálogo de dados, linhagem, mascaramento, LGPD/GDPR|
|🏆 10|Custos e FinOps de Dados|Modelos de precificação, otimização de custo, egress|
|🏆 11|Multi-Cloud e Portabilidade|Estratégias multi-cloud, ferramentas agnósticas, migração entre nuvens|
|🔬 12|Laboratórios|Experimentação prática isolada (free tier)|
|📖 13|Receitas|Implementações reutilizáveis de consulta rápida|
|🚀 14|Projetos|Pipelines de dados completos na nuvem|
|👑 15|Certificações|Trilhas de certificação oficiais por provedor|

---

# 🌱 NÍVEL 1 — FUNDAMENTOS DE CLOUD

|#|Nota|Tópicos|
|:--|:--|:--|
|1.1|[[Cloud - IaaS, PaaS e SaaS]]|Modelos de serviço, responsabilidade compartilhada|
|1.2|[[Cloud - Regiões e Zonas de Disponibilidade]]|Latência, redundância, escolha de região|
|1.3|[[Cloud - Modelos de Precificação]]|Pay-as-you-go, reservado, spot/preemptible|
|1.4|[[Cloud - AWS, GCP e Azure — Panorama]]|Equivalência de serviços entre os três provedores|
|1.5|[[Cloud - CLI e Consoles]]|`aws cli`, `gcloud`, `az cli`, uso via console vs. IaC|

---

# 🌿 NÍVEL 2 — IAM E SEGURANÇA

|#|Nota|Tópicos|
|:--|:--|:--|
|2.1|[[Cloud - IAM — Conceitos Gerais]]|Identidade, autenticação, autorização|
|2.2|[[AWS - IAM]]|Users, Groups, Roles, Policies|
|2.3|[[GCP - IAM]]|Contas de serviço, papéis predefinidos e customizados|
|2.4|[[Azure - Entra ID (Azure AD)]]|Identidades gerenciadas, RBAC|
|2.5|[[Cloud - Princípio do Menor Privilégio]]|Boas práticas de concessão de acesso a dados|

---

# 🌿 NÍVEL 3 — ARMAZENAMENTO (OBJECT STORAGE)

|#|Nota|Tópicos|
|:--|:--|:--|
|3.1|[[AWS - S3]]|Buckets, classes de armazenamento, versionamento|
|3.2|[[GCP - Cloud Storage]]|Buckets, classes de armazenamento, políticas de acesso|
|3.3|[[Azure - Blob Storage]]|Containers, tiers (hot/cool/archive)|
|3.4|[[Cloud - Políticas de Ciclo de Vida]]|Transição automática entre classes, expiração de objetos|
|3.5|[[Cloud - Formatos de Arquivo para Dados]]|Parquet, Avro, ORC, CSV/JSON — quando usar cada um|

---

# 🌳 NÍVEL 4 — PROCESSAMENTO DISTRIBUÍDO

|#|Nota|Tópicos|
|:--|:--|:--|
|4.1|[[AWS - EMR]]|Clusters Hadoop/Spark gerenciados|
|4.2|[[GCP - Dataproc]]|Spark/Hadoop gerenciado no GCP|
|4.3|[[Azure - HDInsight]]|Big data gerenciado no Azure|
|4.4|[[Cloud - Spark Serverless]]|AWS Glue Jobs, GCP Dataproc Serverless, Databricks|
|4.5|[[Cloud - Escalonamento de Clusters]]|Autoscaling, custo vs. performance|

---

# 🌳 NÍVEL 5 — DATA WAREHOUSE NA NUVEM

|#|Nota|Tópicos|
|:--|:--|:--|
|5.1|[[AWS - Redshift]]|Arquitetura MPP, RA3 nodes, Spectrum|
|5.2|[[GCP - BigQuery]]|Serverless, separação compute/storage, slots|
|5.3|[[Azure - Synapse Analytics]]|Pools dedicados e serverless|
|5.4|[[Cloud - Snowflake]]|Warehouse multi-cloud, arquitetura de camadas|
|5.5|[[Cloud - Comparativo de Data Warehouses]]|Redshift vs. BigQuery vs. Synapse vs. Snowflake — quando escolher cada um|
|5.6|[[Cloud - Views Materializadas e Cache]]|Otimização de custo e performance em consultas analíticas|

---

# 🌳 NÍVEL 6 — DATA LAKE E LAKEHOUSE

|#|Nota|Tópicos|
|:--|:--|:--|
|6.1|[[Cloud - Data Lake — Conceitos]]|Diferença entre data lake e data warehouse|
|6.2|[[Cloud - Delta Lake]]|Transações ACID sobre object storage|
|6.3|[[Cloud - Apache Iceberg]]|Tabelas abertas, evolução de schema|
|6.4|[[Cloud - Lakehouse]]|Arquitetura híbrida (Databricks, BigLake)|
|6.5|[[Cloud - Catálogo de Dados]]|AWS Glue Data Catalog, GCP Data Catalog, Azure Purview|

---

# 🌳 NÍVEL 7 — ORQUESTRAÇÃO E ETL GERENCIADO

|#|Nota|Tópicos|
|:--|:--|:--|
|7.1|[[AWS - Glue]]|ETL serverless, crawlers, jobs|
|7.2|[[GCP - Dataflow]]|Apache Beam gerenciado, batch e streaming unificados|
|7.3|[[Azure - Data Factory]]|Pipelines visuais, integration runtimes|
|7.4|[[Cloud - Airflow Gerenciado]]|AWS MWAA, GCP Cloud Composer|
|7.5|[[Cloud - ETL vs. ELT na Nuvem]]|Quando transformar antes ou depois da carga|

---

# 🌳 NÍVEL 8 — STREAMING NA NUVEM

|#|Nota|Tópicos|
|:--|:--|:--|
|8.1|[[AWS - Kinesis]]|Data Streams, Firehose, Analytics|
|8.2|[[GCP - Pub/Sub]]|Publicação/assinatura, entrega at-least-once|
|8.3|[[Azure - Event Hubs]]|Ingestão de eventos em larga escala|
|8.4|[[Cloud - Kafka Gerenciado]]|Amazon MSK, Confluent Cloud|
|8.5|[[Cloud - Streaming vs. Batch]]|Trade-offs de latência, custo e complexidade|

---

# 🏆 NÍVEL 9 — GOVERNANÇA E QUALIDADE DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|9.1|[[Cloud - Linhagem de Dados (Data Lineage)]]|Rastreabilidade de origem e transformação|
|9.2|[[Cloud - Mascaramento e Anonimização]]|Proteção de dados sensíveis em ambientes analíticos|
|9.3|[[Cloud - LGPD e GDPR na Prática]]|Requisitos de conformidade aplicados a arquiteturas de dados|
|9.4|[[Cloud - Qualidade de Dados]]|Validação, contratos de dados, testes automatizados|
|9.5|[[Azure - Purview]]|Governança unificada de dados no Azure|

---

# 🏆 NÍVEL 10 — CUSTOS E FINOPS DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|10.1|[[Cloud - Custos de Egress]]|Transferência de dados entre nuvens/regiões|
|10.2|[[Cloud - Otimização de Custo em Warehouses]]|Slots reservados, RA3, autoscaling de warehouse|
|10.3|[[Cloud - Tagging e Alocação de Custos]]|Rastreamento de custo por time/projeto|
|10.4|[[Cloud - Ferramentas de FinOps]]|AWS Cost Explorer, GCP Billing, Azure Cost Management|

---

# 🏆 NÍVEL 11 — MULTI-CLOUD E PORTABILIDADE

|#|Nota|Tópicos|
|:--|:--|:--|
|11.1|[[Cloud - Estratégias Multi-Cloud]]|Quando faz sentido, riscos e complexidade|
|11.2|[[Cloud - BigQuery Omni]]|Consulta federada de dados em AWS/Azure a partir do GCP|
|11.3|[[Cloud - Terraform para Dados]]|Infraestrutura como código agnóstica de provedor|
|11.4|[[Cloud - Migração entre Provedores]]|Estratégias de migração de warehouse (ex: Redshift → BigQuery)|

---

# 🔬 NÍVEL 12 — LABORATÓRIOS

|#|Nota|Tópicos|
|:--|:--|:--|
|12.1|[[Lab - Pipeline S3 → Glue → Redshift]]|Pipeline batch completo na AWS (free tier)|
|12.2|[[Lab - Pipeline Cloud Storage → Dataflow → BigQuery]]|Pipeline batch completo no GCP|
|12.3|[[Lab - Streaming com Kinesis/Pub-Sub]]|Ingestão de eventos em tempo real|
|12.4|[[Lab - Data Lake com Delta Lake]]|Versionamento e ACID sobre object storage|
|12.5|[[Lab - IAM com Menor Privilégio]]|Configuração de acesso restrito a um pipeline|

---

# 📖 NÍVEL 13 — RECEITAS

|#|Nota|Tópicos|
|:--|:--|:--|
|13.1|[[Recipe - Upload e Particionamento no S3]]|Estrutura de partições por data para consultas eficientes|
|13.2|[[Recipe - Carga Incremental para o Warehouse]]|Estratégias de merge/upsert|
|13.3|[[Recipe - Agendamento de Pipeline]]|Cron gerenciado, triggers por evento|
|13.4|[[Recipe - Consulta Federada (Omni/Spectrum)]]|Consultar dados sem mover entre nuvens|
|13.5|[[Recipe - Alerta de Custo]]|Configuração de orçamento e alertas automáticos|

---

# 🚀 NÍVEL 14 — PROJETOS

|#|Nota|Tópicos|
|:--|:--|:--|
|14.1|[[Projeto - Pipeline de Vendas na AWS]]|S3 + Glue + Redshift + dashboard|
|14.2|[[Projeto - Pipeline de Eventos em Tempo Real]]|Pub/Sub ou Kinesis + Dataflow/Lambda|
|14.3|[[Projeto - Data Lake Corporativo]]|Lakehouse com catálogo e governança|
|14.4|[[Projeto - Migração de Warehouse]]|Migração simulada entre dois provedores|
|14.5|[[Projeto - Dashboard de Custos de Dados]]|Monitoramento de gastos multi-serviço|

---

# 👑 NÍVEL 15 — CERTIFICAÇÕES

|#|Nota|Tópicos|
|:--|:--|:--|
|15.1|[[Cert - AWS Certified Data Engineer - Associate]]|Escopo oficial, tópicos cobrados|
|15.2|[[Cert - Google Cloud Professional Data Engineer]]|Escopo oficial, tópicos cobrados|
|15.3|[[Cert - Microsoft Azure Data Engineer Associate (DP-203)]]|Escopo oficial, tópicos cobrados|

---

# 📈 Roadmap profissional

|Etapa|Objetivo|Conhecimentos|
|:--|:--|:--|
|🌱 Fundamentos|Entender conceitos de cloud e IAM|IaaS/PaaS/SaaS, regiões, identidade e acesso|
|🌿 Armazenamento e Processamento|Guardar e processar dados na nuvem|Object storage, formatos de arquivo, clusters gerenciados|
|🌳 Analítico|Consultar dados em escala|Data warehouse, data lake, lakehouse|
|🌳 Pipelines|Automatizar movimentação de dados|ETL/ELT gerenciado, orquestração, streaming|
|🏆 Operação Responsável|Operar com governança e custo sob controle|Governança, LGPD/GDPR, FinOps|
|🚀 Avançado|Arquiteturas complexas e portáteis|Multi-cloud, Terraform, migrações|
|👑 Certificação|Validar conhecimento formalmente|Certificações oficiais AWS/GCP/Azure|

---

# 🎯 Critérios de conclusão

|Critério|Descrição|
|:--|:--|
|Conhecimento|Consigo explicar o conceito sem consulta|
|Implementação|Consigo implementar do zero (via console e via CLI/IaC)|
|Depuração|Consigo identificar e corrigir erros comuns|
|Aplicação|Já utilizei em projeto real ou laboratório completo|
|Documentação|Possuo nota própria documentada|
|Exemplo|Tenho exemplo funcional salvo (incluindo custo estimado)|
|Reutilização|Tenho receita pronta para consulta futura|

---

# 📊 Matriz de proficiência

|Status|Significado|
|:--|:--|
|⬜ Não Estudado|Conteúdo ainda não iniciado|
|🟦 Em Estudo|Teoria em andamento|
|🟨 Praticando|Exercícios e laboratórios (free tier)|
|🟩 Aplicado|Utilizado em projeto real|
|🟪 Dominado|Capaz de ensinar e implementar sem consulta|

---

# 📚 Fontes

## Oficiais — AWS

- [AWS Documentation](https://docs.aws.amazon.com/) — portal central de toda a documentação técnica da AWS
- [Amazon S3 — Guia do usuário](https://docs.aws.amazon.com/s3/)
- [Amazon Redshift — Documentação](https://docs.aws.amazon.com/redshift/)
- [AWS Glue — Documentação](https://docs.aws.amazon.com/glue/)
- [Amazon Kinesis — Documentação](https://docs.aws.amazon.com/kinesis/)
- [AWS Skill Builder](https://skillbuilder.aws/) — treinamento oficial gratuito da AWS, inclusive trilhas para certificação

## Oficiais — Google Cloud

- [Google Cloud Documentation](https://cloud.google.com/docs)
- [BigQuery — Documentação](https://cloud.google.com/bigquery/docs)
- [Dataflow — Documentação](https://cloud.google.com/dataflow/docs)
- [Cloud Storage — Documentação](https://cloud.google.com/storage/docs)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google/) — laboratórios práticos oficiais do Google, com créditos temporários de sandbox

## Oficiais — Microsoft Azure

- [Microsoft Learn — Azure](https://learn.microsoft.com/azure/) — documentação oficial e trilhas de aprendizado gratuitas com sandbox integrado
- [Azure Synapse Analytics — Documentação](https://learn.microsoft.com/azure/synapse-analytics/)
- [Azure Data Factory — Documentação](https://learn.microsoft.com/azure/data-factory/)
- [Azure Blob Storage — Documentação](https://learn.microsoft.com/azure/storage/blobs/)

## Ferramentas open source relacionadas (documentação oficial)

- [Delta Lake — Documentação](https://docs.delta.io/)
- [Apache Iceberg — Documentação](https://iceberg.apache.org/docs/latest/)
- [Apache Airflow — Documentação](https://airflow.apache.org/docs/)
- [Terraform — Documentação](https://developer.hashicorp.com/terraform/docs)
- [Snowflake — Documentação](https://docs.snowflake.com/)

## Comparativos e aprofundamento

- [Google Cloud — Guia de migração Redshift → BigQuery](https://docs.cloud.google.com/bigquery/docs/migration/redshift-overview) — bom material para entender diferenças reais entre os dois motores
- _Designing Data-Intensive Applications_ (Martin Kleppmann) — fundamentos que explicam o "porquê" por trás de qualquer serviço gerenciado de dados na nuvem

> [!note] Nota de mercado (2026) BigQuery é serverless e nativo do GCP (não roda em outra nuvem); o **BigQuery Omni** permite consultar dados parados em S3/Blob Storage sem migrá-los, mas o processamento ainda ocorre no GCP. Redshift domina em cargas batch pesadas com boa relação custo/performance via RA3 e Spectrum. Snowflake se destaca em concorrência alta e é o único dos quatro nativamente multi-cloud. Egress (custo de tirar dados da nuvem) é o item de custo mais subestimado em arquiteturas multi-cloud — vale tratar como critério de decisão desde o início, não só depois.

> [!note] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → `[!NOTE]` / `[!TIP]` → exemplos de código/CLI → links relacionados.