# 🎭 Maracutáia

**Uma rede social de fofocas efêmeras onde a Tia Górgona te vigia.** 👁️🐍

[![Status](https://img.shields.io/badge/status-produção-green)](https://t.me/vempramaracutuaiabot)
[![Versão](https://img.shields.io/badge/versão-4.0.0-blue)](https://t.me/vempramaracutuaiabot)
[![Telegram](https://img.shields.io/badge/platform-Telegram-blue)](https://t.me/vempramaracutuaiabot)

---

## 👁️ A Filosofia

> **Postou? A Tia Górgona apareceu.**
> 
> Você fica **20 minutos de castigo**.
> 
> Quer se defender? **30 minutos**.
> 
> Muito deboche e **slow social**: animações e loadings são planejados.
> 
> Aprecie as imagens. Respire entre as ações.
> 
> **Tudo é feature.**

---

## 🐍 O Que É

Maracutáia é um **Telegram Mini App** - uma rede social de microblogging onde:

- ✅ **Fofocas efêmeras** - Posts duram 7 dias (como a vida real)
- ✅ **Slow social intencional** - Rate limits de 20-30 minutos
- ✅ **Sem algoritmo** - Você escolhe quem seguir
- ✅ **Sem app pra baixar** - Roda nativamente no Telegram
- ✅ **Notificações push** - Via Bot Telegram
- ✅ **Moderação** - Shadow ban, admin dashboard, auditoria (Tia Górgona)

---

## ⚡ Como Funciona

### 1. Acesse
Abra o Telegram → Busque Maracutáia → Clique em "Iniciar"

### 2. Postou?
- Escreva sua fofoca (165 caracteres)
- Adicione imagem (opcional, 12MB)
- Publique!
- **Castigo:** 20 minutos até poder postar de novo

### 3. Respondeu?
- Responda posts de outros
- **Reflexão:** 30 minutos até responder de novo

### 4. Seguiu?
- Siga quem você gosta
- Timeline mostra posts de quem segue
- Ou veja posts de todos (se quiser)

### 5. Reagiu?
- 12 emojis disponíveis
- Grid 6×2 para fácil acesso
- Contador de reações

### 6. Expirou?
- Posts somem após 7 dias
- Admin posts são eternos (eles que mandam)
- Countdown mostra tempo restante

---

## 🎯 Funcionalidades

| Feature | Descrição | Limite |
|---------|-----------|--------|
| **Posts** | Microblog de fofocas | 165 chars |
| **Respostas** | Responda posts | 100 chars |
| **Imagens** | Upload opcional | 12MB |
| **Reações** | 12 emojis | Grid 6×2 |
| **Follow** | Siga usuários | Ilimitado |
| **Timeline** | Feed personalizado | Cursor pagination |
| **Notificações** | Push via Bot | Opt-out disponível |
| **Efemeridade** | Expiração automática | 7 dias |
| **Rate Limit** | Slow social | 20-30 min |
| **Moderação** | Shadow ban, ban | Admin dashboard |

---

## 🛠️ Stack Tecnológico

| Camada | Tecnologia |
|--------|-----------|
| **Frontend** | Next.js 15, React 19, TypeScript, Tailwind CSS |
| **API** | tRPC v11 (type-safe end-to-end) |
| **Estado** | TanStack Query |
| **Backend** | Next.js API Routes (Serverless) |
| **Database** | PostgreSQL (Supabase) |
| **ORM** | Drizzle ORM |
| **Storage** | Supabase Storage |
| **Auth** | Telegram WebApp SDK (HMAC-SHA256) |
| **Animações** | Framer Motion |
| **Deploy** | Vercel (Serverless + Cron Jobs) |

---

## 📊 Métricas

| Métrica | Valor |
|---------|-------|
| **Versão** | 4.0.0 |
| **Status** | ✅ Produção |
| **Bundle Size** | 203 KB |
| **Build Time** | 15.8s |
| **First Load** | ~1s |
| **Lighthouse** | 90+ |
| **Commits** | 270+ |
| **Features** | 90+ |
| **Documentação** | ~37.000+ linhas |

---

## 🚀 Como Usar

### 1. Pelo Telegram
```
1. Abra o Telegram
2. Busque por @vempramaracutuaiabot
3. Clique em "Abrir"
4. Pronto!
```

### 2. URL Direta
```
https://t.me/vempramaracutuaiabot
```

---

## 🎨 Conceito Visual

- **Glassmorphism** - Transparências e blur (Para mistura e aproveitamento de cores das imagens de fundo)
- **Backgrounds** - Imagens de fundo coloridas por página
- **Animações 60fps** - Vídeo de publicação (3.74s)
- **Haptic Feedback** - Vibração tátil
- **Page Transitions** - Fade + slide (250ms)
- **Floating Tab Bar** - Navegação com bolha indicadora

---

## 🐍 A Tia Górgona

> *"Na Maracutáia, a Tia Górgona vê tudo. E ela não perdoa, ela debocha."*

### O Castigo
- **Postou?** 20 minutos
- **Respondeu?** 30 minutos
- **Admin?** Bypassa tudo (Tia Górgona quem manda)

### A Efemeridade
- Posts duram 7 dias
- Como a vida real: passou, era só fofoca
- Countdown mostra tempo restante

### O Slow Social
- Animações são **feature**
- Loadings são **feature**
- Respire entre as ações
- Aprecie o momento
- Aprecie as imagens (a idéia é que elas mudem de tempos em tempos, como um mural de artes)

---

## 🔒 Segurança

- ✅ **Autenticação:** Telegram WebApp SDK (HMAC-SHA256)
- ✅ **Sessions:** JWT (7 dias, HTTP-only)
- ✅ **Rate Limiting:** 3 camadas (CloudStorage, DB, fallback)
- ✅ **Moderação:** Shadow ban, ban, auditoria
- ✅ **LGPD:** Opt-out, dados mínimos, transparência

---

## 📈 Roadmap

### ✅ Concluído (v4.0.0)
- Migração Expo → Next.js
- Sistema de replies
- Posts efêmeros (7 dias)
- Notificações via Bot
- Admin dashboard
- Rate limiting híbrido
- Otimização de performance + refatoração

### 📋 Futuro
- Denúncia de conteúdo (community moderation)
- Multi-language support (i18n)
- Melhorias contínuas de performance

---

## 🤝 Contribuindo

### Como Ajudar
1. **Reporte Bugs** - Abra uma issue
2. **Sugira Features** - Compartilhe ideias
3. **Documentação** - Ajude a melhorar

### Código de Conduta
- Seja respeitoso
- Contribua de forma construtiva
- Respeite as diretrizes

---

## 📞 Suporte

- **Aplicação:** https://t.me/vempramaracutuaiabot
- **Issues:** GitHub Issues

---

## 📄 Licença

**Privado - Todos os direitos reservados**

Esta documentação é fornecida apenas para fins informativos.

---

## 🎊 Estado Atual

### ✅ Produção Pronta (v4.0.0)

- ✅ Arquitetura moderna (Next.js 15 + React 19 + tRPC v11)
- ✅ Type-safety end-to-end (TypeScript 5.9.3)
- ✅ Performance otimizada (203KB bundle, ~1s first load)
- ✅ 90+ features implementadas
- ✅ Moderação robusta (shadow ban, ban, auditoria)
- ✅ UX premium (60fps, glassmorphism, haptic)
- ✅ ~38.000+ linhas de documentação
- ✅ LGPD compliant

**Status:** 🚀 **PRODUÇÃO PRONTA**

---

## 👁️🐍


**https://t.me/vempramaracutuaiabot**

---

**Última Atualização:** 12 de Março de 2026  
**Versão:** 4.0.0 (State of the Art)
