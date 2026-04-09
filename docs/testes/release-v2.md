# Casos de Teste — Release v2.0

## Visão Geral

| Módulo | Funcionalidades | User Stories | Requisitos Funcionais |
|--------|----------------|--------------|----------------------|
| Tarefas | Edição inline na lista, modal com clonagem | US-032 | — |
| Feedback | FAB de feedback, integração Jira | US-036, US-036.1 | FR-51 a FR-60 |
| NPS | Formulário, dashboard, QR Code, tarefas | US-037 a US-042 | FR-61 a FR-68 |
| Diagnóstico Comparativo | Radar benchmark/evolução, deltas por pilar | US-009 | FR-10.7 |

**Convenção de IDs**: `CT-{módulo}-{nnn}` — TAR (Tarefas), FDB (Feedback), NPS, DGC (Diagnóstico Comparativo)

---

## 1. Módulo Tarefas

### 1.1 Edição Inline na Visão de Lista

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-TAR-001 | Ativar edição de nome da tarefa | Usuário na visão de lista com sprint aberta | 1. Clicar no nome de uma tarefa na lista | Célula entra em modo de edição com borda gold, texto selecionável e ícone de lápis desaparece |
| CT-TAR-002 | Salvar nome editado com Enter | Célula de nome em modo de edição | 1. Alterar o texto do nome 2. Pressionar Enter | Nome é salvo, célula volta ao modo read-only com o novo valor |
| CT-TAR-003 | Cancelar edição com Esc | Célula de nome em modo de edição | 1. Alterar o texto do nome 2. Pressionar Esc | Célula volta ao modo read-only com o valor original (sem salvar) |
| CT-TAR-004 | Navegar entre células com Tab | Célula de nome em modo de edição | 1. Pressionar Tab | Foco move para a próxima célula editável da mesma linha (Responsável) |
| CT-TAR-005 | Editar responsável via dropdown | Usuário na visão de lista | 1. Clicar na célula de responsável | Dropdown abre com lista de usuários da escola + admins |
| CT-TAR-006 | Selecionar responsável | Dropdown de responsável aberto | 1. Selecionar um usuário da lista | Responsável é atualizado, dropdown fecha, avatar/nome exibido na célula |
| CT-TAR-007 | Editar poker points via dropdown | Usuário na visão de lista | 1. Clicar na célula de poker | Dropdown abre com opções de pontos (1, 2, 3, 5, 8, 13, 21) |
| CT-TAR-008 | Editar status via dropdown | Usuário na visão de lista | 1. Clicar na célula de status | Dropdown abre com opções: A_FAZER, FAZENDO, CONCLUIDO |
| CT-TAR-009 | Alterar status para CONCLUIDO | Dropdown de status aberto | 1. Selecionar CONCLUIDO | Badge de status atualiza com cor verde e texto "Concluído" |
| CT-TAR-010 | Editar prazo via date picker | Usuário na visão de lista | 1. Clicar na célula de prazo | Date picker abre para seleção de data |
| CT-TAR-011 | Indicador hover em célula editável | Usuário na visão de lista | 1. Passar o mouse sobre uma célula editável | Ícone de lápis aparece indicando que a célula é editável |
| CT-TAR-012 | Sprint fechada impede edição | Usuário na visão de lista com sprint fechada selecionada | 1. Clicar em qualquer célula | Célula não entra em modo de edição, campos ficam read-only |
| CT-TAR-013 | Salvar edição ao clicar fora | Célula de nome em modo de edição com texto alterado | 1. Clicar fora da célula (blur) | Nome é salvo automaticamente, célula volta ao modo read-only |

