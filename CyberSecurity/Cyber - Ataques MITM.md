---
tags: [cyber, mitm, arp-spoofing, ssl-stripping]

área: Cibersegurança / Windows e Active Directory

status: draft

matriz: "[[Cybersecurity]]"

---
# 🕵️ Ataques MITM (Man-in-the-Middle)

> [!quote] Princípio Se um atacante consegue se posicionar entre duas partes que confiam uma na outra, ele pode ler, alterar ou até se passar por qualquer uma delas.

---

## 🎯 Conceito Principal

Ataques MITM interceptam a comunicação entre duas partes que acreditam estar se comunicando diretamente. A maioria depende de manipular mecanismos de rede que confiam demais em respostas não autenticadas.

---

## 🕸️ ARP Spoofing (revisão aplicada)

Como visto em [[Cyber - Redes para Pentesters]], o protocolo ARP não autentica respostas. Um atacante na mesma rede local pode enviar respostas ARP forjadas, convencendo dois hosts de que o MAC dele é o do outro — posicionando-se no meio do tráfego entre eles.

```
Sem ataque:
Vítima ←→ Roteador ←→ Internet

Com ARP spoofing:
Vítima ←→ Atacante ←→ Roteador ←→ Internet
        (atacante intercepta e repassa o tráfego)
```

---

## 🔐 SSL Stripping — Conceito

Mesmo com tráfego posicionado no meio (via ARP spoofing, por exemplo), o HTTPS deveria impedir a leitura do conteúdo. SSL Stripping explora o momento em que uma conexão **ainda não migrou** para HTTPS.

> [!NOTE] Como funciona na prática Quando um usuário digita um endereço sem `https://`, o navegador inicialmente tenta conectar via HTTP; o servidor então normalmente redireciona para HTTPS. Um atacante posicionado no meio pode interceptar essa primeira conexão HTTP e nunca deixar o navegador da vítima migrar para HTTPS, mantendo a sessão da vítima em texto claro enquanto se conecta ele mesmo ao servidor real via HTTPS — a vítima nunca percebe, a menos que preste atenção ao cadeado do navegador.

> [!TIP] Por que HSTS existe **HSTS** (HTTP Strict Transport Security) é a defesa direta contra SSL stripping: instrui o navegador a **nunca** tentar HTTP para aquele domínio novamente, mesmo que o usuário digite o endereço sem `https://`, eliminando a janela de oportunidade que esse ataque explora.

---

## 🎭 Outros Vetores de MITM

|Vetor|Ideia central|
|---|---|
|**Evil Twin (Wi-Fi)**|AP falso imitando uma rede legítima — ver [[Cyber - Segurança em Redes Wi-Fi]]|
|**DNS Spoofing**|Responder consultas DNS com endereços forjados, redirecionando a vítima para um servidor controlado pelo atacante|
|**Rogue DHCP Server**|Servidor DHCP não autorizado que distribui um gateway/DNS malicioso para novos dispositivos na rede|

---

## 🛡️ Defesas

- **Certificate Pinning** em aplicações críticas (mobile especialmente, ver [[Cyber - Pentest em Aplicativos Android]])
- **HSTS** habilitado em todos os domínios que servem conteúdo sensível
- **Segmentação de rede** e uso de **Dynamic ARP Inspection (DAI)** em switches gerenciados, que validam respostas ARP contra uma tabela confiável
- **VPN** para tráfego sensível em redes não confiáveis (Wi-Fi público)

---

## 🔗 Notas Relacionadas

- [[Cyber - Redes para Pentesters]]
- [[Cyber - Segurança em Redes Wi-Fi]]
- [[Cyber - Pentest em Active Directory]]
- ⬅️ Voltar para [[Cybersecurity]]