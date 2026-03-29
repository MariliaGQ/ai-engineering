# Web AI — Browser Native LLM API

Demos de uso da **API nativa de Language Model do Chrome** (Gemini Nano), que permite executar um LLM diretamente no browser sem servidor, sem API key e sem latência de rede.

---

## Pré-requisito comum a todos os projetos

Todos os projetos desta pasta exigem **Chrome Canary** com as seguintes flags habilitadas:

1. Acesse `chrome://flags/#optimization-guide-on-device-model` → **Enabled BypassPerfRequirement**
2. Acesse `chrome://flags/#prompt-api-for-gemini-nano` → **Enabled**
3. Reinicie o Chrome
4. Acesse `chrome://components/` e aguarde o download do **Optimization Guide On Device Model**

---

## Projetos

### [`web-ai-browser-structure`](web-ai-browser-structure/)

Demo mínima da `LanguageModel` API. Single-file HTML com streaming token a token e renderização Markdown. Ponto de partida para entender a API.

---

### [`web-ai-multimodal`](web-ai-multimodal/)

Interface multimodal com suporte a texto, imagem e áudio. Arquitetura MVC, internacionalização, monitoramento de download do modelo e tratamento de erros para ambientes sem suporte.

---

### [`web-ai-temperature-and-topK`](web-ai-temperature-and-topK/)

Playground interativo para explorar os parâmetros `temperature` e `topK` com sliders em tempo real. Demonstra como esses valores afetam a criatividade e determinismo das respostas.

---

## Por que a API nativa do browser?

| Vantagem | Descrição |
|---------|-----------|
| Zero latência de rede | Inferência acontece localmente na GPU/CPU do usuário |
| Sem custo de API | Não consome tokens de serviços pagos |
| Privacidade | Dados não saem do dispositivo |
| Offline | Funciona sem conexão após download do modelo |

---

## Limitações

- Disponível apenas no Chrome Canary (experimental)
- Requer hardware compatível (memória e GPU suficientes)
- Modelo único: Gemini Nano (não é possível escolher outro modelo)
- API ainda em fase experimental — pode mudar entre versões
