---
tags:
  - devops
  - docker
  - kubernetes
  - git
  - cloud
  - sre
  - matriz
---

# ♾️ DevOps — Matriz da Trilha

> Construir conhecimento reutilizável, não apenas concluir cursos.

---

> [!info] O que é **DevOps** é a cultura e o conjunto de práticas que unem desenvolvimento (Dev) e operações (Ops) para entregar software com mais velocidade, qualidade e confiabilidade — cobrindo desde o terminal e o versionamento até containers, orquestração, infraestrutura como código, entrega contínua, observabilidade e segurança de todo o ciclo de vida.

> [!abstract] Objetivo desta trilha Organizar o estudo de DevOps de forma progressiva, do Linux e redes até Kubernetes, IaC, GitOps, Cloud, Observabilidade e SRE/Platform Engineering — transformando documentação oficial, laboratórios e projetos em base de conhecimento reutilizável, com foco em operar sistemas reais, não só em concluir cursos.

> [!note] Relação com a trilha [[Ferramentas e Devops para Dados]] A trilha [[Ferramentas e Devops para Dados]] cobre o ferramental mínimo (Shell, Git, Docker, Compose, CI/CD básico) necessário para os laboratórios de Banco de Dados e Cloud para Dados. Esta matriz reaproveita exatamente essas mesmas notas — marcadas com 🔗 — e as estende para uma trilha DevOps/Platform Engineering completa e profissional, sem depender de um contexto de dados: Kubernetes, Infraestrutura como Código, GitOps, multi-cloud, observabilidade e segurança.

---

## 🧠 Como usar esta matriz

Cada nota é uma unidade independente de conhecimento. Fluxo recomendado:

**Teoria → Exemplo → Laboratório → Projeto → Documentação própria**

Uma nota só é considerada concluída depois de aplicada em um laboratório ou projeto real — DevOps é uma trilha essencialmente prática.

```text
Linux e Terminal → Redes → Git → Docker → Kubernetes
→ Infraestrutura como Código → CI/CD → GitOps → Cloud
→ Observabilidade → Segurança/DevSecOps → SRE e Platform Engineering
→ Laboratórios → Receitas → Projetos
```

---

## 📚 Resumo da matriz

|Nível|Área|Resumo|
|:--|:--|:--|
|🌱 1|Linux e Terminal|Shell, permissões, variáveis de ambiente, processos, systemd, pacotes, logs, SSH|
|🌱 2|Redes para DevOps|Modelo TCP/IP, IP e sub-redes, DNS, HTTP/TLS, load balancing, firewalls|
|🌿 3|Git e Controle de Versão Profissional|Commits, branches, merge, conflitos, estratégias de branching, monorepos|
|🌿 4|Docker — Fundamentos e Dockerfile|Containers vs. VMs, imagens, camadas, instruções do Dockerfile, multi-stage builds|
|🌿 5|Docker — Compose, Volumes, Redes e Segurança|Múltiplos serviços, persistência, redes de container, usuário não-root, scanning|
|🌳 6|Kubernetes — Fundamentos e Workloads|Arquitetura do cluster, Pods, Deployments, ConfigMaps/Secrets, scheduling, HPA|
|🌳 7|Kubernetes — Redes, Storage e Operação|Services, Ingress/Gateway API, NetworkPolicies, storage, Helm, RBAC, troubleshooting|
|🌳 8|Infraestrutura como Código|Terraform/OpenTofu, módulos, state remoto, Ansible, Pulumi|
|🏆 9|CI/CD Avançado|GitHub Actions, GitLab CI/Jenkins, artefatos, segurança no pipeline, multi-ambiente|
|🏆 10|GitOps e Entrega Contínua|ArgoCD, FluxCD, deploys progressivos (canary, blue-green)|
|🏆 11|Cloud e Provedores|IAM, redes (VPC), AWS/Azure/GCP para DevOps, multi-cloud e FinOps|
|🏆 12|Observabilidade e Monitoramento|Métricas, logs, traces, Prometheus, OpenTelemetry, Grafana, SLO/SLI, alertas|
|🏆 13|Segurança e DevSecOps|Shift left, gestão de segredos, scanning de vulnerabilidades, policy as code, supply chain|
|🏆 14|SRE e Platform Engineering|Gestão de incidentes, on-call, chaos engineering, Internal Developer Platforms, Backstage|
|🔬 15|Laboratórios|Experimentação prática isolada|
|📖 16|Receitas|Implementações reutilizáveis de consulta rápida|
|🚀 17|Projetos|Ambientes e pipelines completos, do básico ao profissional|