### 1.2 Modal de Tarefa e Clonagem

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-TAR-014 | Abrir modal de tarefa | Usuário na visão de lista ou kanban | 1. Clicar no título da tarefa (link) | Modal abre em dois painéis: conteúdo à esquerda, detalhes à direita |
| CT-TAR-015 | Editar título no modal | Modal de tarefa aberto | 1. Clicar no título 2. Alterar texto 3. Clicar fora | Título é atualizado |
| CT-TAR-016 | Editar descrição no modal | Modal de tarefa aberto | 1. Clicar na descrição 2. Alterar texto com toolbar rich text 3. Clicar fora | Descrição é salva |
| CT-TAR-017 | Alterar campos do sidebar | Modal de tarefa aberto | 1. Alterar Status, Responsável, Sprint, Prazo, Poker ou Prioridade no painel direito | Campo é atualizado e reflete na listagem ao fechar o modal |
| CT-TAR-018 | Adicionar subtarefa | Modal de tarefa aberto | 1. Clicar em "Adicionar subtarefa" 2. Digitar título 3. Confirmar | Subtarefa aparece na lista com checkbox, barra de progresso atualiza |
| CT-TAR-019 | Marcar subtarefa como concluída | Modal com subtarefas existentes | 1. Clicar no checkbox de uma subtarefa | Subtarefa riscada, barra de progresso atualiza percentual |
| CT-TAR-020 | Duplicar tarefa | Modal de tarefa aberto | 1. Clicar no botão "Duplicar" | Nova tarefa criada com prefixo "[CÓPIA]" no título, toast de confirmação exibido, todos os campos copiados exceto status (volta para A_FAZER) |
| CT-TAR-021 | Duplicar tarefa preserva subtarefas | Modal de tarefa com subtarefas | 1. Clicar no botão "Duplicar" | Tarefa clonada inclui mesmas subtarefas (todas desmarcadas) |
| CT-TAR-022 | Fechar modal com Esc | Modal de tarefa aberto | 1. Pressionar Esc | Modal fecha, alterações já salvas persistem |
| CT-TAR-023 | Fechar modal clicando no overlay | Modal de tarefa aberto | 1. Clicar fora do modal (no overlay) | Modal fecha |
| CT-TAR-024 | Modal em sprint fechada | Sprint fechada selecionada | 1. Abrir modal de uma tarefa | Todos os campos exibidos como read-only, botão "Duplicar" desabilitado |
| CT-TAR-025 | Criar nova tarefa via modal | Usuário logado com sprint aberta | 1. Clicar em "Nova tarefa" 2. Preencher título e campos 3. Salvar | Tarefa criada aparece na listagem e no kanban |
| CT-TAR-026 | Adicionar comentário | Modal de tarefa aberto | 1. Digitar comentário no campo 2. Clicar "Enviar" | Comentário aparece na lista com nome do autor e timestamp |

---

## 2. Módulo Feedback

### 2.1 Botão Flutuante (FAB)

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-FDB-001 | FAB visível em todas as páginas | Usuário autenticado em qualquer página | 1. Navegar por diferentes páginas da plataforma | Botão flutuante com ícone de megafone visível no canto inferior direito (56px, cor gold) com animação de pulse |
| CT-FDB-002 | Abrir drawer de feedback | FAB visível | 1. Clicar no FAB | Drawer desliza de baixo para cima (420px de largura) com formulário de feedback |
| CT-FDB-003 | Fechar drawer clicando no X | Drawer de feedback aberto | 1. Clicar no botão de fechar (X) | Drawer fecha com animação de slide-down |
| CT-FDB-004 | Fechar drawer clicando fora | Drawer de feedback aberto | 1. Clicar fora do drawer | Drawer fecha |
| CT-FDB-005 | Tooltip no hover do FAB | FAB visível | 1. Passar o mouse sobre o FAB | Tooltip "Enviar feedback" aparece |

### 2.2 Formulário de Feedback

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-FDB-006 | Selecionar tipo Bug | Drawer aberto | 1. Clicar no toggle "Bug" | Toggle marca "Bug" como selecionado com estilo ativo |
| CT-FDB-007 | Selecionar tipo Sugestão | Drawer aberto | 1. Clicar no toggle "Sugestão" | Toggle marca "Sugestão" como selecionado com estilo ativo |
| CT-FDB-008 | Página atual capturada automaticamente | Drawer aberto em `/dashboard/diagnosticos` | 1. Verificar campo "Página" | Campo exibe `/dashboard/diagnosticos` como read-only, preenchido via `window.location.pathname` |
| CT-FDB-009 | Enviar sem título (validação) | Drawer aberto, campo título vazio | 1. Preencher descrição 2. Clicar "Enviar" | Mensagem de erro no campo título, formulário não enviado |
| CT-FDB-010 | Enviar sem descrição (validação) | Drawer aberto, campo descrição vazio | 1. Preencher título 2. Clicar "Enviar" | Mensagem de erro no campo descrição, formulário não enviado |
| CT-FDB-011 | Selecionar prioridade | Drawer aberto | 1. Alterar prioridade de MEDIA (default) para ALTA | Toggle marca "Alta" como selecionado |
| CT-FDB-012 | Upload de vídeo válido | Drawer aberto | 1. Clicar na área de upload 2. Selecionar arquivo MP4 | Nome do arquivo exibido na área de upload com opção de remover |
| CT-FDB-013 | Upload de vídeo formato inválido | Drawer aberto | 1. Tentar upload de arquivo .exe | Arquivo rejeitado, mensagem de erro indicando formatos aceitos (MP4, MOV, WebM) |
| CT-FDB-014 | Remover vídeo anexado | Vídeo anexado ao formulário | 1. Clicar no botão de remover vídeo | Área de upload volta ao estado inicial |
| CT-FDB-015 | Envio com sucesso | Formulário preenchido corretamente | 1. Preencher tipo, título, descrição 2. Clicar "Enviar" | Estado de loading aparece, depois tela de sucesso com mensagem "Feedback enviado!" e chave Jira (ex: `CLAR-147`) |
| CT-FDB-016 | Metadados capturados automaticamente | Usuário autenticado | 1. Enviar feedback | Payload inclui: userId, nome, email, escola, role, browser/user-agent, URL da página |
| CT-FDB-017 | Enviar novo feedback após sucesso | Tela de sucesso exibida | 1. Clicar "Enviar outro" | Formulário reseta para estado inicial, todos os campos limpos |

