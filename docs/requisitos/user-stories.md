# User Stories

## Modulo: Autenticacao e Gestao de Usuarios

### US-001: Login de usuarios

**Como** um usuario (Admin ou Cliente), **quero** fazer login na plataforma **para** acessar as funcionalidades correspondentes ao meu perfil.

- [x] Tela de login com campos email e senha
- [x] Botao "Entrar com Google" para autenticacao via Google OAuth
- [x] Autenticacao segura com JWT
- [x] Redirecionamento para dashboard apos login bem-sucedido
- [x] Mensagem de erro clara para credenciais invalidas
- [x] Opcao "Esqueci minha senha" com recuperacao por email
- [x] Usuario que faz login com Google deve estar pre-cadastrado

### US-002: Cadastro de escolas (Admin)

**Como** um Admin, **quero** cadastrar novas escolas clientes **para** gerenciar seus contratos na plataforma.

- [ ] Formulario com: nome, endereco, logo, tipo de contrato, data inicio
- [ ] Para Start: duracao de 3 meses + campo para selecionar pilar de atuacao
- [ ] Para Corp: campo adicional para setor foco
- [ ] Upload de logo da escola
- [ ] Validacao de campos obrigatorios

### US-003: Cadastro de usuarios (Admin)

**Como** um Admin, **quero** cadastrar usuarios vinculados a uma escola **para** que possam acessar a plataforma.

- [ ] Formulario com: nome, email, cargo, escola vinculada
- [ ] Email de boas-vindas enviado automaticamente
- [ ] Admin pode editar ou desativar usuarios

### US-004: Listagem e gestao de escolas (Admin)

**Como** um Admin, **quero** visualizar todas as escolas cadastradas **para** acompanhar o status dos contratos.

- [ ] Lista com: nome, logo, tipo de contrato, nota atual, status
- [ ] Filtros por tipo de contrato, status, nota
- [ ] Busca por nome
- [ ] Click na escola abre dashboard dela

---

## Modulo: Dashboard/Home

### US-005: Dashboard principal

**Como** um Cliente, **quero** ver o dashboard da minha escola **para** entender rapidamente minha situacao.

- [ ] Header com logo e nome/endereco da escola
- [ ] Carrossel de banners com eventos e avisos
- [ ] Secao "Pilares que sustentam a escola" com 5 pilares clicaveis
- [ ] Card do ultimo diagnostico com nota geral
- [ ] Secao de videos e ferramentas recomendados

### US-006: Selecao de pilar para detalhamento

**Como** um Cliente, **quero** clicar em um pilar **para** ver videos e ferramentas relacionados.

- [ ] Pilares com icones distintos
- [ ] Pilar selecionado fica destacado
- [ ] Secoes de videos e ferramentas filtram pelo pilar

### US-007: Gestao de banners (Admin)

**Como** um Admin, **quero** gerenciar banners do carrossel **para** comunicar eventos e novidades.

- [ ] CRUD completo de banners
- [ ] Upload de imagem, titulo, link, periodo de exibicao
- [ ] Ordenacao drag and drop

---

## Modulo: Diagnostico

### US-008: Aplicacao do diagnostico

**Como** um Cliente, **quero** responder o diagnostico gerencial **para** identificar as lacunas da minha escola.

- [ ] Organizado por pilares (5 pilares)
- [ ] Cada pilar tem multiplos eixos com perguntas
- [ ] Escala de 1 a 5 niveis de maturidade
- [ ] Barra de progresso
- [ ] Salvar automaticamente respostas parciais
- [ ] Perguntas diferentes por tipo de contrato
- [ ] So pode ser preenchido junto com o admin

### US-009: Resultados do diagnostico

**Como** um Cliente, **quero** ver os resultados **para** entender onde preciso melhorar.

- [ ] Nota geral (media ponderada)
- [ ] Grafico radar por pilar
- [ ] Detalhamento por pilar e eixo
- [ ] Indicacao visual de areas criticas
- [ ] Exportar PDF

### US-010: Historico de diagnosticos

**Como** um Cliente, **quero** ver o historico **para** acompanhar minha evolucao trimestral.

- [ ] Dropdown para selecionar diagnostico anterior
- [ ] Grafico de evolucao ao longo do tempo
- [ ] Comparativo entre diagnostico atual e anterior

### US-011: Geracao do plano de acao

**Como** um Cliente, **quero** que o sistema gere um plano de acao **para** saber o que preciso fazer.

- [ ] Gerado automaticamente apos finalizar diagnostico
- [ ] Organizado por pilar e eixo
- [ ] Cada item mostra ferramentas e aulas sugeridas
- [ ] Priorizados por nota (piores = maior prioridade)
- [ ] Admin pode editar/ajustar

### US-012: Acompanhamento do plano de acao

**Como** um Cliente, **quero** acompanhar e marcar itens como concluidos **para** registrar meu progresso.

- [ ] Lista com checkbox de conclusao
- [ ] Ferramentas e aulas sugeridas com acesso rapido
- [ ] Para Start: itens fora do pilar aparecem bloqueados
- [ ] Barra de progresso geral