---

# 🌱 NÍVEL 1 — LINUX E TERMINAL

|#|Nota|Tópicos|
|:--|:--|:--|
|1.1|[[Shell - Navegação e Arquivos]] 🔗|`cd`, `ls`, `pwd`, `mkdir`, `rm`, `mv`, `cp`|
|1.2|[[Shell - Permissões]] 🔗|`chmod`, `chown`, usuários e grupos|
|1.3|[[Shell - Variáveis de Ambiente]] 🔗|`export`, `.bashrc`/`.zshrc`, `PATH`|
|1.4|[[Shell - Pipes e Redirecionamento]] 🔗|`\|`, `>`, `>>`, `xargs`|
|1.5|[[Shell - Scripts Básicos]] 🔗|Shebang, variáveis, condicionais em bash|
|1.6|[[Linux - Gerenciamento de Pacotes]]|`apt`, `dnf`/`yum`, imagens base de distribuições|
|1.7|[[Linux - Processos e Systemd]]|`ps`, `top`/`htop`, `kill`, `systemctl`, unidades (units)|
|1.8|[[Linux - Logs do Sistema]]|`journalctl`, `/var/log`, syslog|
|1.9|[[Linux - SSH e Acesso Remoto]]|Chaves, `~/.ssh/config`, port forwarding, `scp`/`rsync`|

> [!tip] Notas marcadas com 🔗 já fazem parte da trilha [[Ferramentas e Devops para Dados]] — não recrie o conteúdo, apenas linke a nota existente.

---

# 🌱 NÍVEL 2 — REDES PARA DEVOPS

|#|Nota|Tópicos|
|:--|:--|:--|
|2.1|[[Redes - Modelo OSI e TCP-IP]]|Camadas, encapsulamento, protocolos por camada|
|2.2|[[Redes - Endereçamento IP e Sub-redes]]|IPv4/IPv6, máscara, CIDR, NAT|
|2.3|[[Redes - DNS]]|Registros (A, CNAME, MX, TXT), resolução, propagação|
|2.4|[[Redes - HTTP e HTTPS-TLS]]|Métodos, status codes, handshake TLS, certificados|
|2.5|[[Redes - Load Balancing e Proxies Reversos]]|Nginx, HAProxy, balanceamento L4 vs. L7|
|2.6|[[Redes - Firewalls e Portas]]|`iptables`/`nftables`, security groups, exposição mínima|

---

# 🌿 NÍVEL 3 — GIT E CONTROLE DE VERSÃO PROFISSIONAL

|#|Nota|Tópicos|
|:--|:--|:--|
|3.1|[[Git - Conceitos Fundamentais]] 🔗|Repositório, commit, staging area, working tree|
|3.2|[[Git - Branches e Merge]] 🔗|`branch`, `checkout`, `merge`, fast-forward|
|3.3|[[Git - Resolução de Conflitos]] 🔗|Merge conflicts, `rebase` vs. `merge`|
|3.4|[[Git - .gitignore e Boas Práticas]] 🔗|Arquivos a ignorar, commits atômicos, mensagens claras|
|3.5|[[Git - Remoto e Colaboração]] 🔗|`push`, `pull`, `fetch`, Pull Requests|
|3.6|[[Git - Desfazendo Alterações]] 🔗|`reset`, `revert`, `checkout -- arquivo`, `reflog`|
|3.7|[[Git - Estratégias de Branching (Trunk-Based, GitFlow)]]|Comparação entre modelos, quando usar cada um|
|3.8|[[Git - Monorepos e Submódulos]]|`git submodule`, estratégias de repositório único|

---

# 🌿 NÍVEL 4 — DOCKER: FUNDAMENTOS E DOCKERFILE

