---
tags: [matriz, react, testes, jest, testing-library]

área: React JS / Estado da Arte (2026)

status: draft

matriz: "[[React]]"

---
# 🧪 React - Testes com Jest e Testing Library

> [!quote] Princípio Testar o que o usuário vê e faz, não os detalhes internos de implementação — é essa filosofia que diferencia a Testing Library de abordagens mais antigas de teste.

---

## 🎯 Conceito Principal

Assim como em [[ReactNative - Testes]], o React web usa **Jest** (ou o mais recente **Vitest**) como test runner, combinado com a **React Testing Library** para testar componentes do ponto de vista de quem usa a interface.

---

## ⚙️ Setup Básico

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom vitest jsdom
```

```ts
// vitest.config.ts
import { defineConfig } from "vitest/config";

export default defineConfig({
  test: {
    environment: "jsdom", // simula o DOM do navegador em ambiente Node
    globals: true,
    setupFiles: "./src/test/setup.ts",
  },
});
```

> [!NOTE] Vitest vs. Jest Vitest se tornou a escolha mais comum em projetos novos por ser mais rápido (usa Vite por baixo) e ter API quase idêntica à do Jest — a migração entre os dois costuma ser trivial. Projetos legados ainda usam Jest amplamente.

---

## 🧩 Testando Renderização e Interação

```tsx
import { render, screen, fireEvent } from "@testing-library/react";
import { describe, it, expect } from "vitest";
import Contador from "./Contador";

describe("Contador", () => {
  it("renderiza com valor inicial zero", () => {
    render(<Contador />);
    expect(screen.getByText("Contagem: 0")).toBeInTheDocument();
  });

  it("incrementa ao clicar no botão", () => {
    render(<Contador />);
    const botao = screen.getByRole("button", { name: /incrementar/i });

    fireEvent.click(botao);

    expect(screen.getByText("Contagem: 1")).toBeInTheDocument();
  });
});
```

|Método de busca|Prioridade de uso|
|---|---|
|`getByRole`|**Preferido** — reflete como usuários de leitor de tela navegam|
|`getByLabelText`|Ótimo para campos de formulário|
|`getByText`|Bom para conteúdo visível simples|
|`getByTestId`|Último recurso — não reflete experiência real do usuário|

> [!TIP] "Query como um usuário faria" A ordem de prioridade acima não é acidental: `getByTestId` deveria ser evitado sempre que uma opção mais próxima da experiência real do usuário (papel semântico, rótulo, texto) estiver disponível.

---

## 📝 Testando Formulários

```tsx
import { render, screen, fireEvent, waitFor } from "@testing-library/react";
import FormularioLogin from "./FormularioLogin";

it("exibe erro ao submeter formulário vazio", async () => {
  render(<FormularioLogin />);

  fireEvent.click(screen.getByRole("button", { name: /entrar/i }));

  await waitFor(() => {
    expect(screen.getByText(/e-mail é obrigatório/i)).toBeInTheDocument();
  });
});
```

> [!NOTE] `waitFor` para asserções assíncronas Sempre que a mudança esperada na tela depende de uma operação assíncrona (validação, requisição), `waitFor` (ou `findBy*`) evita falsos negativos causados pelo teste checar o resultado antes da atualização acontecer.

---

## 🎭 Mockando Requisições HTTP

```tsx
import { vi } from "vitest";

global.fetch = vi.fn(() =>
  Promise.resolve({
    ok: true,
    json: () => Promise.resolve([{ id: 1, nome: "Produto Teste" }]),
  })
) as any;

it("exibe produtos retornados pela API", async () => {
  render(<ListaProdutos />);

  expect(await screen.findByText("Produto Teste")).toBeInTheDocument();
});
```

> [!TIP] Alternativa mais robusta: MSW (Mock Service Worker) Para projetos maiores, mockar `fetch` diretamente fica difícil de manter — a biblioteca **MSW** intercepta requisições no nível de rede, permitindo simular respostas de API de forma mais realista e reutilizável entre testes.

---

## 🧱 Testando Hooks Customizados

```tsx
import { renderHook, act } from "@testing-library/react";
import { useContador } from "./useContador";

it("incrementa o valor do hook", () => {
  const { result } = renderHook(() => useContador());

  act(() => {
    result.current.incrementar();
  });

  expect(result.current.contagem).toBe(1);
});
```

---

## 🔗 Notas Relacionadas

- [[ReactNative - Testes]]
- [[React - React Compiler]]
- [[React - Formulários com React Hook Form e Zod]]
- ⬅️ Voltar para [[React]]