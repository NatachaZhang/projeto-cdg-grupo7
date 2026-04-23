# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação
### 1.1. Problemas Supervisionados (Modelos De Regressão)
* **Divisão do _Dataset_:** Realizámos testes com duas divisões distintas do dataset, 80/20 e 70/30, de forma aleatória (`random_state=42`) fixa para garantir a reprodutibilidade dos resultados. A divisão 80/20 ficou com 404 amostras de treino e 102 de teste, enquanto a divisão 70/30 ficou com 354 amostras de treino e 152 de teste. Após comparação das métricas obtidas em ambas as divisões, verificou-se que a divisão 70/30 produziu melhores resultados globais superando todas as combinações testadas. Por este motivo, adotámos a divisão 70/30 como estratégia de validação para a fase de otimização, garantindo o isolamento total dos dados de avaliação para evitar perdas de informação (_data leakage_).
* **Métrica de Sucesso:** (p/ex.: "A métrica principal escolhida foi o F1-Score, pois o nosso
dataset é desequilibrado e queremos evitar falsos negativos.")

### 1.2. Problemas Não Supervisionados (Modelos de Agrupamento (_Clustering_))
* **Divisão do _Dataset_:** Para a modelação com algoritmos de clustering, dividiu-se o dataset em 70% para treino e 30% para teste, com `random_state=42`, de forma a garantir a reprodutibilidade e avaliar a estabilidade dos agrupamentos em diferentes amostras.
Foram privilegiadas as variáveis standardizadas e normalizadas, sempre que disponíveis, dado que estes algoritmos são sensíveis à escala e à distância entre observações.A avaliação foi feita através de métricas internas adequadas ao clustering, destacando-se o Coeficiente de Silhueta como métrica principal, complementado pelos índices Calinski-Harabasz e Davies-Bouldin, de modo a apoiar a escolha do modelo final com maior rigor.
* **Métrica de Sucesso:**

## 2. Experiências Realizadas
### 2.1. Problemas Supervisionados
### Modelos De Regressão
#### 2.1.1. Modelo Baseline
* **Algoritmo:** Regressão Linear Simples
* **Justificação:** Escolhemos a Regressão Linear como baseline por ser o modelo de regressão mais simples e interpretável, servindo como patamar mínimo de comparação para todos os modelos candidatos.  
* **Resultado:**
  
| Parâmetros | Treino | Teste | 
| :--- | :--- | :--- |
| RMSE: |  | 4.8757 |
| MAE: |  | 3.5549 |
| R²: |  | 0.6810 |
    
#### 2.1.2. Modelos Candidatos 
Entre os modelos candidatos de regressão, o Random Forest destacou-se como a melhor solução global, apresentando os menores valores de erro no conjunto de teste e o maior coeficiente de determinação. O XGBoost revelou desempenho muito elevado no treino, mas com uma discrepância significativa face ao teste, sugerindo sobreajuste. Já o SVR apresentou resultados inferiores em ambos os conjuntos, evidenciando sinais de subajuste. Assim, o Random Forest foi considerado o modelo mais equilibrado em termos de desempenho e capacidade de generalização.

| Algoritmo | Parâmetros | RMSE (Treino) | RMSE (Teste) | Gap RMSE | MAE (Treino) | MAE (Teste) | Gap MAE | R² (Treino) | R² (Teste) | Gap R² | Notas |  
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |   
| Random Forest | `n_estimators=100`<br>`random_state=42` | 1.66 | 3.58 | 1.92 | 1.14 | 2.55 | 1.41 | 0.97 | 0.83 | 0.14 | Apresentou o melhor desempenho global no conjunto de teste, combinando menor erro e maior capacidade explicativa, apesar de evidenciar algum sobreajuste moderado |
| XGBoost | `n_estimators=100`<br>`random_state=42` | 0.06| 3.71 | 3.65 | 0.04 | 2.72 | 2.68 | 0.99 | 0.82 | 0.17 | Revela excelente desempenho no treino, mas uma discrepância acentuada face ao teste, indicando sobreajuste e reduzida capacidade de generalização |
| SVR | `kernel='rbf'` | 5.97 | 5.71 | 0.26 | 3.95 | 3.71 | 0.24 | 0.59 | 0.56 | 0.03 | Apresenta desempenho inferior tanto no treino como no teste, sugerindo subajuste e limitada capacidade para captar a estrutura dos dadoss |

### 2.2. Problemas Não Supervisionados
### Modelos de Agrupamento (_Clustering_)
#### 2.2.1 Modelo Baseline
* **Algoritmo:** KMeans
* **Justificação:** Escolhemos o KMeans como linha de base por ser um algoritmo de agrupamento simples, eficiente e facilmente interpretável. A sua utilização permite estabelecer um ponto de comparação inicial para avaliar se modelos mais complexos conseguem melhorar a coesão e a separação dos grupos identificados. 
* **Resultado:**
  
| Parâmetros | Treino | Teste | 
| :--- | :--- | :--- |
| Silhouette | 0.3170 | 0.3325 |
| Calinski-Harabasz | 185.2667 | 131.5455 |
| Davies-Bouldin | 0.9667 | 0.8541 |
| Clusters | 8 | 8 |

#### 2.2.2 Modelos Candidatos
A comparação dos modelos candidatos mostra que o DBSCAN apresentou o valor mais elevado de Silhouette no conjunto de teste. No entanto, o Agglomerative Clustering revelou maior estabilidade estrutural, ao manter o mesmo número de clusters em treino e teste e não apresentar pontos de ruído, o que o torna uma solução mais equilibrada do ponto de vista técnico e interpretativo.
| Algoritmo | Parâmetros | Silhouette (Treino) | Silhouette (Teste) | Nº Clusters (Treino) | Nº Clusters (Teste) | Ruído (Treino) | Ruído (Teste) | Gap Treino-Teste | Notas |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |:--- | :--- | :--- |
| DBSCAN | `eps=0.5`<br>`min_samples=8` | 0.4178 | 0.7993 | 3 | 2 | 153 | 74 | 0.3815 | Melhor valor de silhueta no teste, mas com menor estabilidade e elevada sensibilidade ao ruído |
| Agglomerative Clustering | `linkage='complete'`<br>`n_clusters=2` | 0.5889 | 0.7363 | 2 | 2 | 0 | 0 | 0.1474 | Apresenta o melhor equilíbrio entre qualidade dos agrupamentos e estabilidade entre treino e teste |
| KMeans otimizado | `k=4` | 0.5545 | 0.5065 | 4 | 4 |  0 | 0 | 0.0481 | Modelo mais consistente, embora com menor capacidade de separação entre grupos |

## 3. Otimização (Tuning)
### 3.1. 
* **Técnica Utilizada:** (p/ex.: "Utilizámos GridSearchCV para ajustar os hiperparâmetros
`max_depth` e `learning_rate`.")
* **Melhoria obtida:** (p/ex.: "O F1-Score subiu de 0.85 para 0.88 após o ajuste.")

### 3.2.
* **Técnica Utilizada:** (p/ex.: "Utilizámos GridSearchCV para ajustar os hiperparâmetros
`max_depth` e `learning_rate`.")
* **Melhoria obtida:** (p/ex.: "O F1-Score subiu de 0.85 para 0.88 após o ajuste.")
  
## 4. Avaliação do Modelo Final
### 4.1. Matriz de Confusão / Erros
*Analisem onde o modelo mais falha.*
> **Análise:** (p/ex.: "O modelo ainda confunde a Classe A com a Classe B em 10% dos casos devido
à semelhança nos atributos X e Y.")
### 4.2. Importância dos Atributos (Feature Importance)
*Quais as variáveis que o modelo considerou mais importantes para decidir?*
1. [Variável X]
2. [Variável Y]
## 5. Conclusão da Fase de Modelação
*Justifiquem por que razão este modelo está pronto (ou não) para ser apresentado como solução
final.*
---
*Data de última atualização: [23/04/2026]*