|#|Nota|Tópicos|
|:--|:--|:--|
|4.1|[[Docker - Containers vs. Máquinas Virtuais]] 🔗|Virtualização de SO vs. de hardware|
|4.2|[[Docker - Arquitetura]] 🔗|Docker Engine, daemon, client, containerd|
|4.3|[[Docker - Imagens e Camadas]] 🔗|Layers, cache de build, Docker Hub|
|4.4|[[Docker - Ciclo de Vida de um Container]] 🔗|`run`, `start`, `stop`, `rm`, `exec`, `logs`|
|4.5|[[Docker - Instalação e Configuração]] 🔗|Docker Desktop, Docker Engine em Linux|
|4.6|[[Docker - Instruções do Dockerfile]] 🔗|`FROM`, `RUN`, `COPY`, `CMD`, `ENTRYPOINT`, `WORKDIR`|
|4.7|[[Docker - Multi-Stage Builds]] 🔗|Redução de tamanho de imagem final|
|4.8|[[Docker - .dockerignore]] 🔗|Evitar copiar arquivos desnecessários no build|
|4.9|[[Docker - Otimização de Imagens]] 🔗|Imagens `alpine`/`slim`, ordenação de camadas para cache|
|4.10|[[Docker - Variáveis de Build e Runtime]] 🔗|`ARG` vs. `ENV`|

---

# 🌿 NÍVEL 5 — DOCKER: COMPOSE, VOLUMES, REDES E SEGURANÇA

|#|Nota|Tópicos|
|:--|:--|:--|
|5.1|[[Docker Compose - Estrutura do docker-compose.yml]] 🔗|Services, sintaxe básica|
|5.2|[[Docker Compose - Dependências entre Serviços]] 🔗|`depends_on`, health checks|
|5.3|[[Docker Compose - Variáveis de Ambiente]] 🔗|Arquivos `.env`, `environment`|
|5.4|[[Docker Compose - Comandos Essenciais]] 🔗|`up`, `down`, `logs`, `exec`, `build`|
|5.5|[[Docker Compose - Boas Práticas]] 🔗|Organização do YAML, nomes claros de serviço|
|5.6|[[Docker - Volumes Nomeados]] 🔗|Persistência gerenciada pelo Docker|
|5.7|[[Docker - Bind Mounts]] 🔗|Montagem direta de pastas do host|
|5.8|[[Docker - Backup de Volumes]] 🔗|Exportar/importar dados de um volume|
|5.9|[[Docker - Redes Bridge]] 🔗|Comunicação padrão entre containers|
|5.10|[[Docker - Exposição de Portas]] 🔗|`-p`, `EXPOSE`, mapeamento host↔container|
|5.11|[[Docker - Redes Customizadas no Compose]] 🔗|Isolamento de serviços por rede|
|5.12|[[Docker - Usuário Não-Root]] 🔗|Evitar rodar processos como root dentro do container|
|5.13|[[Docker - Imagens Mínimas e Confiáveis]] 🔗|Preferência por imagens oficiais e distroless/alpine|
|5.14|[[Docker - Scanning de Vulnerabilidades]] 🔗|`docker scout`, Trivy|
|5.15|[[Docker - Segredos e Variáveis Sensíveis]] 🔗|Evitar credenciais hardcoded em imagens|

---

# 🌳 NÍVEL 6 — KUBERNETES: FUNDAMENTOS E WORKLOADS

|#|Nota|Tópicos|
|:--|:--|:--|
|6.1|[[K8s - Arquitetura do Cluster]]|Control plane, nodes, etcd, kubelet, kube-proxy|
|6.2|[[K8s - kubeadm e Clusters Locais]]|`kubeadm`, minikube, kind, k3s|
|6.3|[[K8s - Pods]]|Ciclo de vida, multi-container, init containers|
|6.4|[[K8s - Deployments e ReplicaSets]]|Rollout, rollback, estratégias de atualização|
|6.5|[[K8s - ConfigMaps e Secrets]]|Injeção de configuração e dados sensíveis|
|6.6|[[K8s - Scheduling e Afinidade]]|`nodeSelector`, affinity/anti-affinity, taints e tolerations|
|6.7|[[K8s - Autoscaling (HPA e VPA)]]|Escalonamento horizontal e vertical de Pods|

