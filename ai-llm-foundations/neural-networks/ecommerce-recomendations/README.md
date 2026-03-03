# Sistema de Recomendação de E-commerce

Uma aplicação web que exibe perfis de usuários e catálogo de produtos, com a capacidade de rastrear compras de usuários para futuras recomendações usando Redes neurais com TensorFlow.js.

## 📋 Descrição

Este projeto demonstra a integração de um sistema de recomendação inteligente em uma plataforma de e-commerce. A aplicação permite que usuários visualizem seus perfis, histórico de compras passadas e catálogo de produtos disponíveis, enquanto rastreia as interações para alimentar um modelo de machine learning que pode gerar recomendações personalizadas.

## 🏗️ Estrutura do Projeto

```
ecommerce-recomendations/
├── index.html                    # Arquivo HTML principal
├── style.css                     # Estilos da aplicação
├── index.js                      # Ponto de entrada da aplicação
├── package.json                  # Dependências do projeto
├── demo.png                      # Imagem de demonstração
├── README.md                     # Este arquivo
├── data/
│   ├── products.json             # Catálogo de produtos
│   └── users.json                # Dados de usuários
├── src/
│   ├── index.js                  # Script principal
│   ├── controller/               # Controladores (padrão MVC)
│   │   ├── ModelTrainingController.js
│   │   ├── ProductController.js
│   │   ├── TFVisorController.js
│   │   ├── UserController.js
│   │   └── WorkerController.js
│   ├── events/                   # Gerenciamento de eventos
│   │   ├── constants.js
│   │   └── events.js
│   ├── service/                  # Lógica de negócios
│   │   ├── ProductService.js
│   │   └── UserService.js
│   ├── view/                     # Componentes de visualização
│   │   ├── ModelTrainingView.js
│   │   ├── ProductView.js
│   │   ├── TFVisorView.js
│   │   ├── UserView.js
│   │   ├── View.js
│   │   └── templates/            # Templates HTML
│   │       ├── past-purchase.html
│   │       └── product-card.html
│   └── workers/                  # Web Workers
│       └── modelTrainingWorker.js
```

## 🚀 Configuração e Execução

### Pré-requisitos
- Node.js (v14 ou superior)
- npm (v6 ou superior)

### Instalação

1. Clone ou acesse o repositório
2. Instale as dependências:
```bash
npm install
```

3. Inicie a aplicação:
```bash
npm start
```

4. Abra seu navegador e acesse `http://localhost:8080`

## ✨ Funcionalidades

- **Seleção de Perfil de Usuário**: Visualize informações detalhadas de diferentes usuários
- **Histórico de Compras**: Exibição das compras passadas de cada usuário
- **Catálogo de Produtos**: Lista completa de produtos disponíveis para compra
- **Rastreamento de Compras**: Registro de novas compras usando sessionStorage
- **Visualização TensorFlow.js**: Interface para monitorar o treinamento do modelo
- **Web Workers**: Processamento de treinamento de modelo em background

## 🛠️ Tecnologias Utilizadas

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Machine Learning**: TensorFlow.js
- **Arquitetura**: Padrão MVC (Model-View-Controller)
- **Web APIs**: Web Workers, sessionStorage
- **Build Tool**: Node.js / npm

## 📚 Padrões de Arquitetura

### Padrão MVC
- **Model**: Serviços (ProductService, UserService)
- **View**: Classes de visualização (ProductView, UserView, etc.)
- **Controller**: Controladores que conectam views e services

### Separação de Responsabilidades
- **Controllers**: Gerenciam a lógica de aplicação e comunicação entre componentes
- **Services**: Manipulam dados e lógica de negócios
- **Views**: Responsáveis apenas pela renderização do DOM
- **Events**: Sistema centralizado de eventos para comunicação entre componentes

## 🔄 Fluxo da Aplicação

1. Usuário seleciona um perfil
2. Sistema exibe informações do usuário e histórico de compras
3. Produtos são carregados e exibidos
4. Usuário pode realizar compras ("Buy Now")
5. Compras são rastreadas para treinamento de modelo
6. Modelo de recomendação é treinado em background usando Web Workers



### Para Desenvolvedores

1. Revise a estrutura em `src/` para entender a arquitetura
2. Modifique os dados em `data/products.json` e `data/users.json`
3. Estenda os Services para adicionar novas funcionalidades
4. Crie novos Controllers conforme necessário
5. Execute testes e valide as mudanças

### Para Usuários

1. Selecione um usuário no painel lateral
2. Visualize suas informações e compras anteriores
3. Navegue pelo catálogo de produtos
4. Clique em "Buy Now" para registrar uma compra
5. Observe o treinamento do modelo na seção TensorFlow.js

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

## 📝 Licença

Este é um projeto educacional.
MIT.

