# Arquitetura Frontend

**Repositório:** [ZagoConsultoria/claraval-front](https://github.com/ZagoConsultoria/claraval-front)

## Stack

| Camada | Tecnologia | Versão |
|--------|-----------|--------|
| Framework | Next.js (App Router) | 16.1 |
| Linguagem | TypeScript (strict) | 5 |
| UI | React + Tailwind CSS | 19.2 / v4 |
| Ícones | Lucide React | 0.575 |
| Auth | JWT + Google OAuth | — |
| Charts | Chart.js + react-chartjs-2 | 4.5 |
| Vídeo | hls.js | 1.6 |
| Testes | Vitest + Testing Library | 4.0 |
| Formatação | Prettier (com plugin Tailwind) | 3.8 |

## Estrutura de Pastas

```
src/
├── app/                    # Rotas (Next.js App Router)
│   ├── (auth)/             # Rotas públicas — login, recuperar senha
│   ├── (dashboard)/        # Rotas protegidas — área do usuário
│   ├── admin/              # Rotas protegidas — painel administrativo
│   └── dev/                # Showcase de componentes (dev only)
│
├── components/
│   ├── ui/                 # Primitivos: Button, Input, Modal, Table, etc.
│   ├── layout/             # Header, Footer, Sidebar, PageContainer
│   ├── admin/              # Componentes compartilhados do admin
│   ├── dashboard/          # Cards, seções do dashboard
│   ├── diagnostico/        # Formulário, resultados, radar chart
│   ├── elearning/          # Player, trilhas, playlist
│   ├── live/               # Player de live streaming
│   └── documentos/         # Gestão de documentos
│
├── hooks/                  # 24+ custom hooks (estado + lógica)
├── lib/                    # API client, tipos, utilitários
│   ├── api.ts              # Wrapper HTTP com retry e refresh
│   ├── auth.ts             # Token storage/refresh
│   ├── types.ts            # Todas as interfaces TypeScript (~650 linhas)
│   └── utils.ts            # Helpers compartilhados
│
├── middleware.ts            # Redirect básico (auth e client-side)
└── __tests__/              # Testes organizados por sessão
```

### Por que essa estrutura?

- **Route Groups** `(auth)` e `(dashboard)`: Separação clara entre rotas públicas e protegidas sem afetar a URL.
- **components/ui/**: Componentes "burros" e composáveis, sem lógica de negócio.
- **components/{feature}/**: Componentes de domínio que encapsulam lógica específica.
- **hooks/**: Toda lógica de estado e comunicação com API vive aqui. Componentes ficam focados em renderização.

## Estado: Context + Hooks

Padrão dos hooks de feature:

```tsx
const { data, isLoading, error, actions } = useFeature();
```

Cada hook encapsula: fetch de dados, estado de loading/error, e ações (CRUD).

### Hooks Disponíveis

**Usuário:**
`useAuth`, `useSchool`, `useDashboard`, `useDiagnostic`, `useDiagnosticResults`, `useElearning`, `useDocumentos`, `useLive`, `useBanners`, `useTarefas`, `useVideoPlayer`

**Admin:**
`useAdminEscolas`, `useAdminUsuarios`, `useAdminDiagnostico`, `useAdminActionPlan`, `useAdminBanners`, `useAdminEventos`, `useAdminDocumentos`, `useAdminRelatorios`, `useAdminLive`, `useAdminTrails`, `useAdminVideos`, `useAdminConfiguracoes`

**Genérico:**
`useAdminResource<T>()` — hook genérico de CRUD admin. Todos os hooks `useAdmin*` são wrappers finos sobre ele.

## API Client (`lib/api.ts`)

Fetch nativo com wrapper customizado (sem Axios). Proxy via Next.js rewrite: `/api/*` → backend (evita CORS).

## Componentes UI

14 componentes base em `components/ui/`:

Avatar, Badge, Breadcrumb, Button, Card, FileUploader, Input, Modal, ProgressBar, Skeleton, Table, Tabs, Toast, Tooltip

Showcase disponível em `/dev/components` (apenas em dev).

## Estilização

Tailwind CSS v4 com variáveis CSS customizadas:

```css
/* globals.css */
--navy-900: #1a1f36;
--gray-50: #f9fafb;
--radius-lg: 0.75rem;
```

Composição via `cn()` (clsx + tailwind-merge):

```tsx
import { cn } from "@/lib/utils";
<div className={cn("p-4 rounded-lg", isActive && "bg-navy-900")} />
```

## Testes

- **Framework**: Vitest + Testing Library + jsdom
- **Organização**: `src/__tests__/` com suites por sessão de desenvolvimento
- **Setup**: `src/__tests__/setup.tsx` com mocks globais (fetch, localStorage, router)
- **Execução**: `npm test` (CI), `npm run test:watch` (dev)

<!-- TODO: Screenshot do Design System Showcase (/dev/components) — referência visual dos componentes disponíveis -->
