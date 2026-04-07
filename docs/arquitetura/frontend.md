# Arquitetura Frontend

**Repositorio:** [ZagoConsultoria/claraval-front](https://github.com/ZagoConsultoria/claraval-front)

## Stack

| Camada | Tecnologia | Versao |
|--------|-----------|--------|
| Framework | Next.js (App Router) | 16.1 |
| Linguagem | TypeScript (strict) | 5 |
| UI | React + Tailwind CSS | 19.2 / v4 |
| Icones | Lucide React | 0.575 |
| Auth | JWT + Google OAuth | — |
| Charts | Chart.js + react-chartjs-2 | 4.5 |
| Video | hls.js | 1.6 |
| Testes | Vitest + Testing Library | 4.0 |
| Formatacao | Prettier (com plugin Tailwind) | 3.8 |

## Estrutura de Pastas

```
src/
├── app/                    # Rotas (Next.js App Router)
│   ├── (auth)/             # Rotas publicas — login, recuperar senha
│   ├── (dashboard)/        # Rotas protegidas — area do usuario
│   ├── admin/              # Rotas protegidas — painel administrativo
│   └── dev/                # Showcase de componentes (dev only)
│
├── components/
│   ├── ui/                 # Primitivos: Button, Input, Modal, Table, etc.
│   ├── layout/             # Header, Footer, Sidebar, PageContainer
│   ├── admin/              # Componentes compartilhados do admin
│   ├── dashboard/          # Cards, secoes do dashboard
│   ├── diagnostico/        # Formulario, resultados, radar chart
│   ├── elearning/          # Player, trilhas, playlist
│   ├── live/               # Player de live streaming
│   └── documentos/         # Gestao de documentos
│
├── hooks/                  # 24+ custom hooks (estado + logica)
├── lib/                    # API client, tipos, utilitarios
│   ├── api.ts              # Wrapper HTTP com retry e refresh
│   ├── auth.ts             # Token storage/refresh
│   ├── types.ts            # Todas as interfaces TypeScript (~650 linhas)
│   └── utils.ts            # Helpers compartilhados
│
├── middleware.ts            # Redirect basico (auth e client-side)
└── __tests__/              # Testes organizados por sessao
```

### Por que essa estrutura?

- **Route Groups** `(auth)` e `(dashboard)`: Separacao clara entre rotas publicas e protegidas sem afetar a URL.
- **components/ui/**: Componentes "burros" e composaveis, sem logica de negocio.
- **components/{feature}/**: Componentes de dominio que encapsulam logica especifica.
- **hooks/**: Toda logica de estado e comunicacao com API vive aqui. Componentes ficam focados em renderizacao.

## Estado: Context + Hooks

Padrao dos hooks de feature:

```tsx
const { data, isLoading, error, actions } = useFeature();
```

Cada hook encapsula: fetch de dados, estado de loading/error, e acoes (CRUD).

### Hooks Disponiveis

**Usuario:**
`useAuth`, `useSchool`, `useDashboard`, `useDiagnostic`, `useDiagnosticResults`, `useElearning`, `useDocumentos`, `useLive`, `useBanners`, `useTarefas`, `useVideoPlayer`

**Admin:**
`useAdminEscolas`, `useAdminUsuarios`, `useAdminDiagnostico`, `useAdminActionPlan`, `useAdminBanners`, `useAdminEventos`, `useAdminDocumentos`, `useAdminRelatorios`, `useAdminLive`, `useAdminTrails`, `useAdminVideos`, `useAdminConfiguracoes`

**Generico:**
`useAdminResource<T>()` — hook generico de CRUD admin. Todos os hooks `useAdmin*` sao wrappers finos sobre ele.

## API Client (`lib/api.ts`)

Fetch nativo com wrapper customizado (sem Axios). Proxy via Next.js rewrite: `/api/*` → backend (evita CORS).

## Componentes UI

14 componentes base em `components/ui/`:

Avatar, Badge, Breadcrumb, Button, Card, FileUploader, Input, Modal, ProgressBar, Skeleton, Table, Tabs, Toast, Tooltip

Showcase disponivel em `/dev/components` (apenas em dev).

## Estilizacao

Tailwind CSS v4 com variaveis CSS customizadas:

```css
/* globals.css */
--navy-900: #1a1f36;
--gray-50: #f9fafb;
--radius-lg: 0.75rem;
```

Composicao via `cn()` (clsx + tailwind-merge):

```tsx
import { cn } from "@/lib/utils";
<div className={cn("p-4 rounded-lg", isActive && "bg-navy-900")} />
```

## Testes

- **Framework**: Vitest + Testing Library + jsdom
- **Organizacao**: `src/__tests__/` com suites por sessao de desenvolvimento
- **Setup**: `src/__tests__/setup.tsx` com mocks globais (fetch, localStorage, router)
- **Execucao**: `npm test` (CI), `npm run test:watch` (dev)

<!-- TODO: Screenshot do Design System Showcase (/dev/components) — referencia visual dos componentes disponiveis -->
