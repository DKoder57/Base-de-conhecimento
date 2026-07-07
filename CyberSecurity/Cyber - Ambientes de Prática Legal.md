---
tags: [cyber, prática, labs, legal]

área: Cibersegurança / Prática (nota avulsa)

status: draft

oculta_da_matriz: true

---
# 🧪 Ambientes de Prática Legal em Pentest

> [!quote] Princípio A diferença entre estudo de segurança e crime não é a técnica usada — é a autorização do alvo. Praticar em ambientes feitos para isso remove qualquer ambiguidade.

> [!NOTE] Nota fora da matriz principal Esta nota não está listada em `[[Cybersecurity]]` por escolha própria — acesse-a apenas pelo link direto a partir de [[Cyber - Técnicas de Evasão de Antivírus e EDR]].

---

## 🎯 Conceito Principal

Todo conteúdo ofensivo do vault (SQLi, XSS, ARP spoofing, ataques AD, Wi-Fi cracking etc.) só deve ser praticado nos ambientes abaixo — construídos de propósito para serem atacados, ou com autorização contratual explícita da plataforma.

---

## 🖥️ Aplicações Propositalmente Vulneráveis (auto-hospedadas)

|Ambiente|Foco|Como rodar|
|---|---|---|
|**DVWA** (Damn Vulnerable Web App)|SQLi, XSS, CSRF, upload malicioso, níveis de dificuldade ajustáveis|Docker: `docker run --rm -it -p 80:80 vulnerables/web-dvwa`|
|**OWASP Juice Shop**|Aplicação moderna (Node/Angular) com toda a gama do OWASP Top 10|`docker run -p 3000:3000 bkimminich/juice-shop`|
|**OWASP WebGoat**|Lições guiadas passo a passo, cada vulnerabilidade com explicação teórica|`docker run -p 8080:8080 webgoat/webgoat`|
|**Metasploitable 2/3**|VM Linux cheia de serviços vulneráveis, foco em infraestrutura|Download direto da Rapid7 / VulnHub|

> [!TIP] Sempre isolado Rode esses ambientes em uma rede virtual isolada (NAT interno do VirtualBox/VMware, ou rede Docker própria), nunca exposto diretamente à internet.

---

## 🏆 Plataformas com Autorização Contratual

|Plataforma|O que autoriza|
|---|---|
|**TryHackMe**|Termos de serviço autorizam explicitamente atacar as máquinas da plataforma|
|**Hack The Box**|Idem — inclusive incentiva e premia _writeups_ de máquinas retiradas (retired)|
|**PicoCTF**|Competição educacional, autorização implícita ao competir|
|**VulnHub**|VMs para download, você mesmo hospeda e ataca localmente|
|**GOAD** (Game of Active Directory)|Ambiente completo de AD para prática de ataques de domínio, self-hosted|
|**CTFtime**|Agregador de CTFs ao redor do mundo, todos com regras e autorização próprias|

---

## ✅ Checklist Antes de Praticar Qualquer Técnica do Vault

- [ ] O alvo é um ambiente que eu mesmo hospedei, OU
- [ ] O alvo está dentro de uma plataforma que autoriza explicitamente esse tipo de teste (TryHackMe, HTB, VulnHub, CTFs)
- [ ] Estou dentro de uma rede isolada/laboratório, sem exposição à internet
- [ ] Não estou usando essas técnicas contra nenhum sistema de terceiros sem contrato formal (ver [[Cyber - Segurança da Informação e Pentest]])

---

## 📝 Registrando o Aprendizado — Writeups

Depois de resolver uma máquina/desafio (especialmente em HTB/THM, após ela ser "retirada" — _retired_ — do ativo), documentar o processo em um _writeup_ é uma prática valorizada na comunidade e ótima para portfólio:

1. Reconhecimento (o que foi encontrado, com prints/output de comando)
2. Vulnerabilidade identificada (qual, por que ocorre)
3. Exploração (passo a passo do que foi feito **naquele ambiente autorizado**)
4. Pós-exploração/escalonamento, se aplicável
5. Licões aprendidas / como se defenderia contra isso

> [!TIP] Ver [[Cyber - Writeup Exemplo (DVWA - SQL Injection)]] para um modelo pronto desse formato, usando o DVWA como base.

---

## 🔗 Notas Relacionadas

- [[Cyber - Técnicas de Evasão de Antivírus e EDR]]
- [[Cyber - Writeup Exemplo (DVWA - SQL Injection)]]
- [[Cyber - Segurança da Informação e Pentest]]
- [[Cyber - Técnicas de Evasão de Antivírus e EDR]]