---

tags: [react, react-native, frontend, web, mobile, matriz]

área: React

status: draft

---
---

# ⚛️ React — Matriz da Aba

> [!quote] Princípio: Documentar é transformar consumo em domínio. Arquivo de navegação central para todos os tópicos de React JS e React Native do vault.

---

## Seção R1 — React JS: Fundamentos

|ID|Nota|Conteúdo principal|
|---|---|---|
|R1.1|[[React - Fundamentos e JSX]]|O que é React, Virtual DOM, Create React App, estrutura de pastas, JSX|
|R1.2|[[React - Componentes e Props]]|Functional vs Class components, props, composição e reutilização|
|R1.3|[[React - State e Hooks Essenciais]]|useState, useEffect, useContext, useRef — conceitos e exemplos|
|R1.4|[[React - Eventos e Renderização Condicional]]|Eventos sintéticos (camelCase), if/ternário/&&, listas e keys|
|R1.5|[[React - Formulários]]|Controlled vs uncontrolled, múltiplos campos, validação, select/checkbox/radio|

---

## Seção R2 — React JS: Avançado

|ID|Nota|Conteúdo principal|
|---|---|---|
|R2.1|[[React - Ciclo de Vida]]|Mounting/Updating/Unmounting, métodos de classe, equivalentes com useEffect|
|R2.2|[[React - Roteamento com React Router]]|BrowserRouter, Routes, Link, rotas dinâmicas, useParams, Navigate, useNavigate|
|R2.3|[[React - Requisições HTTP]]|fetch, Axios, estados de loading/error, POST, integração com Firebase Firestore|
|R2.4|[[React - Gerenciamento de Estado]]|Context API (createContext, Provider, useContext), Redux Toolkit (slice, store, useSelector, useDispatch)|
|R2.5|[[React - Performance e Deploy]]|React.memo, useMemo, useCallback, useReducer, lazy loading, react-window, Vercel, Netlify, GitHub Pages, CI/CD|

---

## 🆕 Seção R3 — React JS: Estado da Arte (2026)

> Cobre o que mudou estruturalmente no React desde a v19 (dez/2024) — o "mental model" atual da comunidade é servidor-primeiro, com o Compiler cuidando da maior parte da otimização manual que antes era feita à mão.

| ID   | Nota                                               | Conteúdo principal                                                                                                                           |
| ---- | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| R3.1 | [[React - TypeScript e Tipagem Avançada]]          | Tipagem nativa do React 19 (sem `@types/react` obrigatório), props tipadas, generics em hooks customizados, `React.FC` deprecado             |
| R3.2 | [[React - Server Components e Next.js App Router]] | RSC vs Client Components (`'use client'`), streaming com Suspense, App Router, quando cada tipo de componente é apropriado                   |
| R3.3 | [[React - Actions e Novos Hooks do React 19]]      | `use()`, `useActionState`, `useOptimistic`, Server Actions (`'use server'`), formulários sem API route manual                                |
| R3.4 | [[React - React Compiler]]                         | Memoização automática, quando `useMemo`/`useCallback`/`React.memo` ainda são necessários, migração gradual                                   |
| R3.5 | [[React - Testes com Jest e Testing Library]]      | Testes unitários e de componente para React web (paralelo ao que já existe em [[ReactNative - Testes]]), Vitest como alternativa mais rápida |
| R3.6 | [[React - Formulários com React Hook Form e Zod]]  | Validação de schema, integração com Server Actions, redução de re-renders em formulários grandes                                             |


---

## Seção RN1 — React Native: Fundamentos

|ID|Nota|Conteúdo principal|
|---|---|---|
|RN1.1|[[ReactNative - Fundamentos]]|O que é, vantagens, apps reais, comparação com Flutter e Ionic|
|RN1.2|[[ReactNative - Ambiente e Estrutura de Pastas]]|Setup, Android SDK, variáveis de ambiente, pastas src/components/screens, boas práticas|
|RN1.3|[[ReactNative - Componentes e Estilo]]|View, Text, Image, TextInput, StyleSheet, Flexbox, temas e estilos globais|
|RN1.4|[[ReactNative - Estado e Comunicação]]|Props, useState, comunicação entre componentes, Context API global|

---

## Seção RN2 — React Native: Avançado

|ID|Nota|Conteúdo principal|
|---|---|---|
|RN2.1|[[ReactNative - Navegação]]|Stack, Tab, Drawer navigation, navegação aninhada, boas práticas|
|RN2.2|[[ReactNative - Integração com APIs]]|fetch, Axios, React Query, cache e atualização de dados|
|RN2.3|[[ReactNative - Armazenamento Local]]|AsyncStorage (chave-valor), SQLite (estruturado)|
|RN2.4|[[ReactNative - Animações e Gestos]]|Animated API, Reanimated, Gesture Handler|
|RN2.5|[[ReactNative - Testes]]|Jest, Testing Library, testes E2E com Detox|

