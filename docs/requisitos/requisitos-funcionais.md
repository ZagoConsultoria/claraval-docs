# Requisitos Funcionais

## Autenticação e Usuários

| ID | Requisito | Status |
|----|-----------|--------|
| FR-01 | Dois perfis: Admin (consultores) e Cliente (gestores) | Implementado |
| FR-01.1 | Todos os Admins com mesmo nível de acesso | Implementado |
| FR-02 | Admins acessam qualquer escola | Implementado |
| FR-03 | Clientes só acessam dados da própria escola | Implementado |
| FR-03.1 | Múltiplos usuários por escola, mesma permissão | Implementado |
| FR-04 | Email de boas-vindas com link para definir senha | Implementado |
| FR-05 | Senhas: mínimo 8 caracteres com letras e números | Implementado |
| FR-05.1 | Login via Google OAuth para usuários pré-cadastrados | Implementado |

## Diagnóstico

| ID | Requisito | Status |
|----|-----------|--------|
| FR-06 | Perguntas filtradas por targetAudience (CLUBE, CORP, START, AMBOS) | Implementado |
| FR-06.1 | Diagnóstico preenchido pelo Admin junto com Cliente | Implementado |
| FR-07 | Cada pergunta com 5 níveis de maturidade | Implementado |
| FR-08 | Nota geral = média ponderada dos pilares | Implementado |
| FR-09 | Diagnósticos trimestrais com histórico completo | Implementado |
| FR-10 | Plano de ação gerado automaticamente | Implementado |
| FR-10.1 | Admin edita perguntas via interface visual | Implementado |
| FR-10.2 | Versionamento (não afeta diagnósticos respondidos) | Implementado |
| FR-10.3 | Itens do plano mostram ferramentas e aulas sugeridas | Implementado |
| FR-10.4 | Start: ferramentas fora do pilar aparecem bloqueadas | Implementado |
| FR-10.5 | Templates com contractType (nullable) | Implementado |
| FR-10.6 | Editor admin com abas por tipo de contrato | Implementado |
| FR-10.7 | Resultados do diagnóstico exibem benchmark de cluster: média de notas de escolas do mesmo cluster sobreposta no gráfico radar | Pendente |

## Escolas

| ID | Requisito | Status |
|----|-----------|--------|
| FR-48 | Campo `cluster` da escola deve ser um enum (`ATE_300`, `DE_300_A_500`, `DE_500_A_1000`, `ACIMA_DE_1000`) — não texto livre | Pendente |
| FR-49 | Cadastro de escola deve ter select obrigatório para cluster | Pendente |
| FR-50 | Filtros de listagem de escolas, vídeos, trilhas e relatórios devem incluir filtro por cluster (select com enum) | Pendente |

## Ferramentas

| ID | Requisito | Status |
|----|-----------|--------|
| FR-11 | Três tipos: Template, Score, Checklist | Parcial |
| FR-11.1 | Liberação híbrida: contrato + admin por escola | Implementado |
| FR-12 | Auto-save de progresso | Pendente |
| FR-13 | Histórico de versões de preenchimentos | Pendente |
| FR-14 | Exportação em PDF | Pendente |
| FR-15 | Vincular a pilares e itens do plano | Implementado |

## E-Learning

| ID | Requisito | Status |
|----|-----------|--------|
| FR-16 | Vídeos categorizados por pilar e cluster | Parcial (clusters pendente) |
| FR-17 | Rastreamento de progresso de visualização | Implementado |
| FR-18 | Vídeos organizados em trilhas ordenadas | Implementado |
| FR-43 | Live streaming via MediaMTX (RTMP → HLS) | Implementado |
| FR-44 | Apenas autenticados acessam stream | Implementado |
| FR-45 | Detecção automática de live ativa | Implementado |

## Documentos

| ID | Requisito | Status |
|----|-----------|--------|
| FR-25 | Upload organizado por pilar e categoria | Implementado |
| FR-26 | Múltiplos documentos por categoria | Implementado |
| FR-27 | Admin configura categorias por pilar | Implementado |
| FR-28 | Histórico de envios por categoria | Implementado |
| FR-45 | Restrição de acesso por usuário (tabela vazia = total) | Implementado |
| FR-46 | Filtragem server-side por categorias permitidas | Implementado |
| FR-47 | Admin com acesso irrestrito | Implementado |

