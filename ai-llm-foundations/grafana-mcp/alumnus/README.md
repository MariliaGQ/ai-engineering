N|Sentinel Infrastructure

[![alumnus E2E Tests](https://github.com/erickwendel/actions/workflows/alumnus-tests.yaml/badge.svg)](https://github.com/erickwendel/actions/workflows/alumnus-tests.yaml)

Este diretório contém a infraestrutura completa de observabilidade e monitoramento do N|Sentinel, incluindo rastreamento distribuído, coleta de métricas, agregação de logs e alertas.

## 🏗️ Visão Geral da Arquitetura

```
┌─────────────┐
│  Demo App   │ ──────┐
└─────────────┘       │
                      │ OTLP (gRPC)
                      ▼
            ┌──────────────────────┐
            │ OpenTelemetry        │
            │ Collector            │
            │ (Hub Central)        │
            └──────────────────────┘
                      │
        ┌─────────────┼─────────────┬─────────────┐
        │             │             │             │
        ▼             ▼             ▼             ▼
   ┌────────┐   ┌────────┐   ┌────────┐   ┌────────┐
   │ Tempo  │   │  Loki  │   │ Prom   │   │        │
   │(Traces)│   │ (Logs) │   │(Métricas)│  │        │
   └────────┘   └────────┘   └────────┘   └────────┘
        │             │             │             │
        └─────────────┴─────────────┴─────────────┘
                      │
                      ▼
                ┌──────────┐
                │ Grafana  │
                │(Visualização)│
                └──────────┘
```

> **Nota Importante**: As aplicações enviam dados de telemetria apenas para o **OpenTelemetry Collector** via protocolo OTLP. O collector distribui esses dados para os sistemas de backend apropriados (Tempo, Loki, Prometheus) com base no tipo de dado.

## 📦 Componentes

### 🔄 OpenTelemetry Collector (`otel-collector/`)

**Hub central de dados de telemetria** que recebe, processa e exporta dados de observabilidade.

**Responsabilidades**:

- Recebe dados OTLP (traces, métricas, logs) das aplicações via gRPC (porta 4317)
- Distribui traces para o **Tempo**
- Encaminha logs para o **Loki** via OTLP
- Exporta métricas para o **Prometheus**
- Expõe suas próprias métricas na porta 8889

**Configuração**: `otel-collector/otel-collector-config.yaml`

**Portas**:

- `4317`: Receptor OTLP gRPC (as aplicações enviam dados aqui)
- `8889`: Exportador de métricas Prometheus (exposto ao host)

**Fluxo de Dados**:

```
Aplicação → OTLP (gRPC) → Collector → {
    Traces  → Tempo
    Logs    → Loki
    Métricas → Prometheus
}
```

---

### 📊 Prometheus (`prometheus/`)

**Motor de coleta de métricas e alertas** que coleta e armazena dados de séries temporais.

**Responsabilidades**:

- Coleta métricas do OpenTelemetry Collector (porta 8889)
- Monitora a saúde dos serviços via Blackbox Exporter
- Avalia regras de alerta
- Armazena métricas com suporte a exemplares para correlação com traces
- Fornece interface de consulta para o Grafana

**Configuração**:

- `prometheus/prometheus.yaml`: Configurações de coleta e feature flags
- `prometheus/alerts.yaml`: Regras de alerta para disponibilidade e desempenho de serviços

**Funcionalidades Habilitadas**:

- Receptor de escrita OTLP
- Receptor de escrita remota
- Armazenamento de exemplares (vincula métricas a traces)
- Histogramas nativos

**Portas**: `9090` (Interface Web e API, exposto ao host)

---

### 🔍 Tempo (`tempo/`)

**Backend de rastreamento distribuído** otimizado para armazenamento de traces em alto volume.

**Responsabilidades**:

- Recebe traces do OpenTelemetry Collector via OTLP
- Armazena traces de forma eficiente usando formato de armazenamento em objeto
- Fornece API de consulta de traces para o Grafana
- Suporta correlação de traces com logs e métricas

**Configuração**: `tempo/tempo-config.yaml`

**Portas**:

- `3200`: API HTTP (o Grafana consulta aqui, exposto ao host)
- `4317`: Receptor OTLP gRPC (do collector, apenas interno)

**Armazenamento**: Sistema de arquivos local (`./storage/tempo`)

---

### 🗂️ Loki (`loki/`)

**Sistema de agregação de logs** projetado para armazenamento e consulta eficientes de logs.

**Responsabilidades**:

- Recebe logs do OpenTelemetry Collector via OTLP
- Indexa logs por labels (não por texto completo)
- Fornece interface de consulta LogQL
- Correlaciona logs com traces via IDs de trace

**Configuração**: `loki/loki-config.yaml`

**Portas**:

- `3100`: API HTTP (o Grafana consulta aqui, exposto ao host)
- Endpoint OTLP: `http://loki:3100/otlp/v1/logs`

**Armazenamento**: Sistema de arquivos local (`./storage/loki`)

---

### 📈 Grafana (`grafana/`)

**Plataforma unificada de observabilidade** para visualização e exploração.

**Responsabilidades**:

- Visualiza métricas do Prometheus
- Explora traces do Tempo
- Consulta logs do Loki
- Exibe alertas e dashboards
- Correlaciona traces, logs e métricas

**Configuração**:

- `grafana/provisioning/datasources/`: Configurações de fontes de dados
- `grafana/provisioning/dashboards/`: Provisionamento de dashboards
- `grafana/dashboards/`: Arquivos JSON de dashboards
- `grafana/alerting/`: Regras de alerta

**Dashboards**:

1. **Dashboard de Monitoramento de Serviços**: Saúde da infraestrutura e monitoramento blackbox
2. **Métricas HTTP OpenTelemetry**: Métricas de desempenho da aplicação
3. **Visão Geral de Traces**: Acesso rápido às ferramentas de rastreamento

**Fontes de Dados**:

- **Prometheus**: Métricas e alertas
- **Loki**: Agregação de logs com correlação de traces
- **Tempo**: Rastreamento distribuído com mapas de serviço

**Portas**: `3000` (Interface Web, exposto ao host)

**Acesso**: http://localhost:3000 (login automático habilitado como Admin)

---

### 🔲 Blackbox Exporter (`blackbox/`)

**Monitoramento externo** para disponibilidade e desempenho de serviços.

**Responsabilidades**:

- Verifica endpoints HTTP para disponibilidade e tempo de resposta
- Testa conectividade TCP (bancos de dados)
- Realiza pings ICMP para conectividade de rede
- Expõe resultados de sondas como métricas Prometheus

**Configuração**: `blackbox/blackbox.yaml`

**Módulos de Sondagem**:

- `http_2xx`: Verificações de saúde HTTP
- `tcp_connect`: Conectividade de porta TCP
- `icmp_ping`: Acessibilidade de rede

**Portas**: `9115` (Endpoint de métricas, exposto ao host)

---

### 🗄️ Aplicação de Demonstração (`_alumnus/`)

**Aplicação Node.js de exemplo** demonstrando instrumentação OpenTelemetry.

**Funcionalidades**:

- Framework web Fastify
- Integração com banco de dados PostgreSQL
- Instrumentação completa OpenTelemetry (traces, métricas, logs)
- Auto-instrumentação para HTTP, banco de dados e framework
- Atributos e métricas de span customizados

**Instrumentação**:

- Usa `@opentelemetry/sdk-node` para instrumentação automática
- Envia toda a telemetria para o OpenTelemetry Collector via OTLP/gRPC
- Inclui instrumentações para Knex e Fastify

**Endpoints**:

- `GET /health`: Verificação de saúde
- `GET /students`: Endpoint de exemplo com consultas ao banco de dados

**Portas**: `9000` (API HTTP, exposto ao host)

**Banco de Dados**: `alumnus-postgres` (PostgreSQL 16)

- **Porta do Host**: `5433` (mapeada para a porta 5432 do container)
- **Conexão**: `postgresql://alumnus:alumnus_dev_password@localhost:5433/alumnus_app`
- **Conexão Interna**: `postgresql://alumnus:alumnus_dev_password@alumnus-postgres:5432/alumnus_app`

---

## 🚀 Primeiros Passos

### Pré-requisitos

- Docker e Docker Compose
- Node.js 22+ (para executar testes localmente)

### Arquivos Docker Compose

Este projeto utiliza múltiplos arquivos Docker Compose para diferentes finalidades:

- **`docker-compose.yaml`**: Arquivo compose principal que inclui a infraestrutura e inicializa a aplicação de demonstração
- **`docker-compose-infra.yaml`**: Serviços apenas de infraestrutura (para executar testes localmente sem a aplicação)
- **`docker-compose.test.yaml`**: Executa os testes E2E em ambiente containerizado (inclui infraestrutura + runner de testes)
- **`_alumnus/`**: Contém o código da aplicação de demonstração e testes

### Iniciando a Infraestrutura

**Opção 1: Stack Completo (Infraestrutura + Aplicação de Demonstração)**

```bash
# Inicia todos os serviços de infraestrutura E a aplicação de demonstração
docker compose up

# Verificar status dos serviços
docker compose ps
```

**Opção 2: Apenas Infraestrutura (para testes locais)**

```bash
# Inicia apenas os serviços de infraestrutura (sem a aplicação)
# Útil quando você quer executar testes localmente contra a infraestrutura
docker compose -f docker-compose-infra.yaml up

# Em outro terminal, execute os testes
cd _alumnus
npm test
```

**Opção 3: Executar Testes em Container**

```bash
# Executa testes em ambiente containerizado com todas as dependências
# É o que o CI/CD usa — garante ambiente de teste consistente
docker compose -f docker-compose.test.yaml up --abort-on-container-exit
```

### Acessando os Serviços

| Serviço                   | URL                           | Descrição                                                     |
| ------------------------- | ----------------------------- | ------------------------------------------------------------- |
| Grafana                   | http://localhost:3000         | Dashboard principal de observabilidade                        |
| Prometheus                | http://localhost:9090         | Métricas e alertas                                            |
| Tempo                     | http://localhost:3200         | API do Tempo                                                  |
| Loki                      | http://localhost:3100         | API do Loki                                                   |
| Aplicação Demo            | http://localhost:9000         | Aplicação de exemplo                                          |
| PostgreSQL da Demo        | localhost:5433                | Banco de dados PostgreSQL (usuário: alumnus, db: alumnus_app) |
| OTel Collector (gRPC)     | localhost:4317                | Endpoint receptor OTLP                                        |
| OTel Collector (métricas) | http://localhost:8889/metrics | Métricas do próprio collector                                 |
| Blackbox Exporter         | http://localhost:9115         | Métricas de sondagem                                          |

### Configurando a Integração MCP

Após iniciar a infraestrutura com `pnpm alumnus:infra:up`, você pode integrar o Grafana ao MCP (Model Context Protocol) do Windsurf para consultar métricas, logs, traces e alertas diretamente da sua IDE.

**Adicione esta configuração ao seu arquivo MCP do Windsurf** (`~/.codeium/windsurf/mcp_config.json`):

```json
{
  "mcpServers": {
    "grafana": {
      "type": "sse",
      "url": "http://localhost:8000/mcp"
    }
  }
}
```

**Exemplos de Prompts para Testar:**

```
Liste todos os alertas ativos no Prometheus

Consulte o Prometheus para a taxa de requisições HTTP da aplicação alumnus na última hora

Busque logs de erro no Loki nos últimos 30 minutos com IDs de trace

Encontre consultas lentas ao banco de dados em traces do Tempo onde operações PostgreSQL levaram mais de 500ms

Consulte diretamente o Tempo por traces com alta latência na última hora
```

Para mais exemplos de prompts e casos de uso, consulte [`grafana-mcp-prompts.md`](./docs/grafana-mcp-prompts.md).

### Parando os Serviços

```bash
# Parar todos os serviços
docker compose down

# Parar e remover volumes
docker compose down -v
```

---

## 📊 Monitoramento e Alertas

### Serviços Monitorados

#### Verificações de Saúde HTTP (via Blackbox)

- Grafana: `http://grafana:3000/api/health`
- Prometheus: `http://prometheus:9090/-/healthy`
- Loki: `http://loki:3100/ready`
- Tempo: `http://tempo:3200/ready`

#### Conectividade TCP

- PostgreSQL: `postgres:5432`
- PostgreSQL da Demo: `alumnus-postgres:5432`

#### Conectividade de Rede (ICMP)

Todos os serviços são monitorados via ping ICMP para acessibilidade básica de rede.

#### OpenTelemetry Collector

- Monitorado via coleta Prometheus na porta 8889
- Expõe métricas sobre telemetria recebida e exportada

### Regras de Alerta

**Alertas Críticos**:

- `ServiceDown`: Serviço HTTP indisponível por 1+ minuto
- `DatabaseDown`: Banco de dados inacessível por 1+ minuto
- `HighErrorRate`: Taxa de erros > 10% por 5 minutos
- `OpenTelemetryCollectorDown`: Collector indisponível por 1+ minuto

**Alertas de Aviso**:

- `ServiceUnreachable`: Falha no ping ICMP por 2+ minutos
- `SlowResponseTime`: Tempo de resposta > 1s por 5 minutos
- `HighMemoryUsage`: Uso de memória > 80%

**Configuração**: Consulte `prometheus/alerts.yaml` e `grafana/alerting/alerts.yaml`

## 🔗 Correlação de Dados

### Traces → Logs

- IDs de trace são extraídos automaticamente dos logs
- Clique no ID do trace no Loki para ir ao Tempo
- Configurado via `derivedFields` do Loki

### Traces → Métricas

- Exemplares vinculam métricas a traces
- O Prometheus armazena IDs de trace junto com amostras de métricas
- Clique no exemplar no Grafana para visualizar o trace

### Logs → Traces

- Configuração `tracesToLogsV2` do Tempo
- Consulta automaticamente o Loki por logs que correspondem ao ID do trace
- Exibe logs na linha do tempo do trace

---

## 📁 Estrutura de Diretórios

```
infra/
├── README.md                          # Este arquivo
├── docker-compose.yml                 # Serviços de infraestrutura
│
├── _alumnus/                          # Aplicação de exemplo
│   ├── Dockerfile
│   ├── package.json
│   └── src/
│       ├── index.js                   # Código da aplicação
│       ├── otel.js                    # Configuração do OpenTelemetry
│       └── db.js                      # Conexão com o banco de dados
│
├── otel-collector/
│   └── otel-collector-config.yaml     # Configuração do Collector
│
├── prometheus/
│   ├── prometheus.yaml                # Configurações de coleta
│   └── alerts.yaml                    # Regras de alerta
│
├── tempo/
│   └── tempo-config.yaml              # Configuração do Tempo
│
├── loki/
│   └── loki-config.yaml               # Configuração do Loki
│
├── blackbox/
│   └── blackbox.yaml                  # Configurações de sondagem
│
└── grafana/
    ├── provisioning/
    │   ├── datasources/
    │   │   └── datasources.yaml       # Configurações de fontes de dados
    │   └── dashboards/
    │       └── dashboards.yaml        # Provisionamento de dashboards
    ├── dashboards/
    │   ├── service-monitoring.json    # Dashboard de infraestrutura
    │   └── app-metrics.json           # Métricas da aplicação
    └── alerting/
        └── alerts.yaml                # Regras de alerta do Grafana
```

---

## 🛠️ Solução de Problemas

### OpenTelemetry Collector Não Está Recebendo Dados

**Verifique a configuração da aplicação**:

```bash
# Verifique o endpoint OTLP
echo $OTEL_EXPORTER_OTLP_ENDPOINT
# Deve ser: http://opentelemetry-collector:4317
```

**Verifique os logs do collector**:

```bash
docker compose logs opentelemetry-collector
```

### Traces Não Aparecem no Tempo

**Verifique se o collector está encaminhando traces**:

```bash
# Verifique as métricas do collector
curl http://localhost:8889/metrics | grep otelcol_exporter_sent_spans
```

**Verifique os logs do Tempo**:

```bash
docker compose logs tempo
```

### Métricas Não Estão no Prometheus

**Verifique os targets do Prometheus**:

- Acesse http://localhost:9090/targets
- Certifique-se de que o target `otel-collector-metrics` está UP

**Verifique o endpoint de métricas do collector**:

```bash
curl http://localhost:8889/metrics
```

### Logs Não Estão no Loki

**Verifique se o Loki está recebendo dados**:

```bash
# Verifique as métricas do Loki
curl http://localhost:3100/metrics | grep loki_distributor_lines_received_total
```

**Verifique os logs do collector em busca de erros**:

```bash
docker compose logs opentelemetry-collector | grep -i loki
```

### Problemas com Fontes de Dados do Grafana

**Recrie o container do Grafana**:

```bash
docker compose up -d --force-recreate grafana
```

**Verifique a saúde das fontes de dados**:

- Grafana → Configuração → Fontes de Dados
- Teste a conexão de cada fonte de dados

---

## 📚 Recursos Adicionais

### Documentação

- [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)
- [Prometheus](https://prometheus.io/docs/)
- [Grafana Tempo](https://grafana.com/docs/tempo/)
- [Grafana Loki](https://grafana.com/docs/loki/)
- [Blackbox Exporter](https://github.com/prometheus/blackbox_exporter)

---
