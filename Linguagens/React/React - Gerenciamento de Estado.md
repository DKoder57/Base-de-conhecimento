---
tags: [matriz, react, estado, redux, context-api]

área: React JS / Avançado

status: draft

matriz: "[[React]]"

---
# 🗃️ React - Gerenciamento de Estado

> [!quote] Princípio `useState` resolve estado local muito bem. O problema começa quando dois componentes distantes na árvore precisam do mesmo dado — é aí que entram soluções de estado global.

---

## 🎯 Conceito Principal

Quando o "prop drilling" (passar props por vários níveis de componentes só para repassar adiante) começa a incomodar, existem duas abordagens principais no ecossistema React: **Context API** (nativa) e **Redux Toolkit** (biblioteca, mais robusta para apps grandes).

---

## 🧩 Context API

Nativa do React, ideal para estado que muda pouco (tema, usuário autenticado, idioma).

```jsx
import { createContext, useContext, useState } from "react";

// 1. Criar o contexto
const TemaContext = createContext();

// 2. Criar o Provider
function TemaProvider({ children }) {
  const [tema, setTema] = useState("claro");

  return (
    <TemaContext.Provider value={{ tema, setTema }}>
      {children}
    </TemaContext.Provider>
  );
}

// 3. Consumir em qualquer componente filho, sem prop drilling
function BotaoTema() {
  const { tema, setTema } = useContext(TemaContext);

  return (
    <button onClick={() => setTema(tema === "claro" ? "escuro" : "claro")}>
      Tema atual: {tema}
    </button>
  );
}
```

> [!WARNING] Context API não é otimizada para estado que muda com frequência Toda vez que o valor do Provider muda, **todos** os componentes que consomem aquele contexto re-renderizam — para estado que muda muito (ex: dados de formulário complexo, listas grandes), Redux Toolkit ou uma lib como Zustand costuma performar melhor.

---

## 🧵 Redux Toolkit (RTK)

Abordagem mais estruturada para aplicações grandes, com um único "store" central.

```bash
npm install @reduxjs/toolkit react-redux
```

```jsx
// carrinhoSlice.js
import { createSlice } from "@reduxjs/toolkit";

const carrinhoSlice = createSlice({
  name: "carrinho",
  initialState: { itens: [] },
  reducers: {
    adicionarItem: (state, action) => {
      state.itens.push(action.payload); // Redux Toolkit permite "mutar" via Immer por baixo dos panos
    },
    removerItem: (state, action) => {
      state.itens = state.itens.filter((item) => item.id !== action.payload);
    },
  },
});

export const { adicionarItem, removerItem } = carrinhoSlice.actions;
export default carrinhoSlice.reducer;
```

```jsx
// store.js
import { configureStore } from "@reduxjs/toolkit";
import carrinhoReducer from "./carrinhoSlice";

export const store = configureStore({
  reducer: { carrinho: carrinhoReducer },
});
```

```jsx
// Uso em um componente
import { useSelector, useDispatch } from "react-redux";
import { adicionarItem } from "./carrinhoSlice";

function Produto({ produto }) {
  const dispatch = useDispatch();
  const itens = useSelector((state) => state.carrinho.itens);

  return (
    <button onClick={() => dispatch(adicionarItem(produto))}>
      Adicionar ({itens.length} no carrinho)
    </button>
  );
}
```

|Conceito|Papel|
|---|---|
|`createSlice`|Define um "pedaço" do estado global + seus reducers de uma vez|
|`store`|Contêiner único de todo o estado global da aplicação|
|`useSelector`|Lê um pedaço do estado global dentro de um componente|
|`useDispatch`|Dispara uma ação que atualiza o estado global|

---

## ⚖️ Context API vs. Redux Toolkit vs. Zustand

|Critério|Context API|Redux Toolkit|Zustand|
|---|---|---|---|
|Curva de aprendizado|Baixa (nativo)|Média/Alta|Baixa|
|Boilerplate|Baixo|Médio (mas bem menor que Redux clássico)|Muito baixo|
|Performance com estado que muda muito|Fraca sem otimização extra|Boa|Boa|
|DevTools dedicado|❌ Não|✅ Redux DevTools|✅ Suporte via middleware|
|Ideal para|Estado simples/pouco mutável (tema, auth)|Apps grandes, times múltiplos|Apps de qualquer porte, API mais enxuta|

> [!NOTE] Sobre a sua stack atual Você já usa **Zustand** nos seus projetos (Jome Cargus, GreenKeeper) — vale registrar aqui como terceira opção real: resolve o mesmo problema do Redux Toolkit com uma API muito mais enxuta e sem a necessidade de Providers envolvendo a árvore de componentes.

---

## 🔗 Notas Relacionadas

- [[React - Ciclo de Vida]]
- [[React - Requisições HTTP]]
- [[ReactNative - Estado e Comunicação]]
- ⬅️ Voltar para [[React]]