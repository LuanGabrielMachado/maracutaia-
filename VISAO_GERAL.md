# 🎭 Maracutáia — Visão Geral

**Versão:** 7.0.0
**Data:** 16 de Março de 2026
**Status:** ✅ Produção

---

## 1. O Conceito

### 1.1 A Ideia Central

**Maracutáia** é uma rede social de **fofocas efêmeras** que roda dentro do Telegram como Mini App.

**Filosofia:**

- Postou? **10 minutos de castigo**
- Respondeu? **15 minutos de reflexão**
- Fofocou? **Se defenda** (se conseguir)
- **Tudo é feature**

### 1.2 A Tia Górgona 👁️🐍

A **Tia Górgona** é a guardiã da plataforma.

- 👁️ **Vigilância** — ela vê tudo
- 🐍 **Sabedoria** — ela sabe tudo
- ⏰ **Paciência** — ela te faz esperar
- 🎭 **Deboche** — ela não perdoa

### 1.3 Slow Social

**Slow Social** é a filosofia de design intencional:

- ✅ **Animações são feature** — planejadas, não acidentais
- ✅ **Loadings são feature** — respire, aprecie as artes de fundo
- ✅ **Rate limits são feature** — pense antes de postar
- ✅ **Efemeridade é feature** — desapega, foi só fofoca
- ✅ **Um post de cada vez** — sem scroll infinito
- ✅ **Feed cronológico** — sem algoritmo, sem manipulação

**Contra o que lutamos:**

- ❌ Scroll infinito — vício
- ❌ Resposta imediata — ansiedade
- ❌ Posts eternos — cringe
- ❌ Algoritmos — manipulação

---

## 2. Como Funciona

### 2.1 Acesso

