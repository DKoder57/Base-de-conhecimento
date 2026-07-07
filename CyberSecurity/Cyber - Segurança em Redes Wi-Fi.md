---
tags: [cyber, mobile, android, malware]

área: Cibersegurança / Mobile

status: draft

matriz: "[[Cybersecurity]]"

---
# 🦠 Malware para Android — Conceitos e Reconhecimento

> [!quote] Princípio Entender como um malware é estruturado é o que permite reconhecê-lo, analisá-lo com segurança e construir defesas — o valor dessa área está na análise, não na criação de artefatos ofensivos reais.

---

## 🎯 Conceito Principal

Esta nota cobre, em nível conceitual, como pesquisadores de segurança **classificam e analisam** malwares Android — o objetivo é reconhecer padrões em amostras (para responder a incidentes, treinar detecção ou estudar em ambientes de laboratório isolados como sandboxes), e não fornecer um guia de criação de código malicioso funcional.

> [!WARNING] Escopo desta nota Não vou detalhar payloads funcionais, código de exploração ou passos operacionais para empacotar/distribuir malware. Esse tipo de conteúdo tem uso real para causar dano e está fora do que posso ajudar a construir. O foco aqui é **reconhecimento, categorização e defesa**.

---

## 🗂️ Categorias Comuns de Malware Mobile

|Categoria|Comportamento típico|
|---|---|
|**Trojan bancário**|Sobrepõe telas falsas (_overlay_) sobre apps de banco reais para capturar credenciais|
|**Spyware**|Coleta dados pessoais, localização, mensagens, sem consentimento|
|**Adware agressivo**|Exibe anúncios excessivos, muitas vezes dificultando o uso do app|
|**Ransomware mobile**|Bloqueia a tela ou criptografa arquivos, exigindo resgate|
|**Stalkerware**|Usado para monitorar vítimas de forma não consensual — tema também ligado a [[Cyber - Privacidade e Anonimato]]|

---

## 🔑 Permissões Abusivas — Sinais de Alerta

Do ponto de vista de **análise e defesa**, o principal indicador em apps maliciosos é a combinação de permissões pedidas versus a função real do app:

|Permissão solicitada|Alerta quando o app não tem relação com...|
|---|---|
|`SMS` / `READ_SMS`|Não é um app de mensagens|
|`ACCESSIBILITY_SERVICE`|Permissão poderosa, usada por trojans bancários para ler telas de outros apps|
|`SYSTEM_ALERT_WINDOW`|Permite sobrepor janelas — usada em ataques de _overlay_|
|`DEVICE_ADMIN`|Dificulta a desinstalação do app pelo usuário|

> [!TIP] Como isso ajuda na defesa Ferramentas de análise (incluindo soluções de MDM corporativo) frequentemente sinalizam apps que pedem permissões desproporcionais à sua categoria na loja — esse é o mesmo raciocínio que um analista de segurança aplica manualmente numa triagem.

---

## 🔁 Persistência — Como Analistas Reconhecem

Persistência é a capacidade de um malware continuar ativo após reinicialização do aparelho ou tentativa de remoção. Em nível de **reconhecimento** (para resposta a incidentes), os pontos comumente auditados são:

- Registro como `BroadcastReceiver` do evento `BOOT_COMPLETED` (reinício automático após boot)
- Abuso do papel de **Device Administrator**, que impede desinstalação direta pelas configurações
- Serviços em primeiro plano (`Foreground Service`) mantendo o processo "vivo"
- Ocultação do ícone do app na gaveta de aplicativos

> [!NOTE] Resposta a incidente em dispositivo comprometido Quando esses indicadores são encontrados, a remoção segura normalmente exige revogar o papel de administrador do dispositivo nas configurações **antes** de desinstalar o app, e, em casos graves, restaurar de fábrica.

---

## 🛡️ Defesa e Boas Práticas (para desenvolvedores e usuários)

- Distribuir apps apenas via Google Play, com o Play Protect ativo
- Revisar permissões concedidas periodicamente (`Configurações > Apps > Permissões`)
- Para desenvolvedores: aplicar **ofuscação de código legítima** (ex: R8/ProGuard) para dificultar engenharia reversa de segredos comerciais — não confundir com técnicas de evasão maliciosas (ver [[Cyber - Técnicas de Evasão de Antivírus e EDR]])
- Monitorar comportamento de rede do app em ambientes de MDM corporativo

---

## 🔗 Notas Relacionadas

- [[Cyber - Pentest em Aplicativos Android]]
- [[Cyber - Análise e Desenvolvimento de Malwares]]
- [[Cyber - Privacidade e Anonimato]]
- ⬅️ Voltar para [[Cybersecurity]]