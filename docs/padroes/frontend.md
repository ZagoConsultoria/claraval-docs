# Padrões Obrigatórios — Frontend

Regras extraídas do `CLAUDE.md` e do onboarding do repositório [claraval-front](https://github.com/ZagoConsultoria/claraval-front).

## Componentes de Página

- **Nenhuma página admin acima de 300 linhas.** Extrair sub-componentes em `components/admin/<entidade>/`.
- Toda página admin deve usar `AdminErrorBoundary` como wrapper.

## Hooks Admin

- **Proibido**: hooks `useAdmin*` com CRUD copy-paste.
- **Obrigatório**: usar `useAdminResource<T>()` genérico para padrões compartilhados (fetch, search, filter, toggle, CRUD, stats).
- Cada hook existente deve ser wrapper fino com lógica específica do domínio (ex: upload em `useAdminVideos`).

```
useAdminResource<T>()          → fetch, search, filter, CRUD, stats
  └── useAdminUsuarios()       → wrapper com logica de aprovacao
  └── useAdminVideos()         → wrapper com logica de upload
  └── useAdminEscolas()        → wrapper com logica de contrato
```

## Tipagem

- **Proibido**: `as unknown as () => void`. Corrigir tipagem na raiz.
- **Proibido**: `any` em qualquer lugar.
- Fix padrão: `onClick={() => handleSubmit()}` ao invés de cast.
- Todos os tipos em `lib/types.ts`.
- **Named exports apenas** (sem `export default`).

## Utilitários

- **Proibido**: `formatDate`, `formatDuration`, `formatDateTime`, `formatFileSize`, `getInitials` definidos inline.
- **Obrigatório**: importar de `lib/utils.ts`.

## Componentes Admin Compartilhados

Sempre usar componentes de `components/admin/`:

| Componente | Uso |
|------------|-----|
| `AdminStatChips` | Chips de estatísticas (total, ativos, etc.) |
| `AdminSearchBar` | Barra de busca + filtros |
| `AdminPagination` | Controles prev/next |
| `ConfirmDeleteModal` | Modal de confirmação de exclusão |
| `AdminErrorBoundary` | Error boundary com retry |

## API

- Usar `api` de `lib/api.ts` para todas chamadas HTTP. **Nunca `fetch` direto.**
- GETs têm retry automático (1x com 1s delay em erros de rede/5xx).
- Mutações (POST/PUT/DELETE) não têm retry.

## Estilização

- Tailwind CSS v4 com variáveis CSS customizadas em `globals.css`.
- Composição de classes via `cn()` de `lib/utils.ts`:

```tsx
import { cn } from "@/lib/utils";
<div className={cn("p-4 rounded-lg", isActive && "bg-navy-900")} />
```

## Diretiva `"use client"`

- Apenas quando necessário (hooks, estado, eventos do browser).
- Páginas que só fazem composição de componentes não precisam.

## Estrutura de Pastas

```
src/
├── app/admin/<entidade>/page.tsx  → max 300 linhas
├── components/admin/              → compartilhados
├── components/admin/<entidade>/   → sub-componentes extraídos
├── components/ui/                 → primitivos sem lógica de negócio
├── hooks/useAdminResource.ts      → hook genérico
├── hooks/useAdmin<Entidade>.tsx   → wrapper fino
├── lib/utils.ts                   → helpers compartilhados
├── lib/api.ts                     → HTTP client com retry
└── lib/types.ts                   → interfaces TypeScript
```

## Testes

- Framework: Vitest + Testing Library + jsdom
- Setup: `src/__tests__/setup.tsx`
- Rodar antes de qualquer PR: `npm test`
- Coverage: `npm run test:coverage`

## Scripts

```bash
npm run dev              # Dev server (:3000)
npm run build            # Build produção
npm run lint             # ESLint
npm run format           # Prettier (auto-fix)
npm run format:check     # Prettier (verificar)
npm test                 # Testes
npm run test:watch       # Testes em watch
npm run test:coverage    # Testes com coverage
```
