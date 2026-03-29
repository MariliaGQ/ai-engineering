# Playwright Navegação — Automação de Formulário com IA

Demo de automação de navegador usando o [Playwright MCP](https://github.com/microsoft/playwright-mcp), onde um agente de IA executa um fluxo completo: lê um formulário, extrai dados de um perfil externo e preenche os campos automaticamente.

---

## O que este projeto demonstra

O uso do Playwright MCP como ferramenta de um agente de IA para:

1. Navegar até um Google Forms e identificar os campos necessários
2. Acessar um perfil público no Sessionize e extrair informações relevantes
3. Selecionar uma palestra em português com JavaScript no título
4. Preencher o formulário com os dados extraídos (sem submeter)

---

## Prompt

O arquivo [`prompt.md`](prompt.md) contém a instrução completa enviada ao agente:

> Navegue até o formulário `https://forms.gle/5mGHXVKDLMFtjwBz7` e veja quais campos são necessários. Então navegue até `https://sessionize.com/erickwendel`, obtenha os dados do perfil, escolha uma palestra em português com JavaScript no título e preencha o formulário. Não aperte submit.

---

## Como executar

### Pré-requisitos

- Claude Code com Playwright MCP configurado
- Chrome instalado

### Configuração do MCP

O arquivo [`example.mcp.json`](example.mcp.json) contém a configuração do servidor Playwright MCP. Adicione ao seu `settings.json` do Claude Code.

### Execução

1. Abra o Claude Code neste diretório
2. Abra o arquivo `prompt.md`
3. Envie o conteúdo como prompt ao agente com Playwright MCP ativo
4. O agente navegará, extrairá dados e preencherá o formulário autonomamente

---

## Tecnologias

- Playwright MCP (automação de navegador via Model Context Protocol)
- Claude Code (agente executor)
- Google Forms (destino do preenchimento)
- Sessionize (fonte de dados)