> [!note] Nota de mercado O exame CKA (Certified Kubernetes Administrator) é atualizado periodicamente para acompanhar uma versão estável recente do Kubernetes e é 100% prático (sem múltipla escolha), com Troubleshooting como domínio de maior peso — reforçando que teoria sem prática de cluster real não é suficiente nesta trilha.

---

# 🌳 NÍVEL 7 — KUBERNETES: REDES, STORAGE E OPERAÇÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|7.1|[[K8s - Services]]|ClusterIP, NodePort, LoadBalancer|
|7.2|[[K8s - Ingress e Gateway API]]|Roteamento externo; Gateway API como evolução do Ingress|
|7.3|[[K8s - NetworkPolicies]]|Isolamento de tráfego entre Pods|
|7.4|[[K8s - CoreDNS]]|Resolução de nomes dentro do cluster|
|7.5|[[K8s - StorageClasses, PV e PVC]]|Provisionamento dinâmico de armazenamento|
|7.6|[[K8s - Helm]]|Charts, releases, templates|
|7.7|[[K8s - Kustomize]]|Overlays declarativos sem templating|
|7.8|[[K8s - RBAC]]|Roles, RoleBindings, ServiceAccounts|
|7.9|[[K8s - CRDs e Operators]]|Extensão da API do cluster|
|7.10|[[K8s - Troubleshooting]]|Eventos, logs, `describe`, debug de Pods e nós|

> [!note] Nota de mercado A Gateway API atingiu maturidade geral (GA) na API do Kubernetes e é adotada como sucessora de longo prazo do Ingress, mas o Ingress ainda é onipresente em clusters existentes — vale a pena estudar os dois.

---

# 🌳 NÍVEL 8 — INFRAESTRUTURA COMO CÓDIGO

|#|Nota|Tópicos|
|:--|:--|:--|
|8.1|[[IaC - Conceitos e Idempotência]]|Infraestrutura declarativa vs. imperativa|
|8.2|[[IaC - Terraform e OpenTofu — Fundamentos]]|HCL, providers, plan/apply, state|
|8.3|[[IaC - Terraform e OpenTofu — Módulos e Workspaces]]|Reuso de código, múltiplos ambientes|
|8.4|[[IaC - Terraform e OpenTofu — State Remoto]]|Backends, locking, colaboração em equipe|
|8.5|[[IaC - Ansible — Fundamentos]]|Playbooks, inventários, módulos, idempotência|
|8.6|[[IaC - Ansible — Roles e Templates]]|Organização reutilizável de automações|
|8.7|[[IaC - Pulumi e Alternativas com Linguagens de Programação]]|IaC com Python/TypeScript em vez de HCL/YAML|

> [!note] Nota de mercado Em 2023 a HashiCorp mudou a licença do Terraform de MPL para Business Source License (BSL), o que levou parte da comunidade a criar o **OpenTofu** — fork mantido pela Linux Foundation e aceito na CNCF, sob licença MPL 2.0. Em 2025 a HashiCorp (e o Terraform) foi adquirida pela IBM. Terraform continua sendo o termo mais presente em vagas por ser incumbente, mas OpenTofu é hoje a opção recomendada para quem está começando do zero em um projeto pessoal, por ser totalmente open source — a sintaxe (HCL) e os providers são praticamente idênticos entre os dois, então aprender um transfere quase 100% para o outro.

---

# 🏆 NÍVEL 9 — CI/CD AVANÇADO

|#|Nota|Tópicos|
|:--|:--|:--|
|9.1|[[CI/CD - Conceitos Gerais]] 🔗|Integração e entrega contínua, pipeline básico|
|9.2|[[GitHub Actions - Fundamentos]] 🔗|Workflows, jobs, steps, `.github/workflows`|
|9.3|[[GitHub Actions - Build e Push de Imagem Docker]] 🔗|Publicar imagem no Docker Hub/GHCR automaticamente|
|9.4|[[CI/CD - Testes Automatizados no Pipeline]] 🔗|Rodar testes antes do build/deploy|
|9.5|[[CI/CD - GitLab CI e Jenkins]]|Comparação com GitHub Actions e cenários de uso|
|9.6|[[CI/CD - Gerenciamento de Artefatos]]|Nexus, Artifactory, GitHub Container Registry|
|9.7|[[CI/CD - Segurança no Pipeline (SAST e SCA)]]|Scanning de código e dependências antes do deploy|
|9.8|[[CI/CD - Estratégias Multi-Ambiente]]|dev/staging/produção, aprovações manuais, secrets por ambiente|

