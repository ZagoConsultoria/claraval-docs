# Setup Frontend

## Pre-requisitos

- **Node.js >= 22** (`nvm use 22`)
- **Backend rodando** em `http://localhost:3001` (Spring Boot + PostgreSQL)

## Instalacao

```bash
git clone https://github.com/ZagoConsultoria/claraval-front.git
cd claraval-front
nvm use 22
npm install
cp .env.local.example .env.local  # ou crie manualmente
npm run dev  # → http://localhost:3000
```

## Variaveis de Ambiente

Crie o arquivo `.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_GOOGLE_CLIENT_ID=<seu-client-id>
NEXT_PUBLIC_APP_NAME=Claraval Academy
```

## Usuario de Teste

| Campo | Valor |
|-------|-------|
| Email | `teste@claraval.com` |
| Senha | `teste123` |
| Role | ROLE_USER |

## Scripts Disponiveis

| Script | Descricao |
|--------|-----------|
| `npm run dev` | Dev server (http://localhost:3000) |
| `npm run build` | Build de producao |
| `npm run lint` | ESLint |
| `npm run format` | Prettier (auto-fix) |
| `npm run format:check` | Prettier (verificar) |
| `npm test` | Rodar todos os testes |
| `npm run test:watch` | Testes em modo watch |
| `npm run test:coverage` | Testes com coverage |

## Recursos para Aprender o Codebase

1. **Comece pelo Dashboard** (`app/(dashboard)/dashboard/page.tsx`) — ponto central que conecta todas as features
2. **Leia `useAuth.tsx` e `useSchool.tsx`** — os dois contexts que permeiam toda a app
3. **Use o Showcase** (`/dev/components`) para conhecer os componentes UI disponiveis
4. **Consulte `lib/types.ts`** para entender os contratos de dados com o backend
5. **O diagnostico e a feature mais complexa** — reserve tempo para entender `useDiagnostic()`
6. **Admin e repetitivo por design** — entenda uma pagina admin e voce entende todas

## Documentacao Interna do Repo

| Documento | Caminho | Conteudo |
|-----------|---------|----------|
| PRD | `docs/prd-claraval-app.md` | Requisitos do produto |
| Onboarding | `docs/ONBOARDING.md` | Guia detalhado para devs |
| User Journeys | `docs/USER-JOURNEYS.md` | Fluxos de usuario com diagramas |
| Modulo Tarefas | `docs/modulo-tarefas-springboot.md` | Spec do modulo de tarefas |
| Coding Guidelines | `CLAUDE.md` | Regras obrigatorias de codigo |
| Design System | `http://localhost:3000/dev/components` | Showcase dos componentes UI |

<!-- TODO: Screenshot do dashboard — primeira coisa que um novo dev ve ao rodar o projeto -->
<!-- TODO: Screenshot do showcase de componentes (/dev/components) — referencia visual essencial -->
