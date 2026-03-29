# Context7 — Geração de Código com MCP

Demonstração do uso do **Context7 MCP** para gerar projetos com documentação atualizada diretamente no IDE, sem depender do knowledge cutoff do modelo.

---

## O que é o Context7?

[Context7](https://context7.com) é um MCP server que injeta documentação atualizada de bibliotecas diretamente no contexto do agente antes de gerar código. Resolve o problema comum de LLMs gerarem código desatualizado ou com APIs obsoletas.

---

## Projeto gerado

### [`nextjs-better-auth-demo`](nextjs-better-auth-demo/)

Demo de autenticação com GitHub OAuth usando:

- **Next.js 15** (App Router)
- **Better Auth** — biblioteca de autenticação moderna para Next.js
- **SQLite** com `better-sqlite3` — persistência local sem banco externo
- **TypeScript** e **Tailwind CSS**

O projeto foi gerado com o Context7 MCP ativo, garantindo que as APIs do Better Auth usadas estejam alinhadas com a versão atual da biblioteca.

---

## Como o Context7 foi usado

O arquivo `prompt.md` (no projeto gerado) contém a instrução enviada ao agente com Context7 MCP ativo. O MCP buscou automaticamente a documentação do Better Auth e Next.js 15 antes de gerar o código.

---

## Como executar o projeto gerado

```bash
cd nextjs-better-auth-demo
npm install
npm run dev
```

Acesse `http://localhost:3000` e faça login com GitHub OAuth.

### Variáveis de ambiente necessárias

```env
GITHUB_CLIENT_ID=...
GITHUB_CLIENT_SECRET=...
BETTER_AUTH_SECRET=...
```

---

## Tecnologias

- Context7 MCP (documentação em tempo real)
- Next.js 15 (App Router)
- Better Auth
- SQLite / better-sqlite3
- TypeScript
- Tailwind CSS