## Dashboard

| ID | Requisito | Status |
|----|-----------|--------|
| FR-29 | Duas variantes: com e sem diagnóstico | Implementado |
| FR-30 | Variante determinada automaticamente | Implementado |
| FR-31 | Planner aparece após diagnóstico gerar plano | Implementado |
| FR-32 | Banners gerenciados pelo Admin via CRUD | Implementado |

## Upload de Vídeos

| ID | Requisito | Status |
|----|-----------|--------|
| FR-33 | Upload de MP4, MOV, WebM, AVI | Implementado |
| FR-34 | Streaming com HTTP Range | Implementado |
| FR-35 | Upload via drag-and-drop (Admin) | Implementado |

## Trilhas (Admin)

| ID | Requisito | Status |
|----|-----------|--------|
| FR-36 | CRUD de trilhas | Implementado |
| FR-37 | Trilhas agrupam vídeos com ordenação | Implementado |
| FR-38 | Trilhas substituem agrupamento por pilar | Implementado |
| FR-39 | Cálculo de progresso por trilha | Implementado |

## Dashboard Admin

| ID | Requisito | Status |
|----|-----------|--------|
| FR-40 | Métricas em tempo real | Implementado |
| FR-41 | Cards detalhados | Implementado |
| FR-42 | Links rápidos para gestão | Implementado |

## Feedback de Usuários

| ID | Requisito | Status |
|----|-----------|--------|
| FR-51 | Formulário de feedback acessível em todas as páginas via botão flutuante | Pendente |
| FR-52 | Tipo de feedback: `BUG` ou `SUGESTAO` (enum) | Pendente |
| FR-52.1 | Formulário deve conter campos obrigatórios: título (resumo) e descrição (detalhamento do bug ou sugestão) | Pendente |
| FR-53 | Página atual capturada automaticamente (`window.location.pathname`) e enviada junto com o feedback | Pendente |
| FR-54 | Upload opcional de vídeo (MP4, MOV, WebM) para demonstrar bugs | Pendente |
| FR-55 | Integração com Jira: feedback cria issue automaticamente via REST API (Basic Auth + API Token) | Pendente |
| FR-56 | Vídeo anexado ao feedback é enviado como attachment na issue do Jira (header `X-Atlassian-Token: no-check`) | Pendente |
| FR-57 | Metadados capturados automaticamente: userId, nome, email, escola, role, browser/user-agent, URL da página | Pendente |
| FR-58 | Confirmação exibe chave da issue criada no Jira (ex: `CLAR-123`) | Pendente |
| FR-59 | Configuração da integração Jira no painel admin (URL, email, API token, projeto, tipos de issue) — credenciais criptografadas | Pendente |
| FR-60 | Admin pode visualizar todos os feedbacks enviados; usuário vê apenas os próprios | Pendente |

## NPS (Net Promoter Score)

| ID | Requisito | Status |
|----|-----------|--------|
| FR-61 | Formulário de NPS personalizável: admin configura perguntas conforme necessidade | Pendente |
| FR-62 | Disponibilização automática do NPS ao final de trilhas dentro da plataforma | Pendente |
| FR-63 | Criação de NPS sob demanda com associação a eventos, aulas ou trilhas | Pendente |
| FR-64 | Geração de QR Code público para acesso ao NPS (sem necessidade de login) | Pendente |
| FR-65 | Área administrativa restrita para exibição de resultados: notas, avaliações e comentários | Pendente |
| FR-66 | Transformar comentários do NPS em tarefas no módulo de sprints (com prazo, responsável e demais atributos) | Pendente |
| FR-67 | Segmentação automática por nota: Leais (9-10), Neutros (7-8), Detratores (0-6) | Pendente |
| FR-67.1 | Leais (9-10): clientes leais e satisfeitos | Pendente |
| FR-67.2 | Neutros (7-8): satisfeitos, mas propensos à concorrência | Pendente |
| FR-67.3 | Detratores (0-6): insatisfeitos | Pendente |
| FR-68 | Cálculo do score NPS: % Leais − % Detratores | Pendente |

## Dados e Armazenamento

| ID | Requisito | Status |
|----|-----------|--------|
| FR-22 | Auto-save de todos os dados | Parcial |
| FR-23 | Log de alterações em dados críticos | Parcial |
| FR-24 | Uploads em storage | Implementado (local) |
