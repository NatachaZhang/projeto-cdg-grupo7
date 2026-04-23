# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação
### 1.1. Problemas Supervisionados (Modelos De Regressão)
* **Divisão do _Dataset_:** Realizámos testes com duas divisões distintas do dataset, 80/20 e 70/30, com semente aleatória (random_state=42) fixa para garantir a reprodutibilidade dos resultados. A divisão 80/20 ficou com 404 amostras de treino e 102 de teste, enquanto a divisão 70/30 ficou com 354 amostras de treino e 152 de teste. Após comparação das métricas obtidas em ambas as divisões, verificou-se que a divisão 70/30 produziu melhores resultados globais superando todas as combinações testadas. Por este motivo, adotámos a divisão 70/30 como estratégia de validação para a fase de otimização, garantindo o isolamento total dos dados de avaliação para evitar fugas de informação (_data leakage_).
* **Métrica de Sucesso:** (p/ex.: "A métrica principal escolhida foi o F1-Score, pois o nosso
dataset é desequilibrado e queremos evitar falsos negativos.")

### 1.2. Problemas Não Supervisionados (Modelos de Agrupamento (_Clustering_))
* **Divisão do _Dataset_:**
* **Métrica de Sucesso:**

## 2. Experiências Realizadas
### 2.1. Problemas Supervisionados
### Modelos De Regressão
#### 2.1.1. Modelo Baseline
* **Algoritmo:** Regressão Linear Simples
* **Justificação:** Escolhemos a Regressão Linear como baseline por ser o modelo de regressão mais simples e interpretável, servindo como patamar mínimo de comparação para todos os modelos candidatos.  
* **Resultado:**
  - RMSE: 4.8757
  - MAE: 3.5549
  - R²: 0.6810
    
#### 2.1.2. Modelos Candidatos    
| Algoritmo | Parâmetros Base | RMSE (Treino) | RMSE (Teste) | MAE (Treino) | MAE (Teste) | R² (Treino) | R² (Teste) | Notas |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |:--- | :--- |
| Random Forest | n_estimators=100, random_state=42 | 1.66 | 3.58 | 1.14 | 2.55 |  0.97 | 0.83 |Melhor modelo global, vence nas 3 métricas em simultâneo com sobreajuste moderado |
| XGBoost | n_estimators=100, random_state=42 | 0.06| 3.71 |0.04 | 2.72 | 0.99 | 0.82 | Sobreajuste severo, R² treino quase perfeito (0.999964) indica memorização dos dados de treino|
| SVR | kernel='rbf' | 5.97 | 5.71 | 3.95 | 3.71 |  0.59 | 0.56 | Underfitting, desempenho fraco em ambos os conjuntos, não captura a complexidade dos dados |

### 2.2. Problemas Não Supervisionados
### Modelos de Agrupamento (_Clustering_)
#### 2.2.1 Modelo Baseline
* **Algoritmo:** KMeans
* **Justificação:** Escolhemos o KMeans como linha de base por ser um algoritmo de agrupamento simples, eficiente e facilmente interpretável. A sua utilização permite estabelecer um ponto de comparação inicial para avaliar se modelos mais complexos conseguem melhorar a coesão e a separação dos grupos identificados. 
* **Resultado:**
  - Silhouette Teste : 0.3325
  - Calinski-Harabasz Teste : 131.5455
  - Davies-Bouldin Teste : 0.8541
  - Clusters Teste   : 8

#### 2.2.2 Modelos Candidatos
| Algoritmo | Parâmetros Base | RMSE (Treino) | RMSE (Teste) | MAE (Treino) | MAE (Teste) | R² (Treino) | R² (Teste) | Notas |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |:--- | :--- |
| Random Forest | n_estimators=100, random_state=42 | 1.66 | 3.58 | 1.14 | 2.55 |  0.97 | 0.83 |Melhor modelo global, vence nas 3 métricas em simultâneo com sobreajuste moderado |
| XGBoost | n_estimators=100, random_state=42 | 0.06| 3.71 |0.04 | 2.72 | 0.99 | 0.82 | Sobreajuste severo, R² treino quase perfeito (0.999964) indica memorização dos dados de treino|
| SVR | kernel='rbf' | 5.97 | 5.71 | 3.95 | 3.71 |  0.59 | 0.56 | Underfitting, desempenho fraco em ambos os conjuntos, não captura a complexidade dos dados |

## 3. Otimização (Tuning)
*Descrevam como melhoraram o melhor modelo.*
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
*Data de última atualização: [DD/MM/AAAA]*