### US-013: Configuracao do diagnostico (Admin)

**Como** um Admin, **quero** configurar perguntas e eixos **para** manter a metodologia atualizada sem desenvolvedor.

- [ ] Interface visual de edicao (form builder)
- [ ] CRUD de pilares, eixos e perguntas
- [ ] Editor inline para textos
- [ ] Definir niveis 1-5 por pergunta
- [ ] Marcar targetAudience (Clube, Corp, Start, Ambos)
- [ ] Abas por tipo de contrato
- [ ] Drag and drop para reordenar
- [ ] Versionamento (nao afeta diagnosticos respondidos)

---

## Modulo: Ferramentas

### US-014: Listagem de ferramentas

**Como** um Cliente, **quero** ver ferramentas disponiveis **para** escolher qual utilizar.

- [ ] Grid de cards com icone, nome, pilar, tipo
- [ ] Indicador se esta no plano de acao
- [ ] Filtros por pilar e tipo

### US-015: Ferramenta tipo Template

**Como** um Cliente, **quero** preencher um template **para** documentar informacoes da minha escola.

- [ ] Campos conforme estrutura (textos, selects, tabelas)
- [ ] Salvar automaticamente
- [ ] Exportar PDF
- [ ] Versionamento com historico

### US-016: Ferramenta tipo Score

**Como** um Cliente, **quero** preencher uma auto-avaliacao **para** obter uma nota.

- [ ] Formulario com escala de resposta
- [ ] Calculo automatico do score
- [ ] Interpretacao do resultado
- [ ] Historico de scores

### US-017: Ferramenta tipo Checklist

**Como** um Cliente, **quero** usar um checklist **para** acompanhar execucao de um processo.

- [ ] Lista com checkbox
- [ ] Agrupamento em secoes
- [ ] Barra de progresso
- [ ] Exportar PDF

---

## Modulo: E-Learning

### US-019: Trilhas por pilar

**Como** um Cliente, **quero** acessar videos por pilar **para** aprender sobre temas que preciso melhorar.

- [ ] Menu com 5 pilares
- [ ] Indicador de video assistido
- [ ] Barra de progresso da trilha

### US-020: Trilhas por cluster

**Como** um Cliente, **quero** filtrar por tamanho de escola **para** ver conteudos relevantes.

- [ ] Filtro: "Ate 300", "300-500", "500-1000", "1000+"
- [ ] Por padrao, mostra conteudo do cluster do cliente

### US-021: Player de video

- [x] Player com streaming HTTP Range
- [x] Controles padrao
- [x] Marcar como assistido ao completar 90%
- [x] Progresso salvo (continuar de onde parou)
- [x] Protecao anti-gravacao

### US-022: Gestao de videos e trilhas (Admin)

- [x] CRUD de videos com upload drag-and-drop
- [x] Streaming com HTTP Range
- [x] CRUD de trilhas com ordenacao

---

## Modulo: Documentos

### US-026: Envio de documentos por pilar

**Como** um Cliente, **quero** enviar documentos organizados por pilar e categoria.

- [ ] Documentos organizados por pilar
- [ ] Categorias configuraveis pelo Admin
- [ ] Upload de multiplos documentos por categoria
- [ ] Formatos: PDF, XLSX, DOCX, PNG, JPG
- [ ] Indicador de status: pendente, enviado, aprovado
- [ ] Historico de envios

### US-027: Gestao de categorias (Admin)

- [ ] CRUD de categorias vinculadas a pilares
- [ ] Ativar/desativar categorias
- [ ] Visualizar status de envio por escola

### US-028: Controle de acesso a documentos (Admin)

- [x] Tabela many-to-many usuario_categorias
- [x] Tabela vazia = acesso irrestrito
- [x] Admin sempre ve todos os documentos
- [x] Filtragem server-side

---

## Modulo: Tarefas e Sprints

### US-029: Gestao de Sprints (Admin)

- [x] CRUD de sprints por escola
- [x] Sprint pode ser fechada (tarefas ficam read-only)
- [x] Dropdown searchable de sprints

### US-030: Board de Tarefas

- [x] Kanban (3 colunas com drag-and-drop)
- [x] Lista (tabela com header sticky)
- [x] Calendario (grid mensal)

### US-031: Filtros do Board

- [x] Filtro por origem, status e responsavel
- [x] Filtros aplicam em todas as views

### US-032: CRUD de Tarefas

- [x] Criar com titulo, descricao, sprint, responsavel, prazo, poker points
- [x] Modal de edicao com subtarefas
- [x] Sprint fechada: campos read-only

### US-033: Responsaveis

- [x] Dropdown inclui usuarios da escola + admins
- [x] Admins podem ser atribuidos a qualquer escola

### US-034: Analytics de Sprints

- [x] Grafico de velocidade por sprint
- [x] Grafico de pontos por pessoa
- [x] Card de capacidade com metricas

### US-035: Integracao com Dashboard

- [x] Calendario do dashboard mostra tarefas de sprint e plano CLA
