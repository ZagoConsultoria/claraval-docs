# User Stories

## Módulo: Autenticação e Gestão de Usuários

### US-001: Login de usuários

**Como** um usuário (Admin ou Cliente), **quero** fazer login na plataforma **para** acessar as funcionalidades correspondentes ao meu perfil.

- [x] Tela de login com campos email e senha
- [x] Botão "Entrar com Google" para autenticação via Google OAuth
- [x] Autenticação segura com JWT
- [x] Redirecionamento para dashboard após login bem-sucedido
- [x] Mensagem de erro clara para credenciais inválidas
- [x] Opção "Esqueci minha senha" com recuperação por email
- [x] Usuário que faz login com Google deve estar pré-cadastrado

### US-002: Cadastro de escolas (Admin)

**Como** um Admin, **quero** cadastrar novas escolas clientes **para** gerenciar seus contratos na plataforma.

- [x] Formulário com: nome, endereço, logo, tipo de contrato, data início
- [ ] Campo **cluster** obrigatório como select (enum: ATE_300, DE_300_A_500, DE_500_A_1000, ACIMA_DE_1000)
- [x] Para Start: duração de 3 meses + campo para selecionar pilar de atuação
- [x] Para Corp: campo adicional para setor foco
- [x] Upload de logo da escola
- [x] Validação de campos obrigatórios

### US-003: Cadastro de usuários (Admin)

**Como** um Admin, **quero** cadastrar usuários vinculados a uma escola **para** que possam acessar a plataforma.

- [x] Formulário com: nome, email, cargo, escola vinculada
- [x] Email de boas-vindas enviado automaticamente
- [x] Admin pode editar ou desativar usuários

### US-004: Listagem e gestão de escolas (Admin)

**Como** um Admin, **quero** visualizar todas as escolas cadastradas **para** acompanhar o status dos contratos.

- [x] Lista com: nome, logo, tipo de contrato, nota atual, status
- [x] Filtros por tipo de contrato, status, nota
- [x] Busca por nome
- [x] Click na escola abre dashboard dela

---

## Módulo: Dashboard/Home

### US-005: Dashboard principal

**Como** um Cliente, **quero** ver o dashboard da minha escola **para** entender rapidamente minha situação.

- [ ] Header com logo e nome/endereço da escola
- [x] Carrossel de banners com eventos e avisos
- [x] Seção "Pilares que sustentam a escola" com 5 pilares clicáveis
- [x] Card do último diagnóstico com nota geral
- [x] Seção de vídeos e ferramentas recomendados

### US-006: Seleção de pilar para detalhamento

**Como** um Cliente, **quero** clicar em um pilar **para** ver vídeos e ferramentas relacionados.

- [x] Pilares com ícones distintos
- [x] Pilar selecionado fica destacado
- [x] Seções de vídeos e ferramentas filtram pelo pilar

### US-007: Gestão de banners (Admin)

**Como** um Admin, **quero** gerenciar banners do carrossel **para** comunicar eventos e novidades.

- [x] CRUD completo de banners
- [x] Upload de imagem, título, link, período de exibição
- [] Ordenação drag and drop

---

## Módulo: Diagnóstico

### US-008: Aplicação do diagnóstico

**Como** um Cliente, **quero** responder o diagnóstico gerencial **para** identificar as lacunas da minha escola.

- [x] Organizado por pilares (5 pilares)
- [x] Cada pilar tem múltiplos eixos com perguntas
- [x] Escala de 1 a 5 níveis de maturidade
- [x] Barra de progresso
- [x] Salvar automaticamente respostas parciais
- [x] Perguntas diferentes por tipo de contrato
- [x] Só pode ser preenchido junto com o admin

### US-009: Resultados do diagnóstico

**Como** um Cliente, **quero** ver os resultados **para** entender onde preciso melhorar.

- [x] Nota geral (média ponderada)
- [x] Gráfico radar por pilar
- [ ] Gráfico radar com benchmark: média de notas de outras escolas do mesmo cluster sobreposta no radar
- [x] Detalhamento por pilar e eixo
- [x] Indicação visual de áreas críticas
- [] Exportar PDF

