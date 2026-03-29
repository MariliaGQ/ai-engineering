# Web AI Multimodal

Interface multimodal usando a **API nativa de Language Model do Chrome** com suporte a entradas de texto, imagem e áudio — sem backend, sem API key.

---

## O que demonstra

- Uso da `LanguageModel` API com inputs multimodais (texto + arquivo)
- Arquitetura **MVC** em JavaScript puro no browser
- Internacionalização com `translationService`
- Monitoramento do download do modelo Gemini Nano
- Streaming de respostas com renderização Markdown incremental
- Tratamento de erros para ambientes sem suporte à API

---

## Estrutura

```
web-ai-multimodal/
├── index.html
├── index.js                        # Bootstrap da aplicação
├── controllers/
│   └── formController.js           # Lógica do formulário e envio
├── services/
│   ├── aiService.js                # Integração com LanguageModel API
│   └── translationService.js      # Internacionalização
└── views/
    └── view.js                     # Manipulação do DOM
```

---

## Como executar

1. Abra `index.html` no Chrome Canary
2. Aguarde o download do modelo (monitorado automaticamente)
3. Faça uma pergunta e, opcionalmente, anexe uma imagem ou arquivo de áudio

### Requisitos

- **Chrome Canary** com flags experimentais habilitadas:
  - `chrome://flags/#optimization-guide-on-device-model` → Enabled BypassPerfRequirement
  - `chrome://flags/#prompt-api-for-gemini-nano` → Enabled
- Modelo Gemini Nano instalado localmente (`chrome://components/`)

---

## Funcionalidades

| Feature | Descrição |
|---------|-----------|
| Upload de imagem | Suporte a arquivos de imagem como entrada multimodal |
| Upload de áudio | Suporte a arquivos de áudio como entrada multimodal |
| Streaming | Tokens gerados incrementalmente no DOM |
| i18n | Mensagens internacionalizadas via `translationService` |
| Validação | Verifica versão do Chrome e disponibilidade da API antes de executar |
| Download monitoring | Detecta e exibe progresso de download do modelo |

---

## Tecnologias

- Browser native `LanguageModel` API (Chrome Gemini Nano)
- JavaScript ES6+ (MVC pattern)
- HTML5 File API
- Markdown rendering
