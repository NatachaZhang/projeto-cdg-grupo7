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
Para responder a este problema, recorre-se ao _Boston Housing Dataset_, composto por 506 observações e 14 variáveis, com o objetivo de identificar os fatores com maior influência no preço, representado pela variável `MEDV` (valor médio em milhares de dólares), e construir modelos preditivos capazes de estimar esse valor de forma fiável.
### Objetivos SMART do Projeto
* **Objetivo 1:** Construir um modelo de previsão supervisionada do preço médio das habitações (`MEDV`), alcançando um R² superior a 0.80 e um RMSE inferior a 3.500 dólares, até ao final do Milestone 3.
* **Objetivo 2:**  Criar um modelo de agrupamento para segmentar as habitações em perfis distintos com base nas suas características socioeconómicas, habitacionais e ambientais, validado pelo método do cotovelo e por um Coeficiente de Silhueta (>0.50), até ao final do Milestone 3.
### Perguntas de Investigação

As perguntas de investigação estruturam o enquadramento científico do estudo, orientando a análise empírica dos dados com o objetivo de identificar os principais determinantes do preço mediano das habitações (`MEDV`), avaliar a sua relevância estatística e preditiva e verificar a capacidade dos modelos desenvolvidos em captar os padrões que explicam as variações no valor habitacional.

**1.** Que perfis distintos de habitações identifica o modelo de clustering, e de que forma diferem entre si nas variáveis socioeconómicas, habitacionais e ambientais?

**2.** Qual é a relação entre o estatuto socioeconómico do bairro (`LSTAT`) e o preço mediano das habitações (`MEDV`) no modelo de regressão?

**3.** A taxa de criminalidade (`CRIM`) é um preditor relevante do preço das habitações (`MEDV`) quando considerada em conjunto com outras variáveis do bairro?

**4.** Que variáveis caracterizam as habitações com os preços mais elevados e mais baixos identificadas pelo modelo?

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

**Modelos Utilizados:**

No desenvolvimento da fase de modelação, foram testados algoritmos com o objetivo de prever o preço médio das habitações, de modo a dar resposta ao nosso primeiro objetivo SMART. Foram considerados os seguintes modelos:

* _Random Forest_
* _XGBoost_
* _SVR_

Foram aplicadas as seguintes técnicas de otimização:
 
* Avaliação de Ajuste (_Fit_)
* Sintonização Fina (_Hyperparameter Tuning_)
* Validação de Robustez
* Validação Cruzada (_K-Fold Cross-Validation_)

**Métricas Principais:**

* RMSE (Raiz do Erro Quadrático Médio)
* R²
* MAE

**Modelo Final:**

O modelo final selecionado foi o Random Forest, escollhido por ter os meslhores resultados nas métricas utilizadas.

**Modelos Utilizados:**

Para o segundo objetivo SMART, foram testados algoritmos com o objetivo de segmentar as habitações em perfins distintos. Foram considerados os seguintes modelos:

* KMeans (_baseline_)
* KMeans otimizado
* _Agglomerative Clustering_
* DBSCAN

**Métricas Principais:**

*  Coeficiente de Silhueta (_Silhouette_)
* _Calinski-Harabasz_
* _Davies_bouldin_
* _Clusters_

**Modelo Final:**

O modelo final selecionado foi o KMeans Otimizado com k=4, que atingiu um Coeficiente de Silhueta de 0.5065 no conjunto de teste, cumprindo o critério de sucesso definido (_Silhouette_ > 0.50). Este modelo destacou-se pela sua estabilidade estrutural, número de clusters consistente entre treino e teste, ausência total de ruído e o menor Gap Treino-Teste registado (0.0481), tornando-o a solução mais equilibrada e reprodutível entre os algoritmos testados.
  
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
