# Portfolio.Dev — Referências visuais e fluxogramas

Este documento reúne os exemplos visuais inicialmente propostos para o Portfolio.Dev. Os mockups são conceituais e deverão orientar a implementação, não impor medidas rígidas aos componentes.

## 1. Página pública

![Mockup conceitual da página pública](assets/mockup-site-publico.svg)

### Elementos demonstrados

- navegação superior;
- Hero com posicionamento profissional e chamadas para ação;
- espaço reservado para fotografia ou avatar;
- cards de tecnologias por categoria;
- projetos apresentados como estudos de caso;
- tema escuro e destaque azul.

## 2. Painel administrativo

![Mockup conceitual do painel administrativo](assets/mockup-painel-admin.svg)

### Elementos demonstrados

- menu lateral;
- indicadores principais;
- atalhos de cadastro;
- tabela de projetos;
- status de publicação;
- mensagens recentes;
- estrutura preparada para os CRUDs.

## 3. Arquitetura geral

```mermaid
flowchart LR
    U[Usuário] --> R[React]
    R --> A[API ASP.NET Core]
    A --> D[(SQL Server)]
    A --> B[Blob Storage]
    A --> G[GitHub API]
```

## 4. Organização do back-end

```mermaid
flowchart TD
    API[PortfolioDev.Api] --> APP[PortfolioDev.Application]
    API --> INFRA[PortfolioDev.Infrastructure]
    INFRA --> APP
    INFRA --> DOMAIN[PortfolioDev.Domain]
    APP --> DOMAIN
    TESTS[PortfolioDev.Tests] --> APP
    TESTS --> DOMAIN
```

### Regra de dependência

O domínio fica no centro e não depende das outras camadas. A infraestrutura implementa os acessos externos definidos pela aplicação, enquanto a API recebe e devolve requisições HTTP.

## 5. Fluxo público de navegação

```mermaid
flowchart TD
    H[Home] --> S[Sobre mim]
    S --> T[Tecnologias]
    T --> E[Experiência]
    E --> P[Projetos]
    P --> C[Certificados]
    C --> F[Contato]
```

Ao selecionar um projeto:

```mermaid
flowchart LR
    C[Card do projeto] --> D[Detalhes]
    D --> A[Arquitetura]
    D --> R[Repositório]
    D --> M[Demonstração]
```

## 6. Fluxo de autenticação JWT

```mermaid
sequenceDiagram
    actor Admin
    participant Web as Painel React
    participant API as API ASP.NET Core
    participant DB as SQL Server
    Admin->>Web: Informa e-mail e senha
    Web->>API: POST /api/auth/login
    API->>DB: Consulta o administrador
    DB-->>API: Usuário e hash da senha
    API-->>Web: Token JWT
    Web->>API: Requisição com Bearer Token
    API-->>Web: Recurso protegido
```

O diagrama representa o fluxo conceitual. Senhas nunca serão armazenadas em texto puro.

## 7. Fluxo de cadastro de projeto

```mermaid
sequenceDiagram
    actor Admin
    participant Web as Painel React
    participant API as API ASP.NET Core
    participant Store as Arquivos
    participant DB as SQL Server
    Admin->>Web: Preenche o projeto
    Web->>API: Envia dados e imagem
    API->>Store: Salva a imagem
    Store-->>API: Retorna a URL
    API->>DB: Salva projeto e tecnologias
    DB-->>API: Confirma o cadastro
    API-->>Web: Retorna o projeto criado
```

## 8. Modelo relacional preliminar

Este modelo será detalhado na Etapa 10.

```mermaid
erDiagram
    USER ||--o{ PROJECT : administra
    PROJECT ||--o{ PROJECT_TECHNOLOGY : possui
    TECHNOLOGY ||--o{ PROJECT_TECHNOLOGY : classifica
    USER ||--o{ CERTIFICATE : administra
    USER ||--o{ EXPERIENCE : administra
    CONTACT }o--|| CONTACT_STATUS : possui
```

## 9. Fluxo de contato

```mermaid
flowchart TD
    V[Visitante preenche formulário] --> X{Dados válidos?}
    X -- Não --> E[Exibir validações]
    X -- Sim --> A[Enviar para API]
    A --> D[(Salvar no SQL Server)]
    D --> S[Exibir confirmação]
```

## 10. Pipeline de CI/CD

```mermaid
flowchart LR
    P[Push] --> B[Build]
    B --> T[Testes]
    T --> I[Imagem Docker]
    I --> D[Deploy Azure]
```

Em caso de falha no build ou nos testes, a publicação será interrompida.

## 11. Arquitetura de produção no Azure

```mermaid
flowchart TD
    U[Usuário] --> W[Front-end]
    W --> A[Azure App Service]
    A --> S[(Azure SQL)]
    A --> B[Azure Blob Storage]
    A --> O[Application Insights]
```

Os serviços definitivos e seus planos serão escolhidos durante a fase de cloud para evitar custos desnecessários.

## 12. Estados visuais obrigatórios

| Estado | Representação esperada |
|---|---|
| Carregando | Skeleton ou indicador discreto |
| Lista vazia | Mensagem explicativa e ação sugerida |
| Erro | Mensagem clara e opção de tentar novamente |
| Sucesso | Confirmação breve sem interromper a navegação |
| Sessão expirada | Redirecionamento para login com aviso |
| Exclusão | Caixa de confirmação com nome do item |

## 13. Uso dos arquivos

Estrutura esperada:

```text
docs/
├── REFERENCIAS_VISUAIS.md
└── assets/
    ├── mockup-painel-admin.svg
    └── mockup-site-publico.svg
```

Ao abrir `REFERENCIAS_VISUAIS.md` no GitHub, os SVGs e os diagramas Mermaid serão renderizados automaticamente.

