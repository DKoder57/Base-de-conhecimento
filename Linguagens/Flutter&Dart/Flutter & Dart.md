---
tags: [flutter, dart, mobile, desenvolvimento]
area: Desenvolvimento Mobile
status: ativo
nivel: completo
---
# 📱 Flutter & Dart — Matriz da Trilha

> Construir conhecimento reutilizável, não apenas concluir cursos.

---

> [!info] O que é **Flutter** é o framework multiplataforma do Google (Android, iOS, Web, Desktop, embarcados) com base de código única. **Dart** é a linguagem usada pelo Flutter: tipagem segura, null safety e bom suporte assíncrono.

> [!abstract] Objetivo desta trilha Organizar o estudo de Dart e Flutter de forma progressiva, transformando documentação, laboratórios e projetos em base de conhecimento reutilizável — com foco em aplicar, não só em concluir cursos.

---

## 🧠 Como usar esta matriz

Cada nota é uma unidade independente de conhecimento. Fluxo recomendado:

**Teoria → Exemplo → Laboratório → Projeto → Documentação própria**

Uma nota só é considerada concluída depois de aplicada em projeto ou laboratório real.

```text
Fundamentos → Dart → Flutter → Widgets → Responsividade → Navegação
→ Estado → Persistência → APIs → Arquitetura → Testes → Deploy
→ Laboratórios → Receitas → Projetos
```

---

## 📚 Resumo da matriz

|Nível|Área|Resumo|
|:--|:--|:--|
|🌱 1|Fundamentos|Algoritmos, variáveis, operadores, condicionais, repetição, funções, estruturas de dados|
|🌿 2|Dart|Sintaxe, coleções, POO, generics, null safety, exceções, programação assíncrona|
|🌿 3|Flutter Fundamentals|Ecossistema, configuração de ambiente, estrutura de projeto, dependências|
|🌿 4|Widgets e Interface|Widget tree, layouts, listas, formulários, elementos de UI|
|🌳 5|Responsividade|MediaQuery, LayoutBuilder, temas, Material Design 3|
|🌳 6|Navegação|Rotas, GoRouter, navegação declarativa, Deep Links|
|🌳 7|Gerenciamento de Estado|setState, Provider, Riverpod, Bloc, MVVM|
|🌳 8|Persistência|Shared Preferences, SQLite, Drift, Hive, Secure Storage|
|🌳 9|APIs e Backend|HTTP, Dio, REST, Firebase, Supabase|
|🏆 10|Arquitetura Profissional|SOLID, Design Patterns, Clean Architecture, Repository Pattern, DI|
|🏆 11|Testes|Unitários, widgets, integração, mocks|
|🏆 12|Deploy|APK, AAB, lojas oficiais, CI/CD|
|🔬 13|Laboratórios|Experimentação prática isolada|
|📖 14|Receitas|Implementações reutilizáveis de consulta rápida|
|🚀 15|Projetos|Aplicações completas, do básico ao profissional|

---

# 🌱 NÍVEL 1 — FUNDAMENTOS DE PROGRAMAÇÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|1.1|[[Prog - Algoritmos]]|Resolução de problemas, fluxogramas, pseudocódigo|
|1.2|[[Prog - Variáveis]]|Declaração, atribuição, tipos, escopo|
|1.3|[[Prog - Operadores]]|Aritméticos, relacionais, lógicos, precedência|
|1.4|[[Prog - Estruturas Condicionais]]|if, else, switch|
|1.5|[[Prog - Estruturas de Repetição]]|for, while, do-while, break, continue|
|1.6|[[Prog - Funções]]|Parâmetros, retorno, escopo, reuso|
|1.7|[[Prog - Estruturas de Dados]]|Arrays, listas, mapas, conjuntos|

---

# 🌿 NÍVEL 2 — DART

