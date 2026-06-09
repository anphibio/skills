# ENVIRONMENT.md

## Ambientes

- DEV
- HML
- PRD

## Configuração

Toda configuração deve vir de variável de ambiente.

## Arquivos

- `.env.example` deve existir.
- `.env` real não deve ser versionado.

## Variáveis comuns

```text
APP_ENV=dev
APP_NAME=nome-do-projeto
DATABASE_URL=postgresql://user:pass@db:5432/app
JWT_SECRET=change-me
JWT_EXPIRE_MINUTES=30
CORS_ORIGINS=http://localhost:3000
LOG_LEVEL=INFO
```