---

# 🏆 NÍVEL 10 — GITOPS E ENTREGA CONTÍNUA

|#|Nota|Tópicos|
|:--|:--|:--|
|10.1|[[GitOps - Conceitos e Princípios]]|Git como fonte única da verdade, reconciliação contínua|
|10.2|[[GitOps - ArgoCD]]|Aplicações declarativas, sync automático, UI de estado|
|10.3|[[GitOps - FluxCD]]|Alternativa nativa do Kubernetes, controllers|
|10.4|[[GitOps - Deploys Progressivos (Canary e Blue-Green)]]|Redução de risco em produção|

---

# 🏆 NÍVEL 11 — CLOUD E PROVEDORES

|#|Nota|Tópicos|
|:--|:--|:--|
|11.1|[[Cloud - IAM e Governança Multi-Conta]]|Usuários, roles, políticas de menor privilégio|
|11.2|[[Cloud - Redes (VPC) e Load Balancing]]|Sub-redes, gateways, balanceadores gerenciados|
|11.3|[[Cloud - AWS para DevOps]]|EC2, ECS/EKS, S3, CloudFormation|
|11.4|[[Cloud - Azure para DevOps]]|VMs, AKS, Azure DevOps/Pipelines|
|11.5|[[Cloud - GCP para DevOps]]|Compute Engine, GKE, Cloud Build|
|11.6|[[Cloud - Estratégias Multi-Cloud e FinOps]]|Portabilidade, custos, evitar vendor lock-in|

---

# 🏆 NÍVEL 12 — OBSERVABILIDADE E MONITORAMENTO

|#|Nota|Tópicos|
|:--|:--|:--|
|12.1|[[Obs - Conceitos (Métricas, Logs, Traces)]]|Os três pilares da observabilidade|
|12.2|[[Obs - Prometheus]]|Modelo pull, PromQL, exporters|
|12.3|[[Obs - OpenTelemetry]]|Instrumentação padronizada e vendor-neutra|
|12.4|[[Obs - Grafana]]|Dashboards, datasources, alerting|
|12.5|[[Obs - Logs Centralizados (Loki e ELK)]]|Agregação e busca de logs|
|12.6|[[Obs - Tracing Distribuído (Tempo e Jaeger)]]|Rastreamento de requisições entre serviços|
|12.7|[[Obs - SLO, SLI e Error Budget]]|Definição de metas de confiabilidade|
|12.8|[[Obs - Alertas e Alertmanager]]|Roteamento de alertas, redução de ruído|

> [!note] Nota de mercado Prometheus e OpenTelemetry são hoje os dois padrões abertos que dominam a observabilidade: Prometheus para métricas (mais maduro, mais usado em produção) e OpenTelemetry para instrumentação de métricas/logs/traces de forma vendor-neutra (crescendo rapidamente). O stack open source mais comum para acompanhá-los é Grafana + Loki (logs) + Tempo (traces), muitas vezes com Mimir para métricas de longo prazo em escala.

---

# 🏆 NÍVEL 13 — SEGURANÇA E DEVSECOPS

|#|Nota|Tópicos|
|:--|:--|:--|
|13.1|[[DevSecOps - Conceitos e Shift Left]]|Segurança integrada desde o início do ciclo, não só no fim|
|13.2|[[DevSecOps - Gestão de Segredos (Vault e OpenBao)]]|Armazenamento seguro de credenciais e rotação|
|13.3|[[DevSecOps - Scanning de Vulnerabilidades e Dependências]]|Trivy, Snyk, Dependabot|
|13.4|[[DevSecOps - Policy as Code (OPA e Gatekeeper)]]|Regras de conformidade aplicadas automaticamente|
|13.5|[[DevSecOps - Supply Chain e SBOM]]|SLSA, Sigstore/cosign, assinatura de artefatos|

