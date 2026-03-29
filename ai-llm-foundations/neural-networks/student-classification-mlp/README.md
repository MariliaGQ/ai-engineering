# Student Classification MLP

Implementação minimal de uma **Rede Neural Multi-Layer Perceptron (MLP)** com TensorFlow.js para classificar estudantes em categorias (premium, medium, basic) com base em atributos como idade, cor favorita e localização.

---

## Objetivo

Demonstrar os conceitos fundamentais de uma rede neural de forma simples e comentada:

- Normalização de features numéricas
- One-hot encoding de variáveis categóricas
- Arquitetura MLP com camada oculta e saída softmax
- Treinamento com Adam e categorical cross-entropy
- Predição com saída probabilística

---

## Arquitetura da rede

```
Entrada (7 neurônios)
  └─ idade normalizada [0,1]
  └─ cor: azul, vermelho, verde (one-hot)
  └─ localização: São Paulo, Rio, Curitiba (one-hot)

Camada oculta: 80 neurônios, ativação ReLU
Saída: 3 neurônios, ativação Softmax → [premium, medium, basic]
```

### Por que 80 neurônios?

Com apenas 3 exemplos de treino, mais neurônios aumentam a capacidade de memorização. Em datasets maiores, esse número seria reduzido para evitar overfitting.

### Por que ReLU?

ReLU filtra ativações negativas (zera tudo que é ≤ 0), passando apenas sinais positivos adiante — simples e eficiente para camadas internas.

### Por que Softmax na saída?

Normaliza os 3 valores de saída em probabilidades que somam 1, ideal para classificação multiclasse exclusiva.

---

## Como executar

### Pré-requisitos

```bash
npm install @tensorflow/tfjs-node
```

### Executar

```bash
node index.js
```

### Saída esperada

```
premium (XX.XX%)
medium (XX.XX%)
basic (XX.XX%)
```

---

## Dataset de exemplo

| Nome | Idade | Cor | Localização | Categoria |
|------|-------|-----|-------------|-----------|
| Erick | 30 | Azul | São Paulo | premium |
| Ana | 25 | Vermelho | Rio | medium |
| Carlos | 40 | Verde | Curitiba | basic |

A normalização da idade usa min-max: `(idade - min) / (max - min)`.

---

## Tecnologias

- Node.js
- TensorFlow.js Node (`@tensorflow/tfjs-node`)
- JavaScript (ES6+ com módulos)
