# Ollama — Inferência Local de LLMs

Demo de como acionar modelos de linguagem localmente via [Ollama](https://ollama.com), usando as APIs REST `/v1/chat/completions` e `/api/generate`.

---

## O que é o Ollama?

Ollama é um runtime local para LLMs que expõe uma API REST compatível com o padrão OpenAI. Permite executar modelos como LLaMA, Gemma e outros diretamente na máquina, sem depender de serviços externos.

---

## Como executar

### Pré-requisitos

- [Ollama](https://ollama.com) instalado e em execução (`ollama serve`)
- `curl` e `jq` disponíveis no terminal

### Baixar os modelos

```bash
ollama pull llama2-uncensored:7b
ollama pull gpt-oss:20b
```

### Rodar o script

```bash
bash request.sh
```

---

## O que o script demonstra

### 1. Chat Completions API (`/v1/chat/completions`)

Endpoint compatível com OpenAI. Retorna resposta estruturada em JSON com `choices`, `usage` e `model`.

```bash
curl -X POST http://localhost:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "llama2-uncensored:7b", "messages": [...]}'
```

### 2. Generate API (`/api/generate`) — sem streaming

Endpoint nativo do Ollama. Suporta acesso ao campo `thinking` de modelos com raciocínio explícito.

```bash
curl -X POST http://localhost:11434/api/generate \
  -d '{"model": "gpt-oss:20b", "prompt": "...", "stream": false}'
```

### 3. Generate API com streaming

Mesmo endpoint, com `"stream": true` — retorna tokens à medida que são gerados.

---

## Modelos usados

| Modelo | Tipo | Observação |
|--------|------|-----------|
| `llama2-uncensored:7b` | Chat | Sem filtros de conteúdo |
| `gpt-oss:20b` | Chat com reasoning | Possui filtros e campo `thinking` no response |

---

## Comparação de comportamento

O script usa a mesma prompt nos dois modelos para ilustrar a diferença de comportamento entre um modelo sem filtros e um com política de conteúdo — o `gpt-oss:20b` recusa e expõe o raciocínio via campo `thinking`.

---

## Tecnologias

- Ollama (runtime local)
- cURL (requisições HTTP)
- jq (parse e formatação de JSON)
