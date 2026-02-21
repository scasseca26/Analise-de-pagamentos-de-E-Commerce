# Análise de Pagamentos — E-commerce
![Excel](https://img.shields.io/badge/Ferramenta-Microsoft%20Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

Projecto de análise de dados em Excel que identifica o Cartão de Crédito como método de pagamento dominante e mapeia preferências regionais de pagamento num E-commerce

---

## Problema do Negócio

A empresa de E-commerce necessitava de compreender melhor o comportamento de pagamento dos seus clientes, a fim de tomar decisões estratégicas sobre quais métodos de pagamento priorizar, como os padrões variam por região e categoria de produto, e se a política de preços estava a ser aplicada correctamente.

O Gestor levantou as seguintes questões para serem respondidas:

1. Houve algum desconto dado nas compras?
2. Qual tipo de pagamento devemos ter mais atenção?
3. Existe diferença entre o método de pagamento em diferentes Regiões?
4. Existe algum produto que se diferencia em relação ao método de pagamento dos demais?

---

## Contexto

A base de dados utilizada contém transacções de um E-commerce com presença em múltiplas regiões (Ásia, América do Norte e Europa), abrangendo diferentes categorias de produtos e métodos de pagamento. A análise foi realizada com o objectivo de responder às perguntas do negócio e gerar insights accionáveis para a equipa de gestão.

>  **Fonte dos dados:** [Kaggle]([https://www.kaggle.com](https://www.kaggle.com/datasets/shreyanshverma27/online-sales-dataset-popular-marketplace-data))

---

## Premissas da Análise

- Os dados foram tratados e analisados no **Microsoft Excel**.
- Foram criadas duas colunas adicionais que não existiam na base de dados original:
  - **Expected Revenue** — calculada como `Units Sold × Unit Price`, representando a receita esperada sem qualquer desconto.
  - **Discount** — calculada como a diferença entre `Expected Revenue` e `Total Revenue`, permitindo identificar se algum desconto foi aplicado.
- Antes de carregar os dados para análise, foi utilizado o **Power Query** para garantir que as colunas numéricas estavam com os tipos de dados correctos:

| Coluna | Tipo de Dado | Localidade |
|--------|-------------|------------|
| `Units Sold` | Número Inteiro | Inglês (Estados Unidos) |
| `Unit Price` | Número Decimal | Inglês (Estados Unidos) |
| `Total Revenue` | Número Decimal | Inglês (Estados Unidos) |

- Todas as transacções foram consideradas válidas para a análise.
- A análise cobre todas as regiões e categorias de produtos presentes na base de dados.

---

##  Estratégia da Solução

### Passo 1 — Resumo do Contexto em Pergunta Aberta
> *Como está o comportamento de pagamento dos clientes do E-commerce?*

### Passo 2 — Transformação em Perguntas Fechadas
> - Os produtos foram vendidos com desconto?
> - Qual método de pagamento gera mais transacções e mais receita?
> - O método de pagamento preferido varia conforme a região do cliente?
> - Existe alguma categoria de produto com um padrão de pagamento diferente das demais?

### Passo 3 — Definição da Coluna Facto
A coluna facto principal é **Total Revenue**, pois representa o valor efectivamente recebido por cada transacção e é a base para medir o desempenho financeiro.

### Passo 4 — Identificação das Dimensões

| Dimensão | Coluna |
|----------|--------|
| Tempo | `Date` |
| Produto | `Product Name`, `Product Category` |
| Geografia | `Region` |
| Pagamento | `Payment Method` |
| Volume | `Units Sold` |

### Passo 5 — Hipóteses Analíticas

- H1: Parte das compras pode ter recebido algum desconto, reduzindo a receita total.
- H2: O cartão de crédito é o método de pagamento mais utilizado e o que mais gera receita.
- H3: O comportamento de pagamento varia significativamente entre regiões.
- H4: Determinadas categorias de produtos têm um padrão de pagamento distinto das demais.

### Passo 6 — Critérios de Priorização

As hipóteses foram priorizadas com base em dois critérios:

- **Impacto Financeiro** — quanto a hipótese afecta directamente a receita da empresa.
- **Relevância Estratégica** — quanto o insight pode influenciar decisões de negócio.

### Passo 7 — Priorização das Hipóteses Analíticas

| Prioridade | Hipótese | Justificativa |
|------------|----------|---------------|
| Alta | H2 — Método de pagamento dominante | Impacto directo na estratégia de pagamentos |
| Alta | H3 — Variação regional | Orienta decisões de expansão e localização |
| Média | H4 — Padrão por categoria de produto | Permite optimizar a experiência de compra por produto |
| Baixa | H1 — Política de descontos | Confirmação operacional da política de preços |

---

## Insights da Análise

### 1 — Política de Descontos
Após a criação da coluna `Expected Revenue` e o cálculo da coluna `Discount`, verificou-se que **não houve qualquer desconto aplicado** nas transacções. O `Total Revenue` foi igual ao `Expected Revenue` em todos os casos, confirmando que todos os produtos foram vendidos pelo preço real.

<img width="454" height="134" alt="Total de Desconto" src="https://github.com/user-attachments/assets/eeca56bd-7509-4fd0-b634-d10c52dbab37" />


### 2 — Método de Pagamento mais Relevante
O **Cartão de Crédito** é o método de pagamento que merece maior atenção, sendo o mais relevante tanto em **volume de transacções** quanto em **receita gerada**. É o principal motor financeiro do E-commerce e deve ser priorizado nas estratégias de pagamento, investimento em segurança e experiência do utilizador.

<img width="48%" height="130" alt="Quantidade por meio de pagamento" src="https://github.com/user-attachments/assets/ecfd9010-c630-4131-ab4c-8980c5d03e6a" /> 
 &nbsp;
<img width="48%" height="311" alt="Receita por meio de pagamento" src="https://github.com/user-attachments/assets/d3b57e00-cbb8-4ab9-a89f-3a34fac943f0" />



### 3 — Variação Regional no Método de Pagamento
Existe uma diferença clara entre regiões:

| Método de Pagamento | Região | Distribuição |
|---------------------|--------|--------------|
| Cartão de Crédito | Ásia | ~1/3 das operações |
| Cartão de Crédito | América do Norte | ~2/3 das operações |
| Cartão de Débito | Ásia | 100% das operações |
| PayPal | Europa | 100% das operações |

Cada região apresenta um método de pagamento dominante, o que indica que a preferência de pagamento é fortemente influenciada pelo contexto geográfico e cultural do cliente.

<img width="684" height="163" alt="Pagamento por regiao" src="https://github.com/user-attachments/assets/f0b0cb30-653e-462e-839f-138c06246171" />


### 4 — Categoria de Produto com Padrão Diferenciado
A categoria **Electronics** é a mais vendida e apresenta um padrão de pagamento bem definido: a maioria das suas transacções é realizada via **Cartão de Crédito**. Isso sugere que produtos de maior valor agregado tendem a ser pagos a crédito, possivelmente pelo parcelamento ou pelos benefícios associados ao cartão.

<img width="940" height="313" alt="Categoria de Produto por meio de pagamento" src="https://github.com/user-attachments/assets/43a05943-1178-4ecf-95e0-c8596e1fbdb6" />

---

## Resultados

<img width="1862" height="695" alt="Analise completa" src="https://github.com/user-attachments/assets/9a7fc739-13fd-4269-84ad-6919caed3f2c" />

Com base na análise, é possível concluir que:

- A empresa aplica a sua **política de preços de forma consistente**, sem concessão de descontos — o que é positivo para a margem de lucro.
- O **Cartão de Crédito** deve ser o foco principal de investimento em infraestrutura de pagamento, segurança e experiência do utilizador, por ser o método com maior impacto financeiro.
- A **estratégia de pagamento deve ser regionalizada**: oferecer Cartão de Débito como opção prioritária na Ásia e fortalecer a integração com o PayPal na Europa pode melhorar a conversão de vendas.
- A categoria **Electronics**, por concentrar compras de maior valor e preferência pelo crédito, pode beneficiar de campanhas específicas com parceiros de cartão de crédito ou programas de fidelidade.

---

## Estrutura do Projecto

```
 analise-de-pagamentos-de-e-commerce
│
├──  dados
│   └── Online_Sales_Data.csv                          # Base de dados original do Kaggle
├──  analise
│   └── analise_de_pagamentos_de_E-Commerce.xlsx       # Base de dados tratada + análises + dashboard
└──  README.md
```

---

## Ferramentas Utilizadas

- **Microsoft Excel** — Para o tratamento e tipagem dos dados via Power Query, colunas calculadas, Tabelas Dinâmicas, Gráficos e Dashboard

---

## Autor

**Santiago Casseca**  
[LinkedIn](www.linkedin.com/in/santiago-casseca-496b84195)
