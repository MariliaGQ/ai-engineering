# AI Engineering

Este repositório representa minha trilha contínua em **Engenharia de Inteligência Artificial**, com foco em **arquitetura de sistemas**, **decisões técnicas**, **trade-offs** e **aplicação responsável de IA em contextos reais**.

Mais do que registrar estudos, este espaço documenta **como penso, projeto e avalio soluções de IA**, considerando custo, risco, manutenção, escalabilidade e impacto organizacional.

---

## 🎯 Propósito

- Projetar sistemas que utilizam IA como **componente arquitetural**, não como fim  
- Tomar decisões técnicas explícitas e justificadas  
- Avaliar quando usar IA, e quando não usar  
- Construir soluções sustentáveis para ambientes corporativos reais  

Este repositório funciona como um **hub conceitual e técnico**, conectando projetos independentes que exploram diferentes aspectos da Engenharia de IA.

---

## 🧭 Princípios da trilha

A evolução desta trilha segue princípios claros:

- Todo projeto parte de um **problema bem definido**  
- Arquitetura vem antes da implementação  
- Decisões importantes são documentadas, inclusive alternativas descartadas  
- IA é tratada como parte de um sistema maior (dados, processos, pessoas)  
- Não há resumos de aula, tutoriais genéricos ou experimentos sem contexto  

Nem todo aprendizado vira conteúdo público.  
Apenas o que se transforma em **decisão técnica, arquitetura ou solução aplicada** é documentado aqui.

---

## 🧩 Estrutura dos projetos

Cada projeto referenciado por esta trilha possui seu próprio repositório, contendo, no mínimo:

- `README.md` — contexto, problema e escopo  
- `architecture.md` — visão arquitetural da solução  
- `decisions.md` — decisões técnicas e trade-offs  
- `lessons-learned.md` — aprendizados reais a partir da execução  

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

## 🛠️ Temas e tecnologias explorados

Os projetos desta trilha podem envolver, conforme o problema:

- LLMs e APIs de IA generativa  
- RAG, embeddings e busca semântica  
- Agentes autônomos e orquestração de fluxos  
- Integração com back-end e sistemas existentes  
- Observabilidade, custo e governança em IA  
- Arquitetura AI-first e sistemas híbridos  

Ferramentas variam.  
Os **critérios de engenharia permanecem**.

---

## 📌 Contexto profissional

Grande parte da minha experiência foi construída em ambientes corporativos com código proprietário.  
Este repositório existe para tornar explícito **meu método de engenharia**, respeitando limites éticos e de propriedade intelectual.

---

## 📈 Estado atual

- Trilha estruturada  
- Repositório inicial criado  
- Projetos em planejamento e execução contínua  

Este repositório evolui conforme os projetos são desenvolvidos e amadurecidos.
