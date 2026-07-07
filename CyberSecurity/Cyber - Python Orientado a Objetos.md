---

tags: [cyber, fundamentos, python, poo]
área: Cibersegurança / Fundamentos

status: draft

matriz: "[[Cybersecurity]]"

---
# 🧱 Python Orientado a Objetos (aplicado a Segurança)

> [!quote] Princípio Ferramentas de pentest crescem rápido em complexidade — POO é o que mantém o código organizado quando um script vira um framework.

---

## 🎯 Conceito Principal

Muitas ferramentas ofensivas reais (Metasploit, sqlmap, Impacket) são estruturadas em classes: cada módulo de exploração, cada protocolo, cada alvo vira um objeto com estado e comportamento próprios. Dominar POO é o que permite migrar de "script solto" para "ferramenta reutilizável".

---

## 🏗️ Classes e Atributos — Modelando um Alvo

```python
class Alvo:
    def __init__(self, ip: str, portas_abertas: list[int]):
        self.ip = ip
        self.portas_abertas = portas_abertas
        self.vulnerabilidades = []

    def adicionar_vulnerabilidade(self, descricao: str):
        self.vulnerabilidades.append(descricao)

    def __str__(self):
        return f"Alvo({self.ip}) - Portas: {self.portas_abertas}"


alvo1 = Alvo("192.168.0.10", [22, 80, 443])
alvo1.adicionar_vulnerabilidade("Apache desatualizado (CVE genérico de exemplo)")
print(alvo1)
```

> [!TIP] `__str__` e `__repr__` Sobrescrever esses métodos mágicos deixa seus relatórios de varredura muito mais legíveis quando você faz `print()` de uma lista de objetos.

---

## 🧬 Herança — Especializando Comportamentos

```python
class ServicoWeb(Alvo):
    def __init__(self, ip, portas_abertas, cms=None):
        super().__init__(ip, portas_abertas)
        self.cms = cms  # ex: WordPress, Joomla

    def verificar_cms(self):
        if self.cms:
            print(f"CMS identificado: {self.cms}")
        else:
            print("Nenhum CMS identificado.")


site = ServicoWeb("10.0.0.5", [80, 443], cms="WordPress")
site.verificar_cms()
```

---

## 🎭 Polimorfismo — Interface Comum para Diferentes Ataques

```python
class TecnicaDeVarredura:
    def executar(self, alvo: Alvo):
        raise NotImplementedError

class VarreduraDePortas(TecnicaDeVarredura):
    def executar(self, alvo: Alvo):
        print(f"Varrendo portas de {alvo.ip}...")

class VarreduraDeVulnerabilidades(TecnicaDeVarredura):
    def executar(self, alvo: Alvo):
        print(f"Buscando vulnerabilidades conhecidas em {alvo.ip}...")


tecnicas = [VarreduraDePortas(), VarreduraDeVulnerabilidades()]
for tecnica in tecnicas:
    tecnica.executar(alvo1)
```

> [!NOTE] Por que isso importa em pentest? Esse padrão (interface comum + implementações diferentes) é exatamente como ferramentas como o Nmap organizam seus _scripts_ (NSE) ou como o Metasploit organiza seus módulos — cada um implementa a mesma "interface" de execução.

---

## 🛡️ Encapsulamento

```python
class Credencial:
    def __init__(self, usuario, senha_hash):
        self.usuario = usuario
        self.__senha_hash = senha_hash  # atributo "privado" por convenção

    def verificar(self, hash_tentativa):
        return self.__senha_hash == hash_tentativa
```

---

## 🔗 Notas Relacionadas

- [[Python - Pilares da OO]]
- [[Cyber - Python Básico e Algoritmos]]
- [[Cyber - Automação em Bug Bounty]]
- ⬅️ Voltar para [[Cybersecurity]]