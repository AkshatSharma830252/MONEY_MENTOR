# AI Money Mentor

## Overview

Full-stack AI-powered personal finance platform for the Indian market. Helps users with financial planning, tax optimization, retirement planning (FIRE), and provides an AI financial advisor.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite (Tailwind CSS, shadcn/ui, Framer Motion, Recharts, React Hook Form)
- **Backend**: Express 5 API server
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **AI**: OpenAI GPT-5.2 via Replit AI Integrations (gpt-5.2)
- **Build**: esbuild (CJS bundle)

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/         # Express API server
│   └── money-mentor/       # React + Vite frontend (served at /)
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   ├── db/                 # Drizzle ORM schema + DB connection
│   ├── integrations-openai-ai-server/  # OpenAI server-side integration
│   └── integrations-openai-ai-react/   # OpenAI React client integration
├── scripts/
├── pnpm-workspace.yaml
├── tsconfig.base.json
├── tsconfig.json
└── package.json
```

## Features

### Frontend Pages (artifacts/money-mentor/)
- `/` — Landing page with product value proposition
- `/dashboard` — Financial overview with stats and toolkit navigation
- `/health-score` — 5-minute financial wellness assessment across 6 dimensions
- `/fire-planner` — FIRE (Financial Independence, Retire Early) path planner with SIP calculator
- `/tax-wizard` — Old vs New tax regime comparison with deduction optimizer
- `/life-event` — Life event financial advisor (bonus, inheritance, marriage, baby, etc.)
- `/chat` — AI chat advisor using GPT-5.2 with streaming responses

### Backend API Routes (artifacts/api-server/)
- `GET/POST /api/openai/conversations` — Conversation management
- `GET/DELETE /api/openai/conversations/:id` — Individual conversation
- `GET/POST /api/openai/conversations/:id/messages` — Message streaming (SSE)
- `POST /api/finance/health-score` — Money health score calculation
- `POST /api/finance/fire-planner` — FIRE plan generation
- `POST /api/finance/tax-wizard` — Tax regime analysis
- `POST /api/finance/life-event` — AI-powered life event advice
- `POST /api/finance/ai-advice` — General AI financial advice (SSE)

## Database Schema

- `conversations` — Chat conversation sessions
- `messages` — Individual messages within conversations

## Development Commands

- `pnpm --filter @workspace/api-server run dev` — Start API server
- `pnpm --filter @workspace/money-mentor run dev` — Start frontend
- `pnpm --filter @workspace/api-spec run codegen` — Regenerate API client from OpenAPI spec
- `pnpm --filter @workspace/db run push` — Push DB schema changes

## Environment Variables

- `DATABASE_URL` — PostgreSQL connection string (auto-set by Replit)
- `AI_INTEGRATIONS_OPENAI_BASE_URL` — OpenAI proxy URL (auto-set)
- `AI_INTEGRATIONS_OPENAI_API_KEY` — OpenAI API key (auto-set)
- `SESSION_SECRET` — Session secret
