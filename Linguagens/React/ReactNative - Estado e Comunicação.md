---
tags: [matriz, react-native, estado, props]

área: React Native / Fundamentos

status: draft

matriz: "[[React]]"

---

# 🔗 ReactNative - Estado e Comunicação

> [!quote] Princípio Componentes isolados não fazem um app — a comunicação entre eles é o que transforma peças soltas em uma experiência coesa.

---

## 🎯 Conceito Principal

Os mesmos conceitos de estado do React web se aplicam ao React Native: **props** para comunicação de pai para filho, **useState** para estado local, e **Context API** (ou uma lib como Zustand) quando o estado precisa ser global.

---

## 📦 Props — Comunicação de Pai para Filho

```jsx
function BotaoPersonalizado({ titulo, onPress, cor = "#22C55E" }) {
  return (
    <TouchableOpacity onPress={onPress} style={{ backgroundColor: cor, padding: 12 }}>
      <Text style={{ color: "#fff" }}>{titulo}</Text>
    </TouchableOpacity>
  );
}

// Uso
<BotaoPersonalizado titulo="Salvar" onPress={() => console.log("Salvo!")} />
```

> [!NOTE] Props são somente leitura Um componente filho nunca deve modificar as props recebidas diretamente — se precisar "mudar" algo do pai, o padrão é o pai passar uma função (como `onPress` acima) que o filho chama.

---

## 🪝 `useState` — Estado Local

```jsx
import { useState } from "react";
import { View, TextInput, Text } from "react-native";

function FormularioBusca() {
  const [termo, setTermo] = useState("");

  return (
    <View>
      <TextInput
        value={termo}
        onChangeText={setTermo}
        placeholder="Buscar produto..."
      />
      <Text>Buscando por: {termo}</Text>
    </View>
  );
}
```

---

## 📢 Comunicação Entre Componentes (sem Context)

Quando dois componentes **irmãos** precisam compartilhar dado, a solução mais simples é "subir" o estado para o pai comum (_lifting state up_).

```jsx
function TelaCarrinho() {
  const [itens, setItens] = useState([]);

  function adicionarItem(produto) {
    setItens((atual) => [...atual, produto]);
  }

  return (
    <View>
      <ListaProdutos onAdicionar={adicionarItem} />
      <ResumoCarrinho itens={itens} />
    </View>
  );
}
```

> [!TIP] Quando "subir estado" não é mais suficiente Se o estado precisa ser acessado por componentes distantes (ex: um "carrinho" acessado no header, na tela de produto e na tela de checkout), subir estado vira impraticável — é o sinal de que chegou a hora de usar Context API global ou Zustand.

---

## 🌍 Context API Global (aplicado ao mobile)

```jsx
import { createContext, useContext, useState } from "react";

const AutenticacaoContext = createContext();

export function AutenticacaoProvider({ children }) {
  const [usuario, setUsuario] = useState(null);

  return (
    <AutenticacaoContext.Provider value={{ usuario, setUsuario }}>
      {children}
    </AutenticacaoContext.Provider>
  );
}

export function useAutenticacao() {
  return useContext(AutenticacaoContext);
}
```

```jsx
// App.js
export default function App() {
  return (
    <AutenticacaoProvider>
      <Navegacao />
    </AutenticacaoProvider>
  );
}
```

```jsx
// Em qualquer tela dentro da árvore
function TelaPerfil() {
  const { usuario } = useAutenticacao();
  return <Text>Olá, {usuario?.nome}</Text>;
}
```

> [!NOTE] Alternativa mais leve: Zustand Para estado global que muda com frequência (ex: carrinho de compras, filtros de busca), uma store Zustand costuma ser mais simples de manter do que Context API, sem precisar envolver a árvore de componentes em Providers — ver [[React - Gerenciamento de Estado]] para a comparação completa.

---

## 🔗 Notas Relacionadas

- [[ReactNative - Componentes e Estilo]]
- [[React - Gerenciamento de Estado]]
- [[ReactNative - Integração com APIs]]
- ⬅️ Voltar para [[React]]