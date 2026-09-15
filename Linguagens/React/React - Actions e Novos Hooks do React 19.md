---
tags: [matriz, react, react-19, actions]

área: React JS / Estado da Arte (2026)

status: draft

matriz: "[[React]]"

---

# ⚙️ React - Actions e Novos Hooks do React 19

> [!quote] Princípio Antes do React 19, tratar loading, erro e atualização otimista de um formulário exigia código manual repetido em todo lugar. Agora isso é parte da própria API do React.

---

## 🎯 Conceito Principal

O React 19 introduziu o conceito de **Actions**: funções (geralmente `async`) que o React entende nativamente, gerenciando automaticamente estado de pendência, erros e atualizações otimistas — reduzindo drasticamente o código manual que antes era feito com `useState` + `try/catch`.

---

## 🧵 `useActionState` — Estado de Formulário Sem Boilerplate

Substitui o padrão antigo de `useState` + `onSubmit` + tratamento manual de loading.

```tsx
import { useActionState } from "react";

async function cadastrarUsuario(estadoAnterior: any, formData: FormData) {
  const nome = formData.get("nome") as string;

  if (!nome) {
    return { erro: "Nome é obrigatório" };
  }

  await salvarUsuario({ nome });
  return { sucesso: true };
}

function FormularioCadastro() {
  const [estado, acao, pendente] = useActionState(cadastrarUsuario, null);

  return (
    <form action={acao}>
      <input name="nome" />
      <button disabled={pendente}>{pendente ? "Salvando..." : "Salvar"}</button>
      {estado?.erro && <p>{estado.erro}</p>}
    </form>
  );
}
```

> [!NOTE] O que `useActionState` resolve automaticamente Estado de `pending` que se integra corretamente ao _scheduler_ concorrente do React, valor de retorno da action tratado como estado, e reset automático após a submissão ser commitada — tudo isso sem precisar de três `useState` separados como antes.

---

## ⚡ `useOptimistic` — Feedback Instantâneo

Mostra a mudança na interface **antes** da confirmação do servidor, revertendo automaticamente se a operação falhar.

```tsx
import { useOptimistic } from "react";

function BotaoCurtir({ post }: { post: { id: string; curtidas: number } }) {
  const [curtidasOtimistas, adicionarCurtidaOtimista] = useOptimistic(
    post.curtidas,
    (curtidasAtuais, incremento: number) => curtidasAtuais + incremento
  );

  async function curtir() {
    adicionarCurtidaOtimista(1); // UI atualiza na hora
    await curtirPostNoServidor(post.id); // requisição real acontece em paralelo
  }

  return <button onClick={curtir}>❤️ {curtidasOtimistas}</button>;
}
```

> [!TIP] Onde isso brilha Ações rápidas e de baixo risco de falha — curtir, favoritar, marcar como lido — são os casos ideais. O usuário sente o app "instantâneo", e o React reverte a UI sozinho caso a requisição real falhe.

---

## 📥 `use()` — Lendo Promises e Context no Render

```tsx
import { use, Suspense } from "react";

function PerfilUsuario({ usuarioPromise }: { usuarioPromise: Promise<Usuario> }) {
  const usuario = use(usuarioPromise); // suspende até resolver
  return <p>{usuario.nome}</p>;
}

function App() {
  const promise = buscarUsuario("123");
  return (
    <Suspense fallback={<p>Carregando...</p>}>
      <PerfilUsuario usuarioPromise={promise} />
    </Suspense>
  );
}
```

> [!WARNING] `use()` pode ser chamado condicionalmente — diferente de outros hooks Ao contrário de `useState`/`useEffect` (que seguem a "regra dos hooks" e não podem estar dentro de `if`), o `use()` pode ser chamado condicionalmente ou dentro de loops, já que ele lê um valor de forma mais parecida com uma leitura direta do que com uma "assinatura" de hook tradicional.

`use()` também substitui `useContext` em muitos casos, com a vantagem de funcionar após um `return` condicional:

```tsx
function RotuloTema({ mostrarTema }: { mostrarTema: boolean }) {
  if (mostrarTema) {
    const tema = use(TemaContext); // funcionaria com erro se fosse useContext aqui
    return <span>{tema}</span>;
  }
  return null;
}
```

---

## 🖥️ Server Actions — Formulários Sem API Route Manual

```tsx
// Marcado como Server Action
async function criarProduto(formData: FormData) {
  "use server";

  const nome = formData.get("nome") as string;
  await db.produtos.create({ data: { nome } });
}

function FormularioProduto() {
  return (
    <form action={criarProduto}>
      <input name="nome" />
      <button type="submit">Criar</button>
    </form>
  );
}
```

> [!NOTE] O que isso elimina Antes: criar uma rota de API, fazer `fetch` do cliente, tratar loading, tratar erro, invalidar cache manualmente — 5 passos para uma única ação. Com Server Actions, o React lida com a chamada de rede automaticamente, com uma função `async` marcada com `"use server"`.

---

## 🔗 Notas Relacionadas

- [[React - Server Components e Next.js App Router]]
- [[React - Formulários com React Hook Form e Zod]]
- [[React - TypeScript e Tipagem Avançada]]
- ⬅️ Voltar para [[React]]