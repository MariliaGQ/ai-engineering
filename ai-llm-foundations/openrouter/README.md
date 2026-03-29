# OpenRouter — Acesso a LLMs via API Unificada

Demo de como consumir modelos de linguagem via [OpenRouter](https://openrouter.ai), plataforma que oferece acesso a múltiplos LLMs com interface compatível com OpenAI.

---

## O que é o OpenRouter?

OpenRouter é uma API gateway que permite acessar dezenas de modelos (Google, Anthropic, Meta, Mistral, etc.) com um único endpoint e formato de requisição OpenAI-compatível. Inclui roteamento por custo, disponibilidade e rastreamento de uso.

---

## Como executar

### Pré-requisitos

- `curl` e `jq` instalados
- Chave de API do OpenRouter: [openrouter.ai/keys](https://openrouter.ai/keys)

### Configuração

Crie um arquivo `.env` na raiz do projeto:

```env
OPENROUTER_API_KEY=sk-or-...
```

### Rodar o script

```bash
bash request.sh
```

---

## O que o script demonstra

Envia uma pergunta em português ao modelo **Google Gemma 3 27B** via OpenRouter e imprime a resposta completa formatada com `jq`.

```bash
curl -X POST https://openrouter.ai/api/v1/chat/completions \
  -H "Authorization: Bearer $OPENROUTER_API_KEY" \
  -H "HTTP-Referer: $OPENROUTER_SITE_URL" \
  -H "X-Title: $OPENROUTER_SITE_NAME" \
  -d '{"model": "google/gemma-3-27b-it:free", "messages": [...], "temperature": 0.3}'
```

### Headers relevantes

| Header | Finalidade |
|--------|-----------|
| `Authorization` | Autenticação com a chave da API |
| `HTTP-Referer` | Identifica a aplicação de origem (para analytics) |
| `X-Title` | Nome exibido no painel do OpenRouter |

### Campos no response

O OpenRouter retorna campos extras além do padrão OpenAI:

- `provider` — qual provedor serviu a requisição (ex: "Google AI Studio")
- `usage.cost` — custo da chamada em USD
- `usage.cost_details` — detalhamento por tokens de prompt e completion

---

## Modelo utilizado

| Modelo | Provider | Tier |
|--------|----------|------|
| `google/gemma-3-27b-it:free` | Google AI Studio | Gratuito |

---

## Tecnologias

- OpenRouter API
- cURL (requisições HTTP)
- jq (parse e formatação de JSON)
- Variáveis de ambiente via `.env`