---

## 🆕 Seção RN3 — React Native: Nova Arquitetura e Produção (2026)

> Cobre a virada estrutural do RN desde a versão 0.76 / Expo SDK 52: a "New Architecture" (JSI + Fabric + TurboModules) deixou de ser experimental e é hoje o padrão — além do ferramental de produção (Expo Router, EAS) que se tornou o caminho recomendado oficialmente pela própria Expo.

|ID|Nota|Conteúdo principal|
|---|---|---|
|RN3.1|[[ReactNative - Nova Arquitetura (JSI, Fabric, TurboModules)]]|Fim da Bridge assíncrona, chamadas nativas síncronas via JSI, Fabric (renderer concorrente), TurboModules (lazy loading), Hermes como engine padrão|
|RN3.2|[[ReactNative - Expo Router]]|Roteamento por sistema de arquivos (`app/`), rotas dinâmicas, grupos `(tabs)`/`(auth)`, deep linking automático, `router.push`/`Link`|
|RN3.3|[[ReactNative - Módulos Nativos e Expo Modules API]]|Quando sair do Expo Go, `expo prebuild`, Expo Modules API (TypeScript-first para Swift/Kotlin), TurboModules com CodeGen|
|RN3.4|[[ReactNative - Notificações Push e Deep Linking]]|`expo-notifications` (Firebase + APNs), permissões, deep links vindos de notificação, universal links|
|RN3.5|[[ReactNative - EAS Build, Update e Publicação]]|Build em nuvem (EAS Build), OTA updates (EAS Update, bytecode diffing), publicação em App Store/Play Store, canais de release|
|RN3.6|[[ReactNative - Listas de Alta Performance (FlashList)]]|Limitações do FlatList em listas grandes, FlashList (recycling de views), comparação com LegendList|

> [!NOTE] Sobre a sua stack atual (Expo SDK 54) Como você já usa Expo SDK 54, a New Architecture (RN3.1) já vem habilitada por padrão no seu projeto GreenKeeper — vale revisar se algum pacote de terceiro que você usa ainda é "Bridge-only", já que ~15% do ecossistema npm ainda não migrou totalmente.

---

## 📎 Fontes Recomendadas (usadas para montar R3 e RN3)

