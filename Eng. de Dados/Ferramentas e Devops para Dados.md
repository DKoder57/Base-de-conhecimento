---

tags:

- docker
- devops
- git
- ferramentas
- matriz

---

# 🛠️ Ferramentas e DevOps para Dados — Matriz da Trilha

> Construir conhecimento reutilizável, não apenas concluir cursos.

---

> [!info] O que cobre esta trilha O ferramental prático que sustenta todas as outras trilhas (Banco de Dados, Python, Cloud): **Docker** para ambientes reprodutíveis, **Git** para versionamento, e o mínimo de **linha de comando/CI** necessário para rodar e automatizar pipelines de dados sem depender de instalação manual.

> [!abstract] Objetivo desta trilha Ser capaz de subir qualquer ambiente de estudo (Postgres, Airflow, Redis etc.) com um comando, versionar o código de forma limpa, e automatizar o básico — sem isso, laboratórios de outras trilhas viram "instalação manual" em vez de prática real.

---

## 🧠 Como usar esta matriz

Cada nota é uma unidade independente de conhecimento. Fluxo recomendado:

**Teoria → Exemplo → Laboratório → Projeto → Documentação própria**

Esta trilha é essencialmente prática: uma nota só conta como concluída se você rodou o comando de verdade no terminal, não se só leu sobre ele.

```text
Terminal e Shell → Git → Docker → Docker Compose
→ Imagens para Dados → Volumes e Persistência → Redes
→ CI/CD Básico → Laboratórios → Receitas → Projetos
```

---

## 📚 Resumo da matriz

|Nível|Área|Resumo|
|:--|:--|:--|
|🌱 1|Terminal e Shell|Navegação, permissões, variáveis de ambiente, scripts básicos|
|🌿 2|Git e Controle de Versão|Commits, branches, merge, conflitos, `.gitignore`|
|🌿 3|Docker — Fundamentos|Containers vs. VMs, imagens, camadas, ciclo de vida|
|🌳 4|Dockerfile|Instruções, multi-stage builds, otimização de imagem|
|🌳 5|Docker Compose|Múltiplos serviços, dependências, variáveis de ambiente|
|🌳 6|Volumes e Persistência|Dados que sobrevivem ao container, bind mounts|
|🌳 7|Redes no Docker|Comunicação entre containers, exposição de portas|
|🏆 8|Docker para Bancos de Dados|Postgres, MySQL, Redis em containers para desenvolvimento|
|🏆 9|Docker para Pipelines de Dados|Airflow, Spark e Jupyter via Compose|
|🏆 10|Segurança em Containers|Usuário não-root, imagens mínimas, scanning de vulnerabilidades|
|🚀 11|CI/CD Básico|GitHub Actions, build e push automatizado de imagens|
|🔬 12|Laboratórios|Experimentação prática isolada|
|📖 13|Receitas|Implementações reutilizáveis de consulta rápida|
|🎯 14|Projetos|Ambientes completos containerizados|

---

# 🌱 NÍVEL 1 — TERMINAL E SHELL