|#|Nota|Tópicos|
|:--|:--|:--|
|2.1|[[Dart - Introdução]]|SDK, ecossistema, casos de uso|
|2.2|[[Dart - Sintaxe Básica]]|Estrutura da linguagem, convenções|
|2.3|[[Dart - Variáveis e Tipos]]|int, double, String, bool, dynamic, final, const|
|2.4|[[Dart - Operadores]]|Aritméticos, relacionais, lógicos|
|2.5|[[Dart - Estruturas Condicionais]]|if, switch, expressões condicionais|
|2.6|[[Dart - Estruturas de Repetição]]|for, while, for-in|
|2.7|[[Dart - Funções]]|Nomeadas, anônimas, arrow functions, parâmetros opcionais|
|2.8|[[Dart - Coleções]]|List, Set, Map|
|2.9|[[Dart - Tratamento de Exceções]]|try, catch, finally, throw|
|2.10|[[Dart - Programação Orientada a Objetos]]|Classes, objetos, construtores|
|2.11|[[Dart - Encapsulamento]]|Getters, setters, privacidade|
|2.12|[[Dart - Herança]]|extends, reutilização|
|2.13|[[Dart - Polimorfismo]]|Sobrescrita de métodos|
|2.14|[[Dart - Classes Abstratas]]|Contratos e abstração|
|2.15|[[Dart - Generics]]|Tipagem genérica|
|2.16|[[Dart - Extensions]]|Extensão de classes existentes|
|2.17|[[Dart - Null Safety]]|Operadores `?`, `!`, `??`|
|2.18|[[Dart - Futures]]|Operações assíncronas|
|2.19|[[Dart - Async Await]]|Simplificação de código assíncrono|
|2.20|[[Dart - Streams]]|Programação reativa|

---

# 🌿 NÍVEL 3 — FLUTTER FUNDAMENTALS

|#|Nota|Tópicos|
|:--|:--|:--|
|3.1|[[Flutter - Arquitetura do Framework]]|Engine, Framework, Render Tree, Widget Tree|
|3.2|[[Flutter - Configuração de Ambiente]]|SDK, Flutter Doctor|
|3.3|[[Flutter - Estrutura de Projeto]]|lib, assets, pubspec|
|3.4|[[Flutter - Gerenciamento de Dependências]]|pubspec.yaml, pub.dev|
|3.5|[[Flutter - Primeiro Aplicativo]]|MaterialApp, Scaffold|
|3.6|[[Flutter - Hot Reload e Hot Restart]]|Ciclo de desenvolvimento|

---

# 🌿 NÍVEL 4 — WIDGETS E INTERFACE

|#|Nota|Tópicos|
|:--|:--|:--|
|4.1|[[Flutter - Widget Tree]]|Estrutura hierárquica|
|4.2|[[Flutter - StatelessWidget]]|Widgets imutáveis|
|4.3|[[Flutter - StatefulWidget]]|Estado local|
|4.4|[[Flutter - Text e RichText]]|Exibição e formatação de texto|
|4.5|[[Flutter - Icons e Assets]]|Ícones e imagens|
|4.6|[[Flutter - Container]]|Espaçamento, decoração|
|4.7|[[Flutter - Row e Column]]|Organização horizontal/vertical|
|4.8|[[Flutter - Stack]]|Sobreposição de componentes|
|4.9|[[Flutter - Expanded e Flexible]]|Distribuição de espaço|
|4.10|[[Flutter - ListView]]|Listagens simples e dinâmicas|
|4.11|[[Flutter - GridView]]|Layouts em grade|
|4.12|[[Flutter - ScrollView]]|Áreas roláveis|
|4.13|[[Flutter - Forms]]|Formulários|
|4.14|[[Flutter - Inputs]]|Campos de entrada e validações|
|4.15|[[Flutter - Dialogs e BottomSheets]]|Interações modais|

---

# 🌳 NÍVEL 5 — RESPONSIVIDADE

|#|Nota|Tópicos|
|:--|:--|:--|
|5.1|[[Flutter - MediaQuery]]|Dimensões, orientação, contexto|
|5.2|[[Flutter - LayoutBuilder]]|Layout adaptativo|
|5.3|[[Flutter - Responsividade]]|Estratégias multi-dispositivo|
|5.4|[[Flutter - Temas]]|ThemeData|
|5.5|[[Flutter - Material Design 3]]|Componentes modernos|

---

# 🌳 NÍVEL 6 — NAVEGAÇÃO

|#|Nota|Tópicos|
|:--|:--|:--|
|6.1|[[Flutter - Rotas e Navegação]]|Push, Pop|
|6.2|[[Flutter - Named Routes]]|Rotas nomeadas|
|6.3|[[Flutter - GoRouter]]|Navegação declarativa|
|6.4|[[Flutter - Deep Links]]|Links externos e URLs|

---

# 🌳 NÍVEL 7 — GERENCIAMENTO DE ESTADO

