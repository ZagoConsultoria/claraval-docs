# Claraval App - Documentacao Tecnica

Plataforma de gestao escolar da **Claraval Consultoria**, que forma gestores de escolas na parte gerencial e administrativa.

## Repositorios

| Repositorio | Stack | Descricao |
|-------------|-------|-----------|
| [claraval-front](https://github.com/ZagoConsultoria/claraval-front) | Next.js 16 + React 19 + TypeScript + Tailwind CSS v4 | Frontend da plataforma |
| [claraval-back](https://github.com/ZagoConsultoria/claraval-back) | Spring Boot 3.5 + Java 17 + PostgreSQL + Flyway | Backend API REST |

## Modulos da Plataforma

| Modulo | Descricao |
|--------|-----------|
| **Diagnostico** | Questionario de maturidade gerencial baseado em 5 pilares, com notas e radar chart |
| **Plano de Acao** | Itens gerados automaticamente a partir do diagnostico + templates configurados |
| **E-Learning** | Videos organizados em trilhas com streaming HLS e progresso por usuario |
| **Ferramentas** | Templates, scores e checklists de gestao escolar |
| **Documentos** | Upload/download de arquivos por escola, organizados por pilar e categoria |
| **Tarefas e Sprints** | Board kanban com sprints, poker points e analytics |
| **Live** | Transmissao ao vivo via MediaMTX (RTMP -> HLS) |
| **Landing Page** | Site institucional publico com formulario de captacao de leads |
| **Admin** | Painel completo para gestao de escolas, usuarios, conteudo e configuracoes |

## Tipos de Contrato

| Tipo | Duracao | Escopo |
|------|---------|--------|
| **Start** | 3 meses | Diagnostico completo, mas mentorias/ferramentas/e-learning restritos a 1 pilar |
| **Club** | 12 meses | Acesso total a todos os 5 pilares |
| **Corp** | 12 meses | Tudo do Club + consultoria hands-on em um setor especifico |

## Os 5 Pilares

1. **Estrategia** — Clareza de proposito e direcionamento (BSC, Missao/Visao/Valores)
2. **Governanca** — Processos e rotinas que sustentam a operacao
3. **Metodo CLA** — Da atracao do lead a retencao da familia (Branding, Comercial, Sucesso do Cliente)
4. **Pessoas** — Liderancas fortes, times alinhados (Organograma, PDI, 1:1)
5. **Resultados** — Dados que viram decisoes (KPIs, OKRs, Dashboards)

## Links Rapidos

- [PRD Completo](prd.md)
- [Arquitetura](arquitetura/visao-geral.md)
- [Referencia da API](api/index.md)
- [Setup do Ambiente](onboarding/setup-frontend.md)
- [Padroes de Codigo](padroes/frontend.md)

<!-- TODO: Adicionar screenshot do dashboard principal aqui — ajuda novos devs a entender o produto visualmente -->
