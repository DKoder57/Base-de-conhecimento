---
tags: [matriz, react-native, ui, flexbox]

área: React Native / Fundamentos

status: draft

matriz: "[[React]]"

---

# 🎨 ReactNative - Componentes e Estilo

> [!quote] Princípio Não existe `<div>` no React Native — cada componente visual tem um propósito específico, e o layout é 100% resolvido com Flexbox.

---

## 🎯 Conceito Principal

O React Native fornece um conjunto próprio de componentes base que se traduzem em elementos nativos de UI, estilizados via `StyleSheet` — uma API parecida com CSS, mas com propriedades em camelCase e sem toda a superfície do CSS web.

---

## 🧱 Componentes Base

|Componente|Equivalente na web|Uso|
|---|---|---|
|`<View>`|`<div>`|Container genérico para layout|
|`<Text>`|`<p>`/`<span>`|**Todo** texto deve estar dentro de um `<Text>`|
|`<Image>`|`<img>`|Exibição de imagens (locais ou remotas)|
|`<TextInput>`|`<input>`|Campo de entrada de texto|
|`<ScrollView>`|—|Container rolável para conteúdo que excede a tela|
|`<FlatList>`|—|Lista performática, renderiza só os itens visíveis|
|`<TouchableOpacity>` / `<Pressable>`|`<button>`|Elementos tocáveis, com feedback visual|

```jsx
import { View, Text, Image, StyleSheet } from "react-native";

function CartaoProduto({ produto }) {
  return (
    <View style={estilos.cartao}>
      <Image source={{ uri: produto.imagemUrl }} style={estilos.imagem} />
      <Text style={estilos.titulo}>{produto.nome}</Text>
      <Text style={estilos.preco}>R$ {produto.preco}</Text>
    </View>
  );
}

const estilos = StyleSheet.create({
  cartao: {
    padding: 12,
    borderRadius: 8,
    backgroundColor: "#fff",
    elevation: 2, // sombra no Android
    shadowColor: "#000", // sombra no iOS
    shadowOpacity: 0.1,
  },
  imagem: {
    width: "100%",
    height: 150,
    borderRadius: 8,
  },
  titulo: {
    fontSize: 16,
    fontWeight: "bold",
    marginTop: 8,
  },
  preco: {
    fontSize: 14,
    color: "#666",
  },
});
```

> [!WARNING] Todo texto precisa estar dentro de `<Text>` Diferente da web, colocar uma string diretamente dentro de uma `<View>` gera erro em tempo de execução — o React Native não sabe como renderizar texto solto fora de um componente `<Text>`.

---

## 📐 Flexbox no React Native

Todo layout é feito com Flexbox — mas com uma diferença importante: **`flexDirection` padrão é `column`**, ao contrário da web (que é `row`).

```jsx
const estilos = StyleSheet.create({
  linha: {
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    padding: 16,
  },
});
```

|Propriedade|Função|
|---|---|
|`flexDirection`|Direção do eixo principal (`row`, `column`)|
|`justifyContent`|Alinhamento no eixo principal|
|`alignItems`|Alinhamento no eixo cruzado|
|`flex: 1`|Componente ocupa todo o espaço disponível restante|

---

## 🎨 Temas e Estilos Globais

Centralizar cores, espaçamentos e tipografia evita repetição e facilita dar suporte a modo claro/escuro.

```js
// theme/index.js
export const cores = {
  primaria: "#22C55E",
  fundo: "#F9FAFB",
  texto: "#111827",
  textoSecundario: "#6B7280",
};

export const espacamento = {
  pequeno: 8,
  medio: 16,
  grande: 24,
};
```

```jsx
import { cores, espacamento } from "../theme";

const estilos = StyleSheet.create({
  container: {
    padding: espacamento.medio,
    backgroundColor: cores.fundo,
  },
});
```

> [!TIP] Bibliotecas de estilo Para projetos maiores, vale considerar **NativeWind** (Tailwind CSS aplicado ao React Native) ou **Styled Components** — ambos reduzem a verbosidade do `StyleSheet.create` puro.

---

## 🔗 Notas Relacionadas

- [[ReactNative - Ambiente e Estrutura de Pastas]]
- [[ReactNative - Estado e Comunicação]]
- [[ReactNative - Animações e Gestos]]
- ⬅️ Voltar para [[React]]