> [!note] Nota de mercado O HashiCorp Vault passou pela mesma mudança de licença (BSL) que o Terraform, e o **OpenBao** — fork sob a Linux Foundation, licença MPL 2.0 — é a alternativa aberta equivalente, já adotada por empresas como Nvidia e GitLab. Vale entender os dois: Vault ainda domina o mercado corporativo, mas OpenBao é a opção sem restrições de licença para estudo e projetos pessoais.

---

# 🏆 NÍVEL 14 — SRE E PLATFORM ENGINEERING

|#|Nota|Tópicos|
|:--|:--|:--|
|14.1|[[SRE - Gestão de Incidentes e Postmortems]]|Resposta a incidentes, análise sem culpados (blameless)|
|14.2|[[SRE - On-call e Runbooks]]|Plantão, documentação de resposta a falhas|
|14.3|[[SRE - Chaos Engineering]]|Testes de resiliência propositais em produção controlada|
|14.4|[[Platform Eng - Internal Developer Platforms]]|Plataformas internas de self-service para times de produto|
|14.5|[[Platform Eng - Backstage]]|Catálogo de serviços e portal de desenvolvedor|

---

# 🔬 NÍVEL 15 — LABORATÓRIOS

|#|Nota|Tópicos|
|:--|:--|:--|
|15.1|[[Lab - Cluster Kubernetes Local (kind ou minikube)]]|Subir e operar um cluster local do zero|
|15.2|[[Lab - Pipeline CI/CD Completo com GitHub Actions]]|Build, teste, scan e deploy automatizados|
|15.3|[[Lab - Infraestrutura AWS com OpenTofu]]|Provisionar recursos reais via IaC|
|15.4|[[Lab - GitOps com ArgoCD em Cluster Local]]|Sincronização automática de um repositório de manifests|
|15.5|[[Lab - Stack de Observabilidade (Prometheus, Grafana e Loki)]]|Monitorar uma aplicação de ponta a ponta|
|15.6|[[Lab - Ambiente Multi-Serviço com Ansible]]|Provisionamento e configuração automatizados|

---

# 📖 NÍVEL 16 — RECEITAS

|#|Nota|Tópicos|
|:--|:--|:--|
|16.1|[[Recipe - docker-compose.yml para Postgres + App]] 🔗|Template pronto de uso recorrente|
|16.2|[[Recipe - .gitignore para Projetos Python/Docker]] 🔗|Template de arquivos a ignorar|
|16.3|[[Recipe - Workflow Git para Projetos Solo]] 🔗|Convenção de branches e commits para projetos individuais|
|16.4|[[Recipe - Dockerfile Otimizado para Node/Python]]|Template com multi-stage e cache eficiente|
|16.5|[[Recipe - Módulo Terraform/OpenTofu Reutilizável]]|Template de módulo parametrizável|
|16.6|[[Recipe - Workflow GitHub Actions para Deploy]]|Pipeline padrão de build + deploy|
|16.7|[[Recipe - Dashboard Grafana Inicial]]|Template de dashboard para uma aplicação nova|

---

# 🚀 NÍVEL 17 — PROJETOS

|#|Nota|Tópicos|
|:--|:--|:--|
|17.1|[[Projeto - Deploy de uma Aplicação Full-Stack em Kubernetes]]|Da imagem Docker ao cluster em produção|
|17.2|[[Projeto - Pipeline CI/CD Ponta a Ponta com GitOps]]|Do commit ao deploy sincronizado por ArgoCD/Flux|
|17.3|[[Projeto - Infraestrutura Completa como Código na AWS]]|Ambiente provisionado inteiramente via OpenTofu|
|17.4|[[Projeto - Plataforma de Observabilidade para um App Real]]|Métricas, logs e traces de uma aplicação própria|
|17.5|[[Projeto - Ambiente de Produção com Segurança e SRE Aplicados]]|Segredos geridos, scanning no pipeline e runbook de incidentes|

---

# 📈 Roadmap profissional

