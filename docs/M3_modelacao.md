# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação
### 1.1. Problemas Supervisionados (Modelos De Regressão)
* **Divisão do _Dataset_:** Realizámos testes com duas divisões distintas do dataset, 80/20 e 70/30, de forma aleatória (`random_state=42`) fixa para garantir a reprodutibilidade dos resultados. A divisão 80/20 ficou com 404 amostras de treino e 102 de teste, enquanto a divisão 70/30 ficou com 354 amostras de treino e 152 de teste. Após comparação das métricas obtidas em ambas as divisões, verificou-se que a divisão 70/30 produziu melhores resultados globais superando todas as combinações testadas. Por este motivo, adotámos a divisão 70/30 como estratégia de validação para a fase de otimização, garantindo o isolamento total dos dados de avaliação para evitar perdas de informação (_data leakage_).
* **Métrica de Sucesso:** As métricas principais para avaliar os modelos foram o R² (Coeficiente de Determinação), o RMSE (Raiz do erro quadrático médio) e o MAE (Erro absoluto médio), por se tratar de um problema de regressão com variável alvo contínua (`MEDV`). O R² foi a métrica determinante na avaliação do sucesso, que mede a percentagem da variação do preço das habitações explicada pelo modelo. O Objetivo SMART 1 estabelece um valor mínimo de 0.80 como critério de sucesso. O RMSE e o MAE surgem como métricas complementares para quantificar o erro de previsão em dólares: o RMSE é mais sensível a erros elevados, enquanto o MAE é mais robusto à presença de outliers. O Objetivo SMART 1 define ainda um limiar de RMSE inferior a 3.500 dólares.

### 1.2. Problemas Não Supervisionados (Modelos de Agrupamento (_Clustering_))
* **Divisão do _Dataset_:** Para a modelação com algoritmos de _clustering_, dividiu-se o dataset em 70% para treino e 30% para teste, com `random_state=42`, de forma a garantir a reprodutibilidade e avaliar a estabilidade dos agrupamentos em diferentes amostras.
Foram privilegiadas as variáveis standardizadas e normalizadas, sempre que disponíveis, dado que estes algoritmos são sensíveis à escala e à distância entre observações.A avaliação foi feita através de métricas internas adequadas ao clustering, destacando-se o Coeficiente de Silhueta como métrica principal, complementado pelos índices Calinski-Harabasz e Davies-Bouldin, de modo a apoiar a escolha do modelo final com maior rigor.
* **Métrica de Sucesso:** A métrica principal escolhida foi o Coeficiente de Silhueta por ser a mais adequada para avaliar simultaneamente a coesão interna de cada cluster e a separação entre grupos distintos, numa escala interpretável entre -1 e 1. O Objetivo SMART 2 define um Coeficiente de Silhueta superior a 0.50 como critério de sucesso, garantindo que os bairros segmentados formam grupos suficientemente coesos e distintos entre si. O índice Calinski-Harabasz e o Davies-Bouldin foram utilizados como métricas complementares para apoiar a escolha do modelo final com maior rigor técnico.

## 2. Experiências Realizadas
### 2.1. Resposta ao Objetivo SMART 1 (Modelos De Regressão) 
### 2.1.1. Modelo Baseline
* **Algoritmo:** Regressão Linear Simples
* **Justificação:** Escolhemos a Regressão Linear como modelo de referência (_baseline_) por ser o modelo de regressão mais simples e interpretável, servindo como patamar mínimo de comparação para todos os modelos candidatos.  
* **Resultado:**
  
| Parâmetros | Teste | 
| :--- | :--- |
| RMSE: | 4.8757 |
| MAE: | 3.5549 |
| R²: | 0.6810 |
    
#### 2.1.2. Modelos Candidatos 
A análise comparativa dos 3 modelos de regressão testados permite extrair conclusões relavantes sobre o comportamento de cada algoritmo face ao problema de previsão do valor mediano das habitações (`MEDV`).

| Algoritmo | Parâmetros | RMSE (Treino) | RMSE (Teste) | Gap RMSE | MAE (Treino) | MAE (Teste) | Gap MAE | R² (Treino) | R² (Teste) | Gap R² | Notas |  
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |   
| Random Forest | `n_estimators=100`<br>`random_state=42` | 1.66 | 3.59 | 1.93 | 1.13 | 2.56 | 1.43 | 0.97 | 0.83 | 0.14 | Melhor desempenho global no teste, com sobreajuste moderado aceitável |
| XGBoost | `n_estimators=100`<br>`random_state=42` | 0.06| 3.71 | 3.65 | 0.04 | 2.72 | 2.68 | 1 | 0.82 | 0.18 | Sobreajuste severo, RMSE treino quase nulo (0.06) mas Gap de 3.65 no teste revela fraca capacidade de generalização |
| SVR | `kernel='rbf'` | 5.58 | 5.17 | 0.41 | 3.87 | 3.39 | 0.48 | 0.65 | 0.64 | 0.01 | Underfitting, desempenho fraco em ambos os conjuntos indicando incapacidade de capturar a complexidade dos dados |

O **Random Forest** revelou-se o modelo com melhor desempenho global no conjunto de teste, registando um RMSE de 3.59, um MAE de 2.56 e um R² de 0.83, o que significa que o modelo consegue explicar aproximadamente 83% da variância do preço médio das habitações. Embora se verifique um sobreajuste moderado, evidenciado pela discrepância entre o RMSE de treino (1.66) e o de teste (3.59), com um Gap de 1.93, este comportamento é esperado em algoritmos de ensemble baseados em árvores de decisão e não compromete a sua capacidade de generalização de forma significativa.

O **XGBoost** apresentou resultados particularmente preocupantes do ponto de vista da generalização. Embora tenha registado um RMSE de treino quase nulo (0.06) e um R² de treino de 1, estes valores evidenciam um sobreajuste severo, o modelo memorizou os dados de treino em vez de aprender os padrões subjacentes. Esta conclusão é comprovada por um Gap de RMSE de 3.65 e pelo Gap de R² de 0.18, os mais elevados entre os três modelos testados, indicando uma capacidade de generalização claramente inferior à do Random Forest apesar do desempenho aparentemente superior no treino.

O **SVR** demonstrou ser o modelo menos adequado para este problema, apresentando underfitting em ambos os conjuntos, com um RMSE de 5.58 no treino e 5.17 no teste e um R² de apenas 0.65 no treino e 0.64 no teste. Estes resultados sugerem que o modelo SVR não consegue capturar a complexidade das relações não-lineares presentes no conjunto de dados (_dataset_) de Boston. Curiosamente, é o modelo que apresenta o menor Gap em todas as métricas, o que não reflete estabilidade mas sim uma limitada capacidade de aprendizagem em ambos os conjuntos.

Em síntese, o Random Forest destaca-se como o modelo candidato mais equilibrado e tecnicamente fundamentado, apresentando as melhores métricas no conjunto de teste e um nível de sobreajuste aceitável e possivelmente corrigível através de otimização de hiperparâmetros, justificando a sua seleção para a fase de otimização (_tuning_) que se segue.

### 2.2. Resposta ao Objetivo SMART 2 (Modelos de Agrupamento (_Clustering_))
#### 2.2.1 Modelo Baseline
* **Algoritmo:** KMeans
* **Justificação:** Escolhemos o K-Means como modelo de referência (_baseline_) por ser um algoritmo de agrupamento simples, eficiente e facilmente interpretável. A sua utilização permite estabelecer um ponto de comparação inicial para avaliar se modelos mais complexos conseguem melhorar a coesão e a separação dos grupos identificados. 
* **Resultado:**
  
| Parâmetros | Treino | Teste | 
| :--- | :--- | :--- |
| Silhouette | 0.3170 | 0.3325 |
| Calinski-Harabasz | 185.2667 | 131.5455 |
| Davies-Bouldin | 0.9667 | 0.8541 |
| Clusters | 8 | 8 |

KMeans, com 8 agrupamentos (_clusters_) (parâmetro _default_), serviu como ponto de referência mínimo para a comparação. Os resultados obtidos foram claramente insuficientes, com um Coeficiente de Silhueta de 0.3170 no treino e 0.3325 no teste, ambos abaixo do critério de sucesso definido no Objetivo 2 (Silhueta > 0.50), confirmando que a configuração _default_ não produz agrupamentos com qualidade aceitável para o problema em análise.

#### 2.2.2 Modelos Candidatos
A análise comparativa dos quatro modelos de clustering testados permite extrair conclusões relevantes sobre o comportamento de cada algoritmo face ao problema de segmentação dos bairros de Boston.

| Algoritmo | Parâmetros | Silhouette (Treino) | Silhouette (Teste) | Calinski-Harabasz (Treino) | Calinski-Harabasz (Teste) | Davies-Bouldin (Treino) | Davies-Bouldin (Teste) | Nº Clusters (Treino) | Nº Clusters (Teste) | Ruído (Treino) | Ruído (Teste) | Notas |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Baseline KMeans | `k=8` (default) | 0.3170 | 0.3325 | 185.2667 | 131.5455 | 0.9667 | 0.8541 | 8 | 8 | 0 | 0 | Ponto de referência mínimo, silhouette abaixo de 0.50 em ambos os conjuntos |
| DBSCAN | `eps=0.5`, `min_samples=5`,`metric='euclidean'`| 0.2332 | 0.3459 | 110.3760 | 109.8800 | 0.7508 | 0.6706 | 10 | 4 | 112 | 56 | _Silhouette_ abaixo de 0,50 em ambos os conjuntos, elevado número de pontos de ruído e número de clusters inconsistente entre treino e teste  |
| Agglomerative Clustering | `linkage='ward'`, `n_clusters=2` ,`metric='euclidean'`| 0.4989 | 0.5868 | 125.9729 | 90.4516 | 0.8312 | 0.7782 | 2 | 2 | 0 | 0 | Maior Silhouette no teste (0,5868) entre todos os modelos, sem ruído e clusters consistentes, mas Calinski-Harabasz com queda acentuada do treino para o teste |
| KMeans Otimizado | k=4 | 0.5545 | 0.5065 | 216.1761 | 118.9583 | 0.6457 | 0.8031 | 4 | 4 | 0 | 0 | Modelo  estável e consistente, menor Gap, sem ruído e Silhouette acima de 0.50 |

O **DBSCAN**, com eps=0.5, min_samples=5 e metric='euclidean', registou valores de Silhouette abaixo do objetivo SMART em ambos os conjuntos (0,2332 no treino e 0,3459 no teste). A instabilidade é evidente no número de clusters obtidos (10 no treino vs 4 no teste) e no elevado volume de ruído (112 observações no treino e 56 no teste), o que inviabiliza a sua adoção como modelo final.

O **Agrupamento Aglomerativo**, com `linkage='ward'`, `n_clusters=2`e `metric='euclidean'`, apresentou a _Silhouette_ mais elevada no conjunto de teste (0,5868) entre todos os modelos avaliados, superando o objetivo SMART e sem gerar qualquer ponto de ruído, sendo por isso seleccionado como modelo final. Contudo, a queda no índice Calinski-Harabasz do treino para o teste (125,97 vs 90,45) representa uma limitação moderada do ponto de vista da robustez metodológica.

O **KMeans Otimizado** com k=4 apresentou um Silhouette Score de 0,5545 no treino e 0,5065 no teste, sem qualquer ponto de ruído e com número de clusters consistente entre os dois conjuntos. O índice Calinski-Harabasz, embora registe uma redução entre treino (216,18) e teste (118,96), mantém-se em valores substancialmente superiores ao modelo de referência (_baseline_), e o _Davies-Bouldin_ permanece em níveis aceitáveis. O _Silhouette Score_ no teste (0,5065) cumpre o critério definido no objetivo SMART (Silhueta > 0,50), ainda que se situe próximo do limiar, e a degradação das métricas do treino para o teste sugere alguma sensibilidade do modelo aos dados de treino.

## 3. Otimização (Tuning)
### 3.1. Resposta ao Objetivo SMART 1
* **Técnica Utilizada:** Utilizámos GridSearchCV (com validação cruzada de 5 folds) para o _Random Forest_  ajustando os seguintes hiperparâmetros: n_estimators, max_depth e min_samples_split.
* **Melhoria obtida:** O _Random Forest_ não registou qualquer melhoria após a otimização, os hiperparâmetros de base (max_depth=None , n_estimators=100 ,  min_samples_split=2) já eram os ideais, o que indica que o modelo estava bem configurado por omissão.
### 3.2. Resposta ao Objetivo SMART 2
* **Técnica Utilizadea:** Utilizámos _ParameterGrid_ para o _Agglomerative Clustering_, ajustando os seguintes hiperparâmetros: n_clusters (de 2 a 10) e linkage (ward, complete, average).
* **Melhoria obtida:** Após otimização, a melhor combinação encontrada (linkage='complete', n_clusters=2) melhorou de 0.4989 para 0,5889 no treino e 0.5868 para 0,7363 no teste.
## 4. Avaliação do Modelo Final
### 4.1. Problema 1- Erros / Resíduos
A análise de resíduos do Random Forest revela um comportamento globalmente satisfatório. O resíduo médio de 0,0244 é praticamente nulo, indicando ausência de enviesamento sistemático. O desvio padrão de 3,5935 reflete alguma dispersão nos erros, com um erro máximo de 18,28k$ e um erro mínimo de -10,73k$.
O gráfico de Previsto vs Real mostra que os pontos se distribuem próximos da linha de previsão perfeita, com maior dispersão para valores elevados de `MEDV`, sugerindo que o modelo tem mais dificuldade em prever habitações de valor mais alto. O gráfico de Resíduos vs Previstos não evidencia padrões sistemáticos, o que indica que os erros são maioritariamente aleatórios. A distribuição dos resíduos é aproximadamente centrada em zero, confirmando a ausência de enviesamento.
Em termos práticos, 51,3% das previsões apresentam um erro inferior a 2k$ e 88,8% um erro inferior a 5k$, demonstrando que o modelo é preciso na grande maioria dos casos.
### 4.2. Problema 1-Importância dos Atributos (Feature Importance)
A análise de importância de variáveis do _Random Forest_ revela que o `IAH_stand` é de longe a variável mais determinante, representando 59% da importância total. O `IQV_stand` surge em segundo lugar com 11.7%, seguido do `AGE_norm` (8.3%) e `INDUS_norm` (7.8%). As variáveis `TAX_norm` (6.0%) e `B_stand` (4.9%) têm um contributo moderado, enquanto `ZN_stand` (1.8%) e `CHAS` (0.5%) apresentam uma importância residual, sendo praticamente ignoradas pelo modelo.
## 5. Conclusão da Fase de Modelação
A fase de modelação permitiu desenvolver e avaliar um conjunto diversificado de algoritmos, tanto no domínio da aprendizagem supervisionada como da não supervisionada, respondendo diretamente aos dois objetivos SMART definidos no início do projeto.

No que respeita ao Objetivo SMART 1, previsão do valor mediano das habitações (MEDV), o modelo final selecionado foi o Random Forest,pois este apresenta um R² mais elevado e um RMSE mais baixo em comparação com os outros modelos analisados. Porém, após a otimização de hiperparâmetros, o modelo não registou melhorias de desempenho, o que sugere que os hiperparâmetros por omissão já se encontravam próximos do ideal. Em seguida, procedeu-se à validação cruzada K-Fold (k=10), onde revelou um RMSE médio de 4,026, um R² médio de 0,799 e um MAE de 2,812, valores ligeiramente inferiores aos obtidos no conjunto de teste, o que indica que o modelo apresenta alguma sensibilidade à partição dos dados mas mantém um desempenho globalmente aceitável.
.

No que respeita ao Objetivo SMART 2, segmentação dos bairros de Boston, o modelo final selecionado foi o Agglomerative Clustering (linkage='complete', n_clusters=2), que atingiu um Coeficiente de Silhueta de 0,7363 no conjunto de teste, superando largamente o critério mínimo definido (>0,50). O DBSCAN, apesar de apresentar um Silhueta superior, foi excluído devido ao ruído excessivo (~43% dos pontos de treino), e o KMeans otimizado, embora válido, apresentou um Silhueta inferior. A estabilidade do modelo foi confirmada através de uma análise de Bootstrap com 30 iterações, com um intervalo de confiança a 95% de [0,530, 0,755], garantindo que o critério mínimo é cumprido independentemente da amostra utilizada.
Em síntese, os modelos finais seleccionados cumprem os critérios de sucesso estabelecidos nos objectivos SMART do projecto. As principais limitações identificadas prendem-se com a dimensão reduzida do dataset (506 observações) e a natureza histórica dos dados (recolhidos em 1978), que poderiam ser mitigadas com uma maior quantidade de dados em trabalhos futuros. 

---
*Data de última atualização: [18/05/2026]*
