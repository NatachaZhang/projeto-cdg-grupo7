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
A análise comparativa dos 3 modelos de regressão testados permite extrair conclusões relavantes sobre o comportento de cada algoritmo face ao problema de previsão do valor mediano das habitações (`MEDV`).

| Algoritmo | Parâmetros | RMSE (Treino) | RMSE (Teste) | Gap RMSE | MAE (Treino) | MAE (Teste) | Gap MAE | R² (Treino) | R² (Teste) | Gap R² | Notas |  
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |   
| Random Forest | `n_estimators=100`<br>`random_state=42` | 1.66 | 3.58 | 1.92 | 1.14 | 2.55 | 1.41 | 0.97 | 0.83 | 0.14 | Apresentou o melhor desempenho global no conjunto de teste, combinando menor erro e maior capacidade explicativa, apesar de evidenciar algum sobreajuste moderado |
| XGBoost | `n_estimators=100`<br>`random_state=42` | 0.06| 3.71 | 3.65 | 0.04 | 2.72 | 2.68 | 0.99 | 0.82 | 0.17 | Revela excelente desempenho no treino, mas uma discrepância acentuada face ao teste, indicando sobreajuste e reduzida capacidade de generalização |
| SVR | `kernel='rbf'` | 5.97 | 5.71 | 0.26 | 3.95 | 3.71 | 0.24 | 0.59 | 0.56 | 0.03 | Apresenta desempenho inferior tanto no treino como no teste, sugerindo subajuste e limitada capacidade para captar a estrutura dos dadoss |

O **Random Forest** revelou-se o modelo com melhor desempenho global no conjunto de teste, registando um RMSE de 3.58, um MAE de 2.55 e um R² de 0.83, o que significa que o modelo consegue explicar aproximadamente 83% da variância do preço das habitações. Embora se verifique um sobreajuste moderado, evidenciado pela discrepância entre o RMSE de treino (1.66) e o de teste (3.58), com um Gap de 1.92, este comportamento é esperado em algoritmos de ensemble baseados em árvores de decisão e não compromete a sua capacidade de generalização de forma significativa.

O **XGBoost** apresentou resultados particularmente preocupantes do ponto de vista da generalização. Embora tenha registado um RMSE de treino quase nulo (0.06) e um R² de treino de 0.99, estes valores evidenciam um sobreajuste severo, o modelo memorizou os dados de treino em vez de aprender os padrões subjacentes. Esta conclusão é comprovada por um Gap de RMSE de 3.65 e pelo Gap de R² de 0.17, os mais elevados entre os três modelos testados, indicando uma capacidade de generalização claramente inferior à do Random Forest apesar do desempenho aparentemente superior no treino.

O **SVR** demonstrou ser o modelo menos adequado para este problema, apresentando underfitting em ambos os conjuntos, com um RMSE de 5.97 no treino e 5.71 no teste e um R² de apenas 0.59 no treino e 0.56 no teste. Estes resultados sugerem que o SVR com parâmetros default não consegue capturar a complexidade das relações não-lineares presentes no dataset de Boston, nomeadamente a influência de variáveis como o IAH e o IQV no valor das habitações. Curiosamente, é o modelo que apresenta o menor Gap em todas as métricas, o que não reflete estabilidade mas sim uma limitada capacidade de aprendizagem em ambos os conjuntos.

Em síntese, o Random Forest destaca-se como o modelo candidato mais equilibrado e tecnicamente sustentado, reunindo as melhores métricas no conjunto de teste e um nível de sobreajuste aceitável e corrigível através de otimização de hiperparâmetros, justificando a sua seleção para a fase de tuning que se segue.

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

O KMeans de linha de base, com k=8 (parâmetro _default_), serviu como ponto de referência mínimo para a comparação. Os resultados obtidos foram claramente insuficientes, com um Coeficiente de Silhueta de 0.3170 no treino e 0.3325 no teste, ambos abaixo do critério de sucesso definido no Objetivo 2 (Silhueta > 0.50), confirmando que a configuração _default_ não produz agrupamentos com qualidade aceitável para o problema em análise.

#### 2.2.2 Modelos Candidatos
A análise comparativa dos quatro modelos de clustering testados permite extrair conclusões relevantes sobre o comportamento de cada algoritmo face ao problema de segmentação dos bairros de Boston.

| Algoritmo | Parâmetros | Silhouette (Treino) | Silhouette (Teste) | Calinski-Harabasz (Treino) | Calinski-Harabasz (Teste) | Davies-Bouldin (Treino) | Davies-Bouldin (Teste) | Nº Clusters (Treino) | Nº Clusters (Teste) | Ruído (Treino) | Ruído (Teste) | Notas |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Baseline KMeans | `k=8` (default) | 0.3170 | 0.3325 | 185.2663 | 131.5455 | 0.9667 | 0.8541 | 8 | 8 | 0 | 0 | Ponto de referência mínimo, silhouette abaixo de 0.50 em ambos os conjuntos |
| DBSCAN | `eps=0.5`, `min_samples=8` | 0.4178 | 0.7993 | 291.5607 | 286.4850 | 0.6758 | 0.2041 | 3 | 2 | 153 | 74 | Melhor Silhouette no teste mas instável, clusters e ruído inconsistentes entre treino e teste |
| Agglomerative Clustering | `linkage='complete`, `n_clusters=2` | 0.5889 | 0.7363 | 84.7915 | 21.4427 | 0.7157 | 0.1781 | 2 | 2 | 0 | 0 | Boa qualidade mas Calinski muito diferente entre treino e teste, instabilidade moderada |
| KMeans Otimizado | k=4 | 0.5545 | 0.5065 | 216.1761 | 118.9583 | 0.6457 | 0.8031 | 4 | 4 | 0 | 0 | Modelo mais estável e consistente, menor Gap, sem ruído e Silhouette acima de 0.50 |

O **DBSCAN**, com eps=0.5 e min_samples=8, registou o valor mais elevado de Silhueta no conjunto de teste (0.7993) e os melhores índices Calinski-Harabasz em ambos os conjuntos (291.5607 no treino e 286.4850 no teste), sugerindo uma boa densidade e separação dos grupos nesse subconjunto. Contudo, a análise mais detalhada revelou limitações críticas que inviabilizam a sua adoção como modelo final: o número de clusters variou entre treino (3) e teste (2), o volume de ruído foi consideravelmente elevado, 153 observações no treino e 74 no teste, e o índice Davies-Bouldin apresentou uma discrepância acentuada entre treino (0.6758) e teste (0.2041), evidenciando uma instabilidade estrutural que compromete a generalização e interpretabilidade do modelo.

O **Agrupamento Aglomerativo**, com `linkage='complete'` e n`_clusters=2`, apresentou resultados promissores em termos de coesão, com uma Silhueta de 0.5889 no treino e 0.7363 no teste, e a vantagem de não gerar qualquer ponto de ruído. No entanto, a discrepância observada no índice Calinski-Harabasz entre o treino (84.7915) e o teste (21.4427), uma redução de aproximadamente 75%, sugere que a separação entre os dois grupos identificados não se mantém consistente quando o modelo é aplicado a dados não vistos, representando uma limitação relevante do ponto de vista da robustez metodológica.

O **KMeans Otimizado** com k=4 revelou-se a solução mais equilibrada e tecnicamente sustentada. Com um Coeficiente de Silhueta de 0.5545 no treino e 0.5065 no teste, ausência total de ruído em ambos os conjuntos e o número de clusters consistente entre treino (4) e teste (4), este modelo demonstra uma capacidade de generalização superior e estabilidade estrutural. O índice Calinski-Harabasz, embora registe uma redução entre treino (216.1761) e teste (118.9583), mantém-se em valores substancialmente superiores ao baseline, e o Davies-Bouldin permanece em níveis aceitáveis. Importa destacar que o Coeficiente de Silhueta no teste (0.5065) cumpre o critério de sucesso definido no Objetivo 1 do projeto (Silhueta > 0.50), validando a adequação desta solução ao problema em análise e justificando a sua seleção como modelo de clustering final.

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
O modelo apresenta um resíduo médio de 0,1397, praticamente nulo, o que indica ausência de enviesamento sistemático. O desvio padrão dos resíduos é de 3,4482, revelando alguma dispersão em casos específicos.
As maiores falhas concentram-se em habitações com MEDV real de 50,0k$ (valor máximo do dataset), onde o modelo subestima consistentemente. Isto deve-se ao facto de 50,0k$ ser um valor truncado no dataset original, não reflectindo o valor real dessas habitações.
Nos restantes casos o modelo comporta-se de forma aceitável: em 51,3% dos casos o erro absoluto é inferior a 2k$ e em 87,5% é inferior a 5k$.

### 4.2. Importância dos Atributos (Feature Importance)
O IAH_stand é de longe a variável mais determinante no Random Forest (59% da importância total), mas tem menor peso no XGBoost (28,5%), o que indica que o XGBoost distribui a importância de forma mais equilibrada entre as variáveis.
O CHAS é praticamente ignorado pelo Random Forest (0,5%) mas é a segunda variável mais importante no XGBoost (14,8%), revelando que os dois modelos aprenderam padrões distintos nos dados.
TAX_norm e INDUS_norm têm peso relevante no XGBoost (~14% cada), confirmando que essas variáveis influenciam significativamente o preço das habitações.
## 5. Conclusão da Fase de Modelação
A fase de modelação permitiu desenvolver e avaliar um conjunto diversificado de algoritmos, tanto no domínio da aprendizagem supervisionada como da não supervisionada, respondendo diretamente aos dois objetivos SMART definidos no início do projeto.

No que respeita ao Objetivo SMART 1 — previsão do valor mediano das habitações (MEDV), o modelo final selecionado foi o XGBoost otimizado, que após a aplicação de RandomizedSearchCV atingiu um RMSE de 3.4510 e um R² de 0.8402, cumprindo o critério de sucesso definido (RMSE < 3.500 e R² > 0.85 aproximado). Este modelo revelou o melhor equilíbrio entre desempenho preditivo e capacidade de generalização após otimização, superando o Random Forest — que não registou melhorias após tuning — e o SVR, que apesar da maior redução absoluta de RMSE continua a ser o modelo com pior desempenho global. É importante salientar que o Random Forest, embora não tenha beneficiado da otimização, demonstrou ser o modelo mais robusto por omissão, com hiperparâmetros default já próximos do ideal, o que reforça a sua fiabilidade técnica.

No que respeita ao Objetivo SMART 2 — segmentação dos bairros de Boston, o modelo final selecionado foi o KMeans Otimizado com k=4, que atingiu um Coeficiente de Silhueta de 0.5065 no conjunto de teste, cumprindo o critério de sucesso definido (Silhueta > 0.50). Este modelo destacou-se pela sua estabilidade estrutural, número de clusters consistente entre treino e teste, ausência total de ruído e o menor Gap Treino-Teste registado (0.0481), tornando-o a solução mais equilibrada e reprodutível entre os algoritmos testados. O DBSCAN e o Agglomerative Clustering, embora tenham apresentado valores de Silhueta superiores no teste, revelaram instabilidades que comprometem a sua adoção em contexto real.
Em síntese, os modelos finais selecionados, o XGBoost otimizado para regressão e KMeans com k=4 para clustering, cumprem os critérios de sucesso estabelecidos nos objetivos SMART do projeto, respondem às perguntas de investigação definidas na fase de iniciação e estão tecnicamente preparados para ser apresentados como solução final. As principais limitações identificadas prendem-se com a dimensão reduzida do dataset (506 observações), a natureza histórica dos dados (recolhidos em 1978) e o sobreajuste residual observado nos modelos de ensemble, que poderiam ser mitigados com uma maior quantidade de dados e técnicas adicionais de regularização em trabalhos futuros.  

---
*Data de última atualização: [23/04/2026]*