|Fonte|Cobertura|
|---|---|
|**[react.dev/blog](https://react.dev/blog/2024/12/05/react-19)**|Blog oficial do React — anúncio e detalhamento do React 19 (Actions, `use()`, Server Components, Document Metadata)|
|**[Expo Documentation](https://docs.expo.dev/)**|Documentação oficial da Expo — Expo Router, EAS Build/Update, Expo Modules API, SDK 52+|
|**[Callstack Blog](https://www.callstack.com/blog)**|Uma das consultorias mais respeitadas do ecossistema RN — cobertura técnica profunda da New Architecture, Nitro Modules, threading|
|**[React Native Architecture Docs](https://reactnative.dev/architecture/overview)**|Documentação oficial sobre JSI, Fabric e TurboModules|
|**[TanStack Query Docs](https://tanstack.com/query/latest)**|Referência oficial para cache/sincronização de dados server-state, usado tanto em R2.3/R3 quanto em RN2.2|

> [!TIP] Por que essas fontes e não uma lista genérica Diferente da cibersegurança (onde plataformas de prática como HTB/TryHackMe são o padrão), em front-end o conteúdo mais confiável em 2026 vem direto da **documentação oficial dos mantenedores** (React, Expo, React Native core team) — blogs de terceiros mudam de opinião rápido, mas a doc oficial é a fonte de verdade sobre o que realmente é suportado em produção.

---

## 🗺️ Mapa de Dependências

```
React - Fundamentos e JSX
└── React - Componentes e Props
    └── React - State e Hooks Essenciais
        ├── React - Eventos e Renderização Condicional
        ├── React - Formulários
        │   └── React - Formulários com React Hook Form e Zod
        ├── React - Ciclo de Vida
        ├── React - Requisições HTTP
        │   └── React - Gerenciamento de Estado
        ├── React - Roteamento com React Router
        ├── React - Performance e Deploy
        │   └── React - React Compiler
        ├── React - TypeScript e Tipagem Avançada
        ├── React - Testes com Jest e Testing Library
        └── React - Actions e Novos Hooks do React 19
            └── React - Server Components e Next.js App Router

ReactNative - Fundamentos
└── ReactNative - Ambiente e Estrutura de Pastas
    └── ReactNative - Componentes e Estilo
        └── ReactNative - Estado e Comunicação
            ├── ReactNative - Navegação
            │   └── ReactNative - Expo Router
            ├── ReactNative - Integração com APIs
            │   └── ReactNative - Armazenamento Local
            ├── ReactNative - Animações e Gestos
            ├── ReactNative - Testes
            ├── ReactNative - Nova Arquitetura (JSI, Fabric, TurboModules)
            │   └── ReactNative - Módulos Nativos e Expo Modules API
            ├── ReactNative - Notificações Push e Deep Linking
            ├── ReactNative - EAS Build, Update e Publicação
            └── ReactNative - Listas de Alta Performance (FlashList)
```

---

## 🔁 Tópicos Compartilhados (React JS ↔ React Native)

|Tópico|React JS|React Native|
|---|---|---|
|Hooks (useState, useEffect)|[[React - State e Hooks Essenciais]]|[[ReactNative - Estado e Comunicação]]|
|Context API|[[React - Gerenciamento de Estado]]|[[ReactNative - Estado e Comunicação]]|
|Axios e fetch|[[React - Requisições HTTP]]|[[ReactNative - Integração com APIs]]|
|Navegação/Rotas|[[React - Roteamento com React Router]]|[[ReactNative - Navegação]] / [[ReactNative - Expo Router]]|
|Props e composição|[[React - Componentes e Props]]|[[ReactNative - Estado e Comunicação]]|
|Cache de dados server-state|(usar TanStack Query, mesmo conceito de R2.3)|[[ReactNative - Integração com APIs]]|
|Testes|[[React - Testes com Jest e Testing Library]]|[[ReactNative - Testes]]|
|Formulários|[[React - Formulários]] / [[React - Formulários com React Hook Form e Zod]]|(mesmo padrão se aplica, sem nota dedicada ainda)|

---

## ✅ Status das Notas

|Nota|Status|
|---|---|
|[[React - Fundamentos e JSX]]|⬜ pendente|
|[[React - Componentes e Props]]|⬜ pendente|
|[[React - State e Hooks Essenciais]]|⬜ pendente|
|[[React - Eventos e Renderização Condicional]]|⬜ pendente|
|[[React - Formulários]]|⬜ pendente|
|[[React - Ciclo de Vida]]|✅ pronta|
|[[React - Roteamento com React Router]]|✅ pronta|
|[[React - Requisições HTTP]]|✅ pronta|
|[[React - Gerenciamento de Estado]]|✅ pronta|
|[[React - Performance e Deploy]]|✅ pronta|
|[[React - TypeScript e Tipagem Avançada]]|⬜ pendente|
|[[React - Server Components e Next.js App Router]]|⬜ pendente|
|[[React - Actions e Novos Hooks do React 19]]|⬜ pendente|
|[[React - React Compiler]]|⬜ pendente|
|[[React - Testes com Jest e Testing Library]]|⬜ pendente|
|[[React - Formulários com React Hook Form e Zod]]|⬜ pendente|
|[[ReactNative - Fundamentos]]|✅ pronta|
|[[ReactNative - Ambiente e Estrutura de Pastas]]|✅ pronta|
|[[ReactNative - Componentes e Estilo]]|✅ pronta|
|[[ReactNative - Estado e Comunicação]]|✅ pronta|
|[[ReactNative - Navegação]]|✅ pronta|
|[[ReactNative - Integração com APIs]]|✅ pronta|
|[[ReactNative - Armazenamento Local]]|✅ pronta|
|[[ReactNative - Animações e Gestos]]|✅ pronta|
|[[ReactNative - Testes]]|✅ pronta|
|[[ReactNative - Nova Arquitetura (JSI, Fabric, TurboModules)]]|⬜ pendente|
|[[ReactNative - Expo Router]]|⬜ pendente|
|[[ReactNative - Módulos Nativos e Expo Modules API]]|⬜ pendente|
|[[ReactNative - Notificações Push e Deep Linking]]|⬜ pendente|
|[[ReactNative - EAS Build, Update e Publicação]]|⬜ pendente|
|[[ReactNative - Listas de Alta Performance (FlashList)]]|⬜ pendente|

---
# 📚 FONTES

## Essenciais

- React Documentation
- React Native Documentation
- Expo Documentation
- TanStack Documentation
- Zustand Documentation
- Epic React
- Jack Herrington
- Bulletproof React

> [!NOTE] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → callouts `[!NOTE]`/`[!TIP]`/`[!WARNING]` → exemplos de código → links relacionados.