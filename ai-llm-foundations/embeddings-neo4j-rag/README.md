# Embeddings + Neo4j RAG

Sistema de **Retrieval-Augmented Generation (RAG)** que processa documentos PDF, gera embeddings localmente com HuggingFace Transformers e armazena vetores no Neo4j para realizar buscas semânticas — combinando o contexto recuperado com um LLM via OpenRouter para gerar respostas.

## Como funciona

```
PDF → Chunking → Embeddings (local) → Neo4j Vector Store
                                              ↓
                         Pergunta → Busca semântica → Contexto → LLM → Resposta
```

1. **Ingestão**: o PDF é carregado, dividido em chunks de 1000 caracteres (overlap de 200) e cada chunk é convertido em um vetor pelo modelo `Xenova/all-MiniLM-L6-v2` rodando localmente
2. **Armazenamento**: os vetores são persistidos no Neo4j como nós do tipo `Chunk` com índice vetorial
3. **Recuperação**: para cada pergunta, os `topK=3` chunks mais similares (score > 0.5) são recuperados
4. **Geração**: o contexto recuperado é passado a um LLM (Google Gemma 3 via OpenRouter) junto com o prompt configurado

## Pré-requisitos

- Node.js `v22.13.1`
- Docker e Docker Compose

## Instalação

```bash
npm ci
```

## Configuração

Copie o `.env` e preencha as variáveis:

```env
# OpenRouter
OPENROUTER_API_KEY=sk-or-v1-...
OPENROUTER_SITE_URL=http://localhost:3000
OPENROUTER_SITE_NAME=RAG Example

# Modelos
NLP_MODEL='google/gemma-3-27b-it:free'
EMBEDDING_MODEL='Xenova/all-MiniLM-L6-v2'

# Neo4j
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_password_here
NEO4J_URI=bolt://localhost:7687
NEO4J_DATABASE=neo4j
```

> O modelo de embedding roda **localmente** via Transformers.js — não requer chave de API.

## Uso

### Subir a infraestrutura (Neo4j)

```bash
npm run infra:up
```

Acesse o Neo4j Browser em [http://localhost:7474](http://localhost:7474) (usuário: `neo4j`, senha: configurada no `.env`).

### Executar o pipeline RAG

```bash
npm start
# ou em modo dev (watch)
npm run dev
```

O script irá:
1. Carregar e dividir o PDF `tensores.pdf`
2. Gerar embeddings e popular o Neo4j
3. Executar perguntas de exemplo e salvar as respostas em `./respostas/`

### Derrubar a infraestrutura

```bash
npm run infra:down
```

## Estrutura do projeto

```
├── src/
│   ├── index.ts            # Ponto de entrada — orquestra todo o pipeline
│   ├── config.ts           # Configurações centralizadas (Neo4j, LLM, embeddings)
│   ├── documentProcessor.ts# Carrega o PDF e divide em chunks
│   ├── ai.ts               # Classe AI — busca vetorial + geração de resposta
│   └── util.ts             # Utilitários
├── prompts/
│   ├── answerPrompt.json   # Configuração do prompt (role, task, constraints)
│   └── template.txt        # Template de prompt com variáveis
├── respostas/              # Respostas geradas (criado em runtime)
├── tensores.pdf            # Documento base do RAG
├── docker-compose.yml      # Neo4j 5.14 com plugin APOC
└── .env                    # Variáveis de ambiente
```

## Stack

| Camada | Tecnologia |
|---|---|
| Runtime | Node.js v22 + TypeScript (strip types) |
| Embeddings | `Xenova/all-MiniLM-L6-v2` via `@huggingface/transformers` |
| Vector Store | Neo4j 5.14 Community + `@langchain/community` |
| LLM | Google Gemma 3 27B via OpenRouter |
| Orquestração | LangChain (`@langchain/core`, `@langchain/openai`) |
| PDF | `pdf-parse` + `PDFLoader` do LangChain |
