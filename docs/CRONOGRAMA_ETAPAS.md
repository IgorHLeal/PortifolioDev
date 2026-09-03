# Portfolio.Dev — Cronograma e verificações

Este documento reproduz as 39 etapas presentes no arquivo `Cronograma portifólio.pdf` e acrescenta a coluna **Verificação**, utilizada para registrar o status e a evidência objetiva de conclusão.

## Legenda

| Indicador | Significado |
|---|---|
| ✅ | Concluída e verificada |
| 🟡 | Pendente ou parcialmente concluída |
| ⬜ | Ainda não iniciada |

## Cronograma

| Fase | Etapa | Atividade | Tecnologias / Conceitos | Resultado esperado | Prazo sugerido | Verificação |
|---|---:|---|---|---|---:|---|
| 1. Planejamento | 1 | Definir objetivo do portfólio | Carreira, posicionamento profissional | Definição clara do foco: Analista de Sistemas / Suporte / Desenvolvedor .NET | 1 dia | ✅ **Concluída:** objetivo, público-alvo e posicionamento registrados no diário. |
| 1. Planejamento | 2 | Definir conteúdo do site | LinkedIn, GitHub, currículo | Lista de experiências, tecnologias, projetos e formação | 1 dia | 🟡 **Pendente:** estrutura inicial definida, mas faltam textos definitivos, fotografia, currículo, certificados e links. |
| 1. Planejamento | 3 | Definir estrutura das páginas | UX/UI, arquitetura de informação | Mapa das seções: Home, Sobre, Tecnologias, Projetos, Experiência e Contato | 1 dia | ✅ **Concluída:** seções públicas e administrativas documentadas. |
| 1. Planejamento | 4 | Definir arquitetura da aplicação | Front-end, API, banco, autenticação | Arquitetura geral documentada | 1 dia | ✅ **Concluída:** arquitetura, camadas e dependências registradas em diagramas. |
| 1. Planejamento | 5 | Criar protótipo visual simples | UI minimalista, responsividade | Referência visual para desenvolver o site | 1 dia | ✅ **Concluída:** protótipo, referências visuais, mockups e fluxogramas criados. |
| 2. Ambiente | 6 | Instalar e configurar ferramentas | Visual Studio, VS Code, Git, SQL Server, SSMS | Ambiente pronto para desenvolvimento | 1 dia | ✅ **Concluída:** ferramentas instaladas e comandos de validação executados com sucesso. |
| 2. Ambiente | 7 | Criar repositório no GitHub | Git, GitHub | Repositório `PortfolioDev` criado | 1 dia | ✅ **Concluída:** repositório público criado, branch `main` publicada e remoto configurado. |
| 2. Ambiente | 8 | Criar solução .NET | .NET, ASP.NET Core | Solution principal criada | 1 dia | ✅ **Concluída:** `PortfolioDev.sln` criada, aberta no Visual Studio e compilada. |
| 2. Ambiente | 9 | Organizar estrutura de projetos | Clean Architecture, organização em camadas | Estrutura inicial organizada | 1 dia | ✅ **Concluída:** cinco projetos criados, relacionados, compilados e testados. |
| 3. Banco de Dados | 10 | Modelar banco de dados | SQL Server, modelagem relacional | Diagrama das entidades e relacionamentos | 1 dia | ⬜ **Não iniciada:** concluir quando o modelo relacional for documentado e revisado. |
| 3. Banco de Dados | 11 | Criar entidades principais | C#, OOP | Classes Project, Technology, Experience, Certificate, Contact e User | 1 dia | ⬜ **Não iniciada:** concluir quando as entidades compilarem e seus testes forem aprovados. |
| 3. Banco de Dados | 12 | Configurar Entity Framework Core | EF Core, DbContext | API conectada ao SQL Server | 1 dia | ⬜ **Não iniciada:** concluir após validar o `DbContext` e a conexão local sem expor segredos. |
| 3. Banco de Dados | 13 | Criar primeira Migration | EF Core Migrations | Banco criado automaticamente | 1 dia | ⬜ **Não iniciada:** concluir após aplicar a migration e conferir as tabelas no SSMS. |
| 3. Banco de Dados | 14 | Criar dados iniciais | Seed, SQL, EF Core | Tecnologias e informações iniciais cadastradas | 1 dia | ⬜ **Não iniciada:** concluir após executar o seed e consultar os registros no banco. |
| 4. API REST | 15 | Criar primeira API REST | ASP.NET Core Web API | Projeto da API funcionando | 1 dia | ⬜ **Não iniciada:** concluir quando a API iniciar localmente e responder sem erro. |
| 4. API REST | 16 | Configurar Swagger / OpenAPI | Swagger | Documentação interativa disponível | 1 dia | ⬜ **Não iniciada:** concluir quando a documentação abrir e listar os endpoints. |
| 4. API REST | 17 | Criar endpoint de projetos | GET | `/api/projects` funcionando | 1 dia | ⬜ **Não iniciada:** validar resposta `200`, contrato JSON e cenário sem registros. |
| 4. API REST | 18 | Criar endpoint de projeto por ID | GET | `/api/projects/{id}` funcionando | 1 dia | ⬜ **Não iniciada:** validar respostas `200` para ID existente e `404` para inexistente. |
| 4. API REST | 19 | Criar cadastro de projeto | POST | Endpoint de criação funcionando | 1 dia | ⬜ **Não iniciada:** validar criação, persistência, resposta `201` e entradas inválidas. |
| 4. API REST | 20 | Criar atualização de projeto | PUT | Endpoint de edição funcionando | 1 dia | ⬜ **Não iniciada:** validar alteração persistida, entradas inválidas e ID inexistente. |
| 4. API REST | 21 | Criar exclusão de projeto | DELETE | Endpoint de exclusão funcionando | 1 dia | ⬜ **Não iniciada:** validar exclusão, resposta adequada e tentativa com ID inexistente. |
| 4. API REST | 22 | Criar CRUD de tecnologias | REST, EF Core | Tecnologias administradas pela API | 1 dia | ⬜ **Não iniciada:** testar criação, consulta, edição, exclusão e regras de duplicidade. |
| 4. API REST | 23 | Criar CRUD de experiências | REST, EF Core | Timeline administrada pela API | 1 dia | ⬜ **Não iniciada:** testar operações e ordenação cronológica das experiências. |
| 4. API REST | 24 | Criar CRUD de certificados | REST, EF Core | Certificados administrados pela API | 1 dia | ⬜ **Não iniciada:** testar operações, links e campos obrigatórios. |
| 4. API REST | 25 | Criar endpoint de contato | POST, SQL | Mensagens do site armazenadas no banco | 1 dia | ⬜ **Não iniciada:** enviar uma mensagem válida, verificar persistência e rejeitar dados inválidos. |
| 5. Boas práticas Backend | 26 | Implementar DTOs | DTO, separação de responsabilidades | Entidades protegidas da exposição direta | 1 dia | ⬜ **Não iniciada:** confirmar que endpoints recebem e retornam DTOs, não entidades diretamente. |
| 5. Boas práticas Backend | 27 | Implementar validações | FluentValidation | Dados validados antes de serem processados | 1 dia | ⬜ **Não iniciada:** testar campos obrigatórios, limites e mensagens de validação. |
| 5. Boas práticas Backend | 28 | Implementar tratamento global de erros | Middleware, exceptions | Respostas de erro padronizadas | 1 dia | ⬜ **Não iniciada:** provocar erro controlado e conferir status, mensagem e identificador da requisição. |
| 5. Boas práticas Backend | 29 | Implementar logging | ILogger, logs estruturados | Registro de erros e operações | 1 dia | ⬜ **Não iniciada:** confirmar logs estruturados sem senhas, tokens ou dados sensíveis. |
| 5. Boas práticas Backend | 30 | Padronizar respostas da API | HTTP Status Codes, REST | API consistente e profissional | 1 dia | ⬜ **Não iniciada:** revisar contratos e códigos HTTP dos principais cenários. |
| 6. Autenticação | 31 | Criar entidade de usuário administrador | Identity, entidade própria | Estrutura para acesso administrativo | 1 dia | ⬜ **Não iniciada:** compilar entidade e validar armazenamento seguro da senha por hash. |
| 6. Autenticação | 32 | Criar login | ASP.NET Core, autenticação | Administrador consegue autenticar | 1 dia | ⬜ **Não iniciada:** testar credenciais válidas, inválidas e usuário inexistente. |
| 6. Autenticação | 33 | Implementar JWT | JWT Bearer | Token gerado no login | 1 dia | ⬜ **Não iniciada:** validar assinatura, expiração, claims e rejeição de token inválido. |
| 6. Autenticação | 34 | Proteger endpoints administrativos | Authorization | POST, PUT e DELETE protegidos | 1 dia | ⬜ **Não iniciada:** confirmar `401/403` sem autorização e sucesso com token válido. |
| 7. Front-end | 35 | Criar projeto do front-end | React, Vite | Aplicação visual criada | 1 dia | ⬜ **Não iniciada:** concluir quando o projeto instalar, compilar e abrir localmente. |
| 7. Front-end | 36 | Criar layout principal | HTML, CSS, responsividade | Estrutura visual do site pronta | 1 dia | ⬜ **Não iniciada:** validar organização geral nas larguras definidas no protótipo. |
| 7. Front-end | 37 | Criar Navbar | Componentização | Menu responsivo | 1 dia | ⬜ **Não iniciada:** testar links, menu móvel, teclado e diferentes larguras. |
| 7. Front-end | 38 | Criar Hero Section | UI/UX | Apresentação profissional inicial | 1 dia | ⬜ **Não iniciada:** conferir título, chamadas para ação, imagem e responsividade. |
| 7. Front-end | 39 | Criar seção Sobre Mim | UI, conteúdo | História profissional apresentada | 1 dia | ⬜ **Não iniciada:** revisar conteúdo, legibilidade e comportamento em celular e desktop. |

## Resumo atual

| Situação | Etapas | Quantidade |
|---|---|---:|
| Concluídas | 1, 3, 4, 5, 6, 7, 8 e 9 | 8 |
| Pendente | 2 | 1 |
| Não iniciadas | 10 a 39 | 30 |

## Regra de atualização

Ao concluir uma etapa:

1. executar a verificação indicada;
2. documentar comandos, arquivos e decisões no `DIARIO_DESENVOLVIMENTO.md`;
3. alterar o indicador da coluna **Verificação** para ✅;
4. atualizar o resumo atual;
5. criar o commit indicado para a etapa;
6. enviar as alterações ao GitHub.

