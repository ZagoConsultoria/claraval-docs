# Jornadas de Usuario

## 1. Primeiro Acesso

```mermaid
sequenceDiagram
    participant A as Admin
    participant S as Sistema
    participant U as Novo Usuario

    A->>S: Cadastra usuario (nome, email, escola)
    S->>U: Envia email de boas-vindas
    U->>S: Clica no link do email
    S->>U: Tela de completar perfil (definir senha)
    U->>S: Define senha
    S->>U: Redireciona para dashboard
```

## 2. Login

```mermaid
flowchart TD
    A[Tela de Login] --> B{Metodo}
    B -->|Email/Senha| C[POST /auth/login]
    B -->|Google OAuth| D[Google OAuth Flow]
    D --> E[Recebe id_token]
    E --> F[POST /auth/google]
    C --> G{Sucesso?}
    F --> G
    G -->|Sim| H[Salva tokens no localStorage]
    H --> I[Redireciona para Dashboard]
    G -->|Nao| J[Exibe mensagem de erro]
```

## 3. Diagnostico de Maturidade

```mermaid
flowchart TD
    A[Admin inicia diagnostico] --> B[Carrega pilares e perguntas]
    B --> C[Filtra por targetAudience]
    C --> D[Exibe formulario por pilar]
    D --> E{Para cada pergunta}
    E --> F[Seleciona nivel 1-5]
    F --> G[Auto-save da resposta]
    G --> E
    E -->|Completo| H[Botao Finalizar]
    H --> I[Backend calcula notas]
    I --> J[Gera plano de acao via templates]
    J --> K[Exibe resultados + radar chart]
```

## 4. E-Learning

```mermaid
flowchart TD
    A[Pagina E-Learning] --> B[Lista trilhas]
    B --> C{Contrato Start?}
    C -->|Sim| D[Mostra trilhas do pilar + bloqueadas com cadeado]
    C -->|Nao| E[Mostra todas as trilhas]
    D --> F[Seleciona trilha]
    E --> F
    F --> G[Lista videos da trilha]
    G --> H[Seleciona video]
    H --> I[Player HLS]
    I --> J[Salva progresso automaticamente]
    J --> K{Progresso >= 90%?}
    K -->|Sim| L[Marca como ASSISTIDO]
    K -->|Nao| M[Salva como EM_ANDAMENTO]
```

## 5. Tarefas e Sprints

```mermaid
flowchart TD
    A[Admin cria Sprint] --> B[Define nome, datas, tamanho]
    B --> C[Board de Tarefas]
    C --> D{Visualizacao}
    D -->|Kanban| E[3 colunas: A Fazer, Fazendo, Concluido]
    D -->|Lista| F[Tabela com filtros]
    D -->|Calendario| G[Grid mensal]
    E --> H[Drag-and-drop muda status]
    F --> I[Click abre modal de edicao]
    G --> I
    H --> J[Analytics atualizam]
    I --> J
```

## 6. Fluxo Admin — Gestao de Conteudo

```mermaid
flowchart LR
    A[Painel Admin] --> B[Escolas]
    A --> C[Usuarios]
    A --> D[Diagnostico Config]
    A --> E[Videos e Trilhas]
    A --> F[Templates Plano]
    A --> G[Banners]
    A --> H[Eventos]
    A --> I[Documentos]
    A --> J[Relatorios]
    A --> K[Live]
    A --> L[Configuracoes]
```

## 7. Ciclo de Trabalho da Consultoria

```mermaid
flowchart TD
    A[Nova Escola] --> B[Cadastro + Contrato]
    B --> C[Diagnostico Inicial]
    C --> D[Plano de Acao Gerado]
    D --> E[Sprints Semanais/Quinzenais]
    E --> F[Mentorias + Ferramentas]
    F --> G{Fim do Trimestre?}
    G -->|Sim| H[Novo Diagnostico]
    H --> I[Comparativo de Evolucao]
    I --> E
    G -->|Nao| E
```

<!-- TODO: Screenshots das telas principais de cada jornada — ajuda muito na contextualizacao visual para novos devs -->
