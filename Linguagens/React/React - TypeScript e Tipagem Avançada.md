---
tags: [matriz, react, typescript]

área: React JS / Estado da Arte (2026)

status: draft

matriz: "[[React]]"

---
# 🔷 React - TypeScript e Tipagem Avançada

> [!quote] Princípio TypeScript não é sobre "escrever mais código" — é sobre descobrir o erro no editor, antes que ele vire um bug em produção.

---

## 🎯 Conceito Principal

Desde o React 19, a biblioteca passou a fornecer **definições de tipo nativas**, eliminando a dependência histórica do pacote `@types/react` para a maioria dos casos de uso — um sinal de que TypeScript deixou de ser "opcional" no ecossistema React e virou o padrão de fato em 2026.

---

## 📦 Tipando Props

```tsx
type BotaoProps = {
  titulo: string;
  onPress: () => void;
  variante?: "primario" | "secundario"; // union type restringe os valores aceitos
  desabilitado?: boolean;
};

function Botao({ titulo, onPress, variante = "primario", desabilitado = false }: BotaoProps) {
  return (
    <button onClick={onPress} disabled={desabilitado} className={variante}>
      {titulo}
    </button>
  );
}
```

> [!WARNING] `React.FC` está sendo abandonado O padrão `React.FC<Props>` era comum, mas a comunidade migrou para tipar as props diretamente na assinatura da função (como acima) — `React.FC` tornava o tipo de `children` implícito mesmo quando o componente não deveria aceitá-lo, e o React 19 se alinha ainda mais com esse padrão mais explícito.

---

## 🪝 Tipando Hooks

```tsx
import { useState } from "react";

type Usuario = {
  id: number;
  nome: string;
  email: string;
};

function usePerfil() {
  // Genérico explícito quando o valor inicial não deixa claro o tipo completo
  const [usuario, setUsuario] = useState<Usuario | null>(null);

  return { usuario, setUsuario };
}
```

### Hooks Customizados Genéricos

```tsx
import { useState, useCallback } from "react";

// <T> torna o hook reutilizável para qualquer tipo de lista
function useListaSelecionavel<T extends { id: number }>(itensIniciais: T[]) {
  const [selecionado, setSelecionado] = useState<T | null>(null);

  const selecionar = useCallback((item: T) => setSelecionado(item), []);

  return { itens: itensIniciais, selecionado, selecionar };
}

// Uso: TypeScript infere automaticamente que T é Produto
const { selecionado } = useListaSelecionavel<Produto>(produtos);
```

---

## ⚡ O Que Mudou no React 19 para TypeScript

|Melhoria|Impacto prático|
|---|---|
|**Tipos nativos** (sem `@types/react`)|Menos um pacote para manter sincronizado com a versão do React|
|**`use()` totalmente tipado**|Inferência automática do tipo resolvido de uma Promise, sem type assertion|
|**Refs genéricos com inferência correta**|`useRef<HTMLInputElement>(null)` infere corretamente sem anotação manual|
|**Server Components tipados como `async`**|Componentes assíncronos (RSC) recebem tipagem apropriada nativamente|

```tsx
// Exemplo: use() com tipagem automática (React 19)
import { use } from "react";

async function buscarUsuario(id: string): Promise<Usuario> {
  const res = await fetch(`/api/usuarios/${id}`);
  return res.json();
}

function PerfilUsuario({ usuarioPromise }: { usuarioPromise: Promise<Usuario> }) {
  const usuario = use(usuarioPromise); // tipado como Usuario, sem cast manual
  return <p>{usuario.nome}</p>;
}
```

> [!TIP] Requisito mínimo Para aproveitar a inferência completa do React 19, é necessário TypeScript 5.0+ — versões mais antigas exigem `@types/react` e não têm a mesma qualidade de inferência para os novos hooks.

---

## 🧩 Tipando Children e Composição

```tsx
type CardProps = {
  titulo: string;
  children: React.ReactNode; // aceita qualquer conteúdo renderizável do React
};

function Card({ titulo, children }: CardProps) {
  return (
    <div className="card">
      <h3>{titulo}</h3>
      {children}
    </div>
  );
}
```

|Tipo|Quando usar|
|---|---|
|`React.ReactNode`|Aceita qualquer coisa renderizável (texto, elemento, array, null)|
|`React.ReactElement`|Especificamente um elemento JSX (não texto puro)|
|`React.PropsWithChildren<T>`|Utilitário que adiciona `children` a um tipo de props existente|

---

## 🔗 Notas Relacionadas

- [[React - State e Hooks Essenciais]]
- [[React - Actions e Novos Hooks do React 19]]
- [[React - Testes com Jest e Testing Library]]
- ⬅️ Voltar para [[React]]