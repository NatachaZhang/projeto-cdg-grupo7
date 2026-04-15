# Análise Preditiva do Mercado Imobiliário de Boston
## Identificação da Equipa
* **Grupo nº:7**
* **Membros:**
  * Diana Figueiredo - nº 2022147039
  * Natacha Zhang - nº 2023136513
  * Sofia Tanganho - nº 2023139766


## Organização do Repositório
A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software:
* **`data/`**: Armazenamento de dados (dados brutos em `raw/` e processados em `processed/`).
* **`docs/`**: Documentação técnica detalhada dividida por Milestones (M1, M2 e M3).
* **`notebooks/`**: Jupyter Notebooks para experimentação, limpeza e modelação.
* **`src/`**: Código-fonte modular (scripts `.py`) para funções reutilizáveis.
* **`reports/`**: Relatórios finais, apresentações e exportação de figuras (`figures/`).
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias.
  
## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
O mercado imobiliário é um dos setores com maior impacto económico e social, influenciando decisões de compra, políticas de habitação e estratégias de investimento. Na área metropolitana de Boston, a avaliação do valor de um imóvel depende de múltiplos fatores socioeconómicos, habitacionais e ambientais, cuja influência relativa no preço final nem sempre é clara ou facilmente quantificável. Esta complexidade dificulta a sua compreensão por parte dos diferentes intervenientes do mercado, desde compradores e vendedores a instituições financeiras e entidades públicas.

O problema central que este projeto procura resolver é a dificuldade em estimar, de forma objetiva e fundamentada, o valor mediano das habitações, tendo em conta as características das zonas onde se inserem. Esta limitação pode conduzir a previsões imprecisas e comprometer a tomada de decisão de investidores, compradores e entidades públicas, que dependem de estimativas fiáveis para avaliar oportunidades, definir preços e desenvolver políticas habitacionais eficazes.
Para responder a este problema, recorre-se ao Boston Housing Dataset, composto por 506 observações e 14 variáveis, com o objetivo de identificar os fatores com maior influência no preço, representado pela variável MEDV (valor médio em milhares de dólares), e construir modelos preditivos capazes de estimar esse valor de forma fiável.
### Objetivos SMART do Projeto
* **Objetivo 1:** Identificar as 3 variáveis que mais influenciam o preço mediano das habitações (`MEDV`) através de análise de correlação e Feature Importance, e segmentar as 506 habitações em grupos distintos com K-Means validado por um Coeficiente de Silhueta superior a 0.50, até ao Milestone 2.
* **Objetivo 2:** Comparar o desempenho de algoritmos de regressão na previsão do valor médio das habitações, selecionar o modelo com melhor `RMSE` e R^2 superior a 0.85, até ao Milestone 3.
### Perguntas de Investigação
**1.** De que forma o modelo de regressão revela qua as condições socioeconómicas do bairro (`LSTAT`) condicionam o valor habitacional mais do que as características físicas da habitação (`RM`), que padrão descreve essa relação?

**2.** O modelo consegue distinguir o efeito direto da criminalidade (`CRIM`) no valor habitacional do efeito mediado pelo estatuto socioeconómico (`LSTAT`), e em que medida a criminalidade constitui um preditor autónomo ou reflete as condições do bairro?

**3.** Como é que o modelo capta a relação entre a qualidade dos recursos educativos (`PTRATIO`) e o valor das habitações, e esse efeito é uniforme ao longo da distribuição de preços ou concentra-se em determinados segmentos do mercado?

**4.** O modelo identifica perfis distintos de outliers em `MEDV`, tanto nos valores extremamente elevados como nos mais baixos, e que combinação de variáveis explica esses casos atípicos, de acordo com o que o modelo aprendeu? 
### Fonte de Dados
* **Dataset:** [Kaggle](https://www.kaggle.com/datasets/fedesoriano/the-boston-houseprice-data)
* **Dimensão:** 506 linhas, 14 colunas
  
## 2. Exploração (Milestone 2)
### Limpeza e Preparação
* A análise de qualidade dos dados revelou que o conjunto de dados (_dataset_) não apresenta valores nulos, registos duplicados nem erros de inserção aparentes, não tendo sido necessário realizar operações de limpeza. Os dados encontram-se prontos para a fase de modelação.
* As variáveis foram posteriormente escalonadas de acordo com a presença de outliers, as variáveis com outliers foram padronizadas (_StandardScaler_), por ser mais robusta a valores extremos, enquanto as variáveis sem outliers foram normalizadas (_MinMaxScaler_).
### Principais Conclusões (EDA)
> ![Matriz de Correlação](https://github.com/NatachaZhang/projeto-cdg-grupo7/blob/main/reports%20/figures/matriz_correlacao.png)
* **Ponto-chave:** [A análise exploratória permitiu identificar as variáveis com maior influência no preço dos imóveis (`MEDV`). O `RM` e o `LSTAT` destacaram-se como as variáveis com correlações mais elevadas com o `MEDV`, de 0,70 e -0,74, respetivamente. Com base nesta análise, foram criadas duas novas variáveis, o `IAH` e o `IQV`, que combinam variáveis complementares para enriquecer a capacidade preditiva do modelo. Foi ainda observada multicolinearidade entre as variáveis `RAD` e `TAX` (r = 0,91), tendo sido decidido remover o `RAD`, uma vez que o `TAX` apresentava uma correlação mais forte com a variável alvo.]
  
## 3. Modelação (Milestone 3)
### Abordagem Técnica
* **Modelos:** [Ex: Random Forest e XGBoost]
* **Métrica Principal:** [Ex: F1-Score ou RMSE]
  
## 4. Finalização (Milestone 4)
### Resposta ao Problema
[Resumo da solução e como ela gera valor para o negócio.]
### Recomendações de Inovação
1. [Sugestão prática baseada nos resultados]
## Como Reproduzir este Projeto
1. Clone o repositório: `git clone [url-do-repo]`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica.
   
## 5. Referências
1.Fedesoriano. (2021). Boston House Prices-Advanced Regression Techniques. Kaggle. https://www.kaggle.com/datasets/fedesoriano/the-boston-houseprice-data  

**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)