### 2.3 Integração Jira e Admin

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-FDB-018 | Issue criada no Jira | Feedback enviado com sucesso | 1. Verificar projeto Jira configurado | Issue criada com título, descrição, tipo correspondente (Bug ou Story/Task), metadados no corpo |
| CT-FDB-019 | Vídeo anexado como attachment no Jira | Feedback com vídeo enviado | 1. Verificar issue criada no Jira | Vídeo aparece como attachment na issue (header `X-Atlassian-Token: no-check`) |
| CT-FDB-020 | Configuração Jira (Admin) | Admin logado no painel admin | 1. Acessar configuração de integração Jira 2. Preencher URL, email, API token, projeto, tipos de issue | Configuração salva com sucesso, credenciais criptografadas |
| CT-FDB-021 | Testar conexão Jira | Configuração Jira preenchida | 1. Clicar "Testar conexão" | Feedback visual: sucesso (conexão OK) ou erro (credenciais inválidas) |
| CT-FDB-022 | Admin visualiza todos os feedbacks | Admin logado | 1. Acessar lista de feedbacks | Lista exibe todos os feedbacks de todos os usuários com filtros |
| CT-FDB-023 | Cliente visualiza apenas próprios feedbacks | Cliente logado | 1. Acessar lista de feedbacks | Lista exibe apenas feedbacks enviados pelo próprio usuário |

---

## 3. Módulo NPS

### 3.1 Criação e Configuração (Admin)

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-001 | Criar NPS com perguntas padrão | Admin logado | 1. Acessar criação de NPS 2. Definir título | NPS criado com pergunta obrigatória de nota (0-10) e campo de comentário |
| CT-NPS-002 | Adicionar pergunta customizada | NPS em edição | 1. Clicar "Adicionar pergunta" 2. Definir tipo (texto livre ou múltipla escolha) 3. Preencher enunciado | Pergunta adicionada à lista com opção de reordenar |
| CT-NPS-003 | Remover pergunta customizada | NPS com perguntas adicionais | 1. Clicar no botão remover de uma pergunta | Pergunta removida da lista |
| CT-NPS-004 | Reordenar perguntas | NPS com múltiplas perguntas | 1. Arrastar pergunta para nova posição | Ordem atualizada |
| CT-NPS-005 | Pré-visualizar formulário | NPS configurado | 1. Clicar "Pré-visualizar" | Preview do formulário como o respondente verá |
| CT-NPS-006 | Vincular NPS a trilha | NPS em edição | 1. Selecionar trilha no campo de associação | NPS vinculado, será exibido ao final da trilha |
| CT-NPS-007 | Criar NPS sob demanda | Admin logado | 1. Criar NPS 2. Associar a evento/aula/trilha 3. Definir período de vigência | NPS criado com datas de início e fim, listado com status "Ativo" |
| CT-NPS-008 | Listar NPS com filtros | Admin logado com NPS existentes | 1. Acessar lista de NPS 2. Filtrar por tipo de associação e status | Lista filtrada corretamente |

### 3.2 QR Code

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-009 | Gerar QR Code | NPS criado e ativo | 1. Clicar "Gerar QR Code" na tela de detalhes | Modal exibe QR Code e URL pública copiável |
| CT-NPS-010 | Copiar link público | Modal de QR Code aberto | 1. Clicar "Copiar link" | URL copiada para clipboard, feedback visual de confirmação |
| CT-NPS-011 | Acessar NPS via QR Code sem login | Usuário não autenticado | 1. Escanear QR Code ou acessar URL pública | Formulário de NPS exibe corretamente sem exigir autenticação |