**Onde:** Telegram Mini App (roda dentro do Telegram)
**URL:** [t.me/vempramaracutaiabot](https://t.me/vempramaracutaiabot)

**Como:**

1. Abra o Telegram
2. Busque @vempramaracutaiabot
3. Clique em "Abrir"
4. Pronto — sem senha, sem email, sem OAuth

**Autenticação:** Telegram ID validado por HMAC-SHA256

### 2.2 Posts

- Microblog de texto — **165 caracteres**
- Imagem opcional — até **12MB**
- Embed de vídeo — YouTube e Vimeo (URL detectada automaticamente, não conta no limite)
- Menções `@usuario` — autocomplete dos seus seguidos, notifica a pessoa
- **Castigo:** 10 minutos até poder postar de novo
- **Efemeridade:** posts somem após 7 dias, incluindo todas as respostas em cascade

### 2.3 Respostas

- Responder posts de outros — **100 caracteres**
- Menções `@usuario` disponíveis também nas respostas
- **Reflexão:** 15 minutos entre respostas
- Autor do post original é notificado via bot

### 2.4 Threads 🧵

O sistema de threads transforma o feed em um explorador de conversas.

- Posts com respostas exibem `Ver thread (x)` no rodapé
- Entrar na thread: post original no topo + replies empilhadas em ordem cronológica
- Navegação em pilha: `← Sair` (nível 1) ou `← Voltar · Sair` (nível 2+)
- Respostas com próprias respostas também têm `Ver thread` — infinitamente
- Clicar na referência de uma reply dentro da thread entra na thread daquela reply

### 2.5 Reações

12 emojis com **motor de física newtoniana próprio**:

> 👍 🖕 😂 😱 💀 🔥 ❤️ 😍 🤔 🍪 🐍 🐮

- Emojis flutuam com colisão, repulsão e thermal noise em 60fps
- Respondem ao giroscópio do celular (Android nativo, iOS com permissão)
- Motor escrito em React com RAF, escrevendo direto no DOM sem re-renders

### 2.6 Follow e Busca

- **Sugestões:** pessoas que você ainda não segue aparecem como bolhas flutuantes
- **Busca 🔍:** bolha especial na grade — clica, digita, resultados aparecem como bolhas
- **Menções:** só pode mencionar quem você segue (anti-spam)
- Timeline mostra posts de quem você segue, em ordem cronológica (id DESC)
- Feed mode: `following` (padrão) ou `all` (todos os posts, se liberado)

### 2.7 Moderação Social

Cada usuário tem controle sobre sua experiência:

- **Bloquear 🚫** — efeito imediato e bidirecional no feed (permanente)
- **Ghostar 👻 por 48h** — a pessoa para de ver seus posts temporariamente, renovável
- **Denunciar 🚨** — chega direto para os admins

Tudo acessível ao tocar na foto de outro usuário.

### 2.8 Notificações

Push via Bot Telegram — 4 tipos:

- **Reply:** `💬 Nome respondeu sua fofoca...`
- **Reaction:** `🔥 Nome reagiu na sua fofoca...`
- **Follow:** `👀 Nome veio bisbilhotar sua vida...`
- **Menção:** `👋 Nome te mencionou numa fofoca...`

Controle: opt-out disponível no perfil. Se bloquear o bot → desativa automaticamente.

### 2.9 Lock Biométrico 🔒

- Proteja o app com Face ID ou impressão digital via Telegram BiometricManager
- Ativa/desativa no perfil — desativar exige autenticação biométrica de confirmação
- Re-trava automaticamente ao voltar do background

### 2.10 Exportação de Dados 📦

- Botão no perfil — exporta conta, posts e lista de seguidos em `.txt`
- Enviado direto na conversa com o bot
- LGPD Art. 18, IV — direito de acesso aos dados

---

## 3. Arquitetura

### 3.1 Visão Geral

```
┌──────────────────────────────────────────────┐
│           Telegram WebApp SDK                │
│  Auth · UI · Haptic · Biometria · Share      │
└───────────────────┬──────────────────────────┘
                    │
┌───────────────────▼──────────────────────────┐
│            Next.js 15 (Vercel)               │
│  13 hooks · 25+ componentes · 48 procedures  │
│  Bot API · 2 Cron Jobs · LogVault 9/9        │
└─────────────┬─────────────────┬──────────────┘
              ▼                 ▼
   ┌──────────────────┐ ┌──────────────────┐
   │  Supabase (DB)   │ │ Supabase Storage │
   │  10 tabelas      │ │  12MB max · CDN  │
   │  19+ índices     │ │                  │
   └──────────────────┘ └──────────────────┘
```

### 3.2 Camadas

**Frontend**

- Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS, Framer Motion

**API**

- tRPC v11 (type-safe end-to-end), Next.js API Routes serverless, Zod

**Dados**

- PostgreSQL via Supabase, Drizzle ORM, Supabase Storage

**Auth**

- Telegram WebApp SDK + HMAC-SHA256 + JWT HTTP-only (7 dias)

### 3.3 Fluxo de Dados

1. Usuário abre app → Telegram SDK inicializa
2. Frontend captura `initData`
3. Envia para backend via `Authorization` header
4. Backend valida HMAC-SHA256
5. Contexto populado: `telegramId`, `isAdmin`, `isModerator`
6. Procedure tRPC executa com type-safety end-to-end
7. Query no banco com shadow ban + bloqueios + efemeridade aplicados
8. Resposta retorna tipada, frontend renderiza

---

## 4. Funcionalidades em Detalhe

### 4.1 Rate Limiting — 3 Camadas

**Intervalos:** Posts: 20min · Respostas: 30min · Admin: bypassa

**Camadas (mais restritivo vence):**

1. **Local** — CloudStorage do Telegram + localStorage (sem latência)
2. **Banco** — `users.lastPostAt` / `lastReplyAt` (fonte da verdade)
3. **Fallback** — tabela posts (para usuários sem `lastPostAt`)

Flag global `lock_posts_global` pode travar todos os posts instantaneamente.

### 4.2 Efemeridade e Cascade

- Cron job diário (3h UTC) deleta posts com mais de 7 dias
- Admin posts são isentos
- FK `replyToPostId → posts.id ON DELETE CASCADE` — delete do original propaga por toda a árvore de replies, infinitamente, em uma operação
- Imagens limpas do Storage via `storageDelete` fire-and-forget
- Countdown mostra tempo restante (atualiza a cada hora, minuteiros nas últimas 24h)

### 4.3 Moderação Hierárquica

**Administradora (`👑 Deusa`):**

- Acesso total ao painel
- Posts sem efemeridade, visíveis a todos
- Broadcast para todos os usuários

**Moderadora (`🛡️ Moderadora`):**

- Pode: deletar posts, usar broadcast, ver audit log e LogVault, ver stats
- Não pode: banir usuários, shadow ban, alterar flags globais
- Posts pessoais expiram normalmente em 7 dias
- Broadcasts publicados sob identidade da admin (alcance total garantido)

**Ferramentas disponíveis:**

- Ban total — usuário não pode logar
- Shadow ban — posta normalmente, ninguém vê
- Delete de qualquer post
- Reset de rate limit
- Alteração de feed mode por usuário
- Flags globais (manutenção, pause de novos usuários, feed global, lock de posts)
- Audit log de todas as ações

### 4.4 Notificações — Fluxo Completo

1. Evento ocorre (reply/reaction/follow/mention)
2. Insert no banco (status: `pending`)
3. Busca recipient + actor em paralelo (`Promise.all`)
4. Envia via Bot API imediatamente
5. Atualiza status (`sent` / `failed` / `skipped`)
6. Cron retry a cada 12h se falhou (máx 3 tentativas)

Deduplicação via unique constraint — mesmo evento nunca é enviado duas vezes.
~95% envio imediato, ~5% via cron retry.

### 4.5 LogVault

Sistema de logging estruturado com 9 contextos, 100% de cobertura:

`notification` · `post` · `reaction` · `follow` · `upload` · `rate_limit` · `cron` · `auth` · `system`

Todos os logs armazenados no banco, consultáveis no painel admin.

---

## 5. Stack Técnico

| Categoria   | Tecnologia       | Versão |
| ----------- | ---------------- | ------ |
| Framework   | Next.js          | 15.x   |
| UI Library  | React            | 19.x   |
| Linguagem   | TypeScript       | 5.x    |
| Estilização | Tailwind CSS     | 3.x    |
| API         | tRPC             | 11.x   |
| Estado      | TanStack Query   | 5.x    |
| ORM         | Drizzle ORM      | 0.44.x |
| Database    | PostgreSQL       | 15+    |
| Storage     | Supabase Storage | —      |
| Animações   | Framer Motion    | 11.x   |
| Deploy      | Vercel           | —      |
| Bot         | Telegram Bot API | —      |

---

## 6. Métricas

### Performance

| Métrica                | Valor   |
| ---------------------- | ------- |
| Bundle Size            | ~780KB  |
| First Load             | ~1s     |
| Lighthouse             | 90+     |
| API Response           | < 200ms |
| Queries no banco       | < 50ms  |
| Animações              | 60fps   |
| Notificações imediatas | ~95%    |

### Código (v7.0.0)

| Métrica                  | Valor      |
| ------------------------ | ---------- |
| Arquivos TS/TSX          | 117        |
| Componentes React        | 25+        |
| Hooks customizados       | 13         |
| Procedures tRPC          | 48         |
| Tabelas no banco         | 10         |
| Migrations               | 14         |
| Índices no banco         | 19+        |
| Cron jobs                | 2          |
| Contextos LogVault       | 9 (100%)   |
| Tempo de desenvolvimento | ~7 semanas |

### Expo → Next.js (histórico)

| Métrica     | Expo (jan 2026) | Next.js (atual) |
| ----------- | --------------- | --------------- |
| Bundle Size | 2.8MB           | ~780KB          |
| First Load  | 3-5s            | ~1s             |
| Lighthouse  | 65-75           | 90+             |

---

## 7. Segurança

- **Autenticação:** HMAC-SHA256 via Telegram WebApp SDK + JWT 7 dias HTTP-only
- **Rate Limiting:** 3 camadas, flag global de emergência
- **Ban check:** verificado em todas as mutations de escrita (protege contra JWT válido pós-ban)
- **Shadow ban:** filtro aplicado em todas as queries de leitura do feed
- **Cascade:** delete propaga para todas as entidades filhas automaticamente
- **LGPD:** opt-out de notificações, exportação de dados, dados mínimos armazenados

---

## 8. Deploy e Infraestrutura

### Onde Roda

**Vercel:** Serverless Functions, auto-scaling, CDN global, CI/CD automático
**Supabase:** PostgreSQL 15+, Storage S3-compatible, 500MB free tier

### Cron Jobs

**Cleanup (3h UTC diário):**

- Deleta posts com mais de 7 dias (admin isentos)
- Cascade no banco remove replies e reações automaticamente
- Imagens removidas do Storage (fire-and-forget)

**Notifications retry (12h UTC):**

- Processa notificações pendentes/falhas
- Máx 3 tentativas por notificação
- Desativa permanentemente se 403 (bot bloqueado)

### Custos Estimados

| Escala            | Custo/mês                        |
| ----------------- | -------------------------------- |
| Até ~10K usuários | $0 (free tiers)                  |
| 10K–50K usuários  | ~$45 (Vercel Pro + Supabase Pro) |

---

## 9. Roadmap

### ✅ Concluído (v7.0.0)

- ✅ MVP funcional completo (posts, follows, reações, perfis)
- ✅ Migração Expo → Next.js (bundle -93%, first load -75%)
- ✅ Sistema de replies com animação
- ✅ Posts efêmeros em cascade (7 dias)
- ✅ Rate limiting híbrido 3 camadas
- ✅ Admin dashboard completo
- ✅ Notificações push via Bot
- ✅ Motor de física newtoniana com giroscópio
- ✅ Sistema de threads navegáveis em pilha infinita
- ✅ Bloqueio bidirecional + Ghosting 48h + Denúncia
- ✅ Embed de vídeo (YouTube + Vimeo)
- ✅ Lock biométrico (Face ID / Digital)
- ✅ Exportação de dados LGPD
- ✅ Menções `@usuario` com autocomplete e notificação
- ✅ Busca global de pessoas
- ✅ Moderação hierárquica (Admin + Moderadora)
- ✅ LogVault 100% de cobertura

### 📋 Futuro

- Multi-language support (i18n)

---

## 10. FAQ

**Por que 10 minutos de rate limit?**
Slow social é feature. Para você pensar antes de postar.

**Por que 7 dias de efemeridade?**
Fofoca é efêmera. Como a vida real. Desapega.

**O que é ghosting de 48h?**
Você pausa alguém temporariamente — a pessoa para de ver seus posts por 48h. Renovável. Diferente de bloquear (permanente e bidirecional).

**Admin pode tudo?**
Sim. Tia Górgona quem manda.

**Posso baixar meus dados?**
Sim — botão no perfil envia um `.txt` com tudo direto pelo bot. LGPD compliance.

**É open-source?**
Não. Privado.

**Quanto custa usar?**
Grátis para o usuário final. Sempre.

---

## 11. Glossário

| Termo                 | Significado                                                          |
| --------------------- | -------------------------------------------------------------------- |
| **Tia Górgona**       | Guardiã/mascote da plataforma                                        |
| **Castigo**           | Rate limit de 10 minutos entre posts                                 |
| **Reflexão**          | Rate limit de 15 minutos entre respostas |
| **Slow Social**       | Filosofia de design intencional contra vício digital                 |
| **Shadow Ban**        | Usuário posta normalmente, mas ninguém vê                            |
| **Ghosting**          | Pausa temporária de 48h — a pessoa para de ver seus posts            |
| **Thread**            | Pilha navegável de respostas a um post                               |
| **Fire-and-Forget**   | Operação async sem bloquear o fluxo principal                        |
| **Cascade**           | Delete que propaga automaticamente para entidades filhas             |
| **Cursor Pagination** | Paginação por id DESC — eficiente e consistente                      |
| **Optimistic Update** | UI atualiza antes da confirmação do servidor                         |
| **LogVault**          | Sistema de logging estruturado com 9 contextos                       |
| **Deduplicação**      | Unique constraint que impede envio duplo de notificações             |

---

## 12. Conclusão

**Maracutáia em uma linha:**

> Uma rede social de fofocas efêmeras com slow social intencional, onde a Tia Górgona te vigia e você fica de castigo se postar demais.

**O que a diferencia:**

- Motor de física newtoniana com giroscópio real em React — A desproporção entre a sofisticação da solução e a frivolidade do contexto é sensacional
- Threads navegáveis em pilha infinita — exploração de conversas sem perder contexto, em pilhas de cards infinitos
- Ghosting de 48h — Um conceito né, obrigado Giovanna
- Efemeridade em cascade — tudo some junto, sem rastro, o estrago é um só, post original sumiu tudo relacionado some
- Slow social real — rate limits que forçam intenção, sem scroll infinito

**Stack:** Next.js 15 + React 19 + tRPC v11 + Drizzle ORM + Supabase + Vercel
**Desenvolvimento:** ~7 semanas (janeiro a março de 2026)
**Status:** ✅ Produção pronta

---

*"Na Maracutáia, a Tia Górgona vê tudo. E ela não perdoa, ela debocha."*

**[t.me/vempramaracutaiabot](https://t.me/vempramaracutaiabot)**

---

👁️🐍


