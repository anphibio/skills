# OBSERVABILITY_FIRST.md

## Regra principal

Toda funcionalidade relevante deve nascer observável.

## Obrigatório por funcionalidade

Ao criar ou alterar funcionalidade, avaliar:

- Logs estruturados
- Auditoria
- Métricas Prometheus
- Healthcheck
- Dashboard Grafana
- Template ou item Zabbix
- Alertas
- Rastreamento de erro

## Logs

Registrar eventos importantes com:

- timestamp
- nível
- request_id
- user_id quando autenticado
- ação
- recurso afetado
- resultado
- duração quando aplicável

## Auditoria

Registrar ações críticas:

- Login
- Logout
- Falha de login
- Criação
- Alteração
- Exclusão
- Exportação
- Importação
- Mudança de permissão
- Alteração de configuração
- Ações administrativas

## Métricas mínimas

Para APIs:

- requests_total
- request_duration_seconds
- request_errors_total

Para jobs:

- job_runs_total
- job_failures_total
- job_duration_seconds

Para integrações:

- integration_requests_total
- integration_errors_total
- integration_latency_seconds

## Critério de aceite

Uma funcionalidade crítica só é considerada concluída se:

- [ ] Possui logs adequados
- [ ] Possui auditoria quando necessário
- [ ] Possui métrica ou justificativa para não possuir
- [ ] Não expõe dados sensíveis
- [ ] Pode ser diagnosticada em produção
