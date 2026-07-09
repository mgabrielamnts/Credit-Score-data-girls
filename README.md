# 📊 Análise de Score de Crédito — Data Girls Finance

[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi)](https://powerbi.microsoft.com/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-lightblue?logo=pandas)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)]()

---

## 📌 Sobre o Projeto

Este projeto foi desenvolvido como trabalho final do **Bootcamp [RE]Start — Data Girls (4ª Edição)**, trilha de **Análise de Dados**.

A análise simula o trabalho de uma equipe de dados da **Data Girls Finance**, uma fintech fictícia que busca compreender melhor o perfil financeiro de seus clientes para apoiar decisões de concessão de crédito e gestão de risco de inadimplência.

> ⚠️ *Dataset sintético disponível no Kaggle para fins educacionais. Os resultados não representam clientes reais.*

---

## 🎯 Perguntas Norteadoras

1. Qual perfil tem maior risco de inadimplência (baixo score)?
2. Quais fatores mais influenciam clientes com score *Ruim*?
3. Existe relação entre renda, contas bancárias, cartões e empréstimos com o score?
4. Clientes com maior atraso médio de pagamento tendem a apresentar pior score?

---

## 📊 Dataset

**Credit Score Classification** — disponível no [Kaggle](https://www.kaggle.com/datasets/parisrohan/credit-score-classification)

| Campo | Descrição |
|---|---|
| Registros | 100.000 entradas / 12.500 clientes únicos |
| Variáveis | 28 colunas originais |
| Target | `Credit_Score` (Poor / Standard / Good) |
| Período | 8 meses |

---

## 🔄 Pipeline do Projeto

### 1️⃣ Exploração Inicial
- Diagnóstico completo com relatório de qualidade customizado (`data_quality_report`)
- Identificação de tipos, nulos, duplicatas e inconsistências

### 2️⃣ Limpeza e Preparação
- Remoção de caracteres inválidos (`_`, `_______`, `!@9#%8`) em 8 colunas
- Imputação de nulos pela **mediana agrupada por `Customer_ID`** (variáveis numéricas) e **moda** (variáveis categóricas)
- Tratamento de outliers em `Num_Bank_Accounts`, `Num_Credit_Card` e `Num_of_Loan` com base em percentis Q95/Q99
- Conversão de `Credit_History_Age` (texto) para `Credit_History_TotalMonths` (meses totais)

### 3️⃣ Análise Exploratória (EDA)
- Análise de 10+ variáveis por classificação de score
- Identificação de padrões em variáveis demográficas e comportamentais
- Feature Engineering: `Debt_to_Income_Ratio`, `Spending_Level`, `Payment_Size`

### 4️⃣ Validação Estatística
- **Teste de Kruskal-Wallis** nas 4 variáveis mais relevantes (p < 0,001 em todas)
- **Teste Qui-quadrado** para `Credit_Mix` × `Credit_Score` (χ² = 40.489, p < 0,001)
- **Correlação de Spearman** entre variáveis numéricas e `Credit_Score`

### 5️⃣ Conclusões e Recomendações
- Respostas diretas às 4 perguntas norteadoras com evidências numéricas
- 4 recomendações estratégicas ancoradas nos dados

### 6️⃣ Dashboard Power BI
- 3 telas interativas com filtros globais
- Identidade visual alinhada ao Data Girls Bootcamp

---

## 💡 Principais Resultados

| Insight | Resultado |
|---|---|
| Clientes com Credit Mix Inadequado | 60,1% classificados como score Ruim |
| Mediana de atraso — grupo Ruim | 27 dias (vs. 10 dias no grupo Bom) |
| Debt-to-Income Ratio — grupo Ruim | 0,062 (5x maior que o grupo Bom) |
| Histórico de crédito — grupo Bom | 288 meses (vs. 161 meses no grupo Ruim) |
| Clientes em zona de risco | 29% da carteira (acima da meta de 25%) |

---

## 🏆 Recomendações para a Data Girls Finance

| Ação | Justificativa | Indicador |
|---|---|---|
| Triagem automática para Credit Mix Inadequado | 60,1% de probabilidade de score Ruim | Credit Mix |
| Alerta para Debt-to-Income > 6,2% | Mediana do grupo Ruim | DTI |
| Alerta operacional para atraso > 20 dias | Ponto entre medianas Regular (18d) e Ruim (27d) | Dias de Atraso |
| Ofertas diferenciadas para Regular com bom perfil | 53,2% da carteira com potencial de migração | Score + Histórico |

---

## 🛠️ Ferramentas e Bibliotecas

| Ferramenta | Uso |
|---|---|
| `Python 3.10+` | Linguagem principal |
| `Pandas` | Manipulação e análise dos dados |
| `Seaborn` / `Matplotlib` | Visualizações |
| `SciPy` | Testes estatísticos (Kruskal-Wallis, Qui-quadrado, Spearman) |
| `Scikit-learn` | Normalização (StandardScaler) |
| `Power BI` | Dashboard interativo |
| `Power Automate` | Automação de alertas por e-mail |

---

## 📁 Estrutura do Repositório

```
📦 credit-score-data-girls
├── 📓 DATA_GIRLS.ipynb
├── 📊 dashboard/
│   ├── dash_data_girls.pbix
│   ├── tela1_visao_geral.png
│   ├── tela2_indicadores_risco.png
│   └── tela3_insights_recomendacoes.png
├── 📂 data/
│   └── train_dashboard.csv
├── 📂 docs/
│   ├── power_automate_fluxo.png
│   ├── power_automate_email.png
│   └── power_automate_execucao.png
└── 📄 README.md
```

---

## 🗺️ Como Usar

### Notebook
1. Clone o repositório
2. Instale as dependências: `pip install pandas numpy matplotlib seaborn scipy scikit-learn`
3. Execute o notebook: `DATA_GIRLS.ipynb`
4. O arquivo `train_dashboard.csv` será gerado automaticamente na Etapa 6

### Dashboard
1. Abra o arquivo `dash_data_girls.pbix` no Power BI Desktop
2. Atualize a fonte de dados apontando para o `train_dashboard.csv` gerado

---

## ⚡ Power Automate — Alerta de Risco

Fluxo automatizado configurado para enviar alerta por e-mail quando o percentual de clientes com Score Ruim ultrapassar 25%.

- **Gatilho:** Manual (para fins de demonstração)
- **Condição:** % Score Ruim > 25%
- **Ação:** E-mail automático com resumo dos indicadores de risco e recomendações práticas

Os prints do fluxo estão disponíveis na pasta `/docs`.

---

## 👩‍💻 Sobre a Autora

**Maria Gabriela Martins de Souza**

Engenheira Química em transição para a área de Dados. Analista de Laboratório e Dados com experiência em implementação de pipelines Python e dashboards em ambiente industrial. Cursando Análise e Desenvolvimento de Sistemas (FATEC).

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conectar-blue?logo=linkedin)](https://linkedin.com/in/mgabrielamnts)
[![GitHub](https://img.shields.io/badge/GitHub-Perfil-black?logo=github)](https://github.com/mgabrielamnts)

---

## 🙏 Agradecimentos

À equipe do **Bootcamp [RE]Start Data Girls** pela oportunidade de aprendizado e pelo ambiente colaborativo ao longo de toda a jornada.