### 3.3 Formulário Público (Respondente)

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-012 | Selecionar nota na escala 0-10 | Formulário público aberto | 1. Clicar em um número de 0 a 10 | Número selecionado com destaque visual; cores: vermelho (0-6), amarelo (7-8), verde (9-10) |
| CT-NPS-013 | Enviar NPS apenas com nota | Nota selecionada | 1. Clicar "Enviar" | NPS registrado com sucesso, tela de agradecimento exibida |
| CT-NPS-014 | Enviar NPS com comentário | Nota selecionada, comentário preenchido | 1. Preencher comentário 2. Clicar "Enviar" | NPS registrado com nota e comentário |
| CT-NPS-015 | Enviar sem selecionar nota (validação) | Formulário aberto, nenhuma nota selecionada | 1. Clicar "Enviar" | Mensagem de erro solicitando seleção de nota |
| CT-NPS-016 | Identificação opcional | Formulário público aberto | 1. Preencher nome e email (opcionais) 2. Enviar | NPS registrado com dados de identificação |
| CT-NPS-017 | Formulário responsivo (mobile) | Acesso via dispositivo móvel | 1. Abrir URL pública no celular | Layout adapta corretamente (mobile-first), botões de nota acessíveis |
| CT-NPS-018 | Pergunta de follow-up condicional | Nota selecionada | 1. Selecionar nota entre 0-6 | Pergunta adicional aparece: "O que podemos melhorar?" |

### 3.4 NPS Automático em Trilhas

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-019 | NPS exibido ao final da trilha | Trilha com NPS vinculado, usuário concluiu última aula | 1. Concluir a última aula da trilha | Formulário de NPS exibido automaticamente |
| CT-NPS-020 | Pular NPS da trilha | NPS automático exibido | 1. Clicar "Pular" ou fechar | NPS não respondido, mas exibição registrada (tracking) |

### 3.5 Dashboard de Resultados (Admin)

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-021 | Exibir score NPS | NPS com respostas registradas | 1. Acessar dashboard do NPS | Score exibido corretamente: % Leais − % Detratores (ex: +42) |
| CT-NPS-022 | Segmentação por categoria | NPS com respostas variadas | 1. Verificar barra de segmentação | Barra exibe proporção: Leais (9-10) em verde, Neutros (7-8) em amarelo, Detratores (0-6) em vermelho |
| CT-NPS-023 | Filtrar comentários por segmento | Dashboard com comentários | 1. Clicar na aba "Detratores" | Lista exibe apenas comentários de respondentes com nota 0-6 |
| CT-NPS-024 | Filtrar por período | Dashboard com respostas em datas variadas | 1. Selecionar intervalo de datas | Resultados e score recalculados para o período selecionado |
| CT-NPS-025 | Exportar resultados | Dashboard com dados | 1. Clicar "Exportar" 2. Selecionar formato (CSV ou PDF) | Arquivo gerado com dados completos do NPS |

### 3.6 Comentário para Tarefa

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-NPS-026 | Criar tarefa a partir de comentário | Dashboard NPS com comentários | 1. Clicar "Criar tarefa" ao lado de um comentário | Modal de criação de tarefa abre com descrição pré-preenchida com o comentário do NPS |
| CT-NPS-027 | Tarefa criada com origem NPS | Modal de tarefa pré-preenchido | 1. Definir sprint, responsável, prazo 2. Salvar | Tarefa criada aparece no board com badge de origem "NPS" |
| CT-NPS-028 | Link entre tarefa e comentário | Tarefa criada a partir de NPS | 1. Abrir tarefa no board | Referência ao comentário original do NPS visível na tarefa |

---

## 4. Módulo Diagnóstico Comparativo

### 4.1 Hero com Comparativo

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-DGC-001 | Exibir nota geral com ScoreCircle | Diagnóstico finalizado | 1. Acessar página de resultados | ScoreCircle (120px) exibe nota geral com animação SVG, cor gold |
| CT-DGC-002 | Badge comparativo — nota subiu | Diagnóstico atual com nota > anterior | 1. Verificar badge ao lado do score | Badge verde com texto "+X.X vs anterior (Y.Y)" e ícone de seta para cima |
| CT-DGC-003 | Badge comparativo — nota caiu | Diagnóstico atual com nota < anterior | 1. Verificar badge ao lado do score | Badge vermelho com texto "-X.X vs anterior (Y.Y)" e ícone de seta para baixo |
| CT-DGC-004 | Badge comparativo — sem diagnóstico anterior | Primeiro diagnóstico da escola | 1. Verificar área do badge | Badge não exibido ou texto "Primeiro diagnóstico" |

