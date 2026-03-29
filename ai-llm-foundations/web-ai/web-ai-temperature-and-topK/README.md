# Web AI Temperature & TopK

Demo interativa para explorar como os parâmetros **temperature** e **topK** influenciam as respostas de um LLM, usando a API nativa do Chrome (Gemini Nano).

---

## O que demonstra

- Ajuste em tempo real de `temperature` e `topK` via sliders
- Recriação de sessão com novos parâmetros sem recarregar a página
- Cancelamento de geração com `AbortController`
- Geração token a token com streaming

---

## Os parâmetros

### Temperature (0 a 2)
Controla a aleatoriedade da geração. Valores baixos tornam o modelo mais determinístico e previsível; valores altos geram respostas mais criativas e variadas.

| Valor | Comportamento |
|-------|--------------|
| ~0.1 | Muito determinístico, respostas repetíveis |
| ~0.7 | Balanceado (uso geral) |
| ~1.5+ | Alta criatividade, pode perder coerência |

### TopK (1 a 128)
Limita o vocabulário considerado a cada token gerado. Com `topK=1` o modelo sempre escolhe a palavra mais provável; valores maiores aumentam a diversidade.

| Valor | Comportamento |
|-------|--------------|
| 1 | Greedy decoding — sempre o token mais provável |
| ~40 | Padrão comum, bom equilíbrio |
| 128 | Máxima diversidade no vocabulário |

---

## Como executar

1. Abra `index.html` no Chrome Canary
2. Ajuste os sliders de temperature e topK
3. Envie uma pergunta e observe como a resposta varia

### Parar a geração

Clique em "Stop" durante a geração — usa `AbortController` para cancelar o stream.

### Requisitos

- **Chrome Canary** com flags:
  - `chrome://flags/#optimization-guide-on-device-model` → Enabled BypassPerfRequirement
  - `chrome://flags/#prompt-api-for-gemini-nano` → Enabled
- Modelo Gemini Nano instalado localmente

---

## Tecnologias

- Browser native `LanguageModel` API (Chrome Gemini Nano)
- `AbortController` (cancelamento de stream)
- HTML range inputs (sliders interativos)
- JavaScript ES6+
