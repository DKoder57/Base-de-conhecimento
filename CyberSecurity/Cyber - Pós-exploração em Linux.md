---

tags: [cyber, linux, pós-exploração, escalação-de-privilégio]

área: Cibersegurança / Programação e Exploits

status: draft
matriz: "[[Cybersecurity]]"

---
# 🐧 Pós-exploração em Linux

> [!quote] Princípio Obter acesso inicial é só o começo — o valor real de um pentest está em mostrar até onde esse acesso pode ir.

---

## 🎯 Conceito Principal

Pós-exploração é a fase depois de obter acesso inicial a um sistema Linux: entender o nível de privilégio atual, buscar formas de escalar, manter acesso e mapear como se mover para outros sistemas da rede.

---

## 🔎 Enumeração Pós-Acesso

Antes de tentar escalar privilégio, é preciso mapear o terreno:

```bash
whoami; id                     # usuário e grupos atuais
uname -a                       # versão do kernel
sudo -l                        # comandos que o usuário pode rodar como root
find / -perm -4000 2>/dev/null # arquivos com bit SUID (ver [[Cyber - Linux e Shell para Pentesters]])
```

|Ferramenta de enumeração|Uso|
|---|---|
|**LinPEAS**|Script automatizado que busca dezenas de vetores conhecidos de escalação|
|**linux-exploit-suggester**|Compara a versão do kernel com exploits públicos conhecidos|

---

## ⬆️ Escalação de Privilégios — Vetores Comuns

|Vetor|Ideia central|
|---|---|
|Binários SUID mal configurados|Executam com privilégio do dono (frequentemente root)|
|Regras de `sudo` mal escopadas|Usuário pode rodar um comando específico como root que permite escapar para um shell|
|Kernel desatualizado|Vulnerável a exploits públicos de escalação conhecidos|
|Cron jobs rodando como root com script gravável|Modificar o script altera o que roda com privilégio elevado|
|Credenciais reutilizadas em arquivos de configuração|Senhas em texto puro encontradas em arquivos do sistema|

> [!TIP] GTFOBins O projeto GTFOBins documenta, para binários Unix legítimos, como eles podem ser abusados para escalar privilégio ou escapar de shells restritos quando mal configurados (ex: certas configurações de `sudo` em `find`, `vim`, `less`) — referência de consulta comum durante a fase de enumeração.

---

## 🔁 Persistência

Manter acesso ao sistema mesmo após reinício ou fechamento da sessão original.

```bash
# Exemplo conceitual: adicionar uma entrada de cron para reconexão periódica
(crontab -l ; echo "*/10 * * * * /caminho/script_de_conexao.sh") | crontab -
```

> [!NOTE] Contexto de uso Persistência só é implementada em pós-exploração dentro do escopo formalmente autorizado de um pentest ou Red Team — o objetivo é demonstrar ao cliente que, sem detecção adequada, um atacante real manteria acesso ao ambiente.

---

## ↔️ Movimentação Lateral

Uma vez com acesso a um host, o próximo passo é identificar outros sistemas alcançáveis na rede:

```bash
# Verificar interfaces de rede e rotas visíveis a partir do host comprometido
ip a
ip route
arp -a
```

Credenciais reutilizadas, chaves SSH sem senha armazenadas no host, e configurações de confiança entre máquinas (`~/.ssh/known_hosts`, `/etc/hosts`) costumam revelar o próximo alvo na cadeia de ataque.

---

## 🔗 Notas Relacionadas

- [[Cyber - Linux e Shell para Pentesters]]
- [[Cyber - Pentest em Infraestrutura de Redes]]
- [[Cyber - Pós-exploração Windows]]
- ⬅️ Voltar para [[Cybersecurity]]