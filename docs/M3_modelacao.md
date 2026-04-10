# Milestone 3: Modelação e Avaliação
## 1. Estratégia de Modelação
*Descrevam como prepararam os dados para os algoritmos.*
* **Divisão do dataset:** Realizámos testes com duas divisões distintas do dataset, 80/20 e 70/30, com semente aleatória (random_state=42) fixa para garantir a reprodutibilidade dos resultados. A divisão 80/20 ficou com 404 amostras de treino e 102 de teste, enquanto a divisão 70/30 ficou com 354 amostras de treino e 152 de teste. Após comparação das métricas obtidas em ambas as divisões, verificou-se que a divisão 70/30 produziu melhores resultados globais superando todas as combinações testadas. Por este motivo, adotámos a divisão 70/30 como estratégia de validação para a fase de otimização, garantindo o isolamento total dos dados de avaliação para evitar fugas de informação (_data leakage_).
* **Métrica de Sucesso:** (p/ex.: "A métrica principal escolhida foi o F1-Score, pois o nosso
dataset é desequilibrado e queremos evitar falsos negativos.")
## 2. Experiências Realizadas
### 2.1. Modelo Baseline
* **Algoritmo:** Regressão Linear Simples
* **Justificação:** Escolhemos a Regressão Linear como baseline por ser o modelo de regressão mais simples e interpretável, servindo como patamar mínimo de comparação para todos os modelos candidatos.  
* **Resultado:**
  - RMSE: 4.7511
  - MAE: 3.3544
  - R²: 0.6922
### 2.2. Modelos Candidatos
*Listagem dos algoritmos testados e a justificação da escolha.*
| Algoritmo | Parâmetros Base | RMSE (Treino) | RMSE (Teste) | MAE (Treino) | MAE (Teste) | R² (Treino) | R² (Teste) | Notas |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |:--- | :--- |
| Random Forest | n_estimators=100, random_state=42 | 1.51 | 3.80 | 1.05 | 2.66 |  0.97 | 0.80 |Sobreajuste moderado - R² treino muito superior ao teste |
| XGBoost | n_estimators=100, random_state=42 | 0.05 | 3.69 |0.04 | 2.73 | 0.99 | 0.81 | Sobreajuste severo - R² treino quase perfeito (0.9999) mas teste inferior|
| SVR | kernel='rbf' | 5.71 | 5.69 | 3.78 | 3.40 |  0.62 | 0.56 | Underfitting - desempenho fraco em treino e teste, não consegue capturar a complexidade dos dados |
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
