---
tags: [cyber, windows, pós-exploração, credenciais]

área: Cibersegurança / Windows e Active Directory

status: draft

matriz: "[[Cybersecurity]]"

---
# 🪟 Pós-exploração Windows

> [!quote] Princípio Windows corporativo raramente é comprometido por um único exploit espetacular — é comprometido por credenciais reaproveitadas de máquina em máquina.

---

## 🎯 Conceito Principal

Após obter acesso inicial a uma máquina Windows, a pós-exploração foca em extrair credenciais armazenadas localmente, entender o nível de privilégio obtido e usar isso como trampolim para outras máquinas da rede — especialmente em ambientes com Active Directory (ver [[Cyber - Pentest em Active Directory]]).

---

## 🔑 Dumping de Credenciais — Conceitos

O Windows armazena credenciais em memória e em bancos locais para permitir Single Sign-On e login automático — esse mesmo mecanismo de conveniência é o alvo de dumping.

|Alvo|O que é|
|---|---|
|**LSASS** (processo)|Guarda hashes NTLM e, em certas configurações, senhas em texto claro na memória|
|**SAM** (Security Account Manager)|Banco local de hashes de senha dos usuários da máquina|
|**Credential Manager**|Armazena credenciais salvas de aplicações e compartilhamentos de rede|

> [!NOTE] Ferramenta de referência **Mimikatz** é a ferramenta historicamente associada à extração de credenciais da memória do processo LSASS — seu funcionamento é amplamente documentado na literatura de segurança justamente porque motivou mudanças defensivas importantes no Windows moderno (como o Credential Guard).

---

## 🎫 Tokens de Acesso

Windows usa **tokens** para representar a identidade e privilégios de um processo em execução — diferente de uma senha, um token já é uma "sessão autenticada" pronta para uso.

|Conceito|Implicação para pós-exploração|
|---|---|
|**Token de acesso primário**|Representa a identidade do usuário dono do processo|
|**Token de impersonation**|Permite que um processo "se passe" temporariamente por outro usuário|
|**Roubo de token**|Se um atacante já tem privilégio de sistema, pode reutilizar tokens de outros usuários logados na mesma máquina, sem precisar da senha deles|

---

## 🛡️ Defesas Modernas Contra Dumping

|Mecanismo|Como mitiga|
|---|---|
|**Credential Guard**|Isola credenciais em um ambiente virtualizado separado do LSASS comum|
|**LSA Protection (RunAsPPL)**|Impede que processos não assinados acessem a memória do LSASS|
|**Desativar armazenamento de credenciais em texto claro (WDigest)**|Reduz o que fica exposto na memória mesmo se o LSASS for acessado|

---

## ↔️ Movimentação Lateral com Credenciais Obtidas

Um padrão comum de ataque conhecido como **Pass-the-Hash** reutiliza o hash NTLM diretamente para autenticação, sem nunca precisar quebrar/decifrar a senha original — já que muitos protocolos Windows aceitam o hash como prova de identidade.

> [!WARNING] Por que Pass-the-Hash funciona Historicamente, o protocolo NTLM autentica com base no **hash**, não na senha em si — por isso, obter o hash já é suficiente para se autenticar em outros sistemas que aceitem as mesmas credenciais, sem nunca precisar saber a senha em texto claro.

---

## 🔗 Notas Relacionadas

- [[Cyber - PowerShell para Pentesters]]
- [[Cyber - Pentest em Active Directory]]
- [[Cyber - Pós-exploração em Linux]]
- ⬅️ Voltar para [[Cybersecurity]]