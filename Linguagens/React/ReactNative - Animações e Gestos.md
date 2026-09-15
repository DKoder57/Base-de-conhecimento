---
tags: [matriz, react-native, animações, gestos]

área: React Native / Avançado

status: draft

matriz: "[[React]]"

---

# 🎬 ReactNative - Animações e Gestos

> [!quote] Princípio Uma animação bem feita não é decoração — é feedback visual que ajuda o usuário a entender o que aconteceu na interface.

---

## 🎯 Conceito Principal

React Native tem duas camadas de animação: a **Animated API** nativa (mais simples, embutida) e a **Reanimated** (biblioteca de terceiros, roda animações na thread de UI para performance superior), geralmente combinada com **Gesture Handler** para interações de toque/arrastar.

---

## 🌀 Animated API (nativa)

```jsx
import { useRef } from "react";
import { Animated, TouchableOpacity, Text } from "react-native";

function BotaoAnimado() {
  const escala = useRef(new Animated.Value(1)).current;

  function aoPressionar() {
    Animated.sequence([
      Animated.timing(escala, { toValue: 0.9, duration: 100, useNativeDriver: true }),
      Animated.timing(escala, { toValue: 1, duration: 100, useNativeDriver: true }),
    ]).start();
  }

  return (
    <TouchableOpacity onPress={aoPressionar} activeOpacity={1}>
      <Animated.View style={{ transform: [{ scale: escala }] }}>
        <Text>Toque aqui</Text>
      </Animated.View>
    </TouchableOpacity>
  );
}
```

> [!TIP] `useNativeDriver: true` Faz a animação rodar diretamente na thread nativa de UI, em vez de depender da thread JavaScript — essencial para manter 60fps mesmo se o JS estiver ocupado processando outra coisa.

---

## ⚡ Reanimated — Animações de Alta Performance

```bash
npx expo install react-native-reanimated
```

```jsx
import Animated, {
  useSharedValue,
  useAnimatedStyle,
  withSpring,
} from "react-native-reanimated";
import { Pressable } from "react-native";

function CartaoExpansivel() {
  const altura = useSharedValue(100);

  const estiloAnimado = useAnimatedStyle(() => ({
    height: altura.value,
  }));

  function alternar() {
    altura.value = withSpring(altura.value === 100 ? 250 : 100);
  }

  return (
    <Pressable onPress={alternar}>
      <Animated.View style={[{ backgroundColor: "#22C55E", borderRadius: 8 }, estiloAnimado]} />
    </Pressable>
  );
}
```

> [!NOTE] Diferença central para a Animated API O Reanimated executa a lógica da animação (incluindo `withSpring`, `withTiming`) **na thread de UI**, não na thread JS — isso o torna significativamente mais fluido para gestos complexos e interativos (como arrastar um card), onde a Animated API tradicional pode apresentar travamentos.

---

## 👆 Gesture Handler — Gestos Nativos

```bash
npx expo install react-native-gesture-handler
```

```jsx
import { GestureDetector, Gesture } from "react-native-gesture-handler";
import Animated, { useSharedValue, useAnimatedStyle } from "react-native-reanimated";

function CartaoArrastavel() {
  const posX = useSharedValue(0);

  const gesto = Gesture.Pan().onUpdate((evento) => {
    posX.value = evento.translationX;
  }).onEnd(() => {
    posX.value = 0; // volta à posição original ao soltar
  });

  const estiloAnimado = useAnimatedStyle(() => ({
    transform: [{ translateX: posX.value }],
  }));

  return (
    <GestureDetector gesture={gesto}>
      <Animated.View style={[{ width: 100, height: 100, backgroundColor: "#3B82F6" }, estiloAnimado]} />
    </GestureDetector>
  );
}
```

|Gesto|Uso comum|
|---|---|
|`Gesture.Pan()`|Arrastar (drag), swipe|
|`Gesture.Tap()`|Toque simples/duplo|
|`Gesture.LongPress()`|Pressionar e segurar|
|`Gesture.Pinch()`|"Beliscar" para zoom|

---

## 🔗 Notas Relacionadas

- [[ReactNative - Componentes e Estilo]]
- [[ReactNative - Testes]]
- [[React - Performance e Deploy]]
- ⬅️ Voltar para [[React]]