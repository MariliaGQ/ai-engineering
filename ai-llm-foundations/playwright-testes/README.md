# Playwright Testes — Geração de Testes com IA

Framework de prompts para geração assistida de testes automatizados com [Playwright](https://playwright.dev) usando o Playwright MCP dentro do Claude Code.

---

## O que este projeto demonstra

Como usar um agente de IA para **gerar testes Playwright de forma confiável**, executando os passos manualmente no browser antes de escrever qualquer código — garantindo que os seletores e fluxos realmente funcionem.

---

## Estrutura

```
playwright-testes/
├── prompts/
│   ├── generate_test.prompt.md   # Prompt principal para geração de testes
│   ├── generate-tests.md         # Variante do prompt de geração
│   └── project-scaffolding.md    # Prompt para setup inicial do projeto Playwright
└── example.mcp.json              # Configuração do Playwright MCP
```

---

## Fluxo de geração de testes

O prompt instrui o agente a seguir este processo:

1. **Executar** cada passo do cenário manualmente usando as ferramentas do Playwright MCP
2. **Observar** os elementos e seletores reais na página
3. **Apenas após** todos os passos serem validados, gerar o código TypeScript
4. **Salvar** o teste no diretório `tests/`
5. **Executar** o teste gerado e iterar até passar

---

## Diretrizes dos prompts

- Usar **Chrome** (não headless) para melhor compatibilidade
- Preferir `getByRole` com nomes semânticos em vez de seletores CSS frágeis
- Testes devem ser **idempotentes** — não dependem de estado pré-existente
- Integração com **GitHub Actions** via relatórios HTML como artefatos

---

## Como usar

### Pré-requisitos

- Claude Code com Playwright MCP configurado
- Node.js e `@playwright/test` instalados (ver `project-scaffolding.md`)

### Configuração do MCP

Adicione o conteúdo de `example.mcp.json` ao `settings.json` do Claude Code.

### Instalação mínima para CI

```bash
npx playwright install chromium --with-deps
```

### Gerar um teste

1. Abra o Claude Code neste diretório
2. Use o conteúdo de `prompts/generate_test.prompt.md` como instrução do agente
3. Descreva o cenário que deseja testar
4. O agente navegará, validará e gerará o teste automaticamente

---

## Tecnologias

- Playwright (`@playwright/test`)
- TypeScript
- Playwright MCP
- GitHub Actions (CI/CD)
- Chrome / Chromium
