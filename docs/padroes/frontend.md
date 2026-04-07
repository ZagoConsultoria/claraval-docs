# Padroes Obrigatorios — Frontend

Regras extraidas do `CLAUDE.md` e do onboarding do repositorio [claraval-front](https://github.com/ZagoConsultoria/claraval-front).

## Componentes de Pagina

- **Nenhuma pagina admin acima de 300 linhas.** Extrair sub-componentes em `components/admin/<entidade>/`.
- Toda pagina admin deve usar `AdminErrorBoundary` como wrapper.

## Hooks Admin

- **Proibido**: hooks `useAdmin*` com CRUD copy-paste.
- **Obrigatorio**: usar `useAdminResource<T>()` generico para padroes compartilhados (fetch, search, filter, toggle, CRUD, stats).
- Cada hook existente deve ser wrapper fino com logica especifica do dominio (ex: upload em `useAdminVideos`).

```
useAdminResource<T>()          → fetch, search, filter, CRUD, stats
  └── useAdminUsuarios()       → wrapper com logica de aprovacao
  └── useAdminVideos()         → wrapper com logica de upload
  └── useAdminEscolas()        → wrapper com logica de contrato
```

## Tipagem

- **Proibido**: `as unknown as () => void`. Corrigir tipagem na raiz.
- **Proibido**: `any` em qualquer lugar.
- Fix padrao: `onClick={() => handleSubmit()}` ao inves de cast.
- Todos os tipos em `lib/types.ts`.
- **Named exports apenas** (sem `export default`).

## Utilitarios

- **Proibido**: `formatDate`, `formatDuration`, `formatDateTime`, `formatFileSize`, `getInitials` definidos inline.
- **Obrigatorio**: importar de `lib/utils.ts`.

## Componentes Admin Compartilhados

Sempre usar componentes de `components/admin/`:

| Componente | Uso |
|------------|-----|
| `AdminStatChips` | Chips de estatisticas (total, ativos, etc.) |
| `AdminSearchBar` | Barra de busca + filtros |
| `AdminPagination` | Controles prev/next |
| `ConfirmDeleteModal` | Modal de confirmacao de exclusao |
| `AdminErrorBoundary` | Error boundary com retry |

## API

- Usar `api` de `lib/api.ts` para todas chamadas HTTP. **Nunca `fetch` direto.**
- GETs tem retry automatico (1x com 1s delay em erros de rede/5xx).
- Mutacoes (POST/PUT/DELETE) nao tem retry.

## Estilizacao

- Tailwind CSS v4 com variaveis CSS customizadas em `globals.css`.
- Composicao de classes via `cn()` de `lib/utils.ts`:

```tsx
import { cn } from "@/lib/utils";
<div className={cn("p-4 rounded-lg", isActive && "bg-navy-900")} />
```

## Diretiva `"use client"`

- Apenas quando necessario (hooks, estado, eventos do browser).
- Paginas que so fazem composicao de componentes nao precisam.

## Estrutura de Pastas

```
src/
├── app/admin/<entidade>/page.tsx  → max 300 linhas
├── components/admin/              → compartilhados
├── components/admin/<entidade>/   → sub-componentes extraidos
├── components/ui/                 → primitivos sem logica de negocio
├── hooks/useAdminResource.ts      → hook generico
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
npm run build            # Build producao
npm run lint             # ESLint
npm run format           # Prettier (auto-fix)
npm run format:check     # Prettier (verificar)
npm test                 # Testes
npm run test:watch       # Testes em watch
npm run test:coverage    # Testes com coverage
```
