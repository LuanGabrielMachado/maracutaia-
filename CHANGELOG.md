# 📝 CHANGELOG — Maracutáia

**Projeto:** Maracutáia — Telegram Mini App de Microblogging Efêmero
**Versão Atual:** 7.0.0
**Status:** ✅ Produção
**Início do Desenvolvimento:** Final de Janeiro de 2026
**Última Atualização:** 16 de Março de 2026

> Este changelog documenta toda a evolução do Maracutáia — do MVP inicial ao lançamento público. Cada versão representa uma iteração real em produção.

---

## 📋 Índice

1. [v7.0.0 — Social Complete Release](#-v700--social-complete-release--16-março-2026)
2. [v6.0.0 — Maracutaia Release](#-v600--maracutaia-release--16-março-2026)
3. [v5.0.0 — Icarus Release](#-v500--icarus-release--14-março-2026)
4. [v4.0.0 — State of the Art](#-v400--state-of-the-art--13-março-2026)
5. [v3.2.0 — Otimização e Estabilidade](#-v320--otimização-e-estabilidade--10-março-2026)
6. [v3.1.0 — Sistema de Notificações](#-v310--sistema-de-notificações--07-08-março-2026)
7. [v3.0.0 — Replies e Efemeridade](#-v300--replies-e-efemeridade--25-fev--06-mar-2026)
8. [v2.1.0 — Feed Swipeable](#-v210--feed-swipeable--02-março-2026)
9. [v2.0.0 — Migração Next.js](#-v200--migração-nextjs--25-fevereiro-2026)
10. [v1.5.0 — Segurança e Sessions](#-v150--segurança-e-sessions--20-24-fevereiro-2026)
11. [v1.0.0 — MVP Next.js](#-v100--mvp-nextjs--18-fevereiro-2026)
12. [v0.8.0 — MVP Expo](#-v080--mvp-expo--final-de-janeiro-2026)
13. [Linha do Tempo](#-linha-do-tempo)
14. [Evolução da Arquitetura](#-evolução-da-arquitetura)
15. [Estatísticas Gerais](#-estatísticas-gerais)

---

## 🚀 v7.0.0 — Social Complete Release — 16 Março 2026

**Tipo:** Feature Release + Auditoria de Estabilidade

Última rodada de features sociais antes do lançamento público. Busca de pessoas com UI de bolha, menções `@usuario` com autocomplete e notificação push, sistema hierárquico de moderação, e faxinão completo de dead code e coesão.

### Busca de Pessoas 🔍

- Bolha `🔍` flutuante aparece na grade da página de seguir — mesma linguagem visual das bolhas de usuário
- Clica → caixa glass desce com spring, input foca automaticamente
- Busca global em tempo real (LIKE case-insensitive, respeita shadow ban e bloqueios)
- Resultados como bolhas — pode seguir direto do resultado
- Fechar ou sair da página limpa a busca (estado local, sem persistência)
- Componente `UserBubble` extraído — eliminou JSX duplicado de bolha entre sugestões e resultados

### Menções `@usuario` 💬

**Frontend:**
- Digita `@` em post ou reply → dropdown glass escuro aparece *acima* da textarea
- Lista os seguidos que combinam com o que foi digitado (até 5 sugestões)
- Seguidos pré-carregados na montagem — autocomplete instantâneo, sem delay de rede
- Clica na sugestão → insere `@nome` completo com espaço e fecha o dropdown
- Fecha automaticamente ao enviar ou ao fechar a reply

**Backend (fire-and-forget após criação do post/reply):**
- Extrai `@nomes` do conteúdo (máx 3 por post, anti-spam)
- Resolve para `telegramId` apenas dos seguidos do autor
- Na reply: não duplica notificação se o mencionado já é o autor do post original
- Notificação via bot: `👋 Nome te mencionou numa fofoca: "..."` + botão para abrir o app
- Tipo `mention` adicionado à tabela de notificações com deduplicação

### Sistema de Moderação Hierárquica 🛡️

Dois níveis de acesso ao painel administrativo, configurados por variáveis de ambiente.

**Administradora (`ADMIN_TELEGRAM_ID`):**
- Acesso total ao painel — todas as seções
- Posts sem efemeridade, visíveis a todos no feed
- Título `👑 Deusa` no topo do painel

**Moderadora (`MODERATOR_TELEGRAM_IDS`):**
- Acesso via double-tap no avatar do perfil
- Pode: ver stats, deletar posts, usar broadcast, ver audit log e LogVault
- Não pode: alterar flags do servidor, ban/shadow ban, alterar feed mode
- Posts pessoais expiram normalmente em 7 dias (sem bypass de efemeridade)
- Broadcasts publicados sob o `telegramId` da admin principal (garantindo alcance total)
- Título `🛡️ Moderadora` no topo do painel
- Auditoria registra quem realmente publicou o broadcast

**Implementação técnica:**
- `adminProcedure` agora aceita `isAdmin || isModerator`
- Procedures sensíveis com guard explícito: `setFlag`, `banUser`, `shadowBanUser`, `resetRateLimit`, `setUserFeedMode`
- `useAuth` expõe `isModerator` e `role: 'deusa' | 'mod' | 'user'`

### Auditoria de Estabilidade 🔒

**Bugs corrigidos:**
- Ban check faltando nas mutations `block`, `ghost` e `report`
- Tipo `Post.author` era não-nullable mas banco retorna `null` — `as unknown as Post[]` removido
- Strings sem acento em popups de UI (`'Confirmar exclusao'`, `'Post nao encontrado'`, `'Usuario'`)
- `replyCount && ...` renderizava `0` como texto — corrigido para `!!replyCount && replyCount > 0`
- `replyCountQuery` sem `gcTime` — padronizado com demais queries
- Flash de tela vazia ao entrar em thread — `isLoading` combinado com `threadRootQuery.isLoading`
- `TelegramUser` duplicado em `use-profile-data.ts` → importa tipo canônico de `telegram.d.ts`
- `*/` órfão em `video-embed.ts` causando erro de regexp no build
- Procedure `posts.search` duplicada no router
- `photoUrl: undefined` → `?? null` em `authorData` do PostCard

**Dead code removido:**
- `getUserStats` — duplicata de `getAdminStats` sem consumidor
- `isBlocked` — exportada mas nunca chamada (bloqueio funciona via subquery no feed)
- `searchPosts` — função e procedure sem consumidor no frontend
- `posts.mentionFollowing` — procedure morta (frontend usa `follows.following` diretamente)
- `renderMentions` e `hasMentions` — funções em `mention.ts` sem uso
- `isPublishing` — prop fantasma do componente `AdminBroadcast`
- `isNotNull` e `blocks` — imports órfãos em `post.repository.ts`
- `src/components/user-action-sheet.tsx` — criado e descontinuado na mesma sessão
- `src/components/device-motion-permission.tsx` — órfão desde v5.0.0

**Refatorações:**
- `handlePickImage` envolto em `useCallback` — elimina warning de exhaustive-deps
- Tipo `role` tipado na fonte do router — elimina cast em `useAuth`
- Duplo `?? 0` desnecessário em contador de posts → `?? posts.length`

### Métricas v7.0.0

| Métrica | v6.0.0 | v7.0.0 |
|---------|--------|--------|
| Arquivos TS/TSX | 115 | 117 |
| Hooks customizados | 12 | 13 |
| Procedures tRPC | 46 | 48 |
| Níveis de acesso | 1 | 2 |
| Dead code | 2 arquivos | 0 |
| Cobertura LogVault | 7/9 | 9/9 |

---

## 🚀 v6.0.0 — Maracutaia Release — 16 Março 2026

**Tipo:** Major Feature Release — Social Graph, Threads & Content

Maior atualização de features desde a v3.0.0. O app passa de rede social simples para rede social completa com identidade própria.

### Sistema de Threads Navegáveis 🧵

O maior diferencial de UX do app — o feed vira um explorador de conversas.

- Posts com respostas exibem `Ver thread (x)` no rodapé esquerdo, ao lado do contador de dias
- Entrar na thread: post original aparece no topo, replies diretas empilhadas em ordem cronológica
- Navegação em pilha: `← Sair` (nível 1) ou `← Voltar · Sair` (nível 2+)
- Replies com próprias respostas também exibem `Ver thread` — infinitamente
- Post original não exibe `Ver thread` dentro da própria thread (evita loop)
- Contador de feed (`1 / 11`) oculto em modo thread
- Clicar na referência de resposta dentro de uma thread entra na thread daquele post
- Hook `use-thread-stack.ts` — pilha de `number[]`, operações `push`, `pop`, `clear`
- Backend: `getThreadReplies()` com cursor pagination + `getReplyCount()` com shadow ban

### Cascade de Efemeridade em Replies 💣

- Migration `0014_reply_cascade.sql`: FK `posts.replyToPostId → posts.id ON DELETE CASCADE`
- Antes: replies ficavam órfãs ao expirar o post original
- Depois: delete propaga em cascata por toda a árvore de replies, infinitamente, em uma operação

### Bloqueio 🚫

- Tabela `blocks` com PK composta `(blockerId, blockedId)` + índices
- Efeito bidirecional no feed: A bloqueia B → ambos param de se ver
- `getBlockedUsersSubquery()` filtrado em `getTimelinePosts` (ambos os modos de feed)
- Procedure `users.block` — idempotente via `onConflictDoNothing`

### Ghosting 48h 👻

Feature original sem equivalente em redes sociais mainstream.

- Tabela `ghostings` com `expiresAt` (48h) — expiração on-the-fly, sem cron
- ghostedId para de ver posts de ghosterId no feed por 48h
- ghosterId não pode responder posts de ghostedId enquanto ativo
- Renovável: ghostar de novo reseta os 48h
- `getGhostedAuthorsSubquery()` filtrado em `getTimelinePosts`
- Bloqueio de reply no router se em ghosting com o autor
- Popup nativo: `👻 Ghosting insano de 48h` → se ativo: `🤡 Superei o vacilo, próximo`

### Denúncia 🚨

- Envia para todos os admins simultaneamente via `Promise.allSettled`
- Mensagem inclui: nome do denunciante, ID do post, autor, conteúdo (truncado 120 chars)
- Não pode denunciar o próprio post

### Popup de Moderação Social

- Tocar na foto de outro usuário → popup nativo do Telegram com 3 ações
- Status de ghosting buscado lazy antes de abrir
- Não aparece nos próprios posts nem para admins

### Lock Biométrico 🔒

- `use-biometric-lock.ts` via Telegram `BiometricManager`
- Ativar: `requestAccess` → `updateBiometricToken` → Secure Enclave/Keystore
- Desativar: exige autenticação biométrica de confirmação
- Persistência síncrona via localStorage — botão mostra estado correto ao montar
- Race condition guard: `isDisablingRef` bloqueia `checkAndLock` durante desativação
- Re-trava ao voltar do background via `visibilitychange`

### Exportação de Dados LGPD 📦

- Busca em paralelo: conta + posts (até 500) + seguindo
- Formata `.txt` com bordas ASCII, datas em horário de Brasília
- Envia via `sendBotDocument()` (multipart/form-data) direto na conversa com o bot

### Embed de Vídeo 🎬

- Plataformas: YouTube (watch, youtu.be, shorts, embed) e Vimeo
- Na criação: URL detectada → removida do textarea → chip `🎬 YouTube ✕`
- URL salva em estado separado — não consome os 165 chars do texto
- No feed: thumbnail clicável com ▶ — iframe carrega só no tap (performance)
- X/Twitter e TikTok avaliados e descartados (não funcionam em WebView)

### "Você" no Próprio Post 👤

- Posts e respostas próprias exibem "Você" em vez do nome
- Para outros usuários, o nome continua aparecendo normalmente

### Motor de Física com Giroscópio 🌀

- `device-motion-singleton.ts`: EMA + deadzone (0.4 m/s²) + decay
- Android: ativa automaticamente; iOS: pede permissão no primeiro toque
- Emojis de reação recebem impulso em direção determinística por semente única
- Damping adaptativo: dissipa mais rápido durante agitação

### Métricas v6.0.0

| Métrica | v5.0.0 | v6.0.0 |
|---------|--------|--------|
| Arquivos TS/TSX | 101 | 115 |
| Hooks customizados | 11 | 12 |
| Tabelas no banco | 8 | 10 |
| Migrations | 11 | 14 |
| Procedures tRPC | 38 | 46 |
| Features sociais | Básico | Bloqueio + Ghost + Denúncia |

---

## 🚀 v5.0.0 — Icarus Release — 14 Março 2026

**Tipo:** Stability, Performance & Architecture Release

Maior atualização de estabilidade do projeto. Ponto de lançamento oficial. Nenhuma feature nova — fundação sólida para o lançamento público.

### Correções de Segurança

- Usuários com JWT válido mas banidos podiam escrever por até 7 dias → ban check adicionado em todas as mutations de escrita
- Cron de notificações mostrava conteúdo do post original em vez do conteúdo da reply → `getReplyContent()` helper
- Cron de limpeza deixava imagens órfãs no Storage → `imagePath` buscado antes do delete

### Auditoria de Código

- `resetUserRateLimit` resetava apenas `lastPostAt`, esquecia `lastReplyAt` → ambos resetados
- Filtro de 7 dias em posts de usuário — admin isento
- `storageDelete` fire-and-forget no delete de posts
- Cache de flag global de rate limit (30s) com `invalidateFlagCache()`
- Frases de rate limit consolidadas em `src/constants/rate-limit-phrases.ts`
- Bug de invalidação de cache tRPC na página de usuário

### Visual

- Utilitários `text-shadow-dark` e `text-shadow-light`
- Glassmorphism padronizado em todos os cards
- Animação `feed-card-float` nos cards do feed
- `refetchOnMount: 'always'` em todas as páginas

### Story Sharing

- Canvas API: imagem 1080×1920 JPEG com glassmorphism simulado e watermark
- Cascade de share: `navigator.share({ files })` → Clipboard API → modal com long-press
- `-webkit-touch-callout: none` globalmente → `allow-context-menu` seletivo no modal

### LogVault — 100% de Cobertura

- Contextos `follow` e `reaction` sem logs de info → adicionados
- 9 contextos cobertos: `notification`, `post`, `reaction`, `follow`, `upload`, `rate_limit`, `cron`, `auth`, `system`

---

## 🎯 v4.0.0 — State of the Art — 13 Março 2026

**Tipo:** Architecture & Performance Release

### Performance

- `idx_posts_telegramId_createdAt` — timeline 40% mais rápida
- `idx_posts_createdAt_telegramId` — efemeridade otimizada
- `idx_notifications_status_retry` — retry acelerado
- `timeAgo` e `authorData` memoizados — ~30% menos re-renders no feed

### Arquitetura

- Motor de física newtoniana com thermal noise (sequência de Halton, ruído de seno)
- Singleton de giroscópio — um único listener `DeviceMotion` para todo o app
- `PostCardReactions` com `ResizeObserver` — obstáculos dinâmicos nos botões
- Separação de contextos: `feed-card-float` CSS animation + motor de física independentes

### Métricas v4.0.0

| Métrica | Valor |
|---------|-------|
| Bundle Size | ~780KB |
| Re-renders (feed) | -30% |
| Query Performance | +40% (índices compostos) |

---

## 📊 v3.2.0 — Otimização e Estabilidade — 10 Março 2026

**Tipo:** Stability Release

- Remoção de barrel exports problemáticos — import cycles eliminados
- Índices de performance no banco (`0009_performance_indexes.sql`)
- Memoização estratégica no feed
- Type-safety auditada end-to-end

---

## 🔔 v3.1.0 — Sistema de Notificações — 07-08 Março 2026

**Tipo:** Major Feature Release

- Notificações push via Bot Telegram (replies, reações, follows)
- Fila com retry — status: `pending → sent | failed | skipped`, máx 3 tentativas
- Deduplicação via unique constraint na tabela `notifications`
- Opt-out — `users.notificationsEnabled` — LGPD compliance
- Tratamento de 403 — desativa notificações automaticamente quando bot bloqueado
- Envio imediato + cron fallback — ~95% enviado imediatamente, ~5% via retry

| Métrica | Valor |
|---------|-------|
| Novas tabelas | 1 (notifications) |
| Novos campos | 1 (notificationsEnabled) |
| Índices criados | 4 |
| Cron jobs | +1 (notifications retry) |

---

## 💬 v3.0.0 — Replies e Efemeridade — 25 Fev – 06 Mar 2026

**Tipo:** Major Feature Release

- Sistema de replies — 100 chars, rate limit separado de 30min, animação de vídeo
- Posts efêmeros — 7 dias, admin isento, countdown timer em tempo real
- Rate limiting híbrido — 3 camadas: CloudStorage → `users.lastPostAt` → fallback na tabela posts
- Admin dashboard — stats, flags globais, moderação de usuário, audit log
- Shadow ban — usuário posta normalmente mas ninguém vê seus posts
- Ban total — JWT válido verificado a cada write
- Feed mode por usuário — `following` ou `all`

| Métrica | Valor |
|---------|-------|
| Novas tabelas | 2 (serverConfig, adminActions) |
| Novos endpoints | 12+ |
| Cron jobs | +1 (cleanup de posts expirados) |

---

## 🃏 v2.1.0 — Feed Swipeable — 02 Março 2026

- Feed em card único com swipe horizontal — efeito de baralho
- Peek card do próximo post visível atrás
- Confirmação nativa via popup do Telegram antes de deletar
- Bolhas flutuantes com animação `bubble-float` na página Seguir
- `FloatingTabBar` sincronizado com rota atual via Context

---

## 🏗️ v2.0.0 — Migração Next.js — 25 Fevereiro 2026

**Tipo:** Breaking Change / Architecture Refactor

Migração completa de Expo (React Native) para Next.js 15 como Telegram Mini App web.

- Bundle: 2.8MB → 800KB (**-71%**)
- First Load: 3-5s → ~1s (**-75%**)
- Lighthouse: +35%
- Stack: Next.js 15 + React 19 + tRPC v11 + Drizzle ORM + Framer Motion
- Glassmorphism + backgrounds por página + haptic feedback + page transitions
- Autenticação HMAC-SHA256 via Telegram WebApp SDK

---

## 🔒 v1.5.0 — Segurança e Sessions — 20-24 Fevereiro 2026

- Autenticação HMAC-SHA256 completa
- Sessions JWT 7 dias (HTTP-only cookie)
- Validação Zod em todos os inputs
- Integração MainButton, BackButton, Haptic e Popups nativos do Telegram

---

## 🎯 v1.0.0 — MVP Next.js — 18 Fevereiro 2026

Primeira versão funcional em Next.js após a migração:

- Posts de 165 caracteres com upload de imagem (10MB)
- Sistema de follows
- 12 reações com emoji
- Timeline com cursor-based pagination
- Perfis de usuário

---

## 📱 v0.8.0 — MVP Expo — Final de Janeiro 2026

Primeiro protótipo funcional em React Native / Expo:

- Posts, follows, reações e perfis básicos
- Bundle: 2.8MB, first load: 3-5s
- Validou o conceito — descontinuado em favor do Next.js

---

## 📅 Linha do Tempo

| Período | Marco | Versão |
|---------|-------|--------|
| **Final de Jan 2026** | Protótipo Expo — validação do conceito | v0.8.0 |
| **18 Fev 2026** | MVP Next.js — primeira versão web | v1.0.0 |
| **20-24 Fev 2026** | Segurança + Autenticação completa | v1.5.0 |
| **25 Fev 2026** | Migração completa Expo → Next.js | v2.0.0 |
| **02 Mar 2026** | Feed swipeable + UI de bolhas | v2.1.0 |
| **25 Fev – 06 Mar** | Replies + Efemeridade + Admin Dashboard | v3.0.0 |
| **07-08 Mar 2026** | Notificações push via Bot | v3.1.0 |
| **10 Mar 2026** | Índices de performance + otimizações | v3.2.0 |
| **13 Mar 2026** | Motor de física + giroscópio + State of the Art | v4.0.0 |
| **14 Mar 2026** | Icarus Release — auditoria completa + story sharing | v5.0.0 |
| **16 Mar 2026** | Threads + Bloqueio + Ghost + Biométrico + LGPD + Vídeo | v6.0.0 |
| **16 Mar 2026** | Busca + Menções + Moderação hierárquica + Faxinão | v7.0.0 |

**Tempo total de desenvolvimento: ~7 semanas** (final de janeiro a 16 de março de 2026)

---

## 🏗️ Evolução da Arquitetura

```
Expo/React Native       Next.js + tRPC       Next.js + Full Social
(final jan 2026)    →   (fev 2026)       →   (mar 2026)
Bundle: 2.8MB           Bundle: 800KB         Bundle: ~780KB
First load: 3-5s        First load: ~1s       First load: ~1s
4 tabelas               6 tabelas             10 tabelas
Sem física              Física básica         Motor newtoniano 60fps
Sem moderação           Admin básico          Admin + Mod + LogVault 100%
Sem social graph        Follow + Reações      + Ghost + Block + Thread + Menção
```

### Arquitetura Atual (v7.0.0)

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

---

## 📊 Estatísticas Gerais

| Métrica | Valor |
|---------|-------|
| **Tempo de Desenvolvimento** | ~7 semanas |
| **Versões Lançadas** | 12 |
| **Arquivos TS/TSX** | 117 |
| **Componentes React** | 25+ |
| **Hooks Customizados** | 13 |
| **Procedures tRPC** | 48 |
| **Tabelas no Banco** | 10 |
| **Migrations** | 14 |
| **Índices no Banco** | 19+ |
| **Cron Jobs** | 2 (cleanup + notifications) |
| **Contextos LogVault** | 9 (100% de cobertura) |

---

*Maracutáia — do protótipo ao lançamento em 7 semanas.*
