---

tags: [matriz, react, react-router]
área: React JS / Avançado
status: draft
matriz: "[[React]]"

---
# 🧭 React - Roteamento com React Router

> [!quote] Princípio React é uma biblioteca de UI, não de roteamento — o React Router é quem transforma sua SPA em algo que se comporta como um site de verdade, com URLs navegáveis.

---

## 🎯 Conceito Principal

O `react-router-dom` permite mapear URLs para componentes, gerenciar navegação sem recarregar a página inteira (SPA), e ler parâmetros dinâmicos da URL.

```bash
npm install react-router-dom
```

---

## 🏗️ Estrutura Básica

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Início</Link>
        <Link to="/produtos">Produtos</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/produtos" element={<Produtos />} />
        <Route path="/produtos/:id" element={<DetalheProduto />} />
        <Route path="*" element={<NaoEncontrado />} />
      </Routes>
    </BrowserRouter>
  );
}
```

|Componente|Função|
|---|---|
|`<BrowserRouter>`|Provider que habilita o roteamento na aplicação inteira|
|`<Routes>`|Agrupa as rotas, renderiza apenas a que combina com a URL atual|
|`<Route>`|Define o mapeamento entre um `path` e um componente|
|`<Link>`|Substitui a tag `<a>`, navega sem recarregar a página|

> [!TIP] `path="*"` como fallback Colocar uma rota `*` por último captura qualquer URL não mapeada — essencial para uma página 404 amigável.

---

## 🔢 Rotas Dinâmicas e `useParams`

```jsx
import { useParams } from "react-router-dom";

function DetalheProduto() {
  const { id } = useParams(); // extrai o valor de :id da URL

  return <p>Exibindo produto de ID: {id}</p>;
}
```

---

## 🧭 Navegação Programática — `useNavigate`

Útil quando a navegação precisa acontecer após uma ação (ex: submissão de formulário), não apenas um clique em link.

```jsx
import { useNavigate } from "react-router-dom";

function FormularioLogin() {
  const navigate = useNavigate();

  async function handleSubmit(e) {
    e.preventDefault();
    const sucesso = await autenticar();
    if (sucesso) {
      navigate("/dashboard"); // redireciona após login
    }
  }

  return <form onSubmit={handleSubmit}>...</form>;
}
```

---

## 🔀 `<Navigate>` — Redirecionamento Declarativo

Útil para proteger rotas que exigem autenticação.

```jsx
import { Navigate } from "react-router-dom";

function RotaProtegida({ autenticado, children }) {
  if (!autenticado) {
    return <Navigate to="/login" replace />;
  }
  return children;
}
```

> [!NOTE] `replace` no histórico A prop `replace` substitui a entrada atual do histórico do navegador em vez de empilhar uma nova — evita que o usuário "volte" para uma página que exigia login após ser redirecionado.

---

## 🔗 Notas Relacionadas

- [[React - Ciclo de Vida]]
- [[React - Gerenciamento de Estado]]
- [[ReactNative - Navegação]]
- ⬅️ Voltar para [[React]]