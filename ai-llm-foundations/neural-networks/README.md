# Neural Networks

Projetos de redes neurais com TensorFlow.js, cobrindo desde classificação simples até sistemas de recomendação e jogos com renderização WebGL.

---

## Projetos

### [`student-classification-mlp`](student-classification-mlp/)

MLP minimal para classificar estudantes em categorias (premium, medium, basic) com base em idade, cor e localização. Implementação single-file com comentários explicativos sobre cada decisão arquitetural da rede.

**Destaques:** normalização min-max, one-hot encoding, ReLU, Softmax, Adam, categorical cross-entropy.

---

### [`ecommerce-recomendations`](ecommerce-recomendations/)

Sistema de recomendação de produtos para e-commerce usando TensorFlow.js no browser. Treina um modelo em background via Web Workers para não bloquear a UI e classifica usuários em perfis de consumo (premium/medium/basic).

**Destaques:** MVC, Web Workers, TensorFlow.js browser, tfjs-visor para visualização, sessionStorage para rastreamento de compras.

---

### [`duckhunt-neural-agent`](duckhunt-neural-agent/)

Implementação completa do jogo Duck Hunt em JavaScript com renderização WebGL via PixiJS, animações com GSAP e áudio com Howler.js. Demonstra integração de múltiplas bibliotecas frontend com Webpack e Babel.

**Destaques:** PixiJS (WebGL/Canvas), GSAP, Howler.js, MovieClip animations, Webpack, Gulp para assets.

---

## Tecnologias comuns

- TensorFlow.js (`@tensorflow/tfjs-node` e versão browser)
- JavaScript ES6+
- Node.js

## Requisitos por projeto

| Projeto | Runtime | Dependências principais |
|---------|---------|------------------------|
| student-classification-mlp | Node.js | `@tensorflow/tfjs-node` |
| ecommerce-recomendations | Browser | TensorFlow.js browser, Browser-Sync |
| duckhunt-neural-agent | Browser | PixiJS, GSAP, Howler.js, Webpack |
