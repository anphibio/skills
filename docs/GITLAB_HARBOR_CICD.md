# GITLAB_HARBOR_CICD.md

## Objetivo

Definir o fluxo padrão de entrega do template para evitar rediscussão de tecnologia de CI/CD em novos projetos.

## Tecnologia padrão

Quando não houver exceção documentada, o projeto deve seguir:

- GitLab CI como orquestrador da pipeline
- GitLab Runner para build e deploy
- Harbor como registry corporativo
- Docker Compose para deploy por stack ou componente

## Modelo adotado

- build e push de imagens independentes para `backend`, `worker` e `frontend`
- tags de imagem por branch e commit curto
- tag adicional `latest-<branch>` quando o time usar esse padrão
- deploy por stack, sem voltar ao modelo de produção em compose único
- migração antes da atualização do `backend`, quando aplicável
- atualização isolada de `worker` e `frontend`

## Variáveis obrigatórias de CI/CD

Definir no GitLab:

- `HARBOR_REGISTRY`
- `HARBOR_PROJECT`
- `HARBOR_USERNAME`
- `HARBOR_PASSWORD`
- `BUILD_RUNNER_TAG`

Definir por ambiente ou branch quando aplicável:

- `DEPLOY_ENABLED`
- `DEPLOY_RUNNER_TAG`
- `DEPLOY_ROOT`
- `DEPLOY_BACKEND_ENV_FILE` opcional
- `DEPLOY_WORKER_ENV_FILE` opcional
- `DEPLOY_FRONTEND_ENV_FILE` opcional

## Ordem padrão do deploy

1. validar manifests e scripts
2. executar testes de `backend`, `worker` e `frontend`
3. buildar e publicar imagens no Harbor
4. atualizar stack do `backend`
5. executar migração do `backend`, quando aplicável
6. atualizar stack do `worker`
7. atualizar stack do `frontend`

## Requisitos mínimos do Runner

- Docker funcional
- Docker Compose Plugin
- bash
- acesso ao Harbor
- acesso ao servidor ou diretório do ambiente quando o deploy for feito pelo runner

## Rollback

O rollback deve ser feito por componente, usando tag ou versão exata da imagem.

O procedimento precisa estar documentado no projeto final.

## Regra do template

Não perguntar novamente qual tecnologia de pipeline usar, salvo quando o projeto já definir outro padrão de forma explícita.
