# OBSERVABILITY.md

## Objetivo

Definir padrões gerais de logs, métricas e rastreabilidade.

Para regras obrigatórias por funcionalidade, consultar:

- `OBSERVABILITY_FIRST.md`
- `MONITORING.md`

## Logs

Padrão:

- JSON estruturado
- request_id
- user_id quando autenticado
- ip
- método HTTP
- rota
- status code
- tempo de resposta

## Métricas

- Total de requisições
- Latência
- Erros por rota
- Uso de CPU
- Uso de memória
- Conexões com banco

## Dashboards

- Saúde da API
- Erros
- Latência
- Banco de dados
- Jobs
- Autenticação
