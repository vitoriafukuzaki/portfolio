# 🐾 Whiskique E-Commerce Analytics & Optimization | Power BI Case Study

![Power BI](https://img.shields.io/badge/Power_BI-F2C94C?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)

## 📌 Contexto do Negócio
A **Whiskique** é uma empresa fictícia de e-commerce de suprimentos para animais de estimação. A empresa possui dois objetivos estratégicos principais:
1. **Aumentar o volume de vendas** através de estratégias de *upsell* (venda incremental de maior quantidade ou valor) e *cross-sell* (venda cruzada de produtos complementares no checkout).
2. **Reduzir custos operacionais de frete**, otimizando a consolidação de envios e simulando cenários operacionais dinâmicos (*What-If Analysis*).

---

## 🛠️️ Habilidades Técnicas Utilizadas
- **Modelagem de Dados Relacional:** Criação de esquemas em estrela (*Star Schema*) e relacionamentos entre tabelas de dimensão e fato.
- **Tratamento de Dados (Power Query Editor):** Limpeza de nulos (`Invoice No`), substituição de valores redundantes, deduplicação de categorias e padronização geográfica.
- **Linguagem DAX Avançada:** Criação de medidas com iteradores (`SUMX`, `FILTER`, `ALLSELECTED`), parâmetros dinâmicos de *What-If* e calculadoras de acumulados (*Running Totals*).
- **Análise de Associação (*Market Basket Analysis*):** Modelagem de tabelas duplicadas conectadas por ID da fatura para identificação de produtos comprados em conjunto.
- **Data Storytelling & UX/UI Design:** Construção de dashboards navegáveis com paleta visual consistente, mapas geográficos e cartões KPI de alto impacto.

---

## 📊 Estrutura dos Dashboards

### 1. Executive Summary
Focado na saúde financeira global do e-commerce para apoio à tomada de decisão da diretoria executiva.
- **Métricas Chave:** Faturamento Total ($1,55 M), Lucro Baseline ($427,34 Mil), Margem de Lucro % (27,50%) e Custo Total de Frete Baseline ($385,15 Mil).
- **Análises Principais:**
  - Distribuição das vendas por estado nos EUA[cite: 11].
  - Decomposição do lucro por categoria de produto (Treemap)[cite: 11].
  - Comparativo de Customer Lifetime Value (LTV) médio por estado[cite: 11].

![Executive Summary](dashboards/screenshots/executive_summary.png)

---

### 2. Shipping Metrics & What-If Analysis
Página analítica e preditiva desenvolvida para testar cenários de redução de custos no frete.
- **Simulação Dinâmica (*What-If*):** Parâmetro dinâmico para testar o impacto do aumento do volume médio por pedido nas margens financeiras.
- **Métricas Chave:** Custo de Envio Baseline vs. Envio Simulado vs. Economia Estimada ($118,19 Mil)[cite: 12].
- **Análises Principais:**
  - Projeção temporal de custos de envio acumulados ao longo do tempo (*Running Total*)[cite: 12].
  - Impacto da quantidade enviada no frete por produto e por categoria[cite: 12].
  - Distribuição geográfica do custo de frete por região dos EUA[cite: 12].

![Shipping Metrics](dashboards/screenshots/shipping_metrics.png)

---

### 3. Market Basket Analysis
Desenvolvido para apoiar a equipe comercial na criação de regras de recomendação no checkout.
- **Objetivo:** Identificar quais itens são comprados juntos com maior frequência (*Cross-Selling*).
- **Análises Principais:**
  - Filtro interativo de produto principal com relação de itens mais associados no carrinho[cite: 13].
  - Gráfico de dispersão (*Scatter Plot*): Quantidade vs. Vendas x Lucro (Tamanho da Bolha)[cite: 13].
  - Relação entre Faturamento Total e Margem de Lucro por Descrição[cite: 13].

![Market Basket Analysis](dashboards/screenshots/market_basket_analysis.png)

---

## 📐 Principais Fórmulas DAX

### 1. Custo de Frete Baseline (Iterativo)
```dax
Shipping (Baseline) = 
SUMX(
    Sales,
    IF(
        Sales[Quantity] = 1,
        Sales[Shipping Cost],
        Sales[Shipping Cost] + ((Sales[Quantity] - 1) * (Sales[Shipping Cost] * 0.7))
    )
)
```

### 2. Total Acumulado Baseline (Running Total)
```dax
Baseline running total = 
SUMX(
    FILTER(
        ALLSELECTED(Sales),
        Sales[Transaction Date] <= MAX(Sales[Transaction Date])
    ),
    [Shipping (Baseline)]
)

```
3. Customer Lifetime Value (LTV Médio)
```dax
Customer LTV (avg) = 
DIVIDE(
    SUM(Sales[Sales]),
    [Number of Customers],
    0
)

```

## 💡 Principais Recomendações de Negócio

1. **Otimização de Frete (*Upsell* de Quantidade):** Promover pacotes promocionais para os produtos com maior custo por 1.000 milhas (ex: rações e areias sanitárias), reduzindo os custos de envio unitários em até 30%.
2. **Recomendação no Checkout (*Cross-Sell*):** Configurar o motor de recomendações do site para sugerir *Dog and Puppy Pads* e *Earth Rated Dog Poop Bags* no momento da compra de itens de alimentação canina.
3. **Foco Geográfico:** Concentrar campanhas regionais nos estados com maior LTV médio (como *North Dakota* e *Delaware*) para maximizar o retorno das campanhas de tráfego pago.  


