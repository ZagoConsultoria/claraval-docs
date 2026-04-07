# Claraval App - Documentação Técnica

Plataforma de gestão escolar da **Claraval Consultoria**, que forma gestores de escolas na parte gerencial e administrativa.

## Repositórios

| Repositório | Stack | Descrição |
|-------------|-------|-----------|
| [claraval-front](https://github.com/ZagoConsultoria/claraval-front) | Next.js 16 + React 19 + TypeScript + Tailwind CSS v4 | Frontend da plataforma |
| [claraval-back](https://github.com/ZagoConsultoria/claraval-back) | Spring Boot 3.5 + Java 17 + PostgreSQL + Flyway | Backend API REST |

## Módulos da Plataforma

| Módulo | Descrição |
|--------|-----------|
| **Diagnóstico** | Questionário de maturidade gerencial baseado em 5 pilares, com notas e radar chart |
| **Plano de Ação** | Itens gerados automaticamente a partir do diagnóstico + templates configurados |
| **E-Learning** | Vídeos organizados em trilhas com streaming HLS e progresso por usuário |
| **Ferramentas** | Templates, scores e checklists de gestão escolar |
| **Documentos** | Upload/download de arquivos por escola, organizados por pilar e categoria |
| **Tarefas e Sprints** | Board kanban com sprints, poker points e analytics |
| **Live** | Transmissão ao vivo via MediaMTX (RTMP -> HLS) |
| **Landing Page** | Site institucional público com formulário de captação de leads |
| **Admin** | Painel completo para gestão de escolas, usuários, conteúdo e configurações |

## Tipos de Contrato

| Tipo | Duração | Escopo |
|------|---------|--------|
| **Start** | 3 meses | Diagnóstico completo, mas mentorias/ferramentas/e-learning restritos a 1 pilar |
| **Club** | 12 meses | Acesso total a todos os 5 pilares |
| **Corp** | 12 meses | Tudo do Club + consultoria hands-on em um setor específico |

## Os 5 Pilares

1. **Estratégia** — Clareza de propósito e direcionamento (BSC, Missão/Visão/Valores)
2. **Governança** — Processos e rotinas que sustentam a operação
3. **Método CLA** — Da atração do lead à retenção da família (Branding, Comercial, Sucesso do Cliente)
4. **Pessoas** — Lideranças fortes, times alinhados (Organograma, PDI, 1:1)
5. **Resultados** — Dados que viram decisões (KPIs, OKRs, Dashboards)

## Links Rápidos

- [PRD Completo](prd.md)
- [Arquitetura](arquitetura/visao-geral.md)
- [Referência da API](api/index.md)
- [Setup do Ambiente](onboarding/setup-frontend.md)
- [Padrões de Código](padroes/frontend.md)

<!-- TODO: Adicionar screenshot do dashboard principal aqui — ajuda novos devs a entender o produto visualmente -->
