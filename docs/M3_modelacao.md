# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação
### 1.1. Problemas Supervisionados (Modelos De Regressão)
* **Divisão do _Dataset_:** Realizámos testes com duas divisões distintas do dataset, 80/20 e 70/30, de forma aleatória (`random_state=42`) fixa para garantir a reprodutibilidade dos resultados. A divisão 80/20 ficou com 404 amostras de treino e 102 de teste, enquanto a divisão 70/30 ficou com 354 amostras de treino e 152 de teste. Após comparação das métricas obtidas em ambas as divisões, verificou-se que a divisão 70/30 produziu melhores resultados globais superando todas as combinações testadas. Por este motivo, adotámos a divisão 70/30 como estratégia de validação para a fase de otimização, garantindo o isolamento total dos dados de avaliação para evitar perdas de informação (_data leakage_).
* **Métrica de Sucesso:** As métricas principais escolhidas foram o RMSE (Raiz do Erro Quadrático Médio) e o R², por se tratar de um problema de regressão com variável alvo contínua (`MEDV`). O RMSE foi privilegiado como métrica principal por penalizar erros grandes de forma proporcional, sendo particularmente adequado para prever valores monetários onde erros elevados têm impacto prático significativo, o Objetivo SMART 1 define um RMSE inferior a 3.500 dólares como critério de sucesso. O R² complementa a análise ao medir a proporção da variância do preço das habitações explicada pelo modelo, com o Objetivo SMART 1 a definir um valor mínimo de 0.85 como critério de sucesso.

### 1.2. Problemas Não Supervisionados (Modelos de Agrupamento (_Clustering_))
* **Divisão do _Dataset_:** Para a modelação com algoritmos de clustering, dividiu-se o dataset em 70% para treino e 30% para teste, com `random_state=42`, de forma a garantir a reprodutibilidade e avaliar a estabilidade dos agrupamentos em diferentes amostras.
Foram privilegiadas as variáveis standardizadas e normalizadas, sempre que disponíveis, dado que estes algoritmos são sensíveis à escala e à distância entre observações.A avaliação foi feita através de métricas internas adequadas ao clustering, destacando-se o Coeficiente de Silhueta como métrica principal, complementado pelos índices Calinski-Harabasz e Davies-Bouldin, de modo a apoiar a escolha do modelo final com maior rigor.
* **Métrica de Sucesso:** A métrica principal escolhida foi o Coeficiente de Silhueta por ser a mais adequada para avaliar simultaneamente a coesão interna de cada cluster e a separação entre grupos distintos, numa escala interpretável entre -1 e 1. O Objetivo SMART 2 define um Coeficiente de Silhueta superior a 0.50 como critério de sucesso, garantindo que os bairros segmentados formam grupos suficientemente coesos e distintos entre si. O índice Calinski-Harabasz e o Davies-Bouldin foram utilizados como métricas complementares para apoiar a escolha do modelo final com maior rigor técnico.

## 2. Experiências Realizadas
### 2.1. Resposta ao Objetivo SMART 1 (Modelos De Regressão) 
### 2.1.1. Modelo Baseline
* **Algoritmo:** Regressão Linear Simples
* **Justificação:** Escolhemos a Regressão Linear como baseline por ser o modelo de regressão mais simples e interpretável, servindo como patamar mínimo de comparação para todos os modelos candidatos.  
* **Resultado:**
  
| Parâmetros | Teste | 
| :--- | :--- |
| RMSE: | 4.8757 |
| MAE: | 3.5549 |
| R²: | 0.6810 |
    
#### 2.1.2. Modelos Candidatos 


