---
tags: [cyber, pentest, evasion, av, edr]
área: Cibersegurança / Pentest
status: draft

matriz: "[[Cybersecurity]]"

---
# 🔵 Detecção Avançada de Evasão de AV/EDR (Blue Team)

> [!quote] Princípio Você não precisa saber executar um ataque para detectá-lo — precisa saber qual **rastro** ele deixa, e é isso que a engenharia de detecção estuda.

---

## 🎯 Conceito Principal

Esta nota é o complemento avançado de [[Cyber - Técnicas de Evasão de Antivírus e EDR]]: em vez de "como o atacante burla a defesa", o foco é **qual telemetria observar** para detectar cada categoria de técnica de evasão, mesmo sem entrar no "como fazer" ofensivo. É o mesmo raciocínio usado por analistas de SOC (Security Operations Center) e times de _threat hunting_.

> [!NOTE] Referência-mãe: MITRE ATT&CK O **MITRE ATT&CK** mantém uma matriz pública chamada **Defense Evasion** que cataloga, por nome, as categorias de técnicas que atacantes usam para não serem detectados. Times de defesa usam essa matriz como checklist para saber "o que meu ambiente consegue enxergar" — sem que isso signifique aprender a executar a técnica.

---
# 🛡️ Cyber - Técnicas de Evasão de Antivírus e EDR

> [!quote] Princípio  
> Em um pentest realista, a detecção por AV/EDR é o maior obstáculo pós-exploração. Dominar técnicas de evasão permite manter o acesso e operar sem alertas.

---

## 🎯 Conceito Principal

Antivírus (AV) tradicionais e soluções modernas de **Endpoint Detection and Response (EDR)** combinam detecção estática (assinaturas), heurística, comportamental e baseada em machine learning. Técnicas de evasão buscam burlar essas camadas através de **ofuscação**, **empacotamento (packers)**, execução em memória (**fileless**), manipulação de APIs e bypass de monitoramento comportamental. Essas skills são essenciais para red teaming e operações avançadas de pós-exploração.

---

## 📂 Tipos de Detecção e Estratégias Gerais de Evasão

|Tipo de Detecção|Descrição|Contra-medidas Comuns|
|---|---|---|
|**Estática (Signature-based)**|Busca por padrões conhecidos em arquivos|Ofuscação de código, criptografia, recompilação|
|**Heurística**|Análise de características suspeitas|Packers, crypters, junk code|
|**Comportamental**|Monitora ações em tempo real (API calls, injeção, etc.)|In-memory execution, indirect syscalls, sleep obfuscation|
|**EDR Avançado**|Hooking, ETW, machine learning|Unhooking, BYOVD, call stack spoofing|

---

## 🔐 Ofuscação de Código

A ofuscação altera a aparência do payload sem mudar sua funcionalidade, dificultando a detecção estática e heurística.

- **String encoding / Encryption**: Codificar strings e descriptografar em runtime.
- **Function Call Obfuscation**: Evitar imports estáticos (ex: usar hashing de nomes de funções).
- **Control Flow Manipulation**: Inserir código morto (junk code) e alterar o fluxo.
- **Shellcode Encryption**: Criptografar shellcode e decodificar apenas na memória.

---

## 🧩 Categorias de Evasão e Como Detectá-las (visão de telemetria)

|Categoria (nome usado no MITRE ATT&CK)|O que observar para detectar|
|---|---|
|**Process Injection**|Chamadas incomuns de APIs de manipulação de memória entre processos; um processo "pai" atípico gerando um processo "filho" (ex: Word → PowerShell)|
|**Living Off the Land Binaries (LOLBAS)**|Uso de binários legítimos do próprio sistema (ex: `certutil`, `mshta`, `rundll32`) com argumentos incomuns ou fora do padrão de uso normal|
|**Obfuscated/Encoded Payloads**|Comandos com grandes blocos de texto codificado em Base64, muitos caracteres de escape, ou scripts anormalmente ofuscados|
|**AMSI Bypass** (Windows)|Falhas ou ausência de eventos esperados do **AMSI (Antimalware Scan Interface)** ao executar scripts PowerShell — a ausência de log onde deveria haver é, por si só, um sinal|
|**Fileless Malware**|Atividade maliciosa que existe só em memória — exige monitoramento de processos e uso de memória, não apenas varredura de disco|
|**Timestomping**|Metadados de criação/modificação de arquivo inconsistentes com o restante do sistema|
|**Masquerading**|Binário com nome de processo legítimo (`svchost.exe`), mas rodando de um caminho de disco fora do padrão (ex: pasta de downloads)|

> [!TIP] Padrão comum entre categorias Praticamente toda técnica de evasão tenta parecer "normal" — a defesa eficaz não procura por uma assinatura única, mas por **anomalias de contexto**: um processo certo no lugar errado, um binário legítimo com comportamento atípico, um evento de log que "devia" existir e não existe.

---

## 🧰 Fontes de Telemetria para Construir Detecção

|Fonte|O que fornece|
|---|---|
|**Sysmon** (Windows)|Log detalhado de criação de processo, conexões de rede, criação de arquivos, acesso a processos — muito mais granular que o Event Viewer padrão|
|**ETW (Event Tracing for Windows)**|Fonte de telemetria de baixo nível usada pela maioria dos EDRs comerciais|
|**Auditd** (Linux)|Equivalente ao Sysmon no mundo Linux — monitora chamadas de sistema, execução de binários, acesso a arquivos sensíveis|
|**Logs de rede (NetFlow, proxy, DNS)**|Revelam beaconing (comunicação periódica com C2) mesmo quando o processo em si está bem escondido|

```
# Exemplo conceitual de Event ID do Sysmon relevantes para threat hunting:
Event ID 1  -> Criação de processo (linha de comando completa, hash do binário)
Event ID 3  -> Conexão de rede
Event ID 7  -> Carregamento de imagem/DLL
Event ID 8  -> CreateRemoteThread (indicador clássico de injeção de processo)
Event ID 11 -> Criação de arquivo
```

---

## 📜 Regras de Detecção — Sigma e YARA

Duas linguagens-padrão usadas por analistas para formalizar o que "procurar":

- **Sigma**: formato genérico de regra de detecção baseado em **logs/eventos** (ex: "alertar se `powershell.exe` for executado com `-EncodedCommand` a partir de um processo pai `winword.exe`"), convertível para a sintaxe de várias plataformas SIEM
- **YARA**: formato de regra baseado em **padrões binários/textuais** dentro de arquivos ou memória, usado para identificar famílias de malware por características estruturais, não apenas hash

> [!NOTE] Repositórios públicos de regras Projetos como o **SigmaHQ** e o **YARA Rules Project** mantêm milhares de regras de detecção open-source, criadas pela comunidade de defesa, permitindo que qualquer analista comece a detectar sem escrever tudo do zero.

---

## 🔍 Threat Hunting — Postura Proativa

Em vez de esperar um alerta automático, o _threat hunter_ parte de uma hipótese e busca ativamente evidências:

```
Hipótese: "Pode haver processos legítimos do Windows sendo
usados para baixar payloads externos (LOLBAS)"

Consulta conceitual (pseudo-KQL, comum em Microsoft Sentinel/Defender):

DeviceProcessEvents
| where FileName in ("certutil.exe", "mshta.exe", "regsvr32.exe")
| where ProcessCommandLine has_any ("http://", "https://")
```

> [!TIP] Hunting como ciclo contínuo Cada hipótese testada — confirmada ou não — deve virar uma **regra de detecção permanente** (Sigma) se representar um padrão real de risco, fechando o ciclo entre threat hunting e detecção automatizada.

---

## 🏢 Maturidade de Detecção — Onde Investir Primeiro

1. **Visibilidade** — sem Sysmon/ETW/Auditd habilitados, não há o que detectar
2. **Centralização** — enviar logs para um SIEM (Splunk, Elastic, Sentinel) para correlação entre hosts
3. **Regras de detecção** — Sigma/YARA aplicadas de forma consistente
4. **Threat Hunting proativo** — ir além do alerta automático
5. **Resposta a incidente treinada** — ter um playbook pronto para quando a detecção funcionar

---



## 🔗 Notas Relacionadas

- [[Cyber - Técnicas de Evasão de Antivírus e EDR]]
- [[Cyber - Pós-exploração Windows]]
- [[Cyber - Análise e Desenvolvimento de Malwares]]
- ⬅️ Voltar para [[Cybersecurity]]