|#|Nota|Tópicos|
|:--|:--|:--|
|7.1|[[Flutter - setState]]|Estado local, ciclo de vida|
|7.2|[[Flutter - Provider]]|ChangeNotifier, Consumer|
|7.3|[[Flutter - Riverpod]]|Providers, Notifiers, AsyncValue|
|7.4|[[Flutter - Bloc]]|Eventos, estados, Cubit|
|7.5|[[Flutter - MVVM]]|Model-View-ViewModel|

> [!note] Nota de mercado Riverpod é hoje a recomendação oficial do time de arquitetura do Flutter (guia MVVM em docs.flutter.dev). Provider segue relevante para entender os fundamentos antes de migrar.

---

# 🌳 NÍVEL 8 — PERSISTÊNCIA

|#|Nota|Tópicos|
|:--|:--|:--|
|8.1|[[Flutter - Shared Preferences]]|Configurações e dados primitivos|
|8.2|[[Flutter - SQLite]]|CRUD, modelagem, consultas|
|8.3|[[Flutter - Drift]]|ORM, geração de código|
|8.4|[[Flutter - Hive]]|NoSQL local|
|8.5|[[Flutter - Secure Storage]]|Tokens e credenciais|

---

# 🌳 NÍVEL 9 — APIS E BACKEND

|#|Nota|Tópicos|
|:--|:--|:--|
|9.1|[[Flutter - HTTP]]|GET, POST, PUT, DELETE|
|9.2|[[Flutter - Dio]]|Interceptadores, autenticação, timeout|
|9.3|[[Flutter - REST APIs]]|Arquitetura cliente-servidor|
|9.4|[[Flutter - JSON]]|Serialização/desserialização|
|9.5|[[Flutter - Firebase]]|Auth, Firestore, Storage, Cloud Functions|
|9.6|[[Flutter - Supabase]]|PostgreSQL, Edge Functions|

---

# 🏆 NÍVEL 10 — ARQUITETURA PROFISSIONAL

|#|Nota|Tópicos|
|:--|:--|:--|
|10.1|[[Arquitetura - SOLID]]|Manutenção, escalabilidade|
|10.2|[[Arquitetura - Design Patterns]]|Factory, Singleton, Strategy, Observer|
|10.3|[[Arquitetura - Clean Architecture]]|Camadas, casos de uso|
|10.4|[[Arquitetura - Repository Pattern]]|Abstração da camada de dados|
|10.5|[[Arquitetura - Dependency Injection]]|GetIt, Provider|
|10.6|[[Arquitetura - Feature First]]|Organização modular|

---

# 🏆 NÍVEL 11 — TESTES

|#|Nota|Tópicos|
|:--|:--|:--|
|11.1|[[Flutter - Unit Tests]]|Regras de negócio|
|11.2|[[Flutter - Widget Tests]]|Renderização e interação|
|11.3|[[Flutter - Integration Tests]]|Fluxos ponta a ponta|
|11.4|[[Flutter - Mockito]]|Mocking|

---

# 🏆 NÍVEL 12 — DEPLOY

|#|Nota|Tópicos|
|:--|:--|:--|
|12.1|[[Flutter - APK]]|Debug e Release|
|12.2|[[Flutter - AAB]]|Android App Bundle|
|12.3|[[Flutter - Google Play]]|Publicação e assinatura|
|12.4|[[Flutter - App Store]]|Certificados e perfis|
|12.5|[[Flutter - GitHub Actions]]|Builds e pipelines|
|12.6|[[Flutter - CI CD]]|Integração e entrega contínua|

---

# 🔬 NÍVEL 13 — LABORATÓRIOS

|#|Nota|Tópicos|
|:--|:--|:--|
|13.1|[[Lab - Widgets]]|Composição de interfaces|
|13.2|[[Lab - SQLite]]|CRUD e persistência|
|13.3|[[Lab - Riverpod]]|Estado avançado em projeto real|
|13.4|[[Lab - APIs]]|Consumo de APIs públicas|
|13.5|[[Lab - Firebase]]|Auth, Firestore, Storage|
|13.6|[[Lab - Supabase]]|Backend completo|
|13.7|[[Lab - Clean Architecture]]|Estruturação em camadas|

---

# 📖 NÍVEL 14 — RECEITAS

|#|Nota|Tópicos|
|:--|:--|:--|
|14.1|[[Recipe - CRUD SQLite]]|Create, Read, Update, Delete|
|14.2|[[Recipe - Consumir API]]|HTTP ou Dio|
|14.3|[[Recipe - Login Firebase]]|E-mail/senha e provedores externos|
|14.4|[[Recipe - Upload Firebase]]|Firebase Storage|
|14.5|[[Recipe - Notificações]]|Locais e push|
|14.6|[[Recipe - GoRouter]]|Rotas protegidas|
|14.7|[[Recipe - Riverpod]]|Estruturação rápida|

