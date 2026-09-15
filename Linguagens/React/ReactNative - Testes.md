---
tags: [matriz, react-native, testes, jest, detox]

área: React Native / Avançado

status: draft

matriz: "[[React]]"

---

# 🧪 ReactNative - Testes

> [!quote] Princípio Um app sem testes funciona até alguém mexer em algo que "não tinha nada a ver" — testes automatizados são a rede de segurança contra esse tipo de surpresa.

---

## 🎯 Conceito Principal

Testes em React Native se dividem em três níveis principais: **testes unitários** (funções isoladas), **testes de componente** (renderização e interação com Testing Library) e **testes E2E** (fluxo completo do app, com Detox).

---

## 🧩 Jest — Testes Unitários

Jest já vem configurado por padrão em projetos criados com `create-expo-app`.

```jsx
// utils/formatarPreco.js
export function formatarPreco(valor) {
  return `R$ ${valor.toFixed(2).replace(".", ",")}`;
}
```

```jsx
// utils/formatarPreco.test.js
import { formatarPreco } from "./formatarPreco";

describe("formatarPreco", () => {
  it("formata um número como preço em reais", () => {
    expect(formatarPreco(19.9)).toBe("R$ 19,90");
  });

  it("arredonda corretamente valores com mais casas decimais", () => {
    expect(formatarPreco(10.999)).toBe("R$ 11,00");
  });
});
```

```bash
npx jest
```

---

## 🖼️ React Native Testing Library — Testes de Componente

Testa componentes do ponto de vista do usuário (o que aparece na tela, o que acontece ao interagir), em vez de detalhes internos de implementação.

```bash
npm install --save-dev @testing-library/react-native
```

```jsx
import { render, screen, fireEvent } from "@testing-library/react-native";
import Contador from "./Contador";

test("incrementa o contador ao pressionar o botão", () => {
  render(<Contador />);

  const botao = screen.getByText("Incrementar");
  fireEvent.press(botao);

  expect(screen.getByText("Contagem: 1")).toBeTruthy();
});
```

> [!TIP] Filosofia da Testing Library A biblioteca incentiva buscar elementos como um usuário real faria — por texto visível (`getByText`), rótulo acessível (`getByLabelText`) — em vez de por detalhes de implementação, tornando os testes mais resistentes a refatorações internas.

---

## 🤖 Detox — Testes E2E (Ponta a Ponta)

Testa o app completo rodando em um simulador/emulador real, simulando o fluxo real do usuário (abrir o app, navegar, preencher formulário, ver resultado).

```bash
npm install --save-dev detox
```

```js
// e2e/login.test.js
describe("Fluxo de login", () => {
  beforeEach(async () => {
    await device.reloadReactNative();
  });

  it("deve logar com credenciais válidas e ir para a home", async () => {
    await element(by.id("input-email")).typeText("usuario@teste.com");
    await element(by.id("input-senha")).typeText("senha123");
    await element(by.id("botao-entrar")).tap();

    await expect(element(by.id("tela-home"))).toBeVisible();
  });
});
```

|Nível de teste|Ferramenta|O que valida|Velocidade|
|---|---|---|---|
|Unitário|Jest|Funções puras, lógica isolada|Muito rápido|
|Componente|Testing Library|Renderização e interação de um componente|Rápido|
|E2E|Detox|Fluxo completo do app, em ambiente real (simulador)|Mais lento|

> [!NOTE] Pirâmide de testes A recomendação clássica é ter **muitos** testes unitários, uma quantidade **moderada** de testes de componente, e **poucos** testes E2E (por serem mais lentos e caros de manter) — cobrindo só os fluxos mais críticos do app (ex: login, checkout).

---

## 🔗 Notas Relacionadas

- [[ReactNative - Integração com APIs]]
- [[ReactNative - Estado e Comunicação]]
- [[Ferramentas]]
- ⬅️ Voltar para [[React]]