---
tags: [cyber, fundamentos, criptografia, senhas]
área: Cibersegurança / Fundamentos
status: draft
matriz: "[[Cybersecurity]]"
---
# 🔑 Criptografia e Senhas

> [!quote] Princípio Criptografia não impede o ataque — ela torna o custo de quebrá-la maior do que o valor da informação protegida.

---

## 🎯 Conceito Principal

Criptografia é a ciência de transformar informação de forma que apenas partes autorizadas consigam interpretá-la. Em segurança ofensiva, entender como as senhas e chaves são armazenadas/transmitidas ajuda a **identificar más práticas** (não a "quebrar tudo").

---

## 🔒 Criptografia Simétrica vs. Assimétrica

|Tipo|Como funciona|Exemplo de uso|
|---|---|---|
|**Simétrica**|Mesma chave cifra e decifra|AES (dados em repouso, VPNs)|
|**Assimétrica**|Par de chaves: pública (cifra) e privada (decifra)|RSA, ECC (TLS/HTTPS, SSH, assinatura digital)|

> [!TIP] Por que combinar as duas? TLS usa criptografia assimétrica só para negociar uma chave simétrica de sessão (mais rápida), e depois cifra o tráfego com simetria — o melhor dos dois mundos.

---

## #️⃣ Hashing — Não é Criptografia Reversível

Hash é uma função **de mão única**: transforma qualquer entrada em uma saída de tamanho fixo, sem possibilidade de reverter matematicamente.

```python
import hashlib

senha = "minhasenha123"
hash_sha256 = hashlib.sha256(senha.encode()).hexdigest()
print(hash_sha256)
```

|Algoritmo|Situação atual|
|---|---|
|MD5|Quebrado/inseguro para senhas (colisões conhecidas)|
|SHA-1|Também considerado fraco|
|SHA-256|Seguro para integridade, mas **rápido demais** para senhas|
|**bcrypt / scrypt / Argon2**|Recomendados para senhas: são propositalmente **lentos** e usam _salt_|

> [!NOTE] Por que "lento" é uma vantagem? Um hash rápido (como SHA-256 puro) permite que um atacante teste bilhões de combinações por segundo em GPU. Algoritmos como bcrypt e Argon2 são desenhados para consumir tempo/memória, tornando ataques de força bruta economicamente inviáveis em escala.

---

## 🧂 Salt e Pepper

- **Salt**: valor aleatório único por senha, armazenado junto ao hash. Impede o uso de _rainbow tables_ (tabelas pré-computadas de hash → senha).
- **Pepper**: valor secreto adicional, mantido fora do banco de dados (ex: variável de ambiente), somando uma camada extra.

```python
import bcrypt

senha = b"minhasenha123"
hash_com_salt = bcrypt.hashpw(senha, bcrypt.gensalt())
print(hash_com_salt)

# Verificação
print(bcrypt.checkpw(senha, hash_com_salt))  # True
```

---

## 📋 Política de Senhas — Boas Práticas

- Priorizar **comprimento** sobre complexidade forçada (uma frase longa é mais forte que `P@ssw0rd!`)
- Usar autenticação multifator (MFA/2FA) sempre que possível
- Nunca reutilizar senhas entre serviços — gerenciadores de senha resolvem isso
- Detectar senhas vazadas com serviços como _Have I Been Pwned_ (via API, sem enviar a senha em texto puro — usa _k-anonymity_ com prefixo de hash)

> [!WARNING] Sobre ataques de senha Ferramentas de quebra de senha (ex: John the Ripper, Hashcat) só devem ser usadas em hashes obtidos de forma autorizada — laboratórios próprios, CTFs, ou pentests com escopo definido. Ver [[Cyber - Metodologias de Pentest]] para o processo de autorização.

---

## 🔗 Notas Relacionadas

- [[Cyber - Python Orientado a Objetos]]
- [[Cyber - Ataques em Aplicações Web]]
- [[Cyber - Privacidade e Anonimato]]
- ⬅️ Voltar para [[Cybersecurity]]