|Etapa|Objetivo|Conhecimentos|
|:--|:--|:--|
|🌱 Fundamentos|Ser produtivo em Linux, redes e versionamento|Terminal, Linux básico, redes, Git|
|🌿 Containers|Empacotar e rodar aplicações de forma isolada e reprodutível|Docker, Dockerfile, Compose|
|🌳 Orquestração|Rodar e operar aplicações em escala|Kubernetes, Infraestrutura como Código|
|🏆 Entrega Contínua|Automatizar build, teste, deploy e infraestrutura|CI/CD avançado, GitOps, Cloud (AWS/Azure/GCP)|
|🚀 Confiabilidade|Garantir visibilidade e segurança em produção|Observabilidade, DevSecOps|
|👑 Especialista|Projetar plataformas internas e liderar prática de engenharia|SRE, Platform Engineering, arquitetura multi-cloud|

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

# 📚 Fontes (revisadas)

## Oficiais

- [roadmap.sh — DevOps Engineer Roadmap](https://roadmap.sh/devops) — trilha comunitária de referência, boa visão geral da sequência de aprendizado
- [Kubernetes Documentation](https://kubernetes.io/docs/) — referência principal, atualizada continuamente
- [CNCF — Certified Kubernetes Administrator (CKA)](https://www.cncf.io/training/certification/cka/)
- [Docker Documentation](https://docs.docker.com/)
- [OpenTofu Documentation](https://opentofu.org/docs/) — fork open source do Terraform (Linux Foundation/CNCF)
- [Terraform Documentation](https://developer.hashicorp.com/terraform) — referência secundária (licença BSL, hoje sob a IBM)
- [Ansible Documentation](https://docs.ansible.com/)
- [Git — Documentação oficial](https://git-scm.com/doc)
- [GitHub Actions — Documentação oficial](https://docs.github.com/actions)
- [GitLab CI/CD — Documentação oficial](https://docs.gitlab.com/ee/ci/)
- [Argo CD Documentation](https://argo-cd.readthedocs.io/)
- [Flux (FluxCD) Documentation](https://fluxcd.io/flux/)
- [Prometheus Documentation](https://prometheus.io/docs/)
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)
- [Grafana Documentation](https://grafana.com/docs/) — inclui Loki, Tempo e Mimir
- [OpenBao Documentation](https://openbao.org/docs/) — fork open source do HashiCorp Vault
- [AWS Documentation](https://docs.aws.amazon.com/)
- [Microsoft Azure Documentation](https://learn.microsoft.com/azure/)
- [Google Cloud Documentation](https://cloud.google.com/docs)
- [Google — Site Reliability Engineering (livro gratuito)](https://sre.google/books/)

## Referências técnicas

- [Kelsey Hightower — Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) — clássico para entender o cluster sem abstrações
- [KodeKloud](https://kodekloud.com/) — labs práticos de Kubernetes, Docker e Terraform
- [TechWorld with Nana (YouTube)](https://www.youtube.com/@TechWorldwithNana) — explicações diretas dos principais conceitos de DevOps
- [CNCF Cloud Native Landscape](https://landscape.cncf.io/) — mapa atualizado do ecossistema cloud native

## Livros

- _The Phoenix Project_ (Gene Kim, Kevin Behr, George Spafford)
- _The DevOps Handbook_ (Gene Kim, Jez Humble, Patrick Debois, John Willis)
- _Accelerate_ (Nicole Forsgren, Jez Humble, Gene Kim)
- _Site Reliability Engineering_ (equipe do Google — também gratuito online)
- _Kubernetes: Up & Running_ (Kelsey Hightower, Brendan Burns, Joe Beda)
- _Terraform: Up & Running_ (Yevgeniy Brikman)

> [!warning] Sobre as fontes de Infraestrutura como Código e Segredos Terraform e HashiCorp Vault são citados como referência por ainda dominarem as vagas de mercado, mas ambos migraram para a Business Source License (BSL) em 2023 e hoje pertencem à IBM. Para estudo prático e projetos pessoais sem restrição de licença, priorize OpenTofu e OpenBao — a sintaxe e os conceitos são praticamente idênticos e transferem diretamente para Terraform/Vault caso um emprego exija especificamente essas ferramentas.

> [!note] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → `[!NOTE]` / `[!TIP]` → exemplos de código/comando → links relacionados.
