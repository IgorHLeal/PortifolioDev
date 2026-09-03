# Portfolio.Dev — Diário de desenvolvimento

Este documento registra tudo o que foi executado no projeto: decisões, comandos, validações, problemas e próximos passos. Deve ser atualizado ao final de cada etapa.

## Padrão obrigatório para novas etapas

Cada etapa deverá conter:

1. objetivo;
2. conceitos estudados;
3. decisões técnicas;
4. arquivos criados ou alterados;
5. comandos executados;
6. explicação dos comandos;
7. validações realizadas;
8. problemas encontrados e soluções;
9. commit criado;
10. resultado e próximo passo.

Nunca registrar neste arquivo senhas, tokens, chaves, strings de conexão reais ou outros segredos.

---

## Situação geral

| Etapa | Atividade | Situação |
|---:|---|---|
| 1 | Definir objetivo do portfólio | Concluída |
| 2 | Definir conteúdo do site | Concluída inicialmente |
| 3 | Definir estrutura das páginas | Concluída |
| 4 | Definir arquitetura da aplicação | Concluída |
| 5 | Criar protótipo visual simples | Pendente |
| 6 | Instalar e configurar ferramentas | Concluída |
| 7 | Criar repositório no GitHub | Concluída |
| 8 | Criar solução .NET | Concluída |
| 9 | Organizar estrutura de projetos | Concluída |
| 10 | Modelar banco de dados | Pendente |

---

## Etapa 1 — Objetivo do portfólio

### Objetivo

Criar um portfólio profissional full stack que, além de apresentar a trajetória de Igor Leal, comprove na prática conhecimentos de C#, ASP.NET Core, APIs REST, SQL Server, React, autenticação, testes, Docker, Azure e CI/CD.

### Público-alvo

- recrutadores de tecnologia;
- gestores de desenvolvimento e suporte de aplicações;
- empresas buscando Analista de Sistemas;
- empresas buscando Desenvolvedor Back-end .NET.

### Posicionamento

```text
Analista de Sistemas | Desenvolvedor .NET | Especialista em Suporte Técnico
```

### Resultado

Objetivo e público-alvo definidos.

---

## Etapa 2 — Conteúdo do site

### Conteúdo definido

- apresentação profissional;
- Sobre mim;
- tecnologias;
- experiências;
- projetos;
- certificados;
- formulário de contato;
- currículo para download;
- painel administrativo.

### Projetos inicialmente previstos

- OneNote Knowledge Hub;
- Diagnóstico de Rede Windows;
- API Troubleshooter;
- KB Assistant;
- Portfolio.Dev.

### Resultado

Conteúdo inicial definido. Os textos e dados definitivos ainda serão revisados antes da publicação.

---

## Etapa 3 — Estrutura das páginas

### Página pública

1. Navbar;
2. Hero;
3. Sobre mim;
4. Tecnologias;
5. Experiências;
6. Projetos;
7. Certificados;
8. Contato;
9. Footer.

### Painel administrativo

- login;
- dashboard;
- CRUD de projetos;
- CRUD de tecnologias;
- CRUD de experiências;
- CRUD de certificados;
- mensagens recebidas.

### Resultado

Mapa inicial das páginas definido.

---

## Etapa 4 — Arquitetura da aplicação

### Stack definida

| Camada | Tecnologia |
|---|---|
| Back-end | C#, .NET 10 e ASP.NET Core Web API |
| Aplicação | Clean Architecture com organização orientada a funcionalidades |
| Persistência | SQL Server e Entity Framework Core |
| Front-end | React, TypeScript, Vite e Tailwind CSS |
| Autenticação | JWT |
| Validação | FluentValidation |
| Testes | xUnit |
| Containers | Docker e Docker Compose |
| Cloud | Azure |
| CI/CD | GitHub Actions |

### Fluxo principal

```text
Usuário -> React -> API ASP.NET Core -> SQL Server
```

### Resultado

Arquitetura inicial definida. Detalhes poderão ser refinados durante a implementação.

---

## Etapa 5 — Protótipo visual

### Situação

Pendente. A preparação técnica foi adiantada antes da criação do protótipo.

### Próximo trabalho

Definir o protótipo da página pública e do painel administrativo antes da modelagem definitiva do banco.

---

## Etapa 6 — Preparação do ambiente

### Ferramentas instaladas

