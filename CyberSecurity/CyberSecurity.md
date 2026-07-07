---

tags: [matriz, cybersecurity, pentest, segurança]
área: Segurança da Informação / Cibersegurança
status: draft
---
# 🛡️ Cybersecurity — Matriz da Aba

> [!quote] Princípio: Documentar é transformar consumo em domínio. Arquivo de navegação central para todos os tópicos de Cibersegurança do vault. Estruturado com base na trilha de estudos em Cibersegurança e Pentest.

---

## 📚 Fontes

|Trilha / Documento|Cobertura|
|:--|:--|
|Lista de Estudos em Cibersegurança|Fundamentos, Pentest, Mobile, Wireless, Automação, Exploits, Windows/AD e tópicos avançados.|

---

## 🟢 Seção 1 — Fundamentos

> Base teórica e técnica necessária antes de qualquer prática ofensiva.

| #   | Nota                                          | Tópicos                                                                  |
| :-- | :-------------------------------------------- | :----------------------------------------------------------------------- |
| 1.1 | [[Cyber - Segurança da Informação e Pentest]] | Pilares da segurança (CIA), tipos de pentest, metodologia geral          |
| 1.2 | [[Cyber - Linux e Shell para Pentesters]]     | Terminal, permissões, gerenciamento de processos, scripts de shell       |
| 1.3 | [[Cyber - Python Básico e Algoritmos]]        | Sintaxe, estruturas de controle, lógica aplicada a segurança             |
| 1.4 | [[Cyber - Criptografia e Senhas]]             | Hashing, criptografia simétrica/assimétrica, quebra e política de senhas |
| 1.5 | [[Cyber - Python Orientado a Objetos]]        | Classes, herança, aplicação de POO em ferramentas ofensivas              |
| 1.6 | [[Cyber - Redes para Pentesters]]             | Modelo OSI/TCP-IP, portas, protocolos, análise de tráfego                |

---

## 🔴 Seção 2 — Pentest

> Ciclo prático de testes de invasão, do reconhecimento à exploração em diferentes ambientes.

| #   | Nota                                            | Tópicos                                                       |
| :-- | :---------------------------------------------- | :------------------------------------------------------------ |
| 2.1 | [[Cyber - Reconhecimento em Pentest]]           | OSINT, footprinting, enumeração ativa e passiva               |
| 2.2 | [[Cyber - Pentest em Infraestrutura de Redes]]  | Varredura de vulnerabilidades, exploração de serviços de rede |
| 2.3 | [[Cyber - Desenvolvimento Web para Pentesters]] | HTTP, requisições, front/back-end na perspectiva ofensiva     |
| 2.4 | [[Cyber - Ataques em Aplicações Web]]           | OWASP Top 10, SQLi, XSS, CSRF, upload de arquivos             |
| 2.5 | [[Cyber - Pentest em Ambientes Cloud]]          | AWS/Azure/GCP, IAM, buckets expostos, configurações inseguras |

---

## 📱 Seção 3 — Mobile

> Segurança ofensiva voltada a aplicativos e ao sistema operacional Android.

| #   | Nota                                                 | Tópicos                                                            |
| :-- | :--------------------------------------------------- | :----------------------------------------------------------------- |
| 3.1 | [[Cyber - Pentest em Aplicativos Android]]           | Engenharia reversa de APK, análise estática e dinâmica, ADB        |
| 3.2 | [[Cyber - Desenvolvimento de Malwares para Android]] | Payloads, permissões abusivas, persistência em dispositivos móveis |

---

## 📶 Seção 4 — Wireless

> Ataque e defesa em redes sem fio.

| #   | Nota                                 | Tópicos                                                         |
| :-- | :----------------------------------- | :-------------------------------------------------------------- |
| 4.1 | [[Cyber - Ataques em Redes Wi-Fi]]   | WPA/WPA2/WPA3, handshake capture, deauth, ataques de dicionário |
| 4.2 | [[Cyber - Segurança em Redes Wi-Fi]] | Hardening de AP, segmentação, detecção de intrusão wireless     |

---

## 🤖 Seção 5 — Automação e Bug Bounty

> Escala de processos ofensivos e aplicação de IA à descoberta de vulnerabilidades.

| #   | Nota                                                       | Tópicos                                                     |
| :-- | :--------------------------------------------------------- | :---------------------------------------------------------- |
| 5.1 | [[Cyber - Automação em Bug Bounty]]                        | Scripts de reconhecimento em massa, pipelines de scanning   |
| 5.2 | [[Cyber - Inteligência Artificial aplicada a Pentest Web]] | Uso de LLMs e IA para fuzzing, geração de payloads, triagem |

---

## 💻 Seção 6 — Programação e Exploits

> Base de programação de baixo nível e técnicas de pós-exploração multiplataforma.

| #   | Nota                                                | Tópicos                                                           |
| :-- | :-------------------------------------------------- | :---------------------------------------------------------------- |
| 6.1 | [[Cyber - Fundamentos de C para Pentesters]]        | Ponteiros, memória, compilação, relação com exploração binária    |
| 6.2 | [[Cyber - Pós-exploração em Linux]]                 | Escalação de privilégios, persistência, movimentação lateral      |
| 6.3 | [[Cyber - Docker para Pentesters]]                  | Containers, isolamento, fuga de container, ambientes de teste     |
| 6.4 | [[Cyber - Metodologias de Pentest]]                 | PTES, OSSTMM, NIST SP 800-115, relatórios técnicos                |
| 6.5 | [[Cyber - Exploração de Jogos e Hardware]]          | Engenharia reversa aplicada a jogos, cheats, proteções anti-cheat |
| 6.6 | [[Cyber - Hardware Hacking]]                        | JTAG, UART, firmware dumping, análise de placas                   |
| 6.7 | [[Cyber - Side-channel Analysis e Fault Injection]] | Análise de canal lateral, glitching, ataques físicos a chips      |

