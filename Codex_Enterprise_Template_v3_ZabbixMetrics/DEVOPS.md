# DEVOPS.md

## Deploy padrão

Todo projeto deve rodar com Docker Compose.

## Arquivos esperados

- Dockerfile backend
- Dockerfile frontend
- docker-compose.yml
- docker-compose.override.yml opcional
- .env.example

## Containers

- Não rodar como root.
- Usar multi-stage build.
- Definir healthcheck.
- Definir restart policy.
- Separar volumes persistentes.
- Não embutir secrets na imagem.

## Ambientes

- DEV
- HML
- PRD

## CI/CD

Pipeline mínimo:

1. Lint
2. Test
3. Build
4. Security scan
5. Docker build
6. Push image
7. Deploy HML
8. Deploy PRD manual

## Monitoramento

Seguir `MONITORING.md` e `OBSERVABILITY_FIRST.md`.

A aplicação deve expor:

- `/health`
- `/ready`
- `/metrics`

O Zabbix deve consumir estes endpoints, principalmente `/metrics`.

Prometheus não é obrigatório neste padrão.
