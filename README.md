# Regressão linear com PIB e Índice ABCR

**Checkpoint 02 – MLAM 2026/2 – FIAP**

## Integrantes

- Renan Eskildssen – RM 571097
- *(adicione os demais integrantes, se o trabalho for em grupo)*

## Tarefa

Investigar se existe uma relação entre a atividade econômica brasileira e o fluxo de veículos nas rodovias. Pesquisar os dados, organizar uma tabela e construir um modelo de regressão linear em Python.

O **Produto Interno Bruto (PIB)** é o valor dos bens e serviços finais produzidos em um país durante um período.

O **índice de volume do PIB** acompanha a evolução da produção, descontando o efeito das mudanças de preços. Ele é construído encadeando as variações reais da produção e adota um período de referência igual a 100. Na série utilizada, a média de 1995 corresponde a 100.

## Dados

| Fonte | Acesso | Série utilizada |
|---|---|---|
| IBGE | [Tabela 1620 do SIDRA](https://sidra.ibge.gov.br/tabela/1620) | Brasil, "PIB a preços de mercado", índice de volume trimestral, sem ajuste sazonal |
| ABCR | [Índice ABCR](https://melhoresrodovias.org.br/indice-abcr_2/) ("Ver histórico") | Brasil, fluxo total de veículos, série original, mensal |

Período: **2006 a 2025 (20 anos completos)**.

| Coluna | Conteúdo |
|---|---|
| `Ano` | Ano de referência dos dois indicadores |
| `PIB_indice` | Média dos 4 índices trimestrais do PIB |
| `ABCR_indice` | Média dos 12 índices mensais da ABCR |

## Método

1. Coleta do PIB pela API do SIDRA e do Índice ABCR pelo histórico em Excel da ABCR.
2. Agregação anual (média de 4 trimestres / 12 meses) com verificação de que todos os anos estão completos.
3. Gráfico de dispersão (PIB no eixo X, ABCR no eixo Y) e correlação de Pearson/Spearman.
4. `LinearRegression` do scikit-learn: `X = PIB_indice`, `y = ABCR_indice`; **treino = 16 primeiros anos (2006–2021), teste = 4 últimos (2022–2025)**, em ordem cronológica, sem embaralhar.
5. Avaliação no teste com **MAE, MSE e R²**, tabela de valores observados x previstos e interpretação.

## Resultados


| Métrica (teste 2022–2025) | Valor |
|---|---|
| MAE | 4.949 |
| MSE | 25.950 |
| R²  | 0.4849 |

Correlação de Pearson entre PIB_indice e ABCR_indice: **0.964**
Reta ajustada: `ABCR_indice = -56.785 + 1.215 x PIB_indice`

224

## Estrutura do repositório

```
├── Checkpoint02_Regressao_PIB_ABCR.ipynb   # notebook com fontes, código, resultados e conclusão
├── README.md
├── requirements.txt
├── dados/
│   ├── pib_trimestral.csv      # PIB trimestral (SIDRA 1620)
│   ├── abcr_mensal.csv         # Índice ABCR mensal
│   ├── abcr_XXXX.xlsx          # arquivo original baixado da ABCR
│   └── base_anual.csv          # base final: Ano, PIB_indice, ABCR_indice
└── resultados/                 # gráficos (.png), métricas e previsões (.csv)
```

## Como executar

1. Abra o notebook no [Google Colab](https://colab.research.google.com) ou no Jupyter (`pip install -r requirements.txt`).
2. Execute todas as células (precisa de internet na primeira execução para baixar os dados).
3. Se o link do Excel da ABCR falhar, baixe o arquivo em "Ver histórico" na página da ABCR e salve em `dados/` com nome `abcr*.xlsx`.
4. Baixe as pastas `dados/` e `resultados/` geradas e envie ao repositório.

## Tecnologias

Python, Pandas, NumPy, Matplotlib, scikit-learn, Requests e OpenPyXL.
