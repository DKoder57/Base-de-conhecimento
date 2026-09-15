---
tags: [matriz, react, http, firebase]

área: React JS / Avançado

status: draft

matriz: "[[React]]"

---
# 🌐 React - Requisições HTTP

> [!quote] Princípio Toda aplicação real conversa com um servidor — a diferença entre um app amador e um profissional está em como ele trata o tempo de espera e os erros dessa conversa.

---

## 🎯 Conceito Principal

React não tem uma forma "oficial" de fazer requisições HTTP — usa-se a API nativa `fetch` ou bibliotecas como `axios`, sempre combinadas com estados de carregamento (`loading`) e erro (`error`) para uma boa experiência de usuário.

---

## 📡 `fetch` — API Nativa do Navegador

```jsx
import { useState, useEffect } from "react";

function ListaProdutos() {
  const [produtos, setProdutos] = useState([]);
  const [carregando, setCarregando] = useState(true);
  const [erro, setErro] = useState(null);

  useEffect(() => {
    fetch("https://api.exemplo.com/produtos")
      .then((res) => {
        if (!res.ok) throw new Error("Falha na requisição");
        return res.json();
      })
      .then(setProdutos)
      .catch(setErro)
      .finally(() => setCarregando(false));
  }, []);

  if (carregando) return <p>Carregando...</p>;
  if (erro) return <p>Erro: {erro.message}</p>;

  return (
    <ul>
      {produtos.map((p) => (
        <li key={p.id}>{p.nome}</li>
      ))}
    </ul>
  );
}
```

> [!WARNING] `fetch` não rejeita em erro HTTP Diferente do que se espera, `fetch` só rejeita a Promise em falha de rede — um erro 404 ou 500 ainda "resolve" normalmente. Por isso é necessário checar `res.ok` manualmente, como no exemplo acima.

---

## 📦 Axios — Alternativa Popular

```bash
npm install axios
```

```jsx
import axios from "axios";

async function buscarProdutos() {
  try {
    const { data } = await axios.get("https://api.exemplo.com/produtos");
    return data;
  } catch (erro) {
    if (axios.isAxiosError(erro)) {
      console.error("Erro na requisição:", erro.response?.status);
    }
    throw erro;
  }
}
```

|Recurso|`fetch`|`axios`|
|---|---|---|
|Rejeita em erro HTTP (4xx/5xx)|❌ Não (precisa checar `res.ok`)|✅ Sim, automaticamente|
|Parse de JSON automático|❌ Precisa chamar `.json()`|✅ Automático em `data`|
|Interceptors (ex: adicionar token em toda requisição)|❌ Não nativo|✅ Sim, `axios.interceptors`|
|Cancelamento de requisição|`AbortController`|`CancelToken` / `AbortController`|

---

## 📮 Requisições POST

```jsx
async function criarProduto(novoProduto) {
  const resposta = await fetch("https://api.exemplo.com/produtos", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(novoProduto),
  });

  if (!resposta.ok) throw new Error("Erro ao criar produto");
  return resposta.json();
}
```

---

## 🔥 Integração com Firebase Firestore

Firestore usa seu próprio SDK, com listeners em tempo real em vez de requisições tradicionais.

```jsx
import { collection, getDocs, addDoc } from "firebase/firestore";
import { db } from "./firebaseConfig";

// Leitura
async function buscarProdutos() {
  const snapshot = await getDocs(collection(db, "produtos"));
  return snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
}

// Escrita
async function criarProduto(dados) {
  await addDoc(collection(db, "produtos"), dados);
}
```

> [!TIP] Tempo real com `onSnapshot` Diferente de `fetch`/`axios`, o Firestore permite "escutar" mudanças em tempo real com `onSnapshot`, atualizando a UI automaticamente sem precisar re-buscar os dados manualmente — útil para chats, dashboards ao vivo, etc.

> [!NOTE] Padrão que você já usa Como seu stack atual usa Supabase (Postgres) em vez de Firestore, o equivalente lá é o client `supabase-js`, que também suporta _subscriptions_ em tempo real via `supabase.channel()`.

---

## 🔗 Notas Relacionadas

- [[React - Ciclo de Vida]]
- [[React - Gerenciamento de Estado]]
- [[ReactNative - Integração com APIs]]
- ⬅️ Voltar para [[React]]