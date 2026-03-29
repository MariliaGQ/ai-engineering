# Grafana MCP — Observabilidade com IA

Demonstração de stack completa de observabilidade integrada com **Grafana MCP**, permitindo que agentes de IA consultem métricas, traces e logs diretamente do IDE.

---

## O que é o Grafana MCP?

O Grafana MCP server expõe as APIs do Grafana como ferramentas para agentes de IA (Claude Code, Cursor, etc.), permitindo consultar dashboards, explorar traces no Tempo, buscar logs no Loki e analisar métricas do Prometheus sem sair do IDE.

---

## Projeto

### [`alumnus`](alumnus/)

Stack completa de observabilidade com uma aplicação demo instrumentada com OpenTelemetry.

**Infraestrutura:**

```
App Fastify + PostgreSQL
      ↓ OTLP (gRPC)
OTel Collector
      ↓
┌─────┬──────┬────────────┐
Tempo  Loki  Prometheus
      ↓
   Grafana
```

**Componentes:**

| Serviço | Função | Porta |
|---------|--------|-------|
| Grafana | Visualização e alertas | 3000 |
| Prometheus | Métricas + regras de alerta | 9090 |
| Grafana Tempo | Distributed tracing | 3200 |
| Grafana Loki | Agregação de logs | 3100 |
| OTel Collector | Recepção e roteamento de telemetria | — |
| Blackbox Exporter | Health checks externos | — |
| App demo (Fastify) | Aplicação instrumentada | 9000 |
| PostgreSQL | Banco da aplicação demo | 5433 |

**Recursos da stack:**
- Correlação trace ↔ logs (clique em um trace e veja os logs relacionados)
- Exemplars linkando métricas a traces específicos
- Auto-instrumentação OpenTelemetry no Node.js
- Alertas: `ServiceDown`, `DatabaseDown`, `HighErrorRate`
- Múltiplos cenários via Docker Compose (infra, app, testes)

---

## Como executar

```bash
cd alumnus
docker compose up -d
```

Ver [`alumnus/README.md`](alumnus/README.md) para instruções detalhadas de cada cenário.

---

## Tecnologias

- Docker & Docker Compose
- OpenTelemetry (SDK Node.js + Collector)
- Grafana, Prometheus, Tempo, Loki
- Blackbox Exporter
- Fastify + PostgreSQL (app demo)
- Grafana MCP server