- Visual Studio;
- .NET SDK 10.0.400;
- SQL Server 2025 Developer;
- SQL Server Management Studio 22;
- Git 2.55.0;
- Node.js 24.20.0;
- npm;
- Postman;
- WSL 2 com Ubuntu;
- Docker Desktop;
- Azure CLI.

GitHub Desktop não foi instalado por decisão do desenvolvedor. O Git será utilizado no terminal e o GitHub será acessado pelo navegador.

### Validações principais

```powershell
dotnet --version
dotnet --list-sdks
git --version
ssh -V
node --version
npm --version
npx --version
wsl --status
wsl --list --verbose
docker --version
docker compose version
az version
```

### Problemas e soluções

| Problema | Solução aplicada |
|---|---|
| Certificado local do SQL Server não reconhecido pelo SSMS | Certificado do servidor marcado como confiável na conexão local |
| PowerShell bloqueou `npm.ps1` | Política do usuário alterada para `RemoteSigned` |
| Telas específicas do Git não apareceram | Instalação validada diretamente pelos comandos Git e OpenSSH |
| Ubuntu abriu automaticamente | WSL estava finalizando a instalação normalmente |

### Resultado

Ambiente de desenvolvimento instalado e validado.

---

## Etapa 7 — Git e GitHub

### Repositório

O repositório público `PortfolioDev` foi criado no GitHub e conectado à cópia local.

### Comandos principais

```powershell
git init
dotnet new gitignore
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/PortfolioDev.git
git add .
git commit -m "chore: cria estrutura inicial da solução"
git push -u origin main
```

### Validações

```powershell
git remote -v
git status
git log --oneline
```

### Resultado

- branch `main` publicada;
- primeiro commit disponível no GitHub;
- `bin` e `obj` ignoradas;
- repositório público funcionando.

---

## Etapa 8 — Criação da solução .NET

### Comandos executados

```powershell
dotnet new sln --name PortfolioDev --format sln
dotnet new webapi --name PortfolioDev.Api --output backend/PortfolioDev.Api --use-controllers
dotnet new classlib --name PortfolioDev.Domain --output backend/PortfolioDev.Domain
dotnet new classlib --name PortfolioDev.Application --output backend/PortfolioDev.Application
dotnet new classlib --name PortfolioDev.Infrastructure --output backend/PortfolioDev.Infrastructure
dotnet new xunit --name PortfolioDev.Tests --output backend/PortfolioDev.Tests
```

### Projetos

| Projeto | Responsabilidade |
|---|---|
| `PortfolioDev.Api` | Endpoints HTTP, middlewares e configuração da aplicação |
| `PortfolioDev.Application` | Casos de uso, DTOs, interfaces e validações |
| `PortfolioDev.Domain` | Entidades e regras centrais |
| `PortfolioDev.Infrastructure` | SQL Server, EF Core, repositórios e serviços externos |
| `PortfolioDev.Tests` | Testes automatizados |

### Resultado

Solução criada e aberta corretamente no Visual Studio.

---

## Etapa 9 — Organização e dependências

### Estrutura

```text
PortfolioDev/
├── backend/
│   ├── PortfolioDev.Api/
│   ├── PortfolioDev.Application/
│   ├── PortfolioDev.Domain/
│   ├── PortfolioDev.Infrastructure/
│   └── PortfolioDev.Tests/
├── frontend/
├── docs/
├── .gitignore
└── PortfolioDev.sln
```

As pastas `frontend` e `docs` não aparecem no GitHub enquanto estiverem vazias, pois o Git não controla diretórios sem arquivos.

### Referências configuradas

```text
Api -> Application
Api -> Infrastructure
Infrastructure -> Application
Infrastructure -> Domain
Application -> Domain
Tests -> Application
Tests -> Domain
```

### Validações

```powershell
dotnet restore
dotnet build
dotnet test
dotnet sln PortfolioDev.sln list
git status
```

### Resultado registrado

- cinco projetos visíveis no Visual Studio;
- build concluído sem erros;
- testes aprovados;
- primeiro commit criado;
- diretórios `bin` e `obj` ignorados pelo Git.

---

## Modelo para a próxima etapa

Copie esta estrutura ao iniciar uma nova etapa:

```markdown
## Etapa XX — Nome

### Objetivo

### Conceitos estudados

### Decisões técnicas

### Arquivos criados ou alterados

### Comandos executados

### Explicação dos comandos

### Validações

### Problemas e soluções

### Commit

### Resultado e próximo passo
```