### US-010: Histórico de diagnósticos

**Como** um Cliente, **quero** ver o histórico **para** acompanhar minha evolução trimestral.

- [x] Dropdown para selecionar diagnóstico anterior
- [x] Gráfico de evolução ao longo do tempo
- [x] Comparativo entre diagnóstico atual e anterior

### US-011: Geração do plano de ação

**Como** um Cliente, **quero** que o sistema gere um plano de ação **para** saber o que preciso fazer.

- [x] Gerado automaticamente após finalizar diagnóstico
- [x] Organizado por pilar e eixo
- [x] Cada item mostra ferramentas e aulas sugeridas
- [x] Priorizados por nota (piores = maior prioridade)
- [] Admin pode editar/ajustar

### US-012: Acompanhamento do plano de ação

**Como** um Cliente, **quero** acompanhar e marcar itens como concluídos **para** registrar meu progresso.

- [x] Lista com checkbox de conclusão
- [x] Ferramentas e aulas sugeridas com acesso rápido
- [x] Para Start: itens fora do pilar aparecem bloqueados
- [x] Barra de progresso geral

### US-013: Configuração do diagnóstico (Admin)

**Como** um Admin, **quero** configurar perguntas e eixos **para** manter a metodologia atualizada sem desenvolvedor.

- [x] Interface visual de edição (form builder)
- [x] CRUD de pilares, eixos e perguntas
- [x] Editor inline para textos
- [x] Definir níveis 1-5 por pergunta
- [x] Marcar targetAudience (Clube, Corp, Start, Ambos)
- [x] Abas por tipo de contrato
- [x] Drag and drop para reordenar
- [x] Versionamento (não afeta diagnósticos respondidos)

---

## Módulo: Ferramentas

### US-014: Listagem de ferramentas

**Como** um Cliente, **quero** ver ferramentas disponíveis **para** escolher qual utilizar.

- [x] Grid de cards com ícone, nome, pilar, tipo
- [x] Indicador se está no plano de ação
- [x] Filtros por pilar e tipo

### US-015: Ferramenta tipo Template

**Como** um Cliente, **quero** preencher um template **para** documentar informações da minha escola.

- [x] Campos conforme estrutura (textos, selects, tabelas)
- [x] Salvar automaticamente
- [x] Exportar PDF
- [x] Versionamento com histórico

### US-016: Ferramenta tipo Score

**Como** um Cliente, **quero** preencher uma autoavaliação **para** obter uma nota.

- [ ] Formulário com escala de resposta
- [ ] Cálculo automático do score
- [ ] Interpretação do resultado
- [ ] Histórico de scores

### US-017: Ferramenta tipo Checklist

**Como** um Cliente, **quero** usar um checklist **para** acompanhar execução de um processo.

- [ ] Lista com checkbox
- [ ] Agrupamento em seções
- [ ] Barra de progresso
- [ ] Exportar PDF

---

## Módulo: E-Learning

### US-019: Trilhas por pilar

**Como** um Cliente, **quero** acessar vídeos por pilar **para** aprender sobre temas que preciso melhorar.

- [x] Menu com 5 pilares
- [x] Indicador de vídeo assistido
- [x] Barra de progresso da trilha

### US-020: Trilhas por cluster

**Como** um Cliente, **quero** filtrar por tamanho de escola **para** ver conteúdos relevantes.

- [x] Filtro: "Até 300", "300-500", "500-1000", "1000+"
- [x] Por padrão, mostra conteúdo do cluster do cliente

### US-021: Player de vídeo

- [x] Player com streaming HTTP Range
- [x] Controles padrão
- [x] Marcar como assistido ao completar 90%
- [x] Progresso salvo (continuar de onde parou)
- [x] Proteção anti-gravação

### US-022: Gestão de vídeos e trilhas (Admin)

- [x] CRUD de vídeos com upload drag-and-drop
- [x] Streaming com HTTP Range
- [x] CRUD de trilhas com ordenação

---

## Módulo: Documentos

### US-026: Envio de documentos por pilar

