# PRD: Claraval App - Plataforma de Gestao Escolar

## Introducao

A Claraval e uma consultoria de educacao que forma gestores de escolas na parte gerencial e administrativa. A empresa utiliza uma metodologia propria baseada em 5 pilares (Estrategia, Governanca, Metodo CLA, Pessoas e Resultados) para diagnosticar e melhorar a gestao das instituicoes de ensino.

Este PRD descreve a reconstrucao completa do MVP existente (desenvolvido no Base44), criando uma plataforma robusta que permita:

- Aplicar diagnosticos gerenciais nas escolas clientes
- Gerar planos de acao baseados nas lacunas identificadas
- Disponibilizar ferramentas de gestao (templates, scores, checklists)
- Oferecer trilhas de conhecimento (e-learning) personalizadas
- Acompanhar a evolucao trimestral dos clientes
- Padronizar e escalar a entrega da consultoria

### Contexto de Negocio

**Tres tipos de contrato:**

- **Start**: Plano de entrada — ciclo de **3 meses**. Diagnostico completo nos 5 pilares, mas mentorias, ferramentas e e-learning restritos a apenas 1 pilar escolhido pela escola.
- **Club**: Contrato de **12 meses**, visao sistemica/generalista da escola como um todo. Acesso total a todos os 5 pilares.
- **Corp**: Contrato de **12 meses**, inclui tudo do Club + consultoria hands-on em um setor especifico da escola (Comercial, Financeiro, Sucesso do Aluno, etc.).

**Beneficios inclusos em todos os contratos:**

- Grupo de WhatsApp exclusivo com a equipe Claraval
- Botao de emergencia para suporte imediato
- Acesso as aulas ao vivo semanais

**Regras do contrato Start:**

- O pilar e identificado por UUID (`selectedPillarId`) na entidade School
- O diagnostico e feito completo (todos os pilares, perguntas targetAudience AMBOS)
- O acesso a conteudo e restrito ao pilar selecionado
- Trilhas bloqueadas aparecem com icone de cadeado
- No dashboard, so aparecem videos do pilar permitido
- No plano de acao, ferramentas/aulas fora do pilar aparecem bloqueadas

**Ciclo de trabalho:**

- Start: 3 meses (1 diagnostico + acompanhamento focado em 1 pilar)
- Club/Corp: 12 meses com diagnostico trimestral
- Mentorias e encontros semanais (todos os contratos)
- Reunioes de resultados trimestrais (Club e Corp)

### Metodologia — Os 5 Pilares

**1. Estrategia** — Clareza de proposito e direcionamento. Mapa estrategico, BSC, Missao/Visao/Valores, rituais de gestao.

**2. Governanca** — Processos e rotinas que sustentam a operacao. Mapeamento de processos, maturidade tecnologica, matriz de produtos internos.

**3. Metodo CLA** — Da atracao do lead a retencao da familia:

- 3.1 Branding e Atracao: Presenca digital, posicionamento competitivo
- 3.2 Comercial: Funil de matriculas, follow-up, gestao a vista
- 3.3 Sucesso do Cliente: NPS, jornada do aluno, KPIs de retencao

**4. Pessoas** — Liderancas fortes, times alinhados. Organograma funcional, rotinas de lideranca, PDI.

**5. Resultados** — Dados que viram decisoes. Arvore de KPIs, OKRs trimestrais, dashboards.

!!! note "Nomenclatura"
    No codigo, "Experiencia do Cliente" (antiga) = **Metodo CLA**. "Processos" (antiga) = **Governanca**.

---

## Goals

- Centralizar toda a gestao do contrato cliente em unica plataforma
- Diagnostico gerencial completo baseado nos 5 pilares
- Gerar automaticamente planos de acao a partir das lacunas
- Ferramentas de gestao digitais (substituindo Excel/Word)
- Trilhas de conhecimento segmentadas por pilar e tamanho
- Acompanhar evolucao da nota de maturidade ao longo do tempo
- Padronizar e escalar a entrega da consultoria

---

## Non-Goals (Fora do Escopo)

- Criacao de ferramentas pelo Admin via interface (feito por dev)
- Integracao com Google Calendar
- App mobile nativo (plataforma e web responsiva)
- Chat/mensagens internas (usa WhatsApp)
- Pagamentos/faturamento
- Modulo pedagogico (foco e gestao administrativa)
- Multi-idioma (apenas pt-BR)
- Integracoes com ERPs escolares

---

## Design Considerations

### Identidade Visual

- Amarelo/dourado como cor primaria, azul escuro como secundaria
- Logo Claraval no header
- Design limpo e profissional

### UX/UI

- Dashboard como ponto central
- Menu superior: Home, Diagnosticos, Ferramentas, E-Learning
- Cards para listagens
- Grafico radar para diagnostico
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

- **Adocao:** 100% dos clientes usando em ate 30 dias
- **Diagnostico:** Tempo medio < 45 minutos
- **Engajamento:** Taxa de login semanal > 70%
- **Ferramentas:** Media de 3+ preenchidas por cliente/mes
- **E-Learning:** 50%+ dos videos recomendados assistidos/trimestre
- **Satisfacao:** NPS > 50

---

*Documento original: 29/01/2026*
*Atualizada: 31/03/2026*
*Stakeholder: Heloisa Cunha (Claraval)*
*Product Owner: Gabriel Mendes*
