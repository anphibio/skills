# MONITORING.md

## Objetivo

Definir padrões de monitoramento para aplicações corporativas.

## Endpoints recomendados

- `/health`
- `/ready`
- `/metrics`

## Healthcheck

O healthcheck deve validar:

- Aplicação em execução
- Conexão com banco
- Dependências críticas
- Filas ou workers quando aplicável

## Métricas Prometheus

Quando aplicável, expor:

- Total de requisições
- Latência por rota
- Erros por rota
- Status codes
- Uso de CPU
- Uso de memória
- Conexões com banco
- Tempo de resposta do banco
- Jobs executados
- Jobs com erro
- Filas pendentes
- Logins com sucesso
- Falhas de login

## Grafana

Todo sistema relevante deve possuir dashboard com:

- Saúde da API
- Requisições por minuto
- Latência
- Erros 4xx/5xx
- Banco de dados
- Jobs
- Autenticação
- Recursos do container

## Zabbix

Quando o ambiente utilizar Zabbix, criar ou preparar:

- Template de aplicação
- Itens para healthcheck
- Itens para métricas principais
- Triggers de indisponibilidade
- Triggers de erro elevado
- Triggers de latência elevada
- Dashboard básico

## Alertas

Alertar em:

- API indisponível
- Banco indisponível
- Erro 5xx elevado
- Latência elevada
- Falha de backup
- Disco cheio
- Falha de job crítico
