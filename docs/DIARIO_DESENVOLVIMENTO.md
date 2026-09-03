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
| 5 | Criar protótipo visual simples | Em validação |
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

Especificação inicial criada no arquivo `docs/PROTOTIPO_VISUAL.md` e aguardando validação antes de ser considerada concluída.

### Decisões registradas

- tema escuro com azul como cor de destaque;
- página pública organizada em Navbar, Hero, Sobre, Tecnologias, Experiência, Projetos, Certificados, Contato e Footer;
- página própria para detalhes de cada projeto;
- painel administrativo separado da navegação pública;
- componentes responsivos para celular, tablet e desktop;
- estados de carregamento, vazio, erro e sucesso previstos;
- acessibilidade e redução de movimento consideradas desde o protótipo.

### Arquivo criado

```text
docs/PROTOTIPO_VISUAL.md
docs/REFERENCIAS_VISUAIS.md
docs/assets/mockup-site-publico.svg
docs/assets/mockup-painel-admin.svg
```

O documento de referências visuais reúne os mockups da página pública e do painel, além dos fluxos de arquitetura, autenticação, cadastro de projeto, contato, banco preliminar, CI/CD e Azure.

### Validação pendente

- confirmar título profissional;
- aprovar paleta e organização das seções;
- definir uso de fotografia ou avatar;
- confirmar projetos e estrutura do painel.

### Próximo trabalho

Validar o protótipo. Após a aprovação, marcar a Etapa 5 como concluída e iniciar a Etapa 10 — modelagem do banco de dados.

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

---

## Documentação geral — README principal

### Objetivo

Criar a página inicial do repositório para apresentar o propósito, a arquitetura, as tecnologias, o estado atual, as instruções de execução e o roadmap do Portfolio.Dev.

### Arquivo criado

```text
README.md
```

### Conteúdo registrado

- apresentação e objetivos;
- mockups da página pública e do painel;
- arquitetura geral e dependências do back-end;
- tecnologias utilizadas e planejadas;
- funcionalidades separadas por área;
- estrutura do repositório;
- execução do estado atual;
- índice dos documentos;
- status e roadmap;
- padrão de commits;
- cuidados com segredos;
- identificação do autor.

### Validação prevista

- conferir a renderização dos SVGs e diagramas Mermaid no GitHub;
- validar todos os links relativos da documentação;
- executar `dotnet restore`, `dotnet build` e `dotnet test` a partir das instruções;
- substituir o placeholder do LinkedIn antes da publicação final.

### Commit recomendado

```text
docs: cria readme principal do projeto
```

### Problema de renderização do Mermaid

**Problema:** o GitHub exibiu `Unable to render rich display` no fluxograma de arquitetura.

**Causa provável:** incompatibilidade do renderizador com a combinação de identificadores, rótulos sem aspas e formas especiais utilizada na primeira versão.

**Correção:** os fluxogramas foram convertidos para a sintaxe mais conservadora `graph`, receberam identificadores descritivos e passaram a utilizar rótulos entre aspas. As formas especiais de banco foram substituídas por caixas simples para aumentar a compatibilidade.

**Arquivos alterados:**

```text
README.md
docs/REFERENCIAS_VISUAIS.md
docs/DIARIO_DESENVOLVIMENTO.md
```

**Commit recomendado:**

```text
fix: corrige renderização dos diagramas Mermaid
```
