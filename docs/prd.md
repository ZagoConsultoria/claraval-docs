# PRD: Claraval App - Plataforma de Gestão Escolar

## Introdução

A Claraval é uma consultoria de educação que forma gestores de escolas na parte gerencial e administrativa. A empresa utiliza uma metodologia própria baseada em 5 pilares (Estratégia, Governança, Método CLA, Pessoas e Resultados) para diagnosticar e melhorar a gestão das instituições de ensino.

Este PRD descreve a reconstrução completa do MVP existente (desenvolvido no Base44), criando uma plataforma robusta que permita:

- Aplicar diagnósticos gerenciais nas escolas clientes
- Gerar planos de ação baseados nas lacunas identificadas
- Disponibilizar ferramentas de gestão (templates, scores, checklists)
- Oferecer trilhas de conhecimento (e-learning) personalizadas
- Acompanhar a evolução trimestral dos clientes
- Padronizar e escalar a entrega da consultoria

### Contexto de Negócio

**Três tipos de contrato:**

- **Start**: Plano de entrada — ciclo de **3 meses**. Diagnóstico completo nos 5 pilares, mas mentorias, ferramentas e e-learning restritos a apenas 1 pilar escolhido pela escola.
- **Club**: Contrato de **12 meses**, visão sistêmica/generalista da escola como um todo. Acesso total a todos os 5 pilares.
- **Corp**: Contrato de **12 meses**, inclui tudo do Club + consultoria hands-on em um setor específico da escola (Comercial, Financeiro, Sucesso do Aluno, etc.).

**Benefícios inclusos em todos os contratos:**

- Grupo de WhatsApp exclusivo com a equipe Claraval
- Botão de emergência para suporte imediato
- Acesso às aulas ao vivo semanais

**Regras do contrato Start:**

- O pilar é identificado por UUID (`selectedPillarId`) na entidade School
- O diagnóstico é feito completo (todos os pilares, perguntas targetAudience AMBOS)
- O acesso a conteúdo é restrito ao pilar selecionado
- Trilhas bloqueadas aparecem com ícone de cadeado
- No dashboard, só aparecem vídeos do pilar permitido
- No plano de ação, ferramentas/aulas fora do pilar aparecem bloqueadas

**Ciclo de trabalho:**

- Start: 3 meses (1 diagnóstico + acompanhamento focado em 1 pilar)
- Club/Corp: 12 meses com diagnóstico trimestral
- Mentorias e encontros semanais (todos os contratos)
- Reuniões de resultados trimestrais (Club e Corp)

### Metodologia — Os 5 Pilares

**1. Estratégia** — Clareza de propósito e direcionamento. Mapa estratégico, BSC, Missão/Visão/Valores, rituais de gestão.

**2. Governança** — Processos e rotinas que sustentam a operação. Mapeamento de processos, maturidade tecnológica, matriz de produtos internos.

**3. Método CLA** — Da atração do lead à retenção da família:

- 3.1 Branding e Atração: Presença digital, posicionamento competitivo
- 3.2 Comercial: Funil de matrículas, follow-up, gestão à vista
- 3.3 Sucesso do Cliente: NPS, jornada do aluno, KPIs de retenção

**4. Pessoas** — Lideranças fortes, times alinhados. Organograma funcional, rotinas de liderança, PDI.

**5. Resultados** — Dados que viram decisões. Árvore de KPIs, OKRs trimestrais, dashboards.

!!! note "Nomenclatura"
    No código, "Experiência do Cliente" (antiga) = **Método CLA**. "Processos" (antiga) = **Governança**.

---

## Goals

- Centralizar toda a gestão do contrato cliente em única plataforma
- Diagnóstico gerencial completo baseado nos 5 pilares
- Gerar automaticamente planos de ação a partir das lacunas
- Ferramentas de gestão digitais (substituindo Excel/Word)
- Trilhas de conhecimento segmentadas por pilar e tamanho
- Acompanhar evolução da nota de maturidade ao longo do tempo
- Padronizar e escalar a entrega da consultoria

---

## Non-Goals (Fora do Escopo)

- Criação de ferramentas pelo Admin via interface (feito por dev)
- Integração com Google Calendar
- App mobile nativo (plataforma é web responsiva)
- Chat/mensagens internas (usa WhatsApp)
- Pagamentos/faturamento
- Módulo pedagógico (foco é gestão administrativa)
- Multi-idioma (apenas pt-BR)
- Integrações com ERPs escolares

---

## Design Considerations

### Identidade Visual

- Amarelo/dourado como cor primária, azul escuro como secundária
- Logo Claraval no header
- Design limpo e profissional

### UX/UI

- Dashboard como ponto central
- Menu superior: Home, Diagnósticos, Ferramentas, E-Learning
- Cards para listagens
- Gráfico radar para diagnóstico
- Desktop-first, responsivo para tablets

### Modelo de Dados (Entidades Principais)

| Entidade | Campos Chave |
|----------|-------------|
| School | id, name, address, logo, contractType, cluster, selectedPillarId |
| User | id, name, email, role, schoolId |
| Diagnostic | id, schoolId, overallScore, status |
| DiagnosticAnswer | id, diagnosticId, questionId, level, observations |
| ActionPlanItem | id, diagnosticId, pillar, axis, description, priority, status |
| Tool | id, name, type (template/score/checklist), pillar |
| ToolSubmission | id, toolId, schoolId, version, data (JSON) |
| Video | id, title, pillar, cluster, provider |
| Trail | id, title, description, icon, order |
| Sprint | id, escolaId, name, status, tamanho |
| Tarefa | id, sprintId, titulo, status, pokerPoints |

---

## Success Metrics

- **Adoção:** 100% dos clientes usando em até 30 dias
- **Diagnóstico:** Tempo médio < 45 minutos
- **Engajamento:** Taxa de login semanal > 70%
- **Ferramentas:** Média de 3+ preenchidas por cliente/mês
- **E-Learning:** 50%+ dos vídeos recomendados assistidos/trimestre
- **Satisfação:** NPS > 50

---

*Documento original: 29/01/2026*
*Atualizada: 31/03/2026*
*Stakeholder: Heloisa Cunha (Claraval)*
*Product Owner: Gabriel Mendes*
