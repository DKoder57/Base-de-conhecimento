---
tags: [matriz, react-native, api, react-query]

área: React Native / Avançado

status: draft

matriz: "[[React]]"

---

# 🔌 ReactNative - Integração com APIs

> [!quote] Princípio No mobile, rede instável é a regra, não a exceção — cache e revalidação inteligente fazem a diferença entre um app que "parece travado" e um que parece rápido mesmo em 3G.

---

## 🎯 Conceito Principal

Além de `fetch`/`axios` (mesma lógica do React web, ver [[React - Requisições HTTP]]), apps mobile se beneficiam ainda mais de bibliotecas de **cache e sincronização de dados**, já que a conexão do usuário é mais instável que a de um desktop.

---

## 📡 `fetch` e `axios` — Revisão Rápida

```jsx
import { useEffect, useState } from "react";

function useProdutos() {
  const [produtos, setProdutos] = useState([]);
  const [carregando, setCarregando] = useState(true);

  useEffect(() => {
    fetch("https://api.exemplo.com/produtos")
      .then((res) => res.json())
      .then(setProdutos)
      .finally(() => setCarregando(false));
  }, []);

  return { produtos, carregando };
}
```

> [!WARNING] O problema desse padrão manual Toda tela que usa esse hook refaz a requisição do zero, sem cache entre telas, sem revalidação automática ao voltar o app do background, e sem tratamento padronizado de erro/retry — é aqui que o React Query (TanStack Query) resolve boa parte do trabalho manual.

---

## 🔄 React Query (TanStack Query)

```bash
npm install @tanstack/react-query
```

```jsx
// App.js
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Navegacao />
    </QueryClientProvider>
  );
}
```

```jsx
// Uso em uma tela
import { useQuery } from "@tanstack/react-query";

function TelaProdutos() {
  const { data: produtos, isLoading, error, refetch } = useQuery({
    queryKey: ["produtos"],
    queryFn: () => fetch("https://api.exemplo.com/produtos").then((r) => r.json()),
    staleTime: 1000 * 60, // considera os dados "frescos" por 1 minuto
  });

  if (isLoading) return <Text>Carregando...</Text>;
  if (error) return <Text>Erro ao carregar produtos</Text>;

  return (
    <FlatList
      data={produtos}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => <Text>{item.nome}</Text>}
      onRefresh={refetch}
      refreshing={isLoading}
    />
  );
}
```

|Recurso automático do React Query|Benefício|
|---|---|
|**Cache por `queryKey`**|Telas diferentes que pedem o mesmo dado reaproveitam o cache|
|**Revalidação em foco/reconexão**|Refaz a busca automaticamente quando o app volta do background|
|**Retry automático**|Tenta novamente sozinho em falhas de rede temporárias|
|**Estados padronizados**|`isLoading`, `isError`, `isFetching` já vêm prontos|

### Mutações (escrita de dados)

```jsx
import { useMutation, useQueryClient } from "@tanstack/react-query";

function useCriarProduto() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: (novoProduto) =>
      fetch("https://api.exemplo.com/produtos", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(novoProduto),
      }).then((r) => r.json()),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["produtos"] }); // força recarregar a lista
    },
  });
}
```

> [!TIP] `invalidateQueries` é a peça-chave Após criar/editar/remover um dado, invalidar a query correspondente garante que a lista na tela reflita a mudança sem precisar de lógica manual de "atualizar estado local depois do POST".

---

## 🔗 Notas Relacionadas

- [[React - Requisições HTTP]]
- [[ReactNative - Armazenamento Local]]
- [[React - Gerenciamento de Estado]]
- ⬅️ Voltar para [[React]]