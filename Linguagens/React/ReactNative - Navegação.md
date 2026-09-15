---
tags: [matriz, react-native, navegação]

área: React Native / Avançado

status: draft
matriz: "[[React]]"

---

# 🧭 ReactNative - Navegação

> [!quote] Princípio Não existe URL de verdade no mobile — a navegação é uma pilha de telas gerenciada em memória, e o React Navigation é quem organiza essa pilha.

---

## 🎯 Conceito Principal

`@react-navigation` é a biblioteca padrão de fato para navegação em React Native, oferecendo três padrões principais que podem ser combinados: **Stack**, **Tab** e **Drawer**.

```bash
npm install @react-navigation/native @react-navigation/native-stack
npx expo install react-native-screens react-native-safe-area-context
```

---

## 📚 Stack Navigation

Empilha telas umas sobre as outras — o padrão mais comum (ex: Lista → Detalhe → Checkout).

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Detalhe" component={DetalheScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

```jsx
// Navegando e passando parâmetros
function HomeScreen({ navigation }) {
  return (
    <Button
      title="Ver produto"
      onPress={() => navigation.navigate("Detalhe", { produtoId: 42 })}
    />
  );
}

function DetalheScreen({ route }) {
  const { produtoId } = route.params;
  return <Text>Produto: {produtoId}</Text>;
}
```

---

## 🔻 Tab Navigation

Abas fixas, geralmente na parte inferior da tela — comum para as seções principais do app.

```bash
npm install @react-navigation/bottom-tabs
```

```jsx
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";

const Tab = createBottomTabNavigator();

function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Início" component={HomeScreen} />
        <Tab.Screen name="Perfil" component={PerfilScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

---

## 🗄️ Drawer Navigation

Menu lateral deslizante, comum em apps com muitas seções secundárias.

```bash
npm install @react-navigation/drawer
```

```jsx
import { createDrawerNavigator } from "@react-navigation/drawer";

const Drawer = createDrawerNavigator();

function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator>
        <Drawer.Screen name="Início" component={HomeScreen} />
        <Drawer.Screen name="Configurações" component={ConfiguracoesScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

---

## 🪆 Navegação Aninhada

Padrão real de apps profissionais: um Tab Navigator onde cada aba tem seu próprio Stack Navigator interno.

```jsx
function StackInicio() {
  return (
    <Stack.Navigator>
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Detalhe" component={DetalheScreen} />
    </Stack.Navigator>
  );
}

function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="InicioTab" component={StackInicio} options={{ headerShown: false }} />
        <Tab.Screen name="Perfil" component={PerfilScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

> [!TIP] `headerShown: false` na Tab externa Ao aninhar um Stack dentro de uma Tab, geralmente se esconde o header da Tab para não duplicar com o header do Stack interno.

---

## 📐 Boas Práticas

- Centralizar a navegação em `src/navigation/`, separado das telas
- Tipar as rotas com TypeScript (`RootStackParamList`) para autocomplete e checagem de parâmetros
- Evitar lógica de negócio dentro dos arquivos de navegação — eles devem só orquestrar rotas

---

## 🔗 Notas Relacionadas

- [[React - Roteamento com React Router]]
- [[ReactNative - Estado e Comunicação]]
- [[ReactNative - Integração com APIs]]
- ⬅️ Voltar para [[React]]