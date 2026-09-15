---
tags: [matriz, react-native, mobile]
área: React Native / Fundamentos
status: draft
matriz: "[[React]]"
---
# 📱 ReactNative - Fundamentos

> [!quote] Princípio Um único código-fonte JavaScript, rodando como app nativo de verdade em iOS e Android — essa é a proposta central do React Native.

---

## 🎯 Conceito Principal

React Native usa a mesma sintaxe e filosofia de componentes do React, mas em vez de renderizar HTML, traduz os componentes para elementos de UI **nativos** de cada plataforma (via uma ponte/bridge ou, nas versões mais novas, via JSI/Fabric).

---

## ✅ Vantagens

|Vantagem|Explicação|
|---|---|
|**Reuso de código**|Boa parte da lógica de negócio é compartilhada entre iOS e Android|
|**Comunidade e ecossistema**|Vasto catálogo de bibliotecas (navegação, animação, storage etc.)|
|**Hot Reload / Fast Refresh**|Ver mudanças quase instantaneamente durante o desenvolvimento|
|**Performance próxima do nativo**|Componentes de UI são realmente nativos, não uma WebView disfarçada|
|**Curva de aprendizado menor para quem já sabe React**|Mesmos conceitos: componentes, props, hooks, estado|

---

## 📲 Apps Reais Construídos com React Native

Empresas como Meta (criadora da tecnologia), Discord, Shopify e Coinbase usam ou já usaram React Native em produção para partes significativas de seus apps — prova de que a tecnologia escala para uso comercial sério, não apenas protótipos.

---

## ⚖️ Comparação com Flutter e Ionic

|Critério|React Native|Flutter|Ionic|
|---|---|---|---|
|Linguagem|JavaScript/TypeScript|Dart|HTML/CSS/JS (ou frameworks como Angular/React)|
|Renderização|Componentes nativos reais|Motor de renderização próprio (Skia), desenha tudo do zero|WebView (não é nativo)|
|Performance|Muito boa|Excelente, especialmente em animações|Mais limitada, por rodar em WebView|
|Curva de aprendizado|Baixa para quem já sabe React|Média (nova linguagem: Dart)|Baixa para quem já sabe web|
|Ecossistema de bibliotecas|Extenso e maduro|Crescente, mas menor que o do RN|Extenso (reaproveita libs web)|

> [!TIP] Quando escolher cada um **React Native**: já domina JS/React e quer aproveitar isso no mobile. **Flutter**: prioriza consistência visual pixel-perfect entre plataformas e não se importa em aprender Dart. **Ionic**: já tem um site/PWA e quer um "wrapper" rápido para lojas de app, sem preocupação extrema com performance nativa.

---

## 🧰 Expo — Camada de Produtividade sobre o React Native

O **Expo** (usado no seu projeto GreenKeeper, por exemplo) fornece um conjunto de ferramentas e APIs prontas (câmera, notificações, sensores) sem precisar escrever código nativo Swift/Kotlin manualmente, além de um fluxo de build simplificado (EAS Build) e OTA updates (atualizar o JS do app sem passar pela loja).

> [!NOTE] Managed Workflow vs. Bare Workflow O Expo "managed" cobre a grande maioria dos casos de uso sem exigir configuração nativa. Quando um módulo nativo customizado é necessário e o Expo ainda não suporta nativamente, existe o caminho de _prebuild_/_bare workflow_ para acessar o código nativo diretamente.

---

## 🔗 Notas Relacionadas

- [[ReactNative - Ambiente e Estrutura de Pastas]]
- [[ReactNative - Componentes e Estilo]]
- [[React]]
- ⬅️ Voltar para [[React]]