|#|Nota|Tópicos|
|:--|:--|:--|
|1.1|[[Shell - Navegação e Arquivos]]|`cd`, `ls`, `pwd`, `mkdir`, `rm`, `mv`, `cp`|
|1.2|[[Shell - Permissões]]|`chmod`, `chown`, usuários e grupos|
|1.3|[[Shell - Variáveis de Ambiente]]|`export`, `.bashrc`/`.zshrc`, `PATH`|
|1.4|[[Shell - Pipes e Redirecionamento]]|`|
|1.5|[[Shell - Scripts Básicos]]|Shebang, variáveis, condicionais em bash|

---

# 🌿 NÍVEL 2 — GIT E CONTROLE DE VERSÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|2.1|[[Git - Conceitos Fundamentais]]|Repositório, commit, staging area, working tree|
|2.2|[[Git - Branches e Merge]]|`branch`, `checkout`, `merge`, fast-forward|
|2.3|[[Git - Resolução de Conflitos]]|Merge conflicts, `rebase` vs. `merge`|
|2.4|[[Git - .gitignore e Boas Práticas]]|Arquivos a ignorar, commits atômicos, mensagens claras|
|2.5|[[Git - Remoto e Colaboração]]|`push`, `pull`, `fetch`, Pull Requests|
|2.6|[[Git - Desfazendo Alterações]]|`reset`, `revert`, `checkout -- arquivo`, `reflog`|

---

# 🌿 NÍVEL 3 — DOCKER: FUNDAMENTOS

|#|Nota|Tópicos|
|:--|:--|:--|
|3.1|[[Docker - Containers vs. Máquinas Virtuais]]|Virtualização de SO vs. de hardware|
|3.2|[[Docker - Arquitetura]]|Docker Engine, daemon, client, containerd|
|3.3|[[Docker - Imagens e Camadas]]|Layers, cache de build, Docker Hub|
|3.4|[[Docker - Ciclo de Vida de um Container]]|`run`, `start`, `stop`, `rm`, `exec`, `logs`|
|3.5|[[Docker - Instalação e Configuração]]|Docker Desktop, Docker Engine em Linux|

---

# 🌳 NÍVEL 4 — DOCKERFILE

|#|Nota|Tópicos|
|:--|:--|:--|
|4.1|[[Docker - Instruções do Dockerfile]]|`FROM`, `RUN`, `COPY`, `CMD`, `ENTRYPOINT`, `WORKDIR`|
|4.2|[[Docker - Multi-Stage Builds]]|Redução de tamanho de imagem final|
|4.3|[[Docker - .dockerignore]]|Evitar copiar arquivos desnecessários no build|
|4.4|[[Docker - Otimização de Imagens]]|Imagens `alpine`/`slim`, ordenação de camadas para cache|
|4.5|[[Docker - Variáveis de Build e Runtime]]|`ARG` vs. `ENV`|

---

# 🌳 NÍVEL 5 — DOCKER COMPOSE

|#|Nota|Tópicos|
|:--|:--|:--|
|5.1|[[Docker Compose - Estrutura do docker-compose.yml]]|Services, sintaxe básica|
|5.2|[[Docker Compose - Dependências entre Serviços]]|`depends_on`, health checks|
|5.3|[[Docker Compose - Variáveis de Ambiente]]|Arquivos `.env`, `environment`|
|5.4|[[Docker Compose - Comandos Essenciais]]|`up`, `down`, `logs`, `exec`, `build`|
|5.5|[[Docker Compose - Boas Práticas]]|Organização do YAML, nomes claros de serviço|

---

# 🌳 NÍVEL 6 — VOLUMES E PERSISTÊNCIA

|#|Nota|Tópicos|
|:--|:--|:--|
|6.1|[[Docker - Volumes Nomeados]]|Persistência gerenciada pelo Docker|
|6.2|[[Docker - Bind Mounts]]|Montagem direta de pastas do host|
|6.3|[[Docker - Backup de Volumes]]|Exportar/importar dados de um volume|

---

# 🌳 NÍVEL 7 — REDES NO DOCKER

|#|Nota|Tópicos|
|:--|:--|:--|
|7.1|[[Docker - Redes Bridge]]|Comunicação padrão entre containers|
|7.2|[[Docker - Exposição de Portas]]|`-p`, `EXPOSE`, mapeamento host↔container|
|7.3|[[Docker - Redes Customizadas no Compose]]|Isolamento de serviços por rede|

---

# 🏆 NÍVEL 8 — DOCKER PARA BANCOS DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|8.1|[[Docker - PostgreSQL em Container]]|Imagem oficial, variáveis de inicialização, volume de dados|
|8.2|[[Docker - MySQL em Container]]|Imagem oficial, configuração inicial|
|8.3|[[Docker - Redis em Container]]|Cache local para desenvolvimento|
|8.4|[[Docker - Ambiente de BD Completo com Compose]]|Banco + ferramenta de administração (pgAdmin/Adminer)|

---

# 🏆 NÍVEL 9 — DOCKER PARA PIPELINES DE DADOS

|#|Nota|Tópicos|
|:--|:--|:--|
|9.1|[[Docker - Apache Airflow via Compose]]|`docker-compose.yaml` oficial do Airflow|
|9.2|[[Docker - Jupyter em Container]]|Imagens `jupyter/docker-stacks`|
|9.3|[[Docker - Spark Local em Container]]|Ambiente de testes para PySpark|

---

# 🏆 NÍVEL 10 — SEGURANÇA EM CONTAINERS

|#|Nota|Tópicos|
|:--|:--|:--|
|10.1|[[Docker - Usuário Não-Root]]|Evitar rodar processos como root dentro do container|
|10.2|[[Docker - Imagens Mínimas e Confiáveis]]|Preferência por imagens oficiais e distroless/alpine|
|10.3|[[Docker - Scanning de Vulnerabilidades]]|`docker scout`, Trivy|
|10.4|[[Docker - Segredos e Variáveis Sensíveis]]|Evitar credenciais hardcoded em imagens|

---

# 🚀 NÍVEL 11 — CI/CD BÁSICO

|#|Nota|Tópicos|
|:--|:--|:--|
|11.1|[[CI/CD - Conceitos Gerais]]|Integração e entrega contínua, pipeline básico|
|11.2|[[GitHub Actions - Fundamentos]]|Workflows, jobs, steps, `.github/workflows`|
|11.3|[[GitHub Actions - Build e Push de Imagem Docker]]|Publicar imagem no Docker Hub/GHCR automaticamente|
|11.4|[[CI/CD - Testes Automatizados no Pipeline]]|Rodar testes antes do build/deploy|

---

# 🔬 NÍVEL 12 — LABORATÓRIOS

|#|Nota|Tópicos|
|:--|:--|:--|
|12.1|[[Lab - Ambiente Postgres + Adminer via Compose]]|Subir banco e ferramenta de administração juntos|
|12.2|[[Lab - Airflow Local Completo]]|Ambiente de orquestração rodando localmente|
|12.3|[[Lab - Dockerfile Multi-Stage para App Python]]|Redução de tamanho de imagem de uma aplicação real|
|12.4|[[Lab - CI simples com GitHub Actions]]|Pipeline que builda e testa a cada push|

---

# 📖 NÍVEL 13 — RECEITAS

|#|Nota|Tópicos|
|:--|:--|:--|
|13.1|[[Recipe - docker-compose.yml para Postgres + App]]|Template pronto de uso recorrente|
|13.2|[[Recipe - .gitignore para Projetos Python/Docker]]|Template de arquivos a ignorar|
|13.3|[[Recipe - Dockerfile Otimizado para Python]]|Template com multi-stage e cache eficiente|
|13.4|[[Recipe - Backup de Volume Docker]]|Comando pronto de export/import|
|13.5|[[Recipe - Workflow Git para Projetos Solo]]|Convenção de branches e commits para projetos individuais|

---

# 🎯 NÍVEL 14 — PROJETOS

|#|Nota|Tópicos|
|:--|:--|:--|
|14.1|[[Projeto - Ambiente de Desenvolvimento Completo]]|App + banco + cache, tudo via Compose|
|14.2|[[Projeto - Pipeline Local com Airflow + Postgres]]|Orquestração containerizada ponta a ponta|
|14.3|[[Projeto - CI/CD Completo de uma Aplicação]]|Build, teste e push automatizado|

---

# 📈 Roadmap profissional

|Etapa|Objetivo|Conhecimentos|
|:--|:--|:--|
|🌱 Base|Ser produtivo no terminal e versionar código|Shell básico, Git|
|🌿 Containers|Empacotar e rodar aplicações de forma isolada|Docker, Dockerfile|
|🌳 Orquestração Local|Rodar múltiplos serviços juntos|Docker Compose, volumes, redes|
|🏆 Aplicado a Dados|Usar containers para bancos e pipelines|Postgres/MySQL/Redis/Airflow em container|
|🚀 Automação|Automatizar build, teste e deploy|CI/CD básico com GitHub Actions|

---

# 🎯 Critérios de conclusão

|Critério|Descrição|
|:--|:--|
|Conhecimento|Consigo explicar o conceito sem consulta|
|Implementação|Consigo implementar do zero|
|Depuração|Consigo identificar e corrigir erros comuns|
|Aplicação|Já utilizei em projeto real|
|Documentação|Possuo nota própria documentada|
|Exemplo|Tenho exemplo funcional salvo|
|Reutilização|Tenho receita pronta para consulta futura|

---

# 📊 Matriz de proficiência

|Status|Significado|
|:--|:--|
|⬜ Não Estudado|Conteúdo ainda não iniciado|
|🟦 Em Estudo|Teoria em andamento|
|🟨 Praticando|Exercícios e laboratórios|
|🟩 Aplicado|Utilizado em projeto real|
|🟪 Dominado|Capaz de ensinar e implementar sem consulta|

---

# 📚 Fontes

## Oficiais

- [Docker Documentation](https://docs.docker.com/) — documentação oficial, cobre Engine, Compose, build e segurança
- [Docker Compose — Referência oficial](https://docs.docker.com/compose/)
- [Dockerfile — Referência oficial](https://docs.docker.com/reference/dockerfile/)
- [Docker Hub](https://hub.docker.com/) — repositório oficial de imagens (priorizar imagens "Official Image")
- [Git — Documentação oficial](https://git-scm.com/doc)
- [Pro Git (livro oficial, gratuito)](https://git-scm.com/book/pt-br/v2) — disponível em português
- [GitHub Actions — Documentação oficial](https://docs.github.com/actions)
- [Apache Airflow — docker-compose oficial](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)

## Referências técnicas

- [Docker Official Images — Postgres](https://hub.docker.com/_/postgres)
- [Docker Official Images — MySQL](https://hub.docker.com/_/mysql)
- [Docker Official Images — Redis](https://hub.docker.com/_/redis)
- [Play with Docker](https://labs.play-with-docker.com/) — laboratório oficial no navegador, sem instalar nada

## Livros

- _Docker Deep Dive_ (Nigel Poulton)
- _Pro Git_ (Scott Chacon & Ben Straub) — também disponível gratuitamente online

> [!note] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → `[!NOTE]` / `[!TIP]` → exemplos de código/comando → links relacionados.