# Portfolio.Dev — Guia de instalação do ambiente

Este documento descreve a preparação de um computador Windows para desenvolver o **Portfolio.Dev**, uma aplicação com ASP.NET Core, React, SQL Server, Docker e Azure.

## 1. Visão geral

| Ordem | Ferramenta | Utilização no projeto | Obrigatória no início? |
|---:|---|---|---|
| 1 | Visual Studio Community | API ASP.NET Core, depuração e testes | Sim |
| 2 | SQL Server 2025 Developer | Banco de dados local | Sim |
| 3 | SQL Server Management Studio 22 | Administração e consultas no SQL Server | Sim |
| 4 | Git | Versionamento do código | Sim |
| 5 | Node.js LTS | Execução do React, npm e Vite | Sim |
| 6 | Postman | Testes manuais da API | Sim |
| 7 | Docker Desktop | Containers da API, front-end e banco | Não; usado em fase posterior |
| 8 | Azure CLI | Publicação e administração dos recursos Azure | Não; usado em fase posterior |

> O GitHub Desktop é opcional. O projeto utiliza o Git no terminal e o GitHub pelo navegador.

## 2. Pré-requisitos do Windows

Antes das instalações:

1. Execute o Windows Update.
2. Reinicie o computador se houver atualização pendente.
3. Confirme que o Windows é de 64 bits.
4. Reserve espaço livre para Visual Studio, SQL Server, Docker e imagens de containers.
5. Use uma conta com permissão de administrador durante as instalações que solicitarem elevação.

## 3. Visual Studio Community

### Download

- [Visual Studio Community](https://visualstudio.microsoft.com/pt-br/vs/community/)
- [Documentação de instalação](https://learn.microsoft.com/pt-br/visualstudio/install/install-visual-studio)

### Cargas de trabalho

No Visual Studio Installer, selecione:

- **Desenvolvimento ASP.NET e Web**;
- **Armazenamento e processamento de dados**;
- **Desenvolvimento para desktop com .NET**.

Confirme a instalação dos seguintes componentes:

- SDK do .NET 10;
- runtime do .NET 10;
- ferramentas do .NET;
- NuGet;
- Git para Windows;
- IIS Express;
- SQL Server Data Tools, se disponível.

Não é necessário instalar neste projeto: Unity, MAUI, desenvolvimento móvel, Python ou ferramentas de C++.

### Validação

Abra um PowerShell novo:

```powershell
dotnet --version
dotnet --list-sdks
```

O SDK do .NET 10 deve aparecer. No Visual Studio, confirme que o modelo **ASP.NET Core Web API** está disponível.

## 4. SQL Server 2025 Developer

### Download

- [Downloads do SQL Server](https://www.microsoft.com/pt-br/sql-server/sql-server-downloads)
- [Documentação do SQL Server](https://learn.microsoft.com/pt-br/sql/sql-server/)

Selecione a edição gratuita **SQL Server 2025 Developer**. Ela deve ser utilizada somente para desenvolvimento e testes, não como banco de produção.

### Instalação

1. Execute o instalador como administrador.
2. Selecione **Personalizado**.
3. Abra a Central de Instalação.
4. Selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.
5. Aceite os termos e avance nas verificações.
6. Em recursos, selecione **Serviços do Mecanismo de Banco de Dados**.
7. Pesquisa de texto completo é opcional.
8. Não instale Analysis Services, Machine Learning, PolyBase ou Integration Services nesta fase.

### Instância

Use a **instância padrão**, com o identificador:

```text
MSSQLSERVER
```

Ela poderá ser acessada localmente com um destes nomes:

```text
localhost
.
(local)
```

### Autenticação

1. Selecione **Modo de Autenticação do Windows**.
2. Clique em **Adicionar usuário atual**.
3. Confirme que seu usuário aparece como administrador do SQL Server.
4. Mantenha o serviço do mecanismo com inicialização automática.

### Validar o serviço

Execute no PowerShell:

```powershell
Get-Service -Name MSSQLSERVER
```

O estado esperado é `Running`. Se estiver parado:

```powershell
Start-Service -Name MSSQLSERVER
```

O segundo comando precisa de um PowerShell executado como administrador.

## 5. SQL Server Management Studio — SSMS

### Download

- [Instalar o SSMS](https://learn.microsoft.com/pt-br/ssms/install/install)

### Instalação

1. Execute `vs_SSMS.exe`.
2. Mantenha selecionados os componentes principais do SSMS.
3. As cargas Assistência de IA, Business Intelligence, Híbrido e Migração, Ferramentas de Codificação e DevOps de Banco de Dados são opcionais e não são necessárias para este projeto.
4. Selecione **Instalar durante o download**.
5. Clique em **Instalar**.

### Conexão local

Preencha:

| Campo | Valor |
|---|---|
| Nome do servidor | `localhost` |
| Autenticação | Autenticação do Windows |
| Criptografar | Obrigatório |
| Certificado do Servidor de Confiança | Marcado somente no ambiente local |

O certificado confiável é aceito localmente porque a instalação utiliza um certificado autoassinado. Em produção, deve ser usado um certificado válido.

### Consulta de validação

```sql
SELECT
    @@SERVERNAME AS NomeServidor,
    @@VERSION AS VersaoSQLServer,
    DB_NAME() AS BancoAtual;
```

## 6. Rede e firewall do SQL Server

### Quando não configurar o firewall

Se a API e o SQL Server estiverem no mesmo computador e a conexão usar `localhost`, **não é necessário abrir nenhuma porta no Firewall do Windows**.

Nunca exponha a porta do SQL Server diretamente à internet.

### Quando a configuração pode ser necessária

A configuração é necessária somente se outro computador ou container precisar alcançar o SQL Server pela rede.

### Habilitar TCP/IP

1. Abra o **SQL Server Configuration Manager**.
2. Acesse **Configuração de Rede do SQL Server > Protocolos para MSSQLSERVER**.
3. Habilite **TCP/IP**.
4. Abra as propriedades de **TCP/IP**.
5. Na aba **Endereços IP**, localize **IPAll**.
6. Remova o valor de **Portas TCP Dinâmicas**, se houver.
7. Defina **Porta TCP** como `1433`.
8. Reinicie o serviço `SQL Server (MSSQLSERVER)`.

### Criar uma regra restrita à rede local

Abra o PowerShell como administrador:

```powershell
New-NetFirewallRule `
  -DisplayName "PortfolioDev - SQL Server TCP 1433" `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 1433 `
  -RemoteAddress LocalSubnet `
  -Profile Private `
  -Action Allow
```

Essa regra permite conexões somente a partir da sub-rede local e apenas quando o Windows estiver usando o perfil de rede privado.

### Validar a porta

No computador servidor:

```powershell
Get-NetTCPConnection -LocalPort 1433 -State Listen
```

De outro computador autorizado na rede:

```powershell
Test-NetConnection -ComputerName IP_DO_SERVIDOR -Port 1433
```

O resultado esperado é:

```text
TcpTestSucceeded : True
```

### Remover a regra se não for mais necessária

```powershell
Remove-NetFirewallRule -DisplayName "PortfolioDev - SQL Server TCP 1433"
```

Não é necessário liberar UDP 1434 para a instância padrão acessada diretamente pela porta 1433. SQL Browser e UDP 1434 são usados principalmente na descoberta de instâncias nomeadas.

## 7. Git para Windows

### Download

- [Git para Windows](https://git-scm.com/install/windows)
- [Documentação do Git](https://git-scm.com/doc)

Mantenha as opções recomendadas pelo instalador. Algumas versões não exibem separadamente as telas de OpenSSH e terminal.

### Validação

```powershell
git --version
where.exe git
ssh -V
```

O parâmetro de versão do SSH usa `V` maiúsculo.

### Configuração inicial

```powershell
git config --global user.name "Igor Leal"
git config --global user.email "EMAIL_CADASTRADO_NO_GITHUB"
git config --global init.defaultBranch main
git config --global --list
```

## 8. Node.js LTS e npm

### Download

- [Node.js](https://nodejs.org/pt/download)
- [Documentação do npm](https://docs.npmjs.com/)

Selecione a versão **LTS**, para Windows x64, utilizando o instalador `.msi`. Mantenha o npm e a inclusão no `PATH` selecionados.

### Validação

```powershell
node --version
npm --version
npx --version
```

### Erro de política de execução

Se o PowerShell bloquear `npm.ps1`, configure somente o usuário atual:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Confirme a alteração, feche o PowerShell e abra-o novamente. Como teste alternativo:

```powershell
npm.cmd --version
```

## 9. Postman

### Download

- [Postman para desktop](https://www.postman.com/downloads/)
- [Documentação do Postman](https://learning.postman.com/docs/)

Baixe a edição para Windows 64 bits, execute o instalador e abra o aplicativo. A conta gratuita é suficiente para este projeto.

O Postman será utilizado para testar métodos `GET`, `POST`, `PUT` e `DELETE`, autenticação JWT, códigos HTTP e corpos JSON.

## 10. WSL 2

O Docker Desktop utiliza o WSL 2 como mecanismo no Windows.

Abra o PowerShell como administrador:

```powershell
wsl --install
```

Reinicie o computador. O Ubuntu poderá abrir automaticamente para finalizar a instalação. Crie o usuário e a senha solicitados; a senha não aparece enquanto é digitada.

Valide:

```powershell
wsl --status
wsl --list --verbose
```

A distribuição deve mostrar `VERSION 2`.

Se necessário, defina a versão padrão:

```powershell
wsl --set-default-version 2
```

## 11. Docker Desktop

### Download

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Instalação no Windows](https://docs.docker.com/desktop/setup/install/windows-install/)

### Instalação

1. Confirme que o WSL 2 está funcionando.
2. Execute o instalador do Docker Desktop.
3. Use o mecanismo baseado em WSL 2.
4. Reinicie o Windows se solicitado.
5. Abra o Docker Desktop e aguarde o mecanismo iniciar.

### Validação

```powershell
docker --version
docker compose version
docker run hello-world
```

## 12. Azure CLI

### Download

- [Instalar a Azure CLI no Windows](https://learn.microsoft.com/pt-br/cli/azure/install-azure-cli-windows)
- [Documentação da Azure CLI](https://learn.microsoft.com/pt-br/cli/azure/)

Execute o instalador e abra um PowerShell novo.

### Validação

```powershell
az version
```

O login será realizado apenas quando iniciarmos o deploy:

```powershell
az login
```

Não registre tokens, senhas, chaves ou segredos no GitHub.

## 13. Validação geral

Execute em um PowerShell novo:

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

Valide separadamente:

- modelo ASP.NET Core Web API disponível no Visual Studio;
- conexão do SSMS com `localhost`;
- consulta de validação executada com sucesso;
- Postman abrindo normalmente;
- `docker run hello-world` concluído.

## 14. Problemas encontrados durante a preparação

| Problema | Causa | Solução |
|---|---|---|
| SSMS informou cadeia de certificação não confiável | Certificado autoassinado da instância local | Marcar **Certificado do Servidor de Confiança** apenas para o ambiente local |
| `npm.ps1` foi bloqueado | Política de execução do PowerShell | Configurar `RemoteSigned` no escopo `CurrentUser` |
| Telas de OpenSSH e terminal não apareceram no Git | O instalador aplicou opções padrão ou o componente já existia | Validar com `git --version`, `where.exe git` e `ssh -V` |
| Ubuntu abriu depois da reinicialização | WSL estava concluindo a instalação da distribuição | Aguardar, criar usuário e senha e validar a versão 2 |

## 15. Checklist final

- [ ] Visual Studio instalado com ASP.NET e .NET 10.
- [ ] SQL Server Developer instalado.
- [ ] Serviço `MSSQLSERVER` em execução.
- [ ] SSMS conectado ao `localhost`.
- [ ] Firewall mantido fechado para o SQL quando a conexão é somente local.
- [ ] Git instalado e identificado.
- [ ] Nome, e-mail e branch padrão configurados no Git.
- [ ] Node.js LTS, npm e npx funcionando.
- [ ] Postman instalado.
- [ ] WSL executando a distribuição na versão 2.
- [ ] Docker Desktop validado com `hello-world`.
- [ ] Azure CLI respondendo ao comando `az version`.