---

## 🪟 Seção 7 — Windows e Active Directory

> Ataques e pós-exploração no ecossistema Windows corporativo.

| #   | Nota                                     | Tópicos                                                        |
| :-- | :--------------------------------------- | :------------------------------------------------------------- |
| 7.1 | [[Cyber - PowerShell para Pentesters]]   | Scripting ofensivo, bypass de políticas de execução            |
| 7.2 | [[Cyber - Pós-exploração Windows]]       | Dumping de credenciais, tokens, movimentação lateral           |
| 7.3 | [[Cyber - Pentest em Active Directory]]  | Kerberoasting, GPOs, relacionamentos de confiança, BloodHound  |
| 7.4 | [[Cyber - Assembly para Exploits]]       | Arquitetura x86/x64, registradas, desenvolvimento de shellcode |
| 7.5 | [[Cyber - Ataques DOS e Botnets]]        | Negação de serviço, redes zumbi, mitigação                     |
| 7.6 | [[Cyber - Ataques MITM]]                 | ARP spoofing, interceptação de tráfego, SSL stripping          |
| 7.7 | [[Cyber - Phishing e Engenharia Social]] | Pretexting, campanhas de phishing, engenharia social ofensiva  |
| 7.8 | [[Cyber - Privacidade e Anonimato]]      | Tor, VPNs, OPSEC, anonimização de operações                    |

---

## ⚫ Seção 8 — Avançado

> Tópicos de ponta envolvendo IA ofensiva, malwares e evasão de defesas.

| #   | Nota                                              | Tópicos                                                        |
| :-- | :------------------------------------------------ | :------------------------------------------------------------- |
| 8.1 | [[Cyber - LLM Hacking (IA)]]                      | Prompt injection, jailbreaks, exfiltração via modelos de IA    |
| 8.2 | [[Cyber - Análise e Desenvolvimento de Malwares]] | Engenharia reversa, análise estática/dinâmica, criação de PoCs |
| 8.3 | [[Cyber - Técnicas de Evasão de Antivírus e EDR]] | Ofuscação, packers, bypass de detecção comportamental          |


---

## 🗺️ Mapa de Progressão Sugerido

```
1.1 → 1.2 → 1.3 → 1.4 → 1.5 → 1.6
                                  ↓
                        2.1 → 2.2 → 2.3 → 2.4 → 2.5
                                                    ↓
                                    3.1 → 3.2   4.1 → 4.2
                                          ↓           ↓
                                        5.1 → 5.2 ←────┘
                                                    ↓
                        6.1 → 6.2 → 6.3 → 6.4 → 6.5 → 6.6 → 6.7
                                                                ↓
        7.1 → 7.2 → 7.3 → 7.4 → 7.5 → 7.6 → 7.7 → 7.8
                                                        ↓
                                    8.1 → 8.2 → 8.3
```

---

> [!NOTE] Padrão das notas filhas Todas as notas geradas a partir desta matriz devem seguir a estrutura padronizada: frontmatter YAML → conceito principal → callouts `[!NOTE]` / `[!TIP]` → exemplos práticos de código/comandos anotados → links de navegação de retorno.

> [!WARNING] Uso ético Todo o conteúdo desta trilha deve ser aplicado exclusivamente em ambientes controlados, laboratórios próprios ou testes com autorização formal (contrato de pentest). Uso não autorizado de técnicas ofensivas é crime.
> 


### 1. Fontes para estudar cada matéria da lista

**Fundamentos / Redes / Linux**

- **OverTheWire (Bandit)** — linha de comando e Linux para iniciantes, gratuito
- **TryHackMe** — trilhas guiadas ("Complete Beginner", "Jr Penetration Tester"), extremamente guiado, com laboratórios no navegador e trilhas pré-construídas

**Pentest Web**

- **PortSwigger Web Security Academy** — referência no aprendizado de segurança de aplicações web, feito pela empresa dona do Burp Suite, 100% gratuito e cobre bem "Ataques em Aplicações Web"

**Pentest geral / Infra / CTF**

- **Hack The Box + HTB Academy** — HTB Academy organiza os treinamentos em módulos básicos claros, separados por área, ótimo custo-benefício para iniciantes [HackerDNA](https://hackerdna.com/blog/hack-the-box-alternatives)
- **PicoCTF** — CTFs simples e gratuitos, bom para praticar fundamentos

**Active Directory / Windows**

- Labs específicos como "Throwback" e "Holo" do TryHackMe são citados como bons para prática de AD

**Progressão sugerida entre plataformas**: comece pelo TryHackMe para entender conceitos, avance para o Hack The Box para ataques realistas, use o PortSwigger para se especializar em web, e plataformas como OffSec Labs para validar nível profissional [Medium](https://medium.com/@kauan.m/60-plataformas-para-aprender-e-praticar-hacking-2023-c0c9ff3d5c3)

**Mobile/Malware/Hardware/Avançado** (menos coberto por essas plataformas): aqui o ideal é documentação oficial + livros/whitepapers específicos — posso pesquisar fontes dedicadas por tópico (ex: OWASP MASTG para mobile, ChipWhisperer docs para side-channel) se quiser que eu aprofunde algum desses.