---
tags: [matriz, react, server-components, nextjs]

área: React JS / Estado da Arte (2026)

status: draft

matriz: "[[React]]"
---

# 🖥️ React - Server Components e Next.js App Router

> [!quote] Princípio Nem todo componente precisa rodar no navegador — em 2026, a pergunta padrão virou "isso realmente precisa de interatividade no cliente, ou só precisa mostrar dado?"

---

## 🎯 Conceito Principal

React Server Components (RSC) são componentes que rodam **apenas no servidor**, nunca são enviados como JavaScript para o navegador. Isso reduz drasticamente o tamanho do bundle final e permite acessar recursos de servidor (banco de dados, sistema de arquivos) diretamente no componente.

---

## ⚖️ Server Components vs. Client Components

|Característica|Server Component (padrão)|Client Component (`'use client'`)|
|---|---|---|
|Onde executa|Apenas no servidor|Servidor (SSR inicial) + navegador|
|Pode usar `useState`/`useEffect`|❌ Não|✅ Sim|
|Pode usar `async/await` direto no componente|✅ Sim|❌ Não (precisa de `useEffect` ou biblioteca)|
|Acesso direto a banco de dados/arquivos|✅ Sim|❌ Não|
|Enviado como JS para o navegador|❌ Não (só o HTML resultante)|✅ Sim|

```tsx
// Server Component (padrão, sem diretiva) — pode ser async
async function ListaProdutos() {
  const produtos = await db.produtos.findMany(); // acesso direto ao banco

  return (
    <ul>
      {produtos.map((p) => (
        <ProdutoItem key={p.id} produto={p} />
      ))}
    </ul>
  );
}
```

```tsx
// Client Component — precisa da diretiva no topo do arquivo
"use client";

import { useState } from "react";

function ContadorInterativo() {
  const [contagem, setContagem] = useState(0);
  return <button onClick={() => setContagem(contagem + 1)}>{contagem}</button>;
}
```

> [!TIP] Regra prática Comece todo componente como Server Component (o padrão). Só adicione `"use client"` quando precisar de `useState`, `useEffect`, event handlers (`onClick`) ou qualquer API exclusiva do navegador — isso mantém o bundle enviado ao cliente o menor possível.

---

## 🌊 Streaming com Suspense

Server Components permitem enviar HTML **em pedaços**, conforme os dados ficam prontos, em vez de esperar tudo carregar de uma vez.

```tsx
import { Suspense } from "react";

function Pagina() {
  return (
    <div>
      <Header /> {/* renderiza imediatamente */}
      <Suspense fallback={<Skeleton />}>
        <Comentarios /> {/* streaming: aparece quando os dados chegarem */}
      </Suspense>
    </div>
  );
}
```

> [!NOTE] Por que isso melhora a experiência O usuário vê o conteúdo principal da página instantaneamente, enquanto partes mais lentas (que dependem de uma consulta pesada, por exemplo) continuam carregando em segundo plano e "aparecem" no lugar do fallback assim que prontas — sem bloquear a página inteira.

---

## 📁 Next.js App Router — Estrutura

O Next.js é o framework que mais expõe Server Components na prática hoje.

```
app/
├── layout.tsx          # Layout raiz, envolve todas as páginas
├── page.tsx             # Rota "/"
├── produtos/
│   ├── page.tsx          # Rota "/produtos"
│   └── [id]/
│       └── page.tsx       # Rota dinâmica "/produtos/123"
└── api/
    └── produtos/
        └── route.ts        # Rota de API (Route Handler)
```

```tsx
// app/produtos/[id]/page.tsx
async function DetalheProduto({ params }: { params: { id: string } }) {
  const produto = await buscarProduto(params.id); // Server Component: fetch direto
  return <h1>{produto.nome}</h1>;
}

export default DetalheProduto;
```

> [!WARNING] Nem todo projeto precisa de Next.js RSC é um recurso do React, mas hoje só é totalmente suportado em produção via um framework (Next.js sendo o mais usado). Para uma SPA simples sem necessidade de SSR/streaming, o Vite + React continua sendo uma opção mais simples e leve — ver [[React - Roteamento com React Router]] para esse cenário.

---

## 🔗 Notas Relacionadas

- [[React - Actions e Novos Hooks do React 19]]
- [[React - Performance e Deploy]]
- [[React - TypeScript e Tipagem Avançada]]
- ⬅️ Voltar para [[React]]