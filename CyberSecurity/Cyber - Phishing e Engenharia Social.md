---
tags: [cyber, phishing, engenharia-social, red-team]
área: Cibersegurança / Windows e Active Directory
status: draft

matriz: "[[Cybersecurity]]"

---
# 🎣 Phishing e Engenharia Social

> [!quote] Princípio O elo mais fraco de qualquer sistema de segurança quase sempre é humano — engenharia social explora confiança, não código.

---

## 🎯 Conceito Principal

Engenharia social manipula comportamento humano (confiança, urgência, autoridade) para obter acesso ou informação que um controle técnico normalmente impediria. Phishing é a forma mais comum e escalável dessa técnica.

---

## 📧 Tipos de Phishing

|Tipo|Característica|
|---|---|
|**Phishing em massa**|Mensagens genéricas, enviadas a um grande volume de alvos|
|**Spear phishing**|Direcionado a um indivíduo/organização específica, com contexto personalizado|
|**Whaling**|Spear phishing direcionado a executivos de alto escalão|
|**Vishing**|Engenharia social por voz/telefone|
|**Smishing**|Phishing via SMS|

---

## 🧠 Gatilhos Psicológicos Usados

Campanhas eficazes de engenharia social costumam explorar um conjunto pequeno de princípios de influência bem documentados na literatura (Cialdini):

|Princípio|Como aparece em um ataque|
|---|---|
|**Urgência**|"Sua conta será bloqueada em 24h"|
|**Autoridade**|Se passar por um executivo ou por TI interno|
|**Prova social**|"Outros colegas do seu setor já preencheram este formulário"|
|**Escassez**|"Vaga/promoção limitada, responda agora"|

> [!NOTE] Por que isso funciona mesmo em pessoas treinadas Esses gatilhos ativam decisões rápidas e automáticas (pensamento de "sistema 1"), reduzindo a chance de a vítima parar para analisar detalhes técnicos como o domínio real do remetente.

---

## 🎯 Campanhas de Phishing em Contexto de Red Team

Quando conduzida como parte de um teste **autorizado** (Red Team), uma campanha de phishing segue etapas estruturadas:

```
1. Definição de escopo e aprovação legal/RH da campanha
2. Pretexto (cenário de credibilidade, ex: "atualização de benefícios")
3. Infraestrutura de envio (domínio similar, mas nunca se passando ilegalmente por terceiros reais)
4. Métricas: taxa de abertura, taxa de clique, taxa de submissão de credenciais
5. Relatório com recomendações de treinamento, sem expor individualmente quem "caiu"
```

> [!WARNING] Ética e escopo em campanhas de teste Uma campanha de phishing de Red Team deve ser aprovada formalmente (geralmente por jurídico e RH, além do time técnico), e o relatório final deve focar em **melhorar o programa de conscientização**, nunca em punir individualmente colaboradores que clicaram.

---

## 🛡️ Defesa Organizacional

- **Treinamento contínuo**, não apenas um evento anual — simulações regulares fixam melhor o aprendizado
- **MFA obrigatório**, reduzindo o impacto de uma credencial phishada isoladamente
- **DMARC/SPF/DKIM** configurados corretamente no domínio da empresa, dificultando spoofing do próprio domínio corporativo
- **Cultura de reporte sem culpa** — colaboradores devem se sentir seguros para reportar rapidamente um clique suspeito, sem medo de punição

---

## 🔗 Notas Relacionadas

- [[Cyber - Reconhecimento em Pentest]]
- [[Cyber - Privacidade e Anonimato]]
- ⬅️ Voltar para [[Cybersecurity]]