**Como** um Cliente, **quero** enviar documentos organizados por pilar e categoria.

- [x] Documentos organizados por pilar
- [x] Categorias configuráveis pelo Admin
- [x] Upload de múltiplos documentos por categoria
- [x] Formatos: PDF, XLSX, DOCX, PNG, JPG
- [x] Indicador de status: pendente, enviado, aprovado
- [x] Histórico de envios

### US-027: Gestão de categorias (Admin)

- [x] CRUD de categorias vinculadas a pilares
- [x] Ativar/desativar categorias
- [x] Visualizar status de envio por escola

### US-028: Controle de acesso a documentos (Admin)

- [x] Tabela many-to-many usuario_categorias
- [x] Tabela vazia = acesso irrestrito
- [x] Admin sempre vê todos os documentos
- [x] Filtragem server-side

---

## Módulo: Tarefas e Sprints

### US-029: Gestão de Sprints (Admin)

- [x] CRUD de sprints por escola
- [x] Sprint pode ser fechada (tarefas ficam read-only)
- [x] Dropdown searchable de sprints

### US-030: Board de Tarefas

- [x] Kanban (3 colunas com drag-and-drop)
- [x] Lista (tabela com header sticky)
- [x] Calendário (grid mensal)

### US-031: Filtros do Board

- [x] Filtro por origem, status e responsável
- [x] Filtros aplicam em todas as views

### US-032: CRUD de Tarefas

- [x] Criar com título, descrição, sprint, responsável, prazo, poker points
- [x] Modal de edição com subtarefas
- [x] Sprint fechada: campos read-only

### US-033: Responsáveis

- [x] Dropdown inclui usuários da escola + admins
- [x] Admins podem ser atribuídos a qualquer escola

### US-034: Analytics de Sprints

- [x] Gráfico de velocidade por sprint
- [x] Gráfico de pontos por pessoa
- [x] Card de capacidade com métricas

### US-035: Integração com Dashboard

- [x] Calendário do dashboard mostra tarefas de sprint e plano CLA

---

## Módulo: Feedback de Usuários

### US-036: Formulário de feedback e reporte de bugs

**Como** um Cliente ou Admin, **quero** enviar sugestões de melhoria e reportar bugs diretamente pela plataforma **para** que a equipe de desenvolvimento possa corrigir problemas e evoluir o produto.

**Acceptance Criteria:**

- [ ] Botão flutuante (FAB) acessível em todas as páginas da plataforma (ex: ícone de megafone ou interrogação)
- [ ] Modal/drawer de feedback com campos:
    - Tipo: select com opções `BUG` ou `SUGESTAO`
    - Título: campo de texto obrigatório (resumo do feedback)
    - Descrição: textarea obrigatória (detalhamento)
    - Página atual: capturada automaticamente via `window.location.pathname` (exibida como campo read-only para o usuário confirmar)
    - Vídeo (opcional): upload de arquivo de vídeo (MP4, MOV, WebM) para demonstrar o bug
    - Prioridade (opcional): select com `BAIXA`, `MEDIA`, `ALTA` (default: `MEDIA`)
- [ ] Formulário captura automaticamente: ID do usuário, nome, email, escola, role, browser/user-agent
- [ ] Ao enviar, cria issue automaticamente no Jira (projeto configurável) via API REST
- [ ] Vídeo anexado é enviado como attachment na issue do Jira
- [ ] Feedback de sucesso ao usuário: "Feedback enviado com sucesso! Referência: PROJ-123"
- [ ] Exibir a chave da issue do Jira criada na confirmação
- [ ] Histórico de feedbacks enviados pelo usuário (listagem simples)
- [ ] Admin pode ver todos os feedbacks enviados no painel admin

### US-036.1: Configuração da integração Jira (Admin)

**Como** um Admin, **quero** configurar a integração com o Jira **para** que os feedbacks sejam enviados ao projeto correto.

**Acceptance Criteria:**

- [ ] Tela de configuração no painel admin com campos:
    - URL do Jira (ex: `https://empresa.atlassian.net`)
    - Email da conta de serviço
    - API Token
    - Chave do projeto (ex: `CLAR`)
    - Tipo de issue para bugs (ex: `Bug`)
    - Tipo de issue para sugestões (ex: `Story` ou `Task`)
- [ ] Validação de conexão: botão "Testar conexão" que verifica se as credenciais funcionam
- [ ] Credenciais armazenadas de forma segura (criptografadas no banco, nunca expostas na API)

---

## Módulo: NPS (Net Promoter Score)

### US-037: Formulário de NPS personalizável (Admin)

**Como** um Admin, **quero** criar e configurar formulários de NPS com perguntas personalizadas **para** medir a satisfação dos clientes de forma adaptada à necessidade.

**Acceptance Criteria:**

- [ ] Interface de criação de NPS com editor de perguntas (adicionar, remover, reordenar)
- [ ] Escala de nota de 0 a 10 como pergunta obrigatória padrão
- [ ] Campo de comentário aberto opcional configurável
- [ ] Perguntas adicionais customizáveis (texto livre, múltipla escolha)
- [ ] Pré-visualização do formulário antes de publicar

### US-038: NPS automático ao final de trilhas

**Como** um Admin, **quero** que o NPS seja disponibilizado automaticamente ao final de trilhas **para** capturar feedback no momento de maior engajamento.

**Acceptance Criteria:**

- [ ] Opção no cadastro/edição de trilha para vincular um NPS
- [ ] Ao concluir a última aula da trilha, exibir automaticamente o formulário de NPS
- [ ] Usuário pode pular o NPS (não obrigatório)
- [ ] Registrar que o NPS foi exibido mesmo se não respondido (tracking de exibição)

### US-039: NPS sob demanda com associação a eventos, aulas ou trilhas

**Como** um Admin, **quero** criar NPS sob demanda e associá-los a eventos, aulas ou trilhas específicas **para** coletar feedback direcionado.

**Acceptance Criteria:**

- [ ] Criar NPS avulso (não vinculado automaticamente a trilha)
- [ ] Associar NPS a: evento, aula ou trilha via select
- [ ] Listar NPS criados com filtro por tipo de associação e status (ativo/encerrado)
- [ ] Definir período de vigência (data início e fim)

### US-040: QR Code público para NPS

**Como** um Admin, **quero** gerar um QR Code público para um NPS **para** que respondentes possam acessar sem login.

**Acceptance Criteria:**

- [ ] Botão "Gerar QR Code" na tela de detalhes do NPS
- [ ] QR Code aponta para URL pública (sem autenticação)
- [ ] Página pública com formulário de NPS responsivo (mobile-first)
- [ ] Opção de copiar link público para compartilhamento
- [ ] Campos opcionais de identificação do respondente (nome, email) — não obrigatórios

### US-041: Dashboard de resultados do NPS (Admin)

**Como** um Admin, **quero** visualizar os resultados do NPS em uma área administrativa **para** acompanhar a satisfação e tomar decisões.

**Acceptance Criteria:**

- [ ] Score NPS calculado automaticamente: % Leais − % Detratores
- [ ] Segmentação visual por categoria: Leais (9-10), Neutros (7-8), Detratores (0-6)
- [ ] Gráfico de distribuição de notas
- [ ] Lista de comentários com filtro por segmento (Leais, Neutros, Detratores)
- [ ] Filtros por período, trilha, evento ou aula associada
- [ ] Exportação de resultados (CSV ou PDF)

### US-042: Transformar comentário do NPS em tarefa

**Como** um Admin, **quero** transformar comentários do NPS em tarefas no módulo de sprints **para** garantir que o feedback seja tratado.

**Acceptance Criteria:**

- [ ] Botão "Criar tarefa" ao lado de cada comentário do NPS
- [ ] Ao clicar, abre modal de criação de tarefa pré-preenchido com o comentário na descrição
- [ ] Campos disponíveis: título, descrição (pré-preenchida), sprint, responsável, prazo, poker points
- [ ] Tarefa criada aparece no board de sprints com origem identificada como "NPS"
- [ ] Link de referência entre a tarefa e o comentário original do NPS
