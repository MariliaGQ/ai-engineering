# AI LLM Foundations

Este módulo reúne projetos e demos desenvolvidos durante a trilha de fundamentos de **Large Language Models**, cobrindo desde inferência local até sistemas RAG completos, automação com IA e observabilidade de pipelines.

O foco é **entender como LLMs se integram a sistemas reais**: APIs, navegadores, bancos vetoriais, orquestração de agentes e ferramentas de desenvolvimento assistidas por IA.

---

## 📂 Projetos

### 🧠 Redes Neurais

Implementações práticas de redes neurais com TensorFlow.js, explorando conceitos fundamentais de ML aplicados no browser e no Node.js.

| Projeto | Descrição |
|---------|-----------|
| [`neural-networks/student-classification-mlp`](neural-networks/student-classification-mlp/) | MLP simples para classificação de estudantes por age, cor e localização. Implementação single-file com normalização, ReLU e softmax. |
| [`neural-networks/ecommerce-recommendations`](neural-networks/ecommerce-recommendations/) | Sistema de recomendação de e-commerce com TensorFlow.js, MVC e Web Workers para treinamento em background sem bloquear a UI. |
| [`neural-networks/duckhunt-neural-agent`](neural-networks/duckhunt-neural-agent/) | Implementação do jogo Duck Hunt em JavaScript com PixiJS, GSAP e Howler.js — demonstrando renderização WebGL e animações por sprite. |

---

### 🌐 Web AI — Browser Native LLM API

Demonstrações do uso da API nativa de modelos de linguagem do Chrome (Gemini Nano), sem necessidade de servidor externo.

| Projeto | Descrição |
|---------|-----------|
| [`web-ai/web-ai-browser-structure`](web-ai/web-ai-browser-structure/) | Demo mínima da `LanguageModel` API nativa do Chrome com streaming de respostas e renderização Markdown. |
| [`web-ai/web-ai-multimodal`](web-ai/web-ai-multimodal/) | Interface multimodal com suporte a texto, imagem e áudio. Arquitetura MVC, internacionalização e download monitorado do modelo. |
| [`web-ai/web-ai-temperature-and-topk`](web-ai/web-ai-temperature-and-topk/) | Exploração interativa dos parâmetros `temperature` e `topK` com sliders em tempo real, AbortController e geração token a token. |

---

### 🔌 Inferência Local e APIs de LLM

Demonstrações de como acionar modelos de linguagem via CLI e APIs REST.

| Projeto | Descrição |
|---------|-----------|
| [`ollama`](ollama/) | Shell script para inferência local com Ollama — chat completions, geração de texto, streaming e gerenciamento de modelos (llama2, gpt-oss). |
| [`openrouter`](openrouter/) | Shell script para acesso a LLMs via OpenRouter com interface OpenAI-compatível — controle de temperatura, tokens e rastreamento de custo. |

---

### 🗃️ RAG com Embeddings e Banco Vetorial

| Projeto | Descrição |
|---------|-----------|
| [`embeddings-neo4j-rag`](embeddings-neo4j-rag/) | Pipeline RAG completo: ingestão de PDFs → chunks → embeddings locais (HuggingFace `all-MiniLM-L6-v2`) → Neo4j → busca semântica → resposta via OpenRouter (Google Gemma 3 27B). Sem dependência de API para geração de embeddings. |

**Arquitetura:**
```
PDF → Chunking (1000 chars / overlap 200) → Embeddings locais → Neo4j → Busca vetorial (top-3, score > 0.5) → LLM → Resposta salva em disco
```

---

### 🤖 Automação com Playwright MCP

Projetos que exploram automação de navegadores com IA via Model Context Protocol (MCP).

| Projeto | Descrição |
|---------|-----------|
| [`playwright-navegacao`](playwright-navegacao/) | Tarefa de automação: navegar em um Google Forms, extrair dados de um perfil Sessionize e pré-preencher o formulário com JavaScript. |
| [`playwright-testes`](playwright-testes/) | Framework e prompts para geração de testes Playwright com IA — seletores por role, idempotência, integração com GitHub Actions e relatórios HTML. |

---

### 📊 Observabilidade com Grafana MCP

| Projeto | Descrição |
|---------|-----------|
| [`grafana-mcp/alumnus`](grafana-mcp/alumnus/) | Stack completa de observabilidade com OpenTelemetry, Prometheus, Grafana Tempo, Loki e Blackbox Exporter. Inclui app demo em Fastify com PostgreSQL e integração MCP para o IDE. |

**Arquitetura:**
```
App (Fastify) → OTel Collector → Traces (Tempo) + Logs (Loki) + Métricas (Prometheus) → Grafana
```

---

### 🔐 Context7 — Autenticação com Next.js

| Projeto | Descrição |
|---------|-----------|
| [`context7`](context7/) | Demo de autenticação GitHub OAuth com Next.js 15, Better Auth e SQLite local — gerado via Context7 MCP diretamente no IDE. |

---

## 🛠️ Tecnologias cobertas

- **LLMs**: Ollama (local), OpenRouter, Google Gemma, Chrome Gemini Nano
- **Embeddings**: HuggingFace Transformers (`Xenova/all-MiniLM-L6-v2`)
- **Banco vetorial**: Neo4j 5.14 com APOC
- **Orquestração RAG**: LangChain (Node.js)
- **Redes neurais**: TensorFlow.js (Node + Browser)
- **Automação**: Playwright MCP
- **Observabilidade**: OpenTelemetry, Prometheus, Grafana Tempo, Loki
- **Web**: PixiJS, Next.js 15, Better Auth
- **Runtime**: Node.js v22, TypeScript, Docker

---

## 📌 Observações

- Os projetos `playwright-navegacao`, `playwright-testes` e `context7` são orientados por prompts — o código gerado depende do MCP configurado no IDE.
- O projeto `grafana-mcp` pode ser executado isoladamente (apenas infra) ou com o app demo completo via Docker Compose.
- Os projetos de `web-ai` exigem **Chrome Canary** com as flags experimentais de IA habilitadas.
