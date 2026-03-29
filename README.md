# AI Engineering

Este repositório documenta minha trilha prática em **Engenharia de Inteligência Artificial** — organizada em módulos temáticos que cobrem fundamentos, ferramentas e padrões de sistemas com IA.

Cada módulo reúne experimentos, demos e implementações desenvolvidos ao longo dos estudos, com foco em entender **como as peças se conectam em sistemas reais**: APIs, modelos locais, pipelines de dados, automação e observabilidade.

---

## 🎯 Propósito

- Construir fluência prática com as principais tecnologias de IA generativa
- Entender trade-offs reais: custo, latência, qualidade, privacidade
- Explorar integrações entre LLMs e sistemas existentes
- Documentar o que foi feito e o que foi aprendido no processo

---

## 📂 Projetos

### 🔹 [AI LLM Foundations](ai-llm-foundations/)

Fundamentos práticos de Large Language Models — inferência local, APIs de LLM, browser AI, RAG com banco vetorial, redes neurais, automação com Playwright MCP e observabilidade com OpenTelemetry.

| Módulo | Descrição |
|--------|-----------|
| [Ollama](ai-llm-foundations/ollama/) | Inferência local via API REST — chat completions, streaming e comparação de comportamento entre modelos |
| [OpenRouter](ai-llm-foundations/openrouter/) | Acesso a LLMs cloud com interface OpenAI-compatível e rastreamento de custo |
| [Web AI](ai-llm-foundations/web-ai/) | 3 demos da `LanguageModel` API nativa do Chrome (Gemini Nano): estrutura básica, multimodal e exploração de temperature/topK |
| [Redes Neurais](ai-llm-foundations/neural-networks/) | MLP com TensorFlow.js: classificação de estudantes, recomendações de e-commerce e Duck Hunt com PixiJS |
| [RAG com Neo4j](ai-llm-foundations/embeddings-neo4j-rag/) | Pipeline RAG completo: PDF → chunks → embeddings locais (HuggingFace) → Neo4j → busca vetorial → LLM |
| [Playwright MCP](ai-llm-foundations/playwright-navegacao/) | Automação de formulário web com agente de IA — extração de dados e preenchimento autônomo |
| [Playwright Testes](ai-llm-foundations/playwright-testes/) | Geração de testes Playwright com IA — validação real antes de gerar código |
| [Grafana MCP](ai-llm-foundations/grafana-mcp/) | Stack de observabilidade com OTel, Prometheus, Tempo e Loki — integrada ao IDE via MCP |
| [Context7](ai-llm-foundations/context7/) | Geração de código com documentação atualizada via Context7 MCP (demo: Next.js + Better Auth) |

---

## 🛠️ Temas explorados

- LLMs e APIs de IA generativa (Ollama, OpenRouter, Gemini Nano)
- RAG, embeddings e busca semântica
- Redes neurais com TensorFlow.js
- Agentes com ferramentas (MCP — Playwright, Grafana, Context7)
- Observabilidade de pipelines com OpenTelemetry
- Automação de browser e geração de testes com IA

---

## 📌 Contexto

Grande parte da minha experiência foi construída em ambientes corporativos com código proprietário.
Este repositório existe para tornar visível o aprendizado técnico contínuo, de forma aplicada e documentada.

---

## 📈 Estado atual

- Módulo 1 — AI LLM Foundations: **concluído**
- Próximos módulos em desenvolvimento
