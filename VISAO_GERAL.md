# 🎭 Maracutáia - Visão Geral Completa

**Documento Único que Explica Tudo (Mas Bem Por Cima)** 👁️

**Versão:** 4.0.0  
**Data:** 12 de Março de 2026  
**Status:** ✅ Produção

---

## 1. O CONCEITO

### 1.1 A Ideia Central

**Maracutáia** é uma rede social de **fofocas efêmeras** que roda dentro do Telegram.

**Filosofia:**
- Postou? **20 minutos de castigo** (rate limit)
- Respondeu? **30 minutos de reflexão**
- Fofocou? **Se defenda** (se conseguir)
- **Tudo é feature** 


### 1.2 A Tia Górgona 👁️🐍

A **Tia Górgona** é a "mascote" e guardiã da plataforma.

**Ela representa:**
- 👁️ **Vigilância** - Ela vê tudo
- 🐍 **Sabedoria** - Ela sabe tudo
- ⏰ **Paciência** - Ela te faz esperar
- 🎭 **Deboche** - Ela não perdoa

### 1.3 Slow Social

**Slow Social** é a filosofia de design intencional:

- ✅ **Animações são feature** - Não são bugs, são planejadas
- ✅ **Loadings são feature** - Para você respirar e apreciar as artes de fundo
- ✅ **Rate limits são feature** - Para você pensar
- ✅ **Efemeridade é feature** - Para você valorizar
- ✅ **É um exercício de paciência divertido**
- ✅ **Feed Global** - aos domingos, se a tia Górgona estiver de bom humor

**Contra o que lutamos:**
- ❌ Scroll infinito (vício) - um post de cada vez
- ❌ Resposta imediata (ansiedade) - Pense para responder
- ❌ Posts eternos (cringe) - Desapega!
- ❌ Algoritmos (manipulação) - Aqui não, feed cronologico de seus seguidos


---

## 2. COMO FUNCIONA

### 2.1 Acesso

