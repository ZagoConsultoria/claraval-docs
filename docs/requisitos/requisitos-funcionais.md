# Requisitos Funcionais

## Autenticacao e Usuarios

| ID | Requisito | Status |
|----|-----------|--------|
| FR-01 | Dois perfis: Admin (consultores) e Cliente (gestores) | Implementado |
| FR-01.1 | Todos os Admins com mesmo nivel de acesso | Implementado |
| FR-02 | Admins acessam qualquer escola | Implementado |
| FR-03 | Clientes so acessam dados da propria escola | Implementado |
| FR-03.1 | Multiplos usuarios por escola, mesma permissao | Implementado |
| FR-04 | Email de boas-vindas com link para definir senha | Implementado |
| FR-05 | Senhas: minimo 8 caracteres com letras e numeros | Implementado |
| FR-05.1 | Login via Google OAuth para usuarios pre-cadastrados | Implementado |

## Diagnostico

| ID | Requisito | Status |
|----|-----------|--------|
| FR-06 | Perguntas filtradas por targetAudience (CLUBE, CORP, START, AMBOS) | Implementado |
| FR-06.1 | Diagnostico preenchido pelo Admin junto com Cliente | Implementado |
| FR-07 | Cada pergunta com 5 niveis de maturidade | Implementado |
| FR-08 | Nota geral = media ponderada dos pilares | Implementado |
| FR-09 | Diagnosticos trimestrais com historico completo | Implementado |
| FR-10 | Plano de acao gerado automaticamente | Implementado |
| FR-10.1 | Admin edita perguntas via interface visual | Implementado |
| FR-10.2 | Versionamento (nao afeta diagnosticos respondidos) | Implementado |
| FR-10.3 | Itens do plano mostram ferramentas e aulas sugeridas | Implementado |
| FR-10.4 | Start: ferramentas fora do pilar aparecem bloqueadas | Implementado |
| FR-10.5 | Templates com contractType (nullable) | Implementado |
| FR-10.6 | Editor admin com abas por tipo de contrato | Implementado |

## Ferramentas

| ID | Requisito | Status |
|----|-----------|--------|
| FR-11 | Tres tipos: Template, Score, Checklist | Parcial |
| FR-11.1 | Liberacao hibrida: contrato + admin por escola | Implementado |
| FR-12 | Auto-save de progresso | Pendente |
| FR-13 | Historico de versoes de preenchimentos | Pendente |
| FR-14 | Exportacao em PDF | Pendente |
| FR-15 | Vincular a pilares e itens do plano | Implementado |

## E-Learning

| ID | Requisito | Status |
|----|-----------|--------|
| FR-16 | Videos categorizados por pilar e cluster | Parcial (clusters pendente) |
| FR-17 | Rastreamento de progresso de visualizacao | Implementado |
| FR-18 | Videos organizados em trilhas ordenadas | Implementado |
| FR-43 | Live streaming via MediaMTX (RTMP → HLS) | Implementado |
| FR-44 | Apenas autenticados acessam stream | Implementado |
| FR-45 | Deteccao automatica de live ativa | Implementado |

## Documentos

| ID | Requisito | Status |
|----|-----------|--------|
| FR-25 | Upload organizado por pilar e categoria | Implementado |
| FR-26 | Multiplos documentos por categoria | Implementado |
| FR-27 | Admin configura categorias por pilar | Implementado |
| FR-28 | Historico de envios por categoria | Implementado |
| FR-45 | Restricao de acesso por usuario (tabela vazia = total) | Implementado |
| FR-46 | Filtragem server-side por categorias permitidas | Implementado |
| FR-47 | Admin com acesso irrestrito | Implementado |

## Dashboard

| ID | Requisito | Status |
|----|-----------|--------|
| FR-29 | Duas variantes: com e sem diagnostico | Implementado |
| FR-30 | Variante determinada automaticamente | Implementado |
| FR-31 | Planner aparece apos diagnostico gerar plano | Implementado |
| FR-32 | Banners gerenciados pelo Admin via CRUD | Implementado |

## Upload de Videos

| ID | Requisito | Status |
|----|-----------|--------|
| FR-33 | Upload de MP4, MOV, WebM, AVI | Implementado |
| FR-34 | Streaming com HTTP Range | Implementado |
| FR-35 | Upload via drag-and-drop (Admin) | Implementado |

## Trilhas (Admin)

| ID | Requisito | Status |
|----|-----------|--------|
| FR-36 | CRUD de trilhas | Implementado |
| FR-37 | Trilhas agrupam videos com ordenacao | Implementado |
| FR-38 | Trilhas substituem agrupamento por pilar | Implementado |
| FR-39 | Calculo de progresso por trilha | Implementado |

## Dashboard Admin

| ID | Requisito | Status |
|----|-----------|--------|
| FR-40 | Metricas em tempo real | Implementado |
| FR-41 | Cards detalhados | Implementado |
| FR-42 | Links rapidos para gestao | Implementado |

## Dados e Armazenamento

| ID | Requisito | Status |
|----|-----------|--------|
| FR-22 | Auto-save de todos os dados | Parcial |
| FR-23 | Log de alteracoes em dados criticos | Parcial |
| FR-24 | Uploads em storage | Implementado (local) |
