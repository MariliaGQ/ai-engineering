# Web AI Browser Structure

Demo mínima da **API nativa de Language Model do Chrome** (`LanguageModel`), usando o modelo Gemini Nano embutido no browser — sem servidor, sem API key, sem dependências de build.

---

## O que demonstra

- Como verificar e usar os parâmetros padrão do modelo (`defaultTemperature`, `defaultTopK`)
- Como criar uma sessão com `LanguageModel.create()` com system prompt em português
- Como fazer streaming de resposta token a token com `promptStreaming()`
- Como renderizar o output em Markdown no DOM

---

## Como executar

1. Abra o arquivo `index.html` diretamente no Chrome Canary
2. A resposta para "Quem inventou o JavaScript?" será gerada automaticamente na tela

### Requisitos

- **Chrome Canary** (versão 127+) com as flags experimentais habilitadas:
  - `chrome://flags/#optimization-guide-on-device-model` → Enabled BypassPerfRequirement
  - `chrome://flags/#prompt-api-for-gemini-nano` → Enabled
- O modelo Gemini Nano precisa estar baixado localmente (verificar em `chrome://components/`)

---

## Estrutura do código

O arquivo `index.html` contém toda a lógica inline:

```js
const params = await LanguageModel.params()          // lê defaults do browser
const session = await LanguageModel.create({...})    // cria sessão com system prompt
const stream = await session.promptStreaming([...])  // streaming de tokens
for await (const token of stream) { ... }            // renderiza incrementalmente
```

---

## Tecnologias

- Browser native `LanguageModel` API (Chrome Gemini Nano)
- [markdown.js](https://cdn.jsdelivr.net/npm/markdown@0.5.0) via CDN (renderização de Markdown)
- HTML/JavaScript puro — sem build, sem framework
