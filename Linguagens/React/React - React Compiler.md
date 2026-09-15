---
tags: [matriz, react, compiler, performance]

área: React JS / Estado da Arte (2026)
status: draft

matriz: "[[React]]"

---

# 🛠️ React - React Compiler

> [!quote] Princípio A melhor otimização é a que você não precisa escrever — o React Compiler tenta tornar `useMemo`/`useCallback` manuais uma exceção, não a regra.

---

## 🎯 Conceito Principal

O **React Compiler** (antes conhecido pelo codinome "React Forget") é uma ferramenta de build que analisa o código dos componentes e **insere memoização automaticamente**, sem que o desenvolvedor precise escrever `useMemo`, `useCallback` ou `React.memo` manualmente na maioria dos casos.

---

## 🐌 O Problema que Ele Resolve

Antes do Compiler, evitar re-renders desnecessários exigia disciplina manual constante — ver [[React - Performance e Deploy]] para o padrão anterior:

```jsx
// Padrão manual (ainda válido, mas cada vez menos necessário)
const produtosFiltrados = useMemo(
  () => produtos.filter((p) => p.nome.includes(filtro)),
  [produtos, filtro]
);

const handleClique = useCallback((id) => {
  console.log(id);
}, []);
```

Com o React Compiler habilitado, o mesmo componente pode ser escrito de forma direta, e o compilador identifica sozinho o que vale a pena memoizar:

```jsx
// Com o React Compiler, isso já é suficientemente otimizado sem hooks manuais
function ListaProdutos({ produtos, filtro }) {
  const produtosFiltrados = produtos.filter((p) => p.nome.includes(filtro));

  function handleClique(id) {
    console.log(id);
  }

  return (
    <ul>
      {produtosFiltrados.map((p) => (
        <ProdutoItem key={p.id} produto={p} onClick={() => handleClique(p.id)} />
      ))}
    </ul>
  );
}
```

---

## ⚙️ Como Habilitar

```bash
npm install babel-plugin-react-compiler
```

```js
// babel.config.js
module.exports = {
  plugins: [
    ["babel-plugin-react-compiler", {}],
  ],
};
```

> [!NOTE] Funciona em tempo de build, não em runtime O Compiler analisa o código durante o processo de build (Babel) e reescreve os componentes com a memoização já embutida — não há custo adicional em tempo de execução por "decidir" o que memoizar, diferente do que aconteceria se isso fosse feito dinamicamente.

---

## 🤔 `useMemo`/`useCallback` Ainda São Necessários?

|Situação|Ainda precisa de memoização manual?|
|---|---|
|Componente comum, lógica dentro das regras do React|❌ Não — o Compiler cuida|
|Cálculo que depende de estado mutável fora do fluxo do React (ex: `Date.now()` chamado diretamente no render)|⚠️ Pode precisar de ajuste, já que quebra a regra de pureza|
|Bibliotecas de terceiros que dependem de identidade de referência estável de forma não convencional|⚠️ Avaliar caso a caso|
|Código que já usa `useMemo`/`useCallback` manualmente|✅ Continua funcionando, o Compiler não remove|

> [!WARNING] Pré-requisito: seguir as regras do React O Compiler assume que os componentes seguem as **Regras do React** (componentes puros, sem efeitos colaterais durante o render). Código que já viola essas regras (mutação direta de props, side effects fora de `useEffect`) pode não se beneficiar corretamente da otimização automática, ou pode até revelar bugs que antes passavam despercebidos.

---

## 🚦 Estratégia de Migração

1. Habilitar o Compiler em um projeto **novo** ou em uma feature isolada primeiro
2. Rodar a suíte de testes existente (ver [[React - Testes com Jest e Testing Library]]) para garantir que nada quebrou
3. Remover gradualmente `useMemo`/`useCallback` manuais **conforme a confiança aumenta** — não é obrigatório remover tudo de uma vez
4. Usar o ESLint plugin oficial do Compiler para identificar código que viola as regras do React antes mesmo de compilar

> [!TIP] Não é "tudo ou nada" Código antigo com memoização manual continua funcionando normalmente lado a lado com código novo que confia no Compiler — a migração pode ser incremental, componente por componente.

---

## 🔗 Notas Relacionadas

- [[React - Performance e Deploy]]
- [[React - Server Components e Next.js App Router]]
- [[React - TypeScript e Tipagem Avançada]]
- ⬅️ Voltar para [[React]]