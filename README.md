# 🎭 Maracutáia

**Uma rede social de fofocas efêmeras dentro do Telegram.**

[![Status](https://img.shields.io/badge/status-produção-green)](https://t.me/vempramaracutaiabot)
[![Versão](https://img.shields.io/badge/versão-7.0.0-blue)](https://t.me/vempramaracutaiabot)
[![Plataforma](https://img.shields.io/badge/platform-Telegram%20Mini%20App-blue)](https://t.me/vempramaracutaiabot)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)

---

## 👁️ A Filosofia

> Postou? **10 minutos de castigo.**
> Quer se defender? **15 minutos.**
> Slow social intencional. Sem algoritmo. Tudo expira.

Maracutáia é um experimento de **rede social lenta** — onde a escassez de ações cria intenção, e a efemeridade cria leveza.

---

## 🐍 O Que É

Um **Telegram Mini App** de microblogging efêmero:

- 🕰️ **Posts duram 7 dias** — depois somem, sem rastro
- ⏱️ **Slow social** — rate limits de 10-15 minutos entre ações
- 🚫 **Sem algoritmo** — você escolhe quem seguir
- 📱 **Sem app para baixar** — roda nativamente dentro do Telegram
- 🔔 **Notificações push** — via Bot Telegram
- 🧵 **Threads navegáveis** — explore conversas em pilha infinita
- 👻 **Ghosting de 48h** — pause alguém temporariamente
- 🔒 **Lock biométrico** — proteja o app com Face ID ou digital

---

## ⚡ Como Funciona

### Postou

Escreva sua fofoca (165 caracteres), adicione imagem ou vídeo (YouTube/Vimeo), publique.
Você tem **10 minutos** até poder postar de novo.

### Respondeu

Responda posts de quem você segue.
**15 minutos** de intervalo entre respostas.

### Threads

Posts com respostas exibem `Ver thread`. Clique para entrar — o feed vira uma pilha de conversas navegáveis. Volte nível por nível ou saia direto.

### Bloqueio e Ghosting

- **Bloquear** — efeito imediato e bidirecional no feed
- **Ghostar 48h** — a pessoa para de ver seus posts por 48 horas
- **Denunciar** — chega direto para os admins

### Menções

Digite `@nome` em posts ou respostas — autocomplete mostra quem você segue. A pessoa mencionada recebe notificação via bot.

### Expirou

Posts somem após 7 dias. Um countdown mostra o tempo restante.

---

## 🎯 Funcionalidades

| Feature             | Descrição                       | Limite             |
| ------------------- | ------------------------------- | ------------------ |
| **Posts**           | Microblog de texto              | 165 chars          |
| **Imagens**         | Upload opcional                 | 12MB               |
| **Vídeos**          | Embed YouTube / Vimeo           | URL no texto       |
| **Respostas**       | Reply a posts                   | 100 chars          |
| **Threads**         | Navegação em pilha infinita     | Ilimitado          |
| **Reações**         | 12 emojis com física newtoniana | Por post           |
| **Follow**          | Siga usuários                   | Ilimitado          |
| **Menções**         | @usuario com autocomplete       | Máx 3 por post     |
| **Busca**           | Encontre pessoas por nome       | Global             |
| **Bloqueio**        | Efeito bidirecional no feed     | Permanente         |
| **Ghosting**        | Pausa temporária                | 48h, renovável     |
| **Notificações**    | Push via Bot Telegram           | Opt-out disponível |
| **Efemeridade**     | Expiração automática + cascade  | 7 dias             |
| **Rate Limit**      | Slow social                     | 20-30 min          |
| **Lock Biométrico** | Face ID / Digital               | Via Telegram SDK   |
| **Exportação LGPD** | Seus dados em .txt              | Via bot            |
| **Moderação**       | Shadow ban, ban, auditoria      | Admin dashboard    |

---

## 🏗️ Stack Técnico

| Camada           | Tecnologia                                     |
| ---------------- | ---------------------------------------------- |
| **Frontend**     | Next.js 15, React 19, TypeScript, Tailwind CSS |
| **API**          | tRPC v11 (type-safe end-to-end)                |
| **Estado**       | TanStack Query                                 |
| **Backend**      | Next.js API Routes (Serverless)                |
| **Database**     | PostgreSQL via Supabase                        |
| **ORM**          | Drizzle ORM                                    |
| **Storage**      | Supabase Storage                               |
| **Autenticação** | Telegram WebApp SDK (HMAC-SHA256) + JWT        |
| **Animações**    | Framer Motion                                  |
| **Física**       | Motor próprio (RAF, DOM direto, 60fps)         |
| **Deploy**       | Vercel (Serverless + Edge + Cron Jobs)         |

---

## 🎨 Conceito Visual

- **Glassmorphism** — transparências e blur sobre backgrounds coloridos por página
- **Partículas com física** — emojis de reação flutuam com colisão, repulsão e giroscópio real
- **Animação de publicação** — vídeo 60fps (3.74s) com flash em 1.6-2.2s
- **Haptic Feedback** — vibração tátil em cada ação
- **Page Transitions** — fade + slide suave entre rotas
- **Floating Tab Bar** — navegação com indicador animado

---

## 🔒 Segurança

- ✅ **Autenticação:** HMAC-SHA256 via Telegram WebApp SDK
- ✅ **Sessions:** JWT HTTP-only (7 dias)
- ✅ **Rate Limiting:** 3 camadas (CloudStorage → DB → fallback)
- ✅ **Moderação:** Shadow ban, ban, auditoria completa
- ✅ **LGPD:** Exportação de dados, opt-out de notificações, dados mínimos
- ✅ **Cascade:** Delete em cadeia — posts, replies, reações, imagens

---

## 📊 Métricas (v7.0.0)

| Métrica                      | Valor                 |
| ---------------------------- | --------------------- |
| **Status**                   | ✅ Produção            |
| **Tempo de Desenvolvimento** | ~7 semanas            |
| **Versões Lançadas**         | 12                    |
| **Arquivos TS/TSX**          | 117                   |
| **Componentes React**        | 25+                   |
| **Hooks Customizados**       | 13                    |
| **Procedures tRPC**          | 48                    |
| **Tabelas no Banco**         | 10                    |
| **Migrations**               | 14                    |
| **Contextos LogVault**       | 9 (100% de cobertura) |

---

## 🚀 Acesso

```
Telegram → Buscar @vempramaracutaiabot → Abrir
```

Ou acesse diretamente: **https://t.me/vempramaracutaiabot**

---

## 📄 Licença

**Privado — todos os direitos reservados.**

---

**Versão:** 7.0.0 — Social Complete Release
**Última Atualização:** 16 de Março de 2026