---

# 🚀 NÍVEL 15 — PROJETOS

|#|Nota|Tópicos|
|:--|:--|:--|
|15.1|[[Projeto - Calculadora]]|Estado simples, UI básica|
|15.2|[[Projeto - Todo App]]|CRUD e persistência local|
|15.3|[[Projeto - Clima]]|API externa, geolocalização|
|15.4|[[Projeto - Pokédex]]|REST, paginação|
|15.5|[[Projeto - Financeiro]]|Gráficos e relatórios|
|15.6|[[Projeto - GreenKeeper]]|SQLite, notificações, arquitetura|
|15.7|[[Projeto - SaaS Mobile]]|Auth, backend, deploy, escalabilidade|

---

# 📈 Roadmap profissional

|Etapa|Objetivo|Conhecimentos|
|:--|:--|:--|
|🌱 Fundamentos|Base sólida de programação|Algoritmos, variáveis, operadores, condicionais, loops, funções|
|🌿 Dart|Dominar a linguagem|Sintaxe, coleções, POO, generics, null safety, async/await|
|🌿 Flutter Básico|Aplicações simples|Widgets, layouts, navegação, responsividade|
|🌳 Flutter Intermediário|Aplicações completas|Estado, persistência, APIs, Firebase|
|🏆 Flutter Profissional|Boas práticas de mercado|Riverpod, arquitetura, testes, deploy|
|🚀 Flutter Avançado|Projetos escaláveis|Drift, Supabase, CI/CD, modularização|
|👑 Especialista|Sistemas complexos|Arquitetura de software, escalabilidade, observabilidade|

---

# 🎯 Critérios de conclusão

|Critério|Descrição|
|:--|:--|
|Conhecimento|Consigo explicar o conceito sem consulta|
|Implementação|Consigo implementar do zero|
|Depuração|Consigo identificar e corrigir erros comuns|
|Aplicação|Já utilizei em projeto real|
|Documentação|Possuo nota própria documentada|
|Exemplo|Tenho exemplo funcional salvo|
|Reutilização|Tenho receita pronta para consulta futura|

---

# 📊 Matriz de proficiência

|Status|Significado|
|:--|:--|
|⬜ Não Estudado|Conteúdo ainda não iniciado|
|🟦 Em Estudo|Teoria em andamento|
|🟨 Praticando|Exercícios e laboratórios|
|🟩 Aplicado|Utilizado em projeto real|
|🟪 Dominado|Capaz de ensinar e implementar sem consulta|

---

# 📚 Fontes (revisadas)

## Oficiais

- [Flutter Documentation](https://docs.flutter.dev/) — referência principal, atualizada continuamente
- [Learn Flutter (docs.flutter.dev/learn)](https://docs.flutter.dev/learn) — trilhas, codelabs e vídeos oficiais
- [Dart Documentation](https://dart.dev/guides)
- [Flutter Cookbook](https://docs.flutter.dev/cookbook) — receitas oficiais por tarefa
- [Pub.dev](https://pub.dev/) — pacotes
- [Riverpod (oficial)](https://riverpod.dev/) — hoje a recomendação padrão de gerenciamento de estado no guia de arquitetura do Flutter
- [Firebase Documentation](https://firebase.google.com/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [Drift Documentation](https://drift.simonbinder.eu/)
- [Hive Documentation](https://docs.hivedb.dev/)

## Referências técnicas

- [Code With Andrea](https://codewithandrea.com/) — um dos melhores conteúdos gratuitos de nível intermediário/avançado
- [Very Good Ventures — blog](https://verygood.ventures/blog)
- [Flutter YouTube Channel](https://www.youtube.com/@flutterdev)
- [Dart YouTube Channel](https://www.youtube.com/@dartlang)

## Livros

- _Flutter Apprentice_ (Katz, Moore, Ngo)
- _Clean Architecture_ (Robert C. Martin)
- _Clean Code_ (Robert C. Martin)
- _Refactoring_ (Martin Fowler)

> [!warning] Removido da lista original "Reso Coder" e "Flutter Community" (genérico) foram removidos por falta de manutenção recente/relevância verificável. "Flutter Complete Reference" foi removido por não ter edição atualizada confiável. Se algum desses ainda for útil para você, posso reincluir.