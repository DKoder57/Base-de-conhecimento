---
tags: [cyber, fundamentos, python, algoritmos]
área: Cibersegurança / Fundamentos
status: draft

matriz: "[[Cybersecurity]]"

---
# 🐍 Python Básico e Algoritmos

> [!quote] Princípio Python é a linguagem de automação preferida no pentest: rápida de escrever, com bibliotecas prontas para rede, web e parsing de dados.

---

## 🎯 Conceito Principal

Como você já tem uma matriz dedicada de Python fundamentos ([[Python]]), esta nota foca na aplicação da lógica de programação **especificamente para segurança ofensiva**: automatizar reconhecimento, parsear saídas de ferramentas e criar pequenos exploits/PoCs.

---

## 🧠 Estruturas de Controle Aplicadas

```python
# Exemplo: verificar portas comuns abertas (conceito, sem uso de sockets ainda)
portas_comuns = {21: "FTP", 22: "SSH", 80: "HTTP", 443: "HTTPS", 3306: "MySQL"}

for porta, servico in portas_comuns.items():
    print(f"Porta {porta} -> Serviço esperado: {servico}")
```

> [!TIP] Dicionários como "tabelas de referência" Em segurança, dicionários Python são úteis para mapear portas → serviços, códigos HTTP → significado, ou hashes → senhas conhecidas (wordlists).

---

## 🔁 Laços e Listas — Automatizando Tarefas

```python
alvos = ["192.168.0.1", "192.168.0.2", "192.168.0.3"]

for alvo in alvos:
    print(f"Analisando host: {alvo}")
    # aqui entraria a chamada a uma biblioteca de rede, ex: socket ou requests
```

### List Comprehension aplicada

```python
# Filtrar apenas hosts da sub-rede 192.168.0.0/24
hosts = ["192.168.0.5", "10.0.0.1", "192.168.0.20"]
hosts_rede = [h for h in hosts if h.startswith("192.168.0.")]
print(hosts_rede)
```

---

## 📄 Manipulação de Strings e Arquivos

Wordlists, logs e resultados de ferramentas quase sempre chegam como texto puro — saber processá-los é metade do trabalho de automação.

```python
with open("wordlist.txt", "r") as f:
    senhas = [linha.strip() for linha in f.readlines()]

print(f"Total de senhas carregadas: {len(senhas)}")
```

> [!NOTE] Encoding Wordlists e dumps de credenciais nem sempre estão em UTF-8. Ao encontrar erros de leitura, tente `encoding="latin-1"` ou trate exceções com `try/except`.

---

## 🧩 Funções — Organizando Lógica Reutilizável

```python
def validar_ip(ip: str) -> bool:
    partes = ip.split(".")
    if len(partes) != 4:
        return False
    return all(p.isdigit() and 0 <= int(p) <= 255 for p in partes)

print(validar_ip("192.168.0.1"))   # True
print(validar_ip("999.1.1.1"))     # False
```

---

## 🔗 Notas Relacionadas

- [[Python - Estruturas de Repetição]]
- [[Python - Listas]]
- [[Cyber - Python Orientado a Objetos]]
- [[Cyber - Automação em Bug Bounty]]
- ⬅️ Voltar para [[Cybersecurity]]