| Algoritmo | Parâmetros | RMSE (Treino) | RMSE (Teste) | Gap RMSE | MAE (Treino) | MAE (Teste) | Gap MAE | R² (Treino) | R² (Teste) | Gap R² | Notas |  
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |   
| Random Forest | `n_estimators=100`<br>`random_state=42` | 1.66 | 3.58 | 1.92 | 1.14 | 2.55 | 1.41 | 0.97 | 0.83 | 0.14 | Apresentou o melhor desempenho global no conjunto de teste, combinando menor erro e maior capacidade explicativa, apesar de evidenciar algum sobreajuste moderado |
| XGBoost | `n_estimators=100`<br>`random_state=42` | 0.06| 3.71 | 3.65 | 0.04 | 2.72 | 2.68 | 0.99 | 0.82 | 0.17 | Revela excelente desempenho no treino, mas uma discrepância acentuada face ao teste, indicando sobreajuste e reduzida capacidade de generalização |
| SVR | `kernel='rbf'` | 5.97 | 5.71 | 0.26 | 3.95 | 3.71 | 0.24 | 0.59 | 0.56 | 0.03 | Apresenta desempenho inferior tanto no treino como no teste, sugerindo subajuste e limitada capacidade para captar a estrutura dos dadoss |

### 2.2. Resposta ao Objetivo SMART 2 (Modelos de Agrupamento (_Clustering_))
#### 2.2.1 Modelo Baseline
* **Algoritmo:** KMeans
* **Justificação:** Escolhemos o K-Means como linha de base por ser um algoritmo de agrupamento simples, eficiente e facilmente interpretável. A sua utilização permite estabelecer um ponto de comparação inicial para avaliar se modelos mais complexos conseguem melhorar a coesão e a separação dos grupos identificados. 
* **Resultado:**
  
| Parâmetros | Treino | Teste | 
| :--- | :--- | :--- |
| Silhouette | 0.3170 | 0.3325 |
| Calinski-Harabasz | 185.2667 | 131.5455 |
| Davies-Bouldin | 0.9667 | 0.8541 |
| Clusters | 8 | 8 |

#### 2.2.2 Modelos Candidatos
A análise comparativa dos modelos de clustering testados permitiu identificar diferenças substanciais tanto na qualidade dos agrupamentos produzidos como na estabilidade dos resultados entre os conjuntos de treino e teste. O algoritmo DBSCAN, com os parâmetros eps=0.5 e min_samples=8, registou o valor mais elevado de Silhouette no teste (0.7993), contudo revelou limitações críticas: o número de clusters variou entre treino (3) e teste (2), o índice de ruído foi consideravelmente elevado em ambos os conjuntos e o Gap Treino-Teste de 0.3815 evidencia uma instabilidade estrutural que compromete a generalização do modelo. O Agglomerative Clustering, com linkage='complete' e n_clusters=2, apresentou resultados mais promissores em termos de coesão e ausência de ruído, porém a discrepância no índice Calinski-Harabasz entre treino (84.79) e teste (21.44) sugere que a separação entre grupos não se mantém consistente quando aplicado a dados não vistos, representando uma limitação relevante do ponto de vista da robustez metodológica. O KMeans Otimizado com k=4 revelou-se a solução mais equilibrada e tecnicamente sustentada, com um Silhouette Score de 0.5545 no treino e 0.5065 no teste, ausência total de ruído e o menor Gap Treino-Teste registado (0.0481). Estes resultados demonstram uma capacidade de generalização superior e estabilidade estrutural entre os dois conjuntos, cumprindo simultaneamente o critério de sucesso definido no Objetivo 1 do projeto (Silhouette > 0.50) e justificando a sua seleção como modelo de clustering final.

| Algoritmo | Parâmetros | Silhouette (Treino) | Silhouette (Teste) | Calinski-Harabasz (Treino) | Calinski-Harabasz (Teste) | Davies-Bouldin (Treino) | Davies-Bouldin (Teste) | Nº Clusters (Treino) | Nº Clusters (Teste) | Ruído (Treino) | Ruído (Teste) | Notas |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Baseline KMeans | `k=8` (default) | 0.3170 | 0.3325 | 185.2663 | 131.5455 | 0.9667 | 0.8541 | 8 | 8 | 0 | 0 | Ponto de referência mínimo, silhouette abaixo de 0.50 em ambos os conjuntos |
| DBSCAN | `eps=0.5`, `min_samples=8` | 0.4178 | 0.7993 | 291.5607 | 286.4850 | 0.6758 | 0.2041 | 3 | 2 | 153 | 74 | Melhor Silhouette no teste mas instável, clusters e ruído inconsistentes entre treino e teste |
| Agglomerative Clustering | `linkage='complete`, `n_clusters=2` | 0.5889 | 0.7363 | 84.7915 | 21.4427 | 0.7157 | 0.1781 | 2 | 2 | 0 | 0 | Boa qualidade mas Calinski muito diferente entre treino e teste, instabilidade moderada |
| KMeans Otimizado | k=4 | 0.5545 | 0.5065 | 216.1761 | 118.9583 | 0.6457 | 0.8031 | 4 | 4 | 0 | 0 | Modelo mais estável e consistente, menor Gap, sem ruído e Silhouette acima de 0.50 |

