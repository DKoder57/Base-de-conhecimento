---
tags: [matriz, react-native, storage, sqlite]

área: React Native / Avançado

status: draft

matriz: "[[React]]"

---
# 💾 ReactNative - Armazenamento Local

> [!quote] Princípio Nem todo dado precisa (ou deve) depender de conexão com a internet — armazenamento local é o que permite um app funcionar offline, ou pelo menos parecer mais rápido.

---

## 🎯 Conceito Principal

React Native oferece duas abordagens principais de persistência local: **AsyncStorage** (chave-valor simples) e **SQLite** (banco de dados relacional embutido, para dados estruturados e consultas complexas).

---

## 🔑 AsyncStorage — Chave-Valor

Ideal para dados simples: preferências do usuário, token de autenticação, flag de "primeira vez usando o app".

```bash
npx expo install @react-native-async-storage/async-storage
```

```jsx
import AsyncStorage from "@react-native-async-storage/async-storage";

// Salvar
async function salvarToken(token) {
  await AsyncStorage.setItem("@auth_token", token);
}

// Ler
async function obterToken() {
  const token = await AsyncStorage.getItem("@auth_token");
  return token;
}

// Remover
async function removerToken() {
  await AsyncStorage.removeItem("@auth_token");
}
```

> [!WARNING] Não é seguro para dados sensíveis AsyncStorage **não é criptografado** por padrão. Para tokens sensíveis ou credenciais, prefira `expo-secure-store`, que usa Keychain (iOS) e Keystore (Android) para armazenamento criptografado.

```jsx
import * as SecureStore from "expo-secure-store";

await SecureStore.setItemAsync("auth_token", token);
const token = await SecureStore.getItemAsync("auth_token");
```

### Armazenando objetos (JSON)

```jsx
async function salvarPreferencias(prefs) {
  await AsyncStorage.setItem("@preferencias", JSON.stringify(prefs));
}

async function obterPreferencias() {
  const json = await AsyncStorage.getItem("@preferencias");
  return json ? JSON.parse(json) : null;
}
```

---

## 🗄️ SQLite — Dados Estruturados

Para dados com relacionamentos e necessidade de consultas (ex: um app de anotações, catálogo de produtos offline, histórico de treinos).

```bash
npx expo install expo-sqlite
```

```jsx
import * as SQLite from "expo-sqlite";

const db = SQLite.openDatabaseSync("meuapp.db");

// Criar tabela
db.execSync(`
  CREATE TABLE IF NOT EXISTS tarefas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    titulo TEXT NOT NULL,
    concluida INTEGER DEFAULT 0
  );
`);

// Inserir
function adicionarTarefa(titulo) {
  db.runSync("INSERT INTO tarefas (titulo) VALUES (?);", [titulo]);
}

// Consultar
function listarTarefas() {
  return db.getAllSync("SELECT * FROM tarefas;");
}
```

> [!NOTE] Por que usar consultas parametrizadas (`?`) Assim como no back-end (ver [[Cyber - Ataques em Aplicações Web]]), usar `?` em vez de concatenar strings diretamente evita problemas de escaping e é a prática correta mesmo em um banco local.

---

## ⚖️ AsyncStorage vs. SQLite

|Critério|AsyncStorage|SQLite|
|---|---|---|
|Tipo de dado ideal|Chave-valor simples|Dados relacionais/estruturados|
|Consultas complexas (filtros, joins)|❌ Não suportado nativamente|✅ SQL completo|
|Performance com grandes volumes|Degrada com muitos dados|Mantém performance mesmo com milhares de registros|
|Curva de aprendizado|Muito baixa|Exige conhecimento básico de SQL|

---

## 🔗 Notas Relacionadas

- [[ReactNative - Integração com APIs]]
- [[Banco de Dados]]
- [[ReactNative - Testes]]
- ⬅️ Voltar para [[React]]