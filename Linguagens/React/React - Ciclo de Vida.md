---
tags: [matriz, react, javascript]
área: React JS / Avançado
status: draft
matriz: "[[React]]"
---
# 🔄 React - Ciclo de Vida

> [!quote] Princípio Todo componente nasce, atualiza e morre — entender esse ciclo é o que evita bugs de memória e efeit
> Todo componente nasce, atualiza e morre — entender esse ciclo é o que evita bugs de memória e efeitos colaterais fora de hora.

---
## 🎯 Conceito Principal

O ciclo de vida de um componente React se divide em três fases: **Mounting** (criação), **Updating** (atualização) e **Unmounting** (remoção). Em componentes de classe isso era explícito em métodos nomeados; em componentes funcionais (padrão atual), tudo é modelado com o hook `useEffect`.

---

## 🏛️ Componentes de Classe (contexto histórico)

|Fase|Método|Quando roda|
|---|---|---|
|**Mounting**|`constructor`|Antes de renderizar, inicialização de estado|
||`componentDidMount`|Logo após o primeiro render no DOM|
|**Updating**|`componentDidUpdate`|Após re-render por mudança de props/estado|
|**Unmounting**|`componentWillUnmount`|Antes do componente ser removido do DOM|

> [!NOTE] Por que ainda aprender isso? Muito código legado (e provas/testes técnicos) ainda usa classes. Entender a nomenclatura ajuda a ler bases de código antigas e a compreender **por que** o `useEffect` foi desenhado do jeito que é.

---

## 🪝 Equivalência com `useEffect`

```jsx
import { useEffect, useState } from "react";

function Perfil({ usuarioId }) {
  const [dados, setDados] = useState(null);

  // Equivalente a componentDidMount + componentDidUpdate (quando usuarioId muda)
  useEffect(() => {
    let ativo = true;

    async function carregar() {
      const resposta = await fetch(`/api/usuarios/${usuarioId}`);
      const json = await resposta.json();
      if (ativo) setDados(json);
    }

    carregar();

    // Equivalente a componentWillUnmount (função de limpeza)
    return () => {
      ativo = false;
    };
  }, [usuarioId]); // array de dependências: roda de novo só se usuarioId mudar

  if (!dados) return <p>Carregando...</p>;
  return <p>{dados.nome}</p>;
}
```

|Array de dependências|Comportamento|
|---|---|
|`[]` (vazio)|Roda **uma vez**, só na montagem (como `componentDidMount`)|
|`[valor]`|Roda na montagem e sempre que `valor` mudar|
|Ausente (sem array)|Roda em **todo** render — quase sempre um erro|

> [!TIP] Função de limpeza (`return () => {...}`) Sempre que o efeito criar uma subscrição, timer, ou requisição que pode ficar "presa" (como no exemplo acima com `ativo`), a função de limpeza evita atualizar estado de um componente que já foi desmontado — a causa mais comum do aviso "Can't perform a React state update on an unmounted component".

---

## 🔗 Notas Relacionadas

- [[React - Requisições HTTP]]
- [[React - Gerenciamento de Estado]]
- [[React - Performance e Deploy]]
- ⬅️ Voltar para [[React]]