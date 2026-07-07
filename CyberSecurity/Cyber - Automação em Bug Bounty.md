---

tags: [cyber, automação, bug-bounty]
área: Cibersegurança / Automação e Bug Bounty
status: draft
matriz: "[[Cybersecurity]]"

---
# 🤖 Automação em Bug Bounty

> [!quote] Princípio Em bug bounty, quem cobre mais superfície de ataque com qualidade encontra mais falhas — automação é o que permite escalar reconhecimento manual para centenas de alvos.

---

## 🎯 Conceito Principal

Bug bounty envolve testar continuamente um escopo amplo de ativos (subdomínios, endpoints, parâmetros). Fazer isso manualmente não escala — por isso caçadores de recompensas constroem **pipelines de automação** que encadeiam ferramentas especializadas.

---

## 🔗 Encadeando Ferramentas (Recon Pipeline)

Um fluxo comum de reconhecimento em massa combina várias ferramentas de linha de comando via _pipe_:

```bash
# Exemplo conceitual de pipeline de recon (ferramentas comuns na comunidade)
subfinder -d exemplo.com -silent | \
  httpx -silent | \
  nuclei -t vulnerabilidades/ -o resultados.txt
```

|Etapa|Ferramenta comum|Função|
|---|---|---|
|Enumeração de subdomínio|`subfinder`, `amass`|Descobre subdomínios do escopo|
|Verificação de hosts vivos|`httpx`|Filtra quais subdomínios respondem via HTTP|
|Varredura de vulnerabilidades|`nuclei`|Testa templates de vulnerabilidades conhecidas|
|Descoberta de parâmetros|`paramspider`, `arjun`|Encontra parâmetros de URL para testar|

> [!TIP] Templates do Nuclei O Nuclei funciona com templates YAML comunitários — um caçador experiente frequentemente escreve os próprios templates para vulnerabilidades específicas do programa que está testando.

---

## ⏱️ Monitoramento Contínuo (Diffing)

Programas de bug bounty mudam constantemente. Um padrão comum é rodar o pipeline periodicamente e comparar resultados com a execução anterior, alertando apenas sobre **novidades**:

```bash
# Conceito: comparar lista de subdomínios de hoje com a de ontem
diff subdominios_ontem.txt subdominios_hoje.txt
```

> [!NOTE] Por que isso importa Subdomínios recém-criados costumam ter configurações provisórias e mais falhas — monitorar continuamente aumenta a chance de ser o primeiro a encontrar uma vulnerabilidade recém-introduzida.

---

## 🗂️ Organização e Priorização

- Manter um inventário atualizado do escopo (ativos dentro e fora de escopo mudam com frequência)
- Priorizar automação para o "trabalho repetitivo" (recon, triagem inicial) e reservar tempo manual para lógica de negócio complexa, que ferramentas automatizadas não conseguem identificar sozinhas
- Documentar falsos positivos recorrentes para refinar os próprios scripts/templates ao longo do tempo

---

## 🔗 Notas Relacionadas

- [[Cyber - Reconhecimento em Pentest]]
- [[Cyber - Inteligência Artificial aplicada a Pentest Web]]
- [[Cyber - Python Orientado a Objetos]]
- ⬅️ Voltar para [[Cybersecurity]]