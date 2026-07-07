---

tags: [cyber, side-channel, fault-injection, hardware]

área: Cibersegurança / Programação e Exploits

status: draft

matriz: "[[Cybersecurity]]"

---
# ⚡ Side-channel Analysis e Fault Injection

> [!quote] Princípio Nem todo ataque explora um bug de lógica — alguns exploram as leis da física: o quanto um chip consome de energia, ou o que acontece quando ele recebe um pulso elétrico fora do esperado.

---

## 🎯 Conceito Principal

Ataques de canal lateral (_side-channel_) extraem informação secreta (como uma chave criptográfica) observando efeitos **físicos colaterais** da execução — consumo de energia, tempo de processamento, emissão eletromagnética — em vez de atacar o algoritmo matematicamente.

---

## 📊 Análise de Consumo de Energia

Operações criptográficas diferentes (ex: multiplicar por 0 vs. por 1 durante uma operação de chave RSA) consomem quantidades de energia sutilmente diferentes, capturáveis com um osciloscópio.

|Técnica|Ideia central|
|---|---|
|**SPA** (Simple Power Analysis)|Observação direta do traço de energia, buscando padrões visíveis a olho nu|
|**DPA** (Differential Power Analysis)|Análise estatística de milhares de traços para extrair a chave mesmo com ruído|
|**CPA** (Correlation Power Analysis)|Correlaciona o consumo observado com um modelo matemático de consumo esperado para cada byte de chave candidato|

```
Fluxo conceitual de um ataque CPA contra AES:
1. Capturar o traço de energia durante centenas/milhares de operações
   de cifragem com textos diferentes
2. Para cada byte de chave candidato, calcular o consumo teórico esperado
3. Correlacionar estatisticamente o consumo teórico com o real capturado
4. O candidato com maior correlação é, com alta probabilidade, o byte correto
```

> [!NOTE] Por que isso é possível Circuitos CMOS consomem energia proporcional ao número de bits que mudam de estado durante uma operação — esse vazamento físico sutil, agregado estatisticamente ao longo de muitas medições, revela informação sobre os dados processados internamente.

---

## 💥 Fault Injection (Glitching)

Em vez de apenas observar, o atacante **induz um erro controlado** no hardware (queda de tensão momentânea, pulso de clock irregular, laser) para fazer o chip pular uma instrução ou retornar um valor incorreto.

|Técnica|Mecanismo|
|---|---|
|**Voltage glitching**|Queda momentânea de tensão de alimentação no momento exato de uma instrução crítica (ex: verificação de senha)|
|**Clock glitching**|Pulso de clock fora da especificação, causando execução incorreta de uma instrução|
|**Laser fault injection**|Pulso de laser preciso sobre uma região do chip (técnica de laboratório avançada)|

> [!WARNING] Objetivo típico de um glitch Um alvo clássico de fault injection é uma checagem de senha ou verificação de assinatura (`if (senha_correta) { ... }`) — o glitch é temporizado para acontecer exatamente durante essa comparação, tentando fazer o chip "pular" o desvio de fluxo e considerar a verificação bem-sucedida indevidamente.

---

## 🎓 Aprendizado Prático — ChipWhisperer

O **ChipWhisperer** é a plataforma open-source de referência para aprender essa área na prática, com cursos gratuitos que ensinam desde a captura do primeiro traço de energia até a quebra completa de uma implementação de AES-128 em ambiente de laboratório controlado.

---

## 🛡️ Contramedidas

- **Mascaramento (masking)**: randomizar valores intermediários para que o consumo de energia não se correlacione diretamente com a chave real
- **Balanceamento de operações**: implementações que consomem a mesma energia independente do dado processado
- **Detecção de glitch**: circuitos de monitoramento de tensão/clock que zeram registradores sensíveis se detectarem anomalia

---

## 🔗 Notas Relacionadas

- [[Cyber - Hardware Hacking]]
- [[Cyber - Criptografia e Senhas]]
- ⬅️ Voltar para [[Cybersecurity]]