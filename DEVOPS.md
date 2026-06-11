# DEVOPS.md

## Deploy padrão

Todo projeto deve rodar com Docker Compose.

Para facilitar CI/CD em produção, a aplicação deve separar `backend`, `frontend`, `worker` e `db` em arquivos de compose independentes, sem dependência obrigatória entre eles.

Em DEV, é aceitável manter um compose integrado único para acelerar subida local, debug e validação funcional.

## Arquivos esperados

- Dockerfile backend
- Dockerfile frontend
- Dockerfile worker ou estratégia documentada de reaproveitamento da imagem do backend
- compose único de DEV, quando o projeto possuir ambiente integrado local
- docker-compose.backend.yml
- docker-compose.frontend.yml
- docker-compose.worker.yml
- docker-compose.db.yml quando o banco fizer parte do projeto
- Makefile apenas para rotinas de desenvolvimento local
- pipeline CI/CD versionada no repositório
- .env.example

## Estratégia de `.env`

Em DEV, preferir um único arquivo `.env`, separado por blocos para `backend`, `frontend`, `worker` e `db`.

Em HML e PRD, quando as stacks estiverem em servidores diferentes, cada stack deve receber apenas o seu próprio conjunto de variáveis de ambiente.

## Entrega mínima de CI/CD

Ao final do projeto, a entrega deve incluir CI/CD funcional e documentado.

Tecnologia padrão deste template:

- GitLab CI como orquestrador
- GitLab Runner para build e deploy
- Harbor como registry corporativo
- Docker Compose para publicação por stack

Itens mínimos esperados:

- pipeline versionada no repositório, preferencialmente `.gitlab-ci.yml`
- stages de validação, teste, build e deploy
- build de imagem por componente
- publicação de imagens no Harbor
- deploy por stack ou componente
- estratégia de rollback por tag ou versão
- variáveis obrigatórias de CI/CD documentadas
- runners e requisitos de execução documentados
- ordem de deploy documentada, incluindo migração quando aplicável
- tags de imagem por branch e commit documentadas
- deploy automático por branch quando o projeto exigir esse fluxo

## Containers

- Não rodar como root.
- Usar multi-stage build.
- Definir healthcheck.
- Definir restart policy.
- Separar volumes persistentes.
- Não embutir secrets na imagem.
- Configurar logs em todos os containers para facilitar troubleshooting e debug.

## Stacks esperadas no Compose

- `backend`
- `frontend`
- `worker`
- `db` quando o banco for hospedado pelo próprio projeto

Cada stack deve poder ser implantada isoladamente, inclusive em servidores diferentes.

O `worker` deve ser executado como stack separada, sem exposição de porta pública, permitindo deploy, escala e reinício independentes.

## Ambientes

- DEV
- HML
- PRD

## CI/CD

Pipeline mínimo:

1. Lint
2. Test
3. Build backend
4. Build frontend
5. Build worker
6. Security scan
7. Docker build por componente
8. Publicação de imagens no Harbor por componente
9. Deploy HML automatizado por stack quando aplicável
10. Deploy PRD controlado e documentado

## Fluxo padrão de CI/CD

O fluxo padrão deve seguir esta ordem:

1. validar manifests, scripts e variáveis críticas
2. executar testes de `backend`, `worker` e `frontend`
3. gerar imagens independentes por componente
4. publicar imagens no Harbor com tag por branch e commit
5. executar migração antes da atualização da stack do backend, quando aplicável
6. atualizar `worker`
7. atualizar `frontend`

Quando o projeto adotar deploy automático por branch, cada branch deve publicar e atualizar apenas o próprio ambiente.

## Monitoramento

Seguir `MONITORING.md` e `OBSERVABILITY_FIRST.md`.

A aplicação deve expor:

- `/health`
- `/ready`
- `/metrics`

O Zabbix deve consumir estes endpoints, principalmente `/metrics`.

Prometheus não é obrigatório neste padrão.