**Onde:**
- Telegram Mini App (roda dentro do Telegram)
- URL: [vempramaracutuaiabot](https://t.me/vempramaracutuaiabot)

**Como:**
1. Abra o Telegram
2. Busque @vempramaracutuaiabot
3. Clique em "Abrir"
4. Pronto!

**Autenticação:**
- Usa seu Telegram ID automaticamente
- Sem senha, sem email, sem OAuth
- Validação criptográfica (HMAC-SHA256)

### 2.2 Posts

**O que é:**
- Microblog de fofocas
- Limite: **165 caracteres**
- Imagem: **Opcional** (até 12MB)

**Como funciona:**
1. Clica em "Criar Post"
2. Escreve sua fofoca
3. Adiciona imagem (opcional)
4. Publica
5. **Castigo:** 20 minutos até poder postar de novo

**Efemeridade:**
- Posts expiram em **7 dias**
- Admin posts são eternos (eles que mandam)
- Countdown mostra tempo restante

### 2.3 Respostas

**O que é:**
- Responder posts de outros usuários
- Limite: **100 caracteres**

**Como funciona:**
1. Clica no ícone de responder
2. Escreve sua resposta
3. Envia
4. **Reflexão:** 30 minutos até responder de novo

**Notificação:**
- Autor do post original é notificado (se não for você mesmo)
- Via Bot Telegram (push notification)

### 2.4 Reações

**O que é:**
- 12 emojis para reagir
- Grid 6×2 (6 em cima, 6 embaixo)

**Emojis:**
👍 🖕 😂 😱 💀 🔥 ❤️ 😍 🤔 🍪 🐍 🐮

**Como funciona:**
1. Clica em reagir
2. Escolhe emoji
3. Reage
4. Contador atualiza

### 2.5 Follow

**O que é:**
- Seguir usuários que você gosta
- Timeline mostra posts de quem segue em ordem cronológica

**Como funciona:**
1. Vai na página "Seguir"
2. Busca usuários
3. Clica em seguir
4. Notificação enviada (se não for você mesmo)

**Feed Modes:**
- **Following:** Vê posts de quem segue
- **All:** Vê posts de todos (Se a tia liberar)

### 2.6 Timeline

**O que é:**
- Feed de posts
- Baralho cronológico (id DESC)

**Como funciona:**
1. Abre o app
2. Timeline carrega
3. Swipe para navegar
4. Contador mostra posição (X / N)

**Paginação:**
- Cursor-based (id DESC)
- Carrega mais quando chega perto do fim
- 20 posts por página

### 2.7 Notificações

**O que é:**
- Push notifications via Bot Telegram
- 3 tipos: reply, reaction, follow

**Tipos:**
- **Reply:** "💬 João respondeu sua fofoca..."
- **Reaction:** "🔥 Maria reagiu na sua fofoca..."
- **Follow:** "👀 Pedro veio bisbilhotar sua vida..."

**Controle:**
- Opt-out disponível (toggle no perfil)
- Se bloquear o bot → notificações desativadas automaticamente

---

## 3. ARQUITETURA (BEM POR CIMA)

### 3.1 Visão Geral

```
┌─────────────────┐
│   Telegram      │
│   WebApp SDK    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Frontend      │
│   Next.js 15    │
│   React 19      │
└────────┬────────┘
         │
         │ tRPC
         ▼
┌─────────────────┐
│   Backend       │
│   API Routes    │
│   Serverless    │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐  ┌────────┐
│   DB   │  │Storage │
│Postgres│  │S3-like │
└────────┘  └────────┘
```

### 3.2 Camadas

**Camada 1: Frontend**
- Next.js 15 (App Router)
- React 19
- TypeScript 5.9.3
- Tailwind CSS 3.4.17
- Framer Motion (animações)

**Camada 2: API**
- tRPC v11 (type-safe)
- Next.js API Routes
- Serverless (Vercel)
- Zod (validação)

**Camada 3: Dados**
- PostgreSQL 15+ (Supabase)
- Drizzle ORM 0.44.0
- Supabase Storage (imagens)

**Camada 4: Auth**
- Telegram WebApp SDK
- JWT sessions (7 dias)
- HMAC-SHA256 validation

### 3.3 Fluxo de Dados

1. Usuário abre app → Telegram SDK inicializa
2. Frontend captura initData
3. Envia para backend (Authorization header)
4. Backend valida (HMAC-SHA256)
5. Cria JWT session (7 dias)
6. Contexto populado (telegramId, isAdmin)
7. Procedure tRPC executa
8. Database query
9. Resposta retorna
10. Frontend renderiza

---

## 4. FUNCIONALIDADES (DETALHES POR CIMA)

### 4.1 Rate Limiting

**O que é:**
- Sistema de "castigo" entre ações
- 3 camadas de verificação

**Intervalos:**
- Posts: 20 minutos
- Respostas: 30 minutos
- Admin: Bypassa tudo

**Camadas:**
1. **Local** (CloudStorage + localStorage)
2. **Banco** (users.lastPostAt)
3. **Fallback** (tabela posts)

**Regra:** Mais restritivo vence.

### 4.2 Efemeridade

**O que é:**
- Posts expiram automaticamente
- Admin posts são eternos

**Como:**
- Cron job diário (3h UTC)
- Deleta posts > 7 dias
- Deleta reactions associadas
- Replies deletadas via CASCADE

**Countdown:**
- Mostra tempo restante
- Atualiza a cada minuto
- Só aparece nas últimas 24h

### 4.3 Moderação

**O que é:**
- Sistema para controlar conteúdo
- Admin dashboard completo

**Ferramentas:**
- **Ban:** Usuário não pode logar
- **Shadow Ban:** Usuário posta mas ninguém vê
- **Delete Post:** Remove qualquer post
- **Reset Rate Limit:** Permite postar imediatamente
- **Set Feed Mode:** Altera modo do feed

**Auditoria:**
- Todas ações registradas
- Histórico consultável
- Previous value / New value

### 4.4 Notificações

**O que é:**
- Push notifications via Bot
- 3 tipos de evento

**Fluxo:**
1. Evento ocorre (reply/reaction/follow)
2. Insert no DB (status: pending)
3. Busca recipient + actor (Promise.all)
4. Envia via Bot API (imediato)
5. Atualiza status (sent/failed/skipped)
6. Cron retry (se failed, máx 3 tentativas)

**Métricas:**
- ~95% envio imediato
- ~5% retry via cron
- Cron: 12x/dia (12h UTC)

---

## 5. TECNOLOGIAS (RESUMO)

### 5.1 Stack Completo

| Categoria | Tecnologia | Versão |
|-----------|-----------|--------|
| Framework | Next.js | 15.1.0 |
| UI Library | React | 19.0.0 |
| Linguagem | TypeScript | 5.9.3 |
| Estilização | Tailwind CSS | 3.4.17 |
| API | tRPC | 11.0.0 |
| Estado | TanStack Query | 5.90.0 |
| ORM | Drizzle ORM | 0.44.0 |
| Database | PostgreSQL | 15+ |
| Storage | Supabase Storage | - |
| Auth | Telegram WebApp | - |
| Sessions | jose (JWT) | 5.9.0 |
| Validação | Zod | 3.24.0 |
| Animações | Framer Motion | 11.11.0 |
| Ícones | Lucide React | 0.460.0 |
| Deploy | Vercel | - |

### 5.2 Por Que Cada Uma?

**Next.js 15:**
- App Router (novo padrão)
- Server Components
- API Routes integradas
- Deploy automático na Vercel

**React 19:**
- Actions (mutations nativas)
- use() hook (promises em components)
- Melhor SSR

**TypeScript:**
- Type-safety end-to-end
- Inferência automática com tRPC
- Zero erros em produção

**tRPC:**
- Type-safety sem codegen
- Bundle menor que GraphQL
- DX excelente (autocomplete)

**Drizzle ORM:**
- Leve e type-safe
- SQL-like queries
- Migrations portáteis

**Telegram WebApp SDK:**
- Autenticação nativa
- Sem OAuth complexo
- 900M+ usuários potenciais

---

## 6. MÉTRICAS (NÚMEROS REAIS)

### 6.1 Código

| Métrica | Valor |
|---------|-------|
| **Versão** | 4.0.0 |
| **Commits** | 270+ |
| **Arquivos** | 75+ |
| **Linhas de Código** | ~7.805 |
| **Componentes React** | 15 |
| **Procedures tRPC** | 38 |
| **Tabelas no Banco** | 7 |
| **Índices** | 19+ |
| **Features** | 90+ |

### 6.2 Performance

| Métrica | Valor | Benchmark |
|---------|-------|-----------|
| **Bundle Size** | 203 KB | Excelente (< 1MB) |
| **Build Time** | 15.8s | Excelente (< 20s) |
| **First Load** | ~1s | Excelente (< 2s) |
| **Lighthouse** | 90+ | Excelente (90-100) |
| **API Response** | < 200ms | Excelente |
| **Database Queries** | < 50ms | Excelente |
| **Animação** | 60fps | Excelente |

### 6.3 Documentação

| Tipo | Linhas | Localização |
|------|--------|-------------|
| **Interna Completa** | ~28.000+ | /docs/*.md (9 docs) |
| **Pública Sanitizada** | ~9.000+ | /docs/Sanitizados/*.md (11 docs) |
| **CHANGELOG** | ~650 | /CHANGELOG-COMPLETO.md |
| **VISAO_GERAL (este)** | ~800 | /VISAO_GERAL.md |
| **README** | ~400 | /README.md |

**TOTAL:** ~38.850+ linhas de documentação

---

## 7. SEGURANÇA (RESUMO)

### 7.1 Autenticação

**Como funciona:**
- Telegram WebApp initData
- Validação HMAC-SHA256
- JWT sessions (7 dias)
- Cookie HTTP-only

**Segurança:**
- Fallback legacy removido
- Verificação de expiração (5 minutos)
- Validação de ownership
- Ban check antes de upsert

### 7.2 Rate Limiting

**Proteção:**
- 3 camadas de verificação
- Admin bypassa
- Flag global para desativar
- Cache de flag (30s TTL)

### 7.3 Moderação

**Ferramentas:**
- Ban total (não pode logar)
- Shadow ban (posta mas ninguém vê)
- Delete post (admin only)
- Audit log (todas ações registradas)

### 7.4 LGPD

**Compliance:**
- Opt-out de notificações
- Dados mínimos necessários
- Posts efêmeros (auto-destrutivo)
- Transparência (documentação pública)

---

## 8. DEPLOY E INFRA (VISÃO GERAL)

### 8.1 Onde Roda

**Vercel:**
- Serverless Functions
- Auto-scaling
- CDN global
- CI/CD automático

**Supabase:**
- PostgreSQL 15+
- Storage (S3-compatible)
- RLS policies
- 1GB free tier

### 8.2 Cron Jobs

**Cleanup (3h UTC):**
- Deleta posts > 7 dias
- Admin posts isentos
- Deleta reactions manualmente
- Limpa storage (fire-and-forget)

**Notifications (12h UTC):**
- Retry notificações falhas
- Máx 3 tentativas
- ~5% das notificações
- 12x/dia (plano Hobby)

### 8.3 Custos

**Free Tier:**
- Vercel Hobby: 100GB bandwidth/mês
- Supabase Free: 500MB, 50K requests/dia
- Telegram Bot API: Ilimitado
- **Total:** $0/mês (até 10K usuários)

**Scale (10K-50K):**
- Vercel Pro: $20/mês
- Supabase Pro: $25/mês
- **Total:** ~$45/mês

---

## 9. ROADMAP (ONDE ESTAMOS)

### 9.1 Concluído (v4.0.0)

- ✅ Migração Expo → Next.js
- ✅ Sistema de replies
- ✅ Posts efêmeros (7 dias)
- ✅ Notificações via Bot
- ✅ Admin dashboard
- ✅ Rate limiting híbrido
- ✅ Otimização de performance
- ✅ Documentação completa (~38.850+ linhas)

### 9.2 Futuro (Planejamento)

- 📋 Denúncia de conteúdo (community moderation)
- 📋 Multi-language support (i18n)
- 📋 Melhorias contínuas de performance

---

## 10. DOCUMENTAÇÃO (ONDE ENCONTRAR)

### 10.1 Privada, Completa (~38.000+ linhas)

---

## 11. PERGUNTAS FREQUENTES (FAQ)

### 11.1 "Por que 20 minutos de rate limit?"

**Resposta:** Slow social é feature. Para você pensar antes de postar.

### 11.2 "Por que 7 dias de efemeridade?"

**Resposta:** Fofoca é efêmera. Como a vida real.

### 11.3 "Admin pode tudo?"

**Resposta:** Sim. Tia Górgona quem manda.

### 11.4 "Posso baixar os dados?"

**Resposta:** Não tem essa feature (ainda). LGPD compliance via opt-out.

### 11.5 "É open-source?"

**Resposta:** Não. É privado.

### 11.6 "Posso contribuir?"

**Resposta:** Reporte bugs e sugira features. Código: só com permissão.

### 11.7 "Quanto custa?"

**Resposta:** $0/mês até 10K usuários. ~$45/mês para 10K-50K.

### 11.8 "Como ganha dinheiro?"

**Resposta:** Não ganha. É projeto pessoal

---

## 12. GLOSSÁRIO (TERMOS)

| Termo | Significado |
|-------|-----------|
| **Tia Górgona** | Mascote/guardiã da plataforma |
| **Castigo** | Rate limit de 20 minutos |
| **Reflexão** | Rate limit de 30 minutos |
| **Slow Social** | Filosofia de design intencional |
| **Shadow Ban** | Usuário posta mas ninguém vê | 
| **Feed Mode** | 'following' ou 'all' |
| **Cursor Pagination** | Paginação por id DESC |
| **Optimistic Update** | UI atualiza antes da confirmação |
| **Fire-and-Forget** | Async sem await |
| **Deduplicação** | Unique constraint no DB |

---

## 13. CONCLUSÃO

### 13.1 O Que É Maracutáia?

Uma rede social de **fofocas efêmeras** com **slow social intencional**, onde a **Tia Górgona te vigia** e você fica de **castigo** se postar demais.

### 13.2 Por Que Existe?

Para ser **diferente** das outras redes sociais:
- ❌ Sem scroll infinito
- ❌ Sem resposta imediata
- ❌ Sem posts eternos
- ❌ Sem algoritmos

### 13.3 Qual o Diferencial?

**Personalidade:**
- 👁️ Tia Górgona
- 🐍 Muito deboche
- ⏰ Castigo e reflexão
- 🎭 Tudo é feature

**Tecnologia:**
- ✅ Next.js 15 + React 19 + tRPC v11
- ✅ Type-safety end-to-end
- ✅ ~38.850+ linhas de documentação
- ✅ Produção pronta (v4.0.0)

---

## 📈 MÉTRICAS E PERFORMANCE

### Performance Técnica (v4.0.0)

| Métrica | Valor | Benchmark | Status | Detalhe |
|---------|-------|-----------|--------|---------|
| **Bundle Size** | ~203 KB | Excelente (< 1MB) | ✅ Atingido | -36% vs anterior |
| **Build Time** | 15.8s | Excelente (< 20s) | ✅ Atingido | 22-25s → 15.8s (-36%) |
| **First Load** | ~1s | Excelente (< 2s) | ✅ Atingido | Next.js optimization |
| **First Load JS** | 102 KB | Excelente | ✅ Atingido | Code splitting |
| **Lighthouse Score** | 90+ | Excelente (90-100) | ✅ Atingido | Performance, SEO, accessibility |
| **API Response Time** | < 200ms | Excelente | ✅ Atingido | tRPC + Supabase |
| **Database Queries** | < 50ms | Excelente | ✅ Atingido | 19+ índices, cursor pagination |
| **Page Transition** | 250ms | Excelente | ✅ Atingido | Fade + slide, cubic-bezier |
| **Notificações (imediato)** | ~95% | Excelente | ✅ Atingido | Bot API + cron fallback |
| **Cron Success Rate** | > 95% | Excelente | ✅ Atingido | Retry mechanism |
| **Animações Otimizadas** | 60 fps (3.74s) | Excelente | ✅ Atingido | Animação fluida |

### Métricas do Código (ATUALIZADO v4.0.0)

| Categoria | Métrica | Valor | Detalhe |
|-----------|---------|-------|---------|
| **Histórico** | Commits | 270+ | Desde v1.0.0 |
| **Código** | Arquivos de Código | 75+ | Backend + Frontend |
| **Código** | Linhas de Código | ~7.805 | TypeScript + CSS (otimizado) |
| **API** | Procedures tRPC | 35+ | 8 routers |
| **Database** | Tabelas | 7 | usuario, publicação, seguir, emojis, servidor, admin, notificacao |
| **Database** | Índices | 19+ | Performance optimization |
| **Frontend** | Componentes React | 15 | Pages + Components |
| **Features** | Implementadas | 90+ | Core + UX + Notificações + Mecanismos |
| **Infra** | Cron Jobs | 2 | Cleanup (3h UTC) + Notifications (12h UTC) |
| **Infra** | Variáveis Ambiente | 12+ | Configurações do sistema |

### Melhorias v4.0.0

| Tipo | Mudança | Impacto |
|------|---------|---------|
| **REMOVED** | Limpeza de código | -2.5% bundle size |
| **OTIMIZADO** | 3 callbacks removidos | -30% re-renders |
| **OTIMIZADO** | Build time (22-25s → 15.8s) | -36% mais rápido |
| **OTIMIZADO** | Reações com layout compacto | UX melhorada |
| **OTIMIZADO** | Identidade visual consolidada | Visual premium |
| **CORRIGIDO** | Fonte do conteúdo (text-base → text-sm) | Legibilidade |
| **OTIMIZADO** | Refatoração db em .repositories | Melhoria massiva, otimização de querys e leitura de dados |
| **OTIMIZADO** | Refatoração routes em .routers | Rotas divididas, procedures estaveís, responsabilidades bem definidas |
| **OTIMIZADO** | Refatoração postcard em .components | Modularização para manutenção e ganho de desempenho |

### Comparativo: Expo (Anterior) vs Next.js (Atual)

| Métrica | Expo | Next.js | Melhoria |
|---------|------|---------|----------|
| Bundle Size | 2.8MB | 203KB | **93% menor** ⬇️ |
| First Load | 3-5s | ~1s | **75% mais rápido** ⬇️ |
| Lighthouse | 65-75 | 90+ | **+35% melhor** ⬆️ |
| Build Time | 22-25s | 15.8s | **-36% mais rápido** ⬇️ |
| Linhas de Código | ~9.500+ | ~7.805 | **-18% (otimizado)** ⬇️ |
| Componentes | 18+ | 15 | **-3 (otimizado)** ⬇️ |

---


## 👁️🐍

*"Na Maracutáia, a Tia Górgona vê tudo. E ela não perdoa, ela debocha."*

**https://t.me/vempramaracutuaiabot**

---