### 4.2 Gráfico Radar

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-DGC-005 | Modo "Evolução própria" (padrão) | Página de resultados carregada | 1. Verificar radar chart | Radar exibe dois datasets: "Atual" (gold, preenchido) e "Anterior" (cinza, tracejado) com notas por pilar |
| CT-DGC-006 | Alternar para modo "Benchmark cluster" | Radar em modo Evolução | 1. Clicar toggle "Benchmark cluster" | Radar atualiza para dois datasets: "Sua Escola" (gold) e "Média Cluster" (azul), sem linha Meta (4.0) |
| CT-DGC-007 | Alternar de volta para "Evolução própria" | Radar em modo Benchmark | 1. Clicar toggle "Evolução própria" | Radar volta a exibir datasets Atual vs Anterior |
| CT-DGC-008 | Radar sem Meta (4.0) | Qualquer modo do radar | 1. Verificar datasets do gráfico | Nenhuma linha de "Meta (4.0)" presente no gráfico em nenhum modo |
| CT-DGC-009 | Tooltip no hover dos pontos | Radar exibido | 1. Passar mouse sobre um ponto do radar | Tooltip exibe nome do pilar e nota do dataset |
| CT-DGC-010 | Escala do radar 0 a 5 | Radar exibido | 1. Verificar eixos do radar | Escala vai de 0 a 5 com incrementos de 1 |

### 4.3 Detalhamento por Pilar

| ID | Cenário | Pré-condições | Passos | Resultado Esperado |
|----|---------|---------------|--------|-------------------|
| CT-DGC-011 | Exibir pilares com accordion | Página de resultados carregada | 1. Verificar seção de pilares | 5 pilares listados como cards accordion com: nome, ícone, nota, level badge, barra de progresso |
| CT-DGC-012 | Level badge correto | Pilar com nota 4.6 | 1. Verificar badge do pilar | Badge exibe "Excelente" (nota >= 4.5) |
| CT-DGC-013 | Delta por pilar — positivo | Pilar com nota atual > anterior | 1. Verificar delta no header do pilar | Texto verde minimalista "+X.X ↑" |
| CT-DGC-014 | Delta por pilar — negativo | Pilar com nota atual < anterior | 1. Verificar delta no header do pilar | Texto vermelho minimalista "-X.X ↓" |
| CT-DGC-015 | Expandir pilar — eixos | Pilar fechado (accordion) | 1. Clicar no pilar | Accordion expande mostrando eixos com: nome, nota, quantidade de perguntas, delta minimalista |
| CT-DGC-016 | Delta por eixo | Pilar expandido | 1. Verificar delta nos eixos | Cada eixo exibe delta verde (subiu) ou vermelho (caiu) em tamanho reduzido |
| CT-DGC-017 | Cores distintas por pilar | Todos os pilares visíveis | 1. Verificar cores dos pilares | Cada pilar usa sua cor: Estratégia (âmbar), Processos (azul), Experiência (rosa), Pessoas (verde), Resultados (índigo) |

---

## Resumo de Cobertura

| Módulo | Casos de Teste | Requisitos Cobertos |
|--------|---------------|-------------------|
| Tarefas — Edição Inline | 13 | US-032 (edição inline) |
| Tarefas — Modal e Clonagem | 13 | US-032 (clonagem) |
| Feedback — FAB | 5 | FR-51 |
| Feedback — Formulário | 12 | FR-52, FR-52.1, FR-53, FR-54, FR-57 |
| Feedback — Jira e Admin | 6 | FR-55, FR-56, FR-58, FR-59, FR-60 |
| NPS — Configuração | 8 | FR-61, FR-63 |
| NPS — QR Code | 3 | FR-64 |
| NPS — Formulário Público | 7 | FR-67, FR-67.1, FR-67.2, FR-67.3 |
| NPS — Trilhas | 2 | FR-62 |
| NPS — Dashboard | 5 | FR-65, FR-68 |
| NPS — Comentário → Tarefa | 3 | FR-66 |
| Diagnóstico — Hero | 4 | US-009 |
| Diagnóstico — Radar | 6 | FR-10.7 |
| Diagnóstico — Pilares | 7 | US-009 |
| **Total** | **94** | |
