---
tags: [matriz, react-native, setup, expo]

área: React Native / Fundamentos

status: draft

matriz: "[[React]]"

---
# 🗂️ ReactNative - Ambiente e Estrutura de Pastas

> [!quote] Princípio Um projeto mobile mal organizado se torna incontrolável rápido — a estrutura de pastas certa evita esse caos desde o primeiro commit.

---

## 🎯 Conceito Principal

Configurar corretamente o ambiente (SDK do Android, variáveis de ambiente) e adotar uma estrutura de pastas consistente são pré-requisitos antes de qualquer linha de UI.

---

## ⚙️ Setup do Ambiente

```bash
# Criar um novo projeto Expo (SDK atual)
npx create-expo-app meu-app
cd meu-app
npx expo start
```

|Requisito|Para quê|
|---|---|
|**Node.js LTS**|Roda o Metro bundler e as ferramentas de CLI|
|**Android Studio + Android SDK**|Necessário para emulador Android e builds nativos|
|**Xcode** (apenas macOS)|Necessário para simulador iOS e builds nativos|
|**Expo Go** (app no celular)|Testar rapidamente no dispositivo físico sem build nativo|

### Variáveis de Ambiente (Android)

```bash
# Exemplo de configuração no .bashrc/.zshrc (Linux/macOS)
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

> [!TIP] Verificar se está tudo certo O comando `npx expo-doctor` (ou `npx react-native doctor`, no bare workflow) verifica automaticamente se o ambiente está configurado corretamente, apontando o que falta.

---

## 📁 Estrutura de Pastas Recomendada

```
meu-app/
├── src/
│   ├── components/       # Componentes reutilizáveis (Button, Card, Input)
│   ├── screens/          # Telas completas (LoginScreen, HomeScreen)
│   ├── navigation/        # Configuração de rotas (Stack, Tab, Drawer)
│   ├── hooks/             # Hooks customizados (useAuth, useProdutos)
│   ├── services/          # Chamadas de API, integração com Supabase/Firebase
│   ├── store/             # Zustand/Redux — estado global
│   ├── utils/             # Funções auxiliares puras (formatação, validação)
│   └── theme/             # Cores, tipografia, espaçamentos globais
├── assets/                # Imagens, fontes, ícones
├── app.json / app.config.js
├── package.json
└── tsconfig.json
```

> [!NOTE] `components/` vs. `screens/` Um erro comum de iniciante é misturar os dois. `components/` deve conter peças **pequenas e reutilizáveis** (sem lógica de navegação própria); `screens/` contém a composição completa de uma tela, geralmente ligada diretamente a uma rota do `navigation/`.

---

## 📐 Boas Práticas

- Um componente por arquivo, nomeado com PascalCase (`ProdutoCard.tsx`)
- Separar lógica de API (`services/`) da lógica de UI (`screens/`, `components/`)
- Usar aliases de import (`@/components/...`) via `tsconfig.json`/`babel.config.js` para evitar caminhos relativos longos (`../../../components`)
- Manter arquivos de configuração sensíveis (`.env`) fora do controle de versão (`.gitignore`)

```json
// tsconfig.json — exemplo de alias de import
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

---

## 🔗 Notas Relacionadas

- [[ReactNative - Fundamentos]]
- [[ReactNative - Componentes e Estilo]]
- [[Ferramentas]]
- ⬅️ Voltar para [[React]]