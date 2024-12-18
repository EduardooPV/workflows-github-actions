# CI/CD com GitHub Actions

Este repositório contém uma configuração de CI/CD utilizando GitHub Actions para automação do processo de build, análise, deploy e validação de Pull Requests (PRs).
Foi realizada uma integração com o Vercel que permite deploy contínuo tanto para ambientes de Staging quanto de Produção.

## Visão Geral

O fluxo de trabalho do GitHub Actions foi projetado para:

- Construir a aplicação Vue.js sempre que um PR é aberto ou alterado.
- Analisar o código com o CodeQL para garantir a segurança.
- Validar PRs para garantir boas práticas (como título e labels).
- Executar testes unitários com o Vitest.
- Verificar linting e formatação utilizando ESLint e Prettier.
- Deploy automático para Vercel em dois ambientes:
  - **Staging** (quando um PR é enviado para a branch `staging`).
  - **Produção** (quando há um push para a branch `main`).

## Estrutura do Workflow

O repositório possui as seguintes GitHub Actions configuradas:

### 1. Build Vue Application (build)

- **Disparada por**: Alterações nos PRs.
- **Objetivo**: Construir a aplicação Vue.js após a instalação das dependências.

### 2. CodeQL Analysis (codeql-analyze)

- **Disparada por**: Alterações nos PRs.
- **Objetivo**: Realizar a análise de segurança do código.

### 3. Deploy to Vercel (Production) (deploy-prd)

- **Disparada por**: Push para a branch `main`.
- **Objetivo**: Realizar o deploy da aplicação para o ambiente de produção no Vercel.

### 4. Deploy to Vercel (Staging) (deploy-staging)

- **Disparada por**: PR para a branch `staging`.
- **Objetivo**: Realizar o deploy da aplicação para o ambiente de staging no Vercel.

### 5. Lint and Format Check (lint)

- **Disparada por**: Alterações nos PRs.
- **Objetivo**: Verificar se o código segue as regras de linting e formatação.

### 6. Run Tests with Vitest (test)

- **Disparada por**: Alterações nos PRs.
- **Objetivo**: Executar os testes unitários com Vitest.

### 7. Validate Pull Request (validate-pr)

- **Disparada por**: Alterações nos PRs.
- **Objetivo**: Validar o PR quanto a boas práticas de naming, labels e assignees.

## Variáveis e Secrets necessários

Para que as ações de CI/CD funcionem corretamente, é necessário configurar as variáveis e segredos abaixo nas Settings do repositório em Secrets:

- **Variáveis de Ambiente**:
  - `VERCEL_TOKEN`: Token de autenticação do Vercel.
  - `VERCEL_ORG_ID`: ID da organização no Vercel.
  - `VERCEL_PROJECT_ID`: ID do projeto no Vercel.
  - `GITHUB_TOKEN`: Token do GitHub (gerado automaticamente).
