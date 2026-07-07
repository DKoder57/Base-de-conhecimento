---

tags: [cyber, pentest, web, owasp]

área: Cibersegurança / Pentest

status: draft

matriz: "[[Cybersecurity]]"

---
# 🕷️ Ataques em Aplicações Web

> [!quote] Princípio A maioria das falhas web não é sofisticada — é a mesma classe de erro (falta de validação/autorização) se repetindo há 20 anos.

---

## 🎯 Conceito Principal

O **OWASP Top 10** é a referência mais usada da indústria para categorizar os riscos mais críticos em aplicações web. Esta nota cobre os conceitos por trás das categorias mais clássicas — o objetivo é reconhecer o **padrão da falha**, não construir exploits avançados.

---

## 🔟 OWASP Top 10 — Visão Geral

|Categoria (edição mais recente)|Ideia central|
|---|---|
|Broken Access Control|Usuário acessa recursos/ações que não deveria (ex: IDOR)|
|Cryptographic Failures|Dados sensíveis expostos por criptografia ausente/fraca|
|Injection (SQLi, Command Injection etc.)|Entrada do usuário interpretada como código/comando|
|Insecure Design|Falha estrutural, não apenas de implementação|
|Security Misconfiguration|Configurações padrão, painéis expostos, headers ausentes|
|Vulnerable and Outdated Components|Bibliotecas/frameworks desatualizados com CVEs conhecidos|
|Identification and Authentication Failures|Login fraco, sessão mal gerenciada|
|Software and Data Integrity Failures|Confiança indevida em pacotes/atualizações não verificadas|
|Security Logging and Monitoring Failures|Ataques não detectados por falta de log/alerta|
|Server-Side Request Forgery (SSRF)|Servidor é induzido a fazer requisições para onde não deveria|

---

## 💉 SQL Injection (SQLi) — Conceito

Ocorre quando entrada do usuário é concatenada diretamente em uma consulta SQL, permitindo alterar a lógica da query.

```python
# Código vulnerável (nunca fazer isso)
query = f"SELECT * FROM usuarios WHERE nome = '{nome_informado}'"
```

> [!NOTE] A defesa correta Usar **consultas parametrizadas** (prepared statements) elimina a classe inteira de vulnerabilidade, pois a entrada nunca é interpretada como parte do comando SQL:
> 
> ```python
> cursor.execute("SELECT * FROM usuarios WHERE nome = %s", (nome_informado,))
> ```

---

## 🎭 Cross-Site Scripting (XSS) — Conceito

Ocorre quando entrada do usuário é refletida em HTML sem _sanitização_, permitindo injeção de scripts no navegador de outra vítima.

|Tipo|Onde acontece|
|---|---|
|**Refletido**|O payload vem da própria requisição (ex: parâmetro de busca)|
|**Armazenado**|O payload fica salvo no servidor (ex: comentário de blog)|
|**DOM-based**|A falha está no JavaScript do lado do cliente|

> [!TIP] Defesa Escapar/_encode_ toda saída de dados controlados pelo usuário antes de renderizar em HTML, e usar cabeçalhos como `Content-Security-Policy`.

---

## 🔁 Cross-Site Request Forgery (CSRF) — Conceito

Um site malicioso induz o navegador da vítima (já autenticado em outro site) a enviar uma requisição indesejada, aproveitando o cookie de sessão automaticamente enviado pelo navegador.

> [!NOTE] Defesa Uso de **tokens CSRF** únicos por sessão/formulário, além do atributo de cookie `SameSite=Strict` ou `Lax`.

---

## 📤 Upload de Arquivos Malicioso — Conceito

Falha ocorre quando a aplicação aceita upload sem validar corretamente **tipo real** do arquivo, permitindo o envio de um arquivo executável disfarçado de imagem, por exemplo.

> [!WARNING] Pontos de checagem em uma validação correta
> 
> - Validar o conteúdo real do arquivo (magic bytes), não apenas a extensão
> - Renomear o arquivo ao salvar, removendo controle do atacante sobre o nome
> - Armazenar uploads fora do diretório executável pela aplicação
> - Limitar tipos MIME permitidos no back-end (nunca confiar em validação apenas no front-end)

---

## 🧰 Ferramentas de Apoio

|Ferramenta|Uso|
|---|---|
|**Burp Suite**|Proxy de interceptação, ponto central do pentest web|
|**OWASP ZAP**|Alternativa open-source ao Burp|
|**sqlmap**|Automatiza a detecção/exploração de SQLi (uso apenas em ambiente autorizado)|

---

## 🔗 Notas Relacionadas

- [[Cyber - Desenvolvimento Web para Pentesters]]
- [[Cyber - Automação em Bug Bounty]]
- [[Cyber - Inteligência Artificial aplicada a Pentest Web]]
- ⬅️ Voltar para [[Cybersecurity]]