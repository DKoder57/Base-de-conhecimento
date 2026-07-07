---
tags: [cyber, dos, botnets, disponibilidade]
área: Cibersegurança / Windows e Active Directory
status: draft
matriz: "[[Cybersecurity]]"

---
# 💥 Ataques DoS e Botnets

> [!quote] Princípio Ataques de negação de serviço não roubam dados — eles atacam o terceiro pilar da tríade CIA: a disponibilidade.

---

## 🎯 Conceito Principal

Ataques de Negação de Serviço (DoS) buscam tornar um sistema indisponível para usuários legítimos, seja esgotando recursos computacionais, banda de rede, ou explorando falhas de protocolo. Esta nota foca nos conceitos e na defesa — não na operação de ataques reais contra sistemas de terceiros.

---

## 📊 DoS vs. DDoS

|Tipo|Diferença|
|---|---|
|**DoS**|Originado de uma única fonte|
|**DDoS**|Distribuído — múltiplas fontes (frequentemente uma botnet) atacam simultaneamente, dificultando bloqueio por IP|

---

## 🗂️ Categorias de Ataque

|Camada|Exemplo de categoria|Ideia central|
|---|---|---|
|**Volumétrica**|Flood de tráfego|Satura a banda de rede disponível|
|**Protocolo**|Exploração de handshakes/protocolos de rede|Consome recursos do servidor com conexões incompletas ou malformadas|
|**Camada de Aplicação**|Requisições HTTP legítimas em volume anormal|Sobrecarrega a lógica da aplicação (ex: consultas pesadas ao banco), mais difícil de distinguir de tráfego real|

> [!NOTE] Por que ataques de camada de aplicação são mais difíceis de mitigar Como o tráfego se parece com requisições legítimas de usuários reais, filtros baseados apenas em volume não funcionam bem — a defesa exige análise comportamental (ex: um mesmo IP acessando uma página de busca centenas de vezes por segundo).

---

## 🤖 Botnets — Conceito

Uma botnet é uma rede de dispositivos comprometidos (computadores, roteadores, câmeras IoT) controlados remotamente e coordenados por um atacante, geralmente sem o conhecimento dos donos legítimos.

```
Estrutura conceitual:
Atacante → Servidor de Comando e Controle (C2)
                        ↓
        Milhares de dispositivos infectados ("bots")
                        ↓
             Ação coordenada contra o alvo (ex: flood)
```

> [!WARNING] Dispositivos IoT como alvo comum Dispositivos IoT mal protegidos (senhas padrão nunca alteradas, firmware desatualizado) historicamente formaram algumas das maiores botnets já registradas, sendo usados para gerar volume de ataque muito além da capacidade de um único computador.

---

## 🛡️ Mitigação e Defesa

|Estratégia|Como ajuda|
|---|---|
|**CDN / Anycast**|Distribui o tráfego entre múltiplos data centers, diluindo o impacto do ataque|
|**Rate limiting**|Limita quantas requisições uma origem pode fazer em um intervalo|
|**WAF (Web Application Firewall)**|Filtra padrões conhecidos de ataque na camada de aplicação|
|**Scrubbing centers**|Serviços especializados que filtram tráfego malicioso antes de chegar ao destino|
|**Plano de resposta a incidentes**|Ter um processo definido de escalonamento reduz o tempo de reação a um ataque real|

---

## ⚖️ Aspecto Legal

> [!WARNING] Crime tipificado Realizar ataques de DoS/DDoS contra sistemas sem autorização é crime na maioria das jurisdições, incluindo o Brasil, independentemente da motivação alegada. O conhecimento dessa área serve para dimensionar defesas e planos de resposta a incidentes, não para operar ataques.

---

## 🔗 Notas Relacionadas

- [[Cyber - Redes para Pentesters]]
- [[Cyber - Pentest em Infraestrutura de Redes]]
- ⬅️ Voltar para [[Cybersecurity]]