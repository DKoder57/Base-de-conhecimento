---
tags: [matriz, react, performance, deploy]
área: React JS / Avançado

status: draft

matriz: "[[React]]"

---
# ⚡ React - Performance e Deploy

> [!quote] Princípio A maior parte da lentidão em apps React vem de re-renders desnecessários — otimizar é, na maioria das vezes, evitar trabalho que nem precisava acontecer.

---

## 🎯 Conceito Principal

Esta nota cobre as ferramentas de otimização mais usadas do React (memoização, lazy loading, listas virtualizadas) e o processo de colocar a aplicação em produção.

---

## 🧠 `React.memo` — Evitando Re-render de Componentes

```jsx
const Produto = React.memo(function Produto({ nome, preco }) {
  console.log("Renderizando:", nome);
  return <p>{nome} - R$ {preco}</p>;
});
```

`React.memo` faz o componente **pular o re-render** se as props recebidas forem as mesmas da última renderização (comparação rasa).

> [!WARNING] Cuidado com objetos/funções recriados a cada render Se o componente pai recria um objeto ou função a cada render e passa como prop, `React.memo` não ajuda sozinho — o valor "parece" diferente mesmo sendo funcionalmente igual. É aqui que `useMemo` e `useCallback` entram.

---

## 🧮 `useMemo` e `useCallback`

```jsx
import { useMemo, useCallback, useState } from "react";

function ListaProdutos({ produtos }) {
  const [filtro, setFiltro] = useState("");

  // useMemo: evita recalcular a lista filtrada em todo render
  const produtosFiltrados = useMemo(
    () => produtos.filter((p) => p.nome.includes(filtro)),
    [produtos, filtro]
  );

  // useCallback: mantém a mesma referência de função entre renders
  const handleClique = useCallback((id) => {
    console.log("Produto clicado:", id);
  }, []);

  return (
    <ul>
      {produtosFiltrados.map((p) => (
        <ProdutoItem key={p.id} produto={p} onClick={handleClique} />
      ))}
    </ul>
  );
}
```

|Hook|Memoiza|Quando usar|
|---|---|---|
|`useMemo`|Um **valor** calculado|Cálculos custosos que não precisam repetir a cada render|
|`useCallback`|Uma **função**|Passar funções como prop para componentes memoizados com `React.memo`|

> [!TIP] Não otimize prematuramente `useMemo`/`useCallback` têm seu próprio custo de execução. Use quando houver um problema de performance real e mensurável (ex: via React DevTools Profiler), não como hábito automático em todo componente.

---

## 🔁 `useReducer` — Estado Complexo Local

Alternativa ao `useState` quando a lógica de atualização de estado tem múltiplas transições relacionadas.

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "incrementar":
      return { contador: state.contador + 1 };
    case "resetar":
      return { contador: 0 };
    default:
      throw new Error("Ação desconhecida");
  }
}

function Contador() {
  const [state, dispatch] = useReducer(reducer, { contador: 0 });

  return (
    <button onClick={() => dispatch({ type: "incrementar" })}>
      {state.contador}
    </button>
  );
}
```

---

## 🐌 Lazy Loading e `react-window`

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<p>Carregando módulo...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

> [!NOTE] Por que isso importa `lazy` + `Suspense` faz o _bundle_ daquele componente só ser baixado quando necessário (code splitting), reduzindo o tempo de carregamento inicial da aplicação.

Para listas muito grandes (milhares de itens), renderizar tudo de uma vez trava a interface — `react-window` renderiza **apenas os itens visíveis na tela**:

```jsx
import { FixedSizeList } from "react-window";

function ListaGrande({ itens }) {
  return (
    <FixedSizeList height={400} itemCount={itens.length} itemSize={35} width="100%">
      {({ index, style }) => <div style={style}>{itens[index].nome}</div>}
    </FixedSizeList>
  );
}
```

---

## 🚀 Deploy

|Plataforma|Características|
|---|---|
|**Vercel**|Feito pela empresa por trás do Next.js, deploy automático a cada push, ótimo para SSR/SSG|
|**Netlify**|Alternativa consolidada, forte em builds estáticos e funções serverless|
|**GitHub Pages**|Gratuito, ideal para SPAs puramente estáticas (sem back-end integrado)|

```yaml
# Exemplo conceitual de CI/CD com GitHub Actions para deploy automático
name: Deploy
on:
  push:
    branches: [main]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install && npm run build
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

> [!NOTE] Seu fluxo atual No Jome Cargus você já usa Vercel para os front-ends e Railway para o back-end FastAPI — esse par (Vercel + Railway) cobre bem a maioria dos projetos full-stack com React no front.

---

## 🔗 Notas Relacionadas

- [[React - Gerenciamento de Estado]]
- [[React - Ciclo de Vida]]
- [[Ferramentas]]
- ⬅️ Voltar para [[React]]