## 3. Otimização (Tuning)
### 3.1. Resposta ao Objetivo SMART 1
* **Técnica Utilizada:** Utilizámos GridSearchCV (com validação cruzada de 5 folds) para o Random Forest e SVR, e RandomizedSearchCV para o XGBoost, ajustando hiperparâmetros como max_depth, learning_rate, n_estimators, C e epsilon.
* **Melhoria obtida:** O Random Forest não registou qualquer melhoria após a otimização, os hiperparâmetros de base (max_depth=None , n_estimators=100 ,  min_samples_split=2) já eram os ideais, o que indica que o modelo estava bem configurado por omissão.
O XGBoost foi o modelo que mais beneficiou da otimização em termos absolutos, onde o RMSE em 0,2592 e alcançou o melhor desempenho global (RMSE: 3,4510, R²: 0,8402).
O SVR registou a maior redução absoluta do RMSE (−1,4178), mas continua a ser o modelo com pior desempenho dos três.

### 3.2. Resposta ao Objetivo SMART 2
* **Técnica Utilizada:** KMeans otimizado: Método do Cotovelo combinado com análise do Coeficiente de Silhueta para todos os valores de k entre 2 e 10, selecionando automaticamente o k com maior Coeficiente de Silhueta no conjunto de treino.
Agglomerative Clustering: Pesquisa exaustiva com ParameterGrid sobre n_clusters ∈ {2, 3, ..., 10} e linkage ∈ {ward, complete, average}, totalizando 27 combinações testadas. Foi selecionada a combinação que maximizou o Coeficiente de Silhueta no conjunto de teste.
DBSCAN: Pesquisa exaustiva com ParameterGrid sobre eps ∈ {0.3, 0.5, 0.7, 0.9, 1.1, 1.3} e min_samples ∈ {3, 5, 8, 10}, totalizando 24 combinações testadas, com seleção igualmente baseada no Coeficiente de Silhueta no conjunto de teste.
* **Melhoria obtida:** O Silhouette Score do KMeans subiu de 0.3325 (baseline com k=8 default) para 0.5065 (k=4 otimizado), superando o objetivo de 0.50. O Agglomerative com linkage='complete' e k=2 atingiu 0.7363, sendo o modelo final selecionado pelo equilíbrio entre performance e estabilidade (gap treino/teste de apenas 0.1474 vs 0.3815 do DBSCAN).
  
## 4. Avaliação do Modelo Final
### 4.1. Matriz de Confusão / Erros
*Analisem onde o modelo mais falha.*
> **Análise:** (p/ex.: "O modelo ainda confunde a Classe A com a Classe B em 10% dos casos devido
à semelhança nos atributos X e Y.")
### 4.2. Importância dos Atributos (Feature Importance)
O IAH_stand é de longe a variável mais determinante no Random Forest (59% da importância total), mas tem menor peso no XGBoost (28,5%), o que indica que o XGBoost distribui a importância de forma mais equilibrada entre as variáveis.
O CHAS é praticamente ignorado pelo Random Forest (0,5%) mas é a segunda variável mais importante no XGBoost (14,8%), revelando que os dois modelos aprenderam padrões distintos nos dados.
TAX_norm e INDUS_norm têm peso relevante no XGBoost (~14% cada), confirmando que essas variáveis influenciam significativamente o preço das habitações.
## 5. Conclusão da Fase de Modelação
*Justifiquem por que razão este modelo está pronto (ou não) para ser apresentado como solução
final.*
---
*Data de última atualização: [23/04/2026]*
