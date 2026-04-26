# 📊 Sales Insights AI — Análise de Vendas Globais com Prompts de IA

> **Bootcamp XP Inc. – Cloud com Inteligência Artificial | DIO**

![Screenshot_20250524-122136](https://github.com/user-attachments/assets/c76b202f-5b4a-4875-8244-b7935ead3339)

[![Portfólio Sérgio Santos](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)

---

## 1. Problema de Negócio

A **Meganium**, fabricante de consoles portáteis, opera em três marketplaces simultâneos — **AliExpress, Shopee e Etsy** — e vende para sete países. Apesar de um volume crescente de transações, a empresa não possuía uma análise estruturada de seus dados de venda.

Sem essa visão analítica, perguntas críticas ficavam sem resposta:

- Qual país concentra a maior receita e onde o esforço de distribuição deve ser priorizado?
- Qual produto lidera em cada mercado e qual está gerando maior retorno financeiro?
- Existe sazonalidade nas vendas que permita antecipar demanda?
- Os cupons de desconto estão sendo usados de forma estratégica ou indiscriminada?
- Qual marketplace é mais eficiente em receita por unidade vendida?

O objetivo deste projeto é transformar os dados brutos de vendas em **insights acionáveis**, utilizando prompts estruturados de IA, capazes de apoiar decisões de negócio nas áreas de produto, logística e canais de venda.

---

## 2. Contexto

A base de dados analisada — `cpMeganium_Sales_data.xlsx` — contém **60 transações** realizadas entre **maio e outubro de 2024**, distribuídas em 14 colunas:

| Campo | Descrição |
|---|---|
| `SKU` | Código do produto |
| `product_sold` | Nome do console |
| `date_sold` | Data da venda |
| `quantity` | Unidades vendidas por transação |
| `unit_price` | Preço unitário (USD) |
| `total_price` | Receita bruta por transação |
| `currency` | Moeda |
| `site` | Marketplace (AliExpress, Shopee, Etsy) |
| `discount_coupon` | Código do cupom aplicado |
| `discount_value` | Valor do desconto concedido |
| `buyer_name / birth_date` | Dados do comprador |
| `delivery_country` | País de entrega |
| `invoice_id` | ID único da transação |

**Escopo da análise:** 5 produtos, 7 países, 3 canais de venda, 178 unidades totais e **receita bruta acumulada de USD 15.930**.

---

## 3. Premissas da Análise

Para garantir consistência e reprodutibilidade:

- O campo `total_price` foi adotado como **fonte oficial de receita**, sem ajuste por devoluções ou cancelamentos.
- Os valores estão expressos em **dólares americanos (USD)** para todas as transações.
- **100% das 60 transações registraram cupom de desconto aplicado** — foi assumido que isso reflete a política comercial ativa da Meganium nos três canais.
- O período analisado (maio–outubro 2024) representa uma **amostra de seis meses**, suficiente para identificar padrões sazonais de curto prazo.
- Não foram considerados dados de custo de produto, margem bruta ou frete, pois estão ausentes na base.
- As análises são **descritivas e exploratórias**, sem inferência causal ou modelagem preditiva.

---

## 4. Estratégia da Solução

A solução adotou uma abordagem de **análise por camadas**, do geral ao específico:

```
Entendimento do negócio
        ↓
Exploração e mapeamento dos dados (estrutura, tipos, completude)
        ↓
Análise descritiva (receita, volume, preço médio)
        ↓
Segmentação multidimensional (país × produto × canal × tempo)
        ↓
Aplicação de prompts estruturados via ChatGPT
        ↓
Interpretação dos insights e recomendações operacionais
```

**Decisão técnica:** optou-se pelo **ChatGPT** (versão gratuita) como motor de análise via prompts, em vez de ferramentas de BI como Power BI ou Tableau. Essa escolha foi intencional: o objetivo era validar se prompts bem estruturados conseguem substituir, no contexto de pequenos datasets, pipelines analíticos mais complexos. O resultado confirmou que **a qualidade do prompt determina a qualidade do insight** — não apenas a ferramenta.

Os prompts foram organizados em três categorias: análise de vendas, identificação de padrões e otimização logística. Cada prompt foi desenhado para extrair uma resposta específica e acionável, não apenas uma descrição dos dados.

---

## 5. Insights da Análise

### 📍 Concentração Geográfica da Receita

| País | Receita (USD) | Participação |
|---|---|---|
| 🇨🇦 Canadá | $4.090 | 25,7% |
| 🇫🇷 França | $3.210 | 20,1% |
| 🇯🇵 Japão | $2.510 | 15,8% |
| 🇦🇺 Austrália | $2.330 | 14,6% |
| 🇩🇪 Alemanha | $2.010 | 12,6% |
| 🇬🇧 UK | $1.260 | 7,9% |
| 🇺🇸 USA | $520 | 3,3% |

> **Insight:** Canadá e França juntos representam **45,8% da receita total**, indicando onde esforços de reposição de estoque e logística devem ser prioritários. O desempenho baixo dos EUA em comparação com outros mercados é um sinal de subexploração — ou de pricing inadequado para esse mercado.

---

### 📦 Performance por Produto

| Produto | Unidades | Receita (USD) | Preço Médio |
|---|---|---|---|
| NEW MEGANIUM RG 40XXV | 41 | $4.100 | ~$100 |
| NEW MEGANIUM RG35XX | 36 | $3.240 | ~$90 |
| MEGANIUM RG353M | 29 | $3.190 | ~$110 |
| NEW MEGANIUM RG CubeXX | 36 | $2.880 | ~$80 |
| NEW MEGANIUM RG28XX | 36 | $2.520 | ~$70 |

> **Insight:** O **RG 40XXV lidera tanto em volume quanto em receita**, sendo o produto âncora do portfólio. O **RG353M** tem o maior preço médio por unidade — sinal de que um segmento de compradores aceita pagar premium. O **RG28XX** vende bem em volume mas é o de menor retorno, sugerindo revisão de pricing ou posicionamento.

---

### 🏪 Eficiência por Marketplace

| Marketplace | Receita (USD) | Unidades | Receita/Unidade |
|---|---|---|---|
| Shopee | $5.620 | 64 | ~$87,8 |
| Etsy | $5.190 | 56 | ~$92,7 |
| AliExpress | $5.120 | 58 | ~$88,3 |

> **Insight:** Etsy tem a **maior receita por unidade** apesar de vender menos unidades que Shopee — indica compradores com maior ticket médio e menor sensibilidade a preço. Shopee lidera em volume. Uma estratégia diferenciada por canal (premium no Etsy, volume no Shopee) pode maximizar a margem global.

---

### 📅 Sazonalidade das Vendas

| Mês | Receita (USD) |
|---|---|
| Maio/2024 | $1.040 |
| Junho/2024 | $1.770 |
| Julho/2024 | $2.300 |
| Agosto/2024 | **$4.310** ← pico |
| Setembro/2024 | $3.430 |
| Outubro/2024 | $3.080 |

> **Insight:** Há uma **rampa de crescimento clara** de maio a agosto, com pico em agosto (+314% vs. maio) seguido de acomodação. Isso sugere um ciclo sazonal relacionado ao verão no hemisfério norte — principal mercado da Meganium. Agosto deve ser o mês de reforço de estoque e campanhas de marketing.

---

### 🎟️ Impacto dos Cupons de Desconto

- **100% das transações** utilizaram cupom de desconto.
- Desconto médio por transação: **USD 45,84**
- Faixa de variação: de **$4,16** até **$158,09**

> **Insight:** A política de cupons universal elimina seu efeito como **gatilho de conversão** — se todos recebem desconto, ele deixa de ser um diferencial e passa a ser um custo fixo operacional. Recomenda-se segmentar os cupons por mercado ou volume de compra para preservar margem.

---

## 6. Resultados e Recomendações

Com base nos insights gerados, as recomendações práticas para a Meganium são:

**Produto:**
- Priorizar estoque e campanhas do **RG 40XXV** — lidera em receita e volume simultaneamente.
- Revisar o posicionamento do **RG28XX**: preço baixo com volume alto pode indicar canibalização de margem.

**Mercado:**
- Expandir presença no **Canadá e França** (maiores mercados) com logística dedicada.
- Investigar o baixo desempenho dos **EUA** — terceiro menor mercado apesar do potencial.

**Canal:**
- Adotar estratégia diferenciada: produtos premium no **Etsy**, produtos de volume no **Shopee**.
- Testar campanhas no **AliExpress** para aumentar receita por unidade.

**Operação:**
- Reforçar estoque em **julho para capturar o pico de agosto**.
- Revisar a política de cupons universais — segmentar por país ou valor de pedido.

---

## 7. Próximos Passos

- [ ] Integrar dados de **custo de produto e frete** para calcular margem real por transação
- [ ] Construir **dashboard interativo** (Power BI ou Metabase) para monitoramento contínuo
- [ ] Aplicar **análise de coorte** de compradores por país e período
- [ ] Implementar modelo preditivo simples de demanda para antecipar o ciclo sazonal de 2025
- [ ] Testar automação da extração de insights com **API OpenAI** em substituição ao uso manual do ChatGPT

---

## 🛠️ Tecnologias Utilizadas

| Ferramenta | Uso |
|---|---|
| ChatGPT (GPT-4, versão gratuita) | Motor de análise via prompts |
| Microsoft Excel / Google Sheets | Exploração e visualização inicial dos dados |
| GitHub | Versionamento e documentação |
| Markdown | Estruturação dos relatórios de insights |

---

## 📁 Estrutura do Repositório

```
📂 Sales_Insights_AI_DIO/
├── 📜 README.md          ← Você está aqui
├── 📂 data/              ← Dicionário de dados (data.md)
├── 📂 planilha Excel/    ← cpMeganium_Sales_data.xlsx
├── 📂 prompts/           ← Prompts organizados por categoria
├── 📂 insights/          ← Relatórios de resultados gerados
└── 📂 docs/              ← Processo de geração dos insights
```

---

## 💡 Aprendizados

Este projeto reforçou uma lição central sobre análise de dados com IA:

**A qualidade do output depende diretamente da qualidade do input.** Prompts vagos geram respostas genéricas. Prompts que contextualizam o problema de negócio, especificam o formato esperado e delimitam o escopo da resposta geram insights que podem ser usados em decisões reais.

O maior desafio foi estruturar os prompts de forma progressiva — partir do geral (visão por país) para o específico (produto mais vendido por país por canal) — sem perder o fio condutor da análise.

Se fosse refazer, integraria a análise diretamente via API da OpenAI com um script Python, eliminando o trabalho manual de copiar e interpretar respostas. Esse é o próximo passo natural do projeto.

---

## 📬 Contato

[![Portfólio Sérgio Santos](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn Sérgio Santos](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)
