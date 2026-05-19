# Porsche Sales Dashboard

Dashboard executivo desenvolvido em HTML, CSS e JavaScript com foco em análise de vendas da Porsche.

O projeto utiliza visual minimalista inspirado no design oficial da Porsche e apresenta indicadores estratégicos para análise comercial e operacional.

---

# Objetivos do Projeto

O dashboard foi desenvolvido para responder perguntas estratégicas relacionadas às vendas:

- Qual o valor total de venda por modelo?
- Qual estado possui maior valor de venda?
- Qual o tipo de pagamento mais frequente?
- Qual o status de entrega mais frequente?
- Qual o carro mais caro vendido?
- Qual o carro mais barato vendido?
- Qual a evolução das vendas por mês/ano?

---

# Funcionalidades

- Filtros dinâmicos
- Dashboard responsivo
- Visual minimalista
- Insights  ao lado dos gráficos
- Tratamento de dados
- Visualização temporal de vendas
- Cards executivos
- Gráficos interativos com Chart.js

---

# Tecnologias Utilizadas

- HTML5
- CSS3
- JavaScript
- Chart.js

---

# Estrutura do Projeto

```text
porsche-sales-dashboard/
│
├── data/
│   ├── raw/
│   │   └── porsche_sales_raw.csv
│   │
│   └── processed/
│       └── porsche_sales_processed.csv
│
├── dashboard/
│   └── index.html
│
├── assets/
│   └── preview-dashboard.png
│
├── README.md
│
└── LICENSE
```

---

# Base de Dados

O projeto utiliza uma base de vendas da Porsche contendo informações sobre:

- Modelos vendidos
- Datas de venda
- Valores
- Estados e cidades
- Métodos de pagamento
- Status de entrega

## Tratamentos Aplicados

A base original continha registros inválidos e inconsistências de formatação.

Foram realizados os seguintes tratamentos utilizando IA assistida:

- Remoção de registros com data INVALID
- Padronização de datas
- Conversão monetária
- Normalização numérica
- Estruturação dos dados para visualização

---

# Indicadores Implementados

## Valor Total de Venda por Modelo

- Gráfico de barras
- Insight executivo
- Quantidade de vendas

## Valor de Venda por Estado

- Gráfico de barras
- Insight executivo
- Quantidade de vendas

## Tipo de Pagamento Mais Frequente

- Gráfico de colunas

## Status de Entrega

- Gráfico de rosca

## Veículo Mais Caro e Mais Barato

- Cards executivos

## Evolução das Vendas por Mês/Ano

- Série temporal

---

# Filtros Dinâmicos

O dashboard permite filtragem dinâmica por:

- Modelo do carro
- Estado
- Cidade
- Ano do modelo
- Status de entrega
- Data inicial
- Data final

---

# Design

O design do dashboard foi inspirado no conceito visual da Porsche:

- minimalismo
- alto contraste
- foco em performance
- experiência premium
- visual executivo

Referência utilizada:

https://www.porsche.com/brazil/pt/

---

# Development Notes

This dashboard was created using a combination of manual development and AI-assisted coding techniques to accelerate UI prototyping, data visualization structuring, and frontend optimization.

All analytical validations, business logic, and dataset processing were manually reviewed and validated.

---

# Autor

Projeto desenvolvido para fins de estudo, analytics e visualização de dados.

---
