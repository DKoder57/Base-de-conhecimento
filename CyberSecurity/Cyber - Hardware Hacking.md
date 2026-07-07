---

tags: [cyber, hardware, jtag, uart, firmware]

área: Cibersegurança / Programação e Exploits
status: draft`

matriz: "[[Cybersecurity]]"

---
# 🔩 Hardware Hacking

> [!quote] Princípio Todo dispositivo físico tem uma interface de depuração esquecida pelo fabricante — encontrá-la costuma ser o primeiro passo de qualquer análise de hardware.

---

## 🎯 Conceito Principal

Hardware hacking foca em extrair firmware, identificar interfaces de depuração e entender a arquitetura física de dispositivos embarcados (roteadores, IoT, dispositivos industriais) — normalmente o passo anterior a uma análise de firmware mais profunda.

---

## 🔌 Interfaces de Depuração Comuns

|Interface|Função|Ferramenta típica de acesso|
|---|---|---|
|**UART**|Console serial, muitas vezes deixado ativo pelo fabricante para debug|Adaptador USB-Serial (ex: FTDI)|
|**JTAG**|Interface de depuração de baixo nível para acesso direto ao processador|JTAGulator, adaptadores dedicados|
|**SPI**|Barramento usado por chips de memória flash (onde o firmware é armazenado)|Programador SPI (ex: CH341A)|
|**I2C**|Barramento para comunicação entre componentes internos|Analisadores lógicos|

> [!TIP] Identificando pinos desconhecidos Ferramentas como o **JTAGulator** testam automaticamente combinações de pinos em uma placa para identificar quais correspondem a UART ou JTAG, quando a documentação do fabricante não está disponível.

---

## 💾 Extração de Firmware

```
Fluxo conceitual de extração via chip SPI:
1. Identificar o chip de memória flash na placa
2. Conectar um programador SPI diretamente aos pinos do chip
3. Realizar o dump (leitura completa) da memória para um arquivo binário
4. Analisar o binário com ferramentas de extração (ex: binwalk)
```

```bash
# Análise de um firmware extraído em busca de sistemas de arquivos embutidos
binwalk -e firmware.bin
```

> [!NOTE] O que se busca dentro de um firmware Credenciais hardcoded, chaves privadas, certificados, ou binários customizados que possam depois ser analisados estaticamente — o firmware extraído vira insumo direto para engenharia reversa de software (ver [[Cyber - Análise e Desenvolvimento de Malwares]]).

---

## 🖥️ Console Serial via UART

```bash
# Conectar a um console UART identificado (Linux, usando o adaptador USB-Serial)
screen /dev/ttyUSB0 115200
```

Muitos dispositivos embarcados deixam um shell de bootloader (ex: U-Boot) acessível via UART sem autenticação, permitindo interromper o boot normal e acessar um shell privilegiado antes mesmo do sistema operacional carregar completamente.

---

## 🛡️ Boas Práticas para Fabricantes (Defesa)

- Desativar ou remover fisicamente interfaces de debug (UART/JTAG) em produtos finais
- Exigir autenticação mesmo no bootloader
- Cifrar e assinar digitalmente o firmware, verificando integridade no boot (_secure boot_)
- Nunca armazenar segredos (chaves, senhas) em texto puro dentro do firmware

---

## 🔗 Notas Relacionadas

- [[Cyber - Side-channel Analysis e Fault Injection]]
- [[Cyber - Análise e Desenvolvimento de Malwares]]
- [[Cyber - Exploração de Jogos e Hardware]]
- ⬅️ Voltar para [[Cybersecurity]]