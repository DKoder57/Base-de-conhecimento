---
tags: [matriz, react, formularios, react-hook-form, zod]

área: React JS / Estado da Arte (2026)
status: draft

matriz: "[[React]]"

---
# 📋 React - Formulários com React Hook Form e Zod

> [!quote] Princípio Formulários controlados puros (um `useState` por campo) re-renderizam o componente inteiro a cada tecla digitada — em formulários grandes, isso vira um problema de performance real.

---

## 🎯 Conceito Principal

**React Hook Form** gerencia o estado dos campos por fora do ciclo de render do React (via _refs_ não-controlados), minimizando re-renders. **Zod** complementa definindo o _schema_ de validação de forma declarativa e totalmente tipada — a dupla mais usada em projetos React/Next.js em 2026.

---

## ⚙️ Setup Básico

```bash
npm install react-hook-form zod @hookform/resolvers
```

```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

// 1. Define o schema — única fonte de verdade para validação e tipos
const schemaCadastro = z.object({
  nome: z.string().min(2, "Nome muito curto"),
  email: z.string().email("E-mail inválido"),
  idade: z.coerce.number().min(18, "Precisa ser maior de idade"),
});

// 2. Infere o tipo TypeScript diretamente do schema — sem duplicar a definição
type DadosCadastro = z.infer<typeof schemaCadastro>;

function FormularioCadastro() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
  } = useForm<DadosCadastro>({
    resolver: zodResolver(schemaCadastro),
  });

  async function aoEnviar(dados: DadosCadastro) {
    await salvarCadastro(dados);
  }

  return (
    <form onSubmit={handleSubmit(aoEnviar)}>
      <input {...register("nome")} placeholder="Nome" />
      {errors.nome && <p>{errors.nome.message}</p>}

      <input {...register("email")} placeholder="E-mail" />
      {errors.email && <p>{errors.email.message}</p>}

      <input {...register("idade")} type="number" placeholder="Idade" />
      {errors.idade && <p>{errors.idade.message}</p>}

      <button disabled={isSubmitting}>{isSubmitting ? "Enviando..." : "Cadastrar"}</button>
    </form>
  );
}
```

> [!NOTE] Por que `register` evita re-renders `register("nome")` conecta o input diretamente ao formulário via _ref_, sem passar pelo `useState`/re-render do React a cada tecla — só quando o formulário é validado ou submetido é que o componente re-renderiza, ao contrário do padrão 100% controlado tradicional.

---

## 🎯 Zod — Validações Comuns

```ts
const schema = z.object({
  senha: z.string().min(8, "Mínimo 8 caracteres"),
  confirmarSenha: z.string(),
  site: z.string().url("URL inválida").optional(),
  aceitouTermos: z.boolean().refine((v) => v === true, "É necessário aceitar os termos"),
}).refine((dados) => dados.senha === dados.confirmarSenha, {
  message: "As senhas não coincidem",
  path: ["confirmarSenha"], // aponta o erro para o campo específico
});
```

> [!TIP] `.refine()` para validações cruzadas Quando a validação de um campo depende do valor de outro (como confirmação de senha), `.refine()` no schema resolve isso de forma declarativa, sem lógica manual espalhada no componente.

---

## 🔌 Campos Controlados (Select, Checkbox customizados)

Para componentes de UI que não são um `<input>` nativo (ex: um select estilizado de biblioteca de componentes), usa-se o componente `Controller`:

```tsx
import { Controller } from "react-hook-form";
import SelectCustomizado from "./SelectCustomizado";

<Controller
  name="categoria"
  control={control}
  render={({ field }) => (
    <SelectCustomizado value={field.value} onChange={field.onChange} />
  )}
/>
```

---

## 🖥️ Integração com Server Actions (React 19)

```tsx
"use client";

import { useActionState } from "react";
import { criarUsuarioAction } from "./actions";

function FormularioComServerAction() {
  const [estado, acao, pendente] = useActionState(criarUsuarioAction, null);

  return (
    <form action={acao}>
      <input name="nome" />
      <button disabled={pendente}>Salvar</button>
      {estado?.erros?.nome && <p>{estado.erros.nome}</p>}
    </form>
  );
}
```

```ts
// actions.ts
"use server";
import { schemaCadastro } from "./schemas";

export async function criarUsuarioAction(estadoAnterior: any, formData: FormData) {
  const resultado = schemaCadastro.safeParse(Object.fromEntries(formData));

  if (!resultado.success) {
    return { erros: resultado.error.flatten().fieldErrors };
  }

  await salvarUsuario(resultado.data);
  return { sucesso: true };
}
```

> [!NOTE] Zod validando no servidor também O mesmo schema Zod usado no cliente (React Hook Form) pode validar novamente os dados recebidos no Server Action — nunca confie apenas na validação do cliente, ver [[Cyber - Desenvolvimento Web para Pentesters]] sobre por que a validação client-side nunca é suficiente sozinha.

---

## 🔗 Notas Relacionadas

- [[React - Formulários]]
- [[React - Actions e Novos Hooks do React 19]]
- [[React - Testes com Jest e Testing Library]]
- ⬅️ Voltar para [[React]]