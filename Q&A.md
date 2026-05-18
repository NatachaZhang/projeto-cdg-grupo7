### 3 possíveis dúvidas sobre o modelo
#### Pergunta 1. Porque foram criados os indicadores `IQV` e `IAH` em vez de usar as variáveis originais diretamente?
As variáveis originais do conjunto de dados (_dataset_), como a taxa de criminalidade, o nível de poluição ou o rácio aluno-professor, são úteis individualmente, mas difíceis de interpretar em conjunto. A criação do `IQV` (Índice de Qualidade de Vida) e do `IAH` (Índice de Atratividade Habitacional) serviu dois propósitos: Reduzir a dimensionalidade, em vez de analisar várias variáveis separadas, passamos a ter indicadores sintéticos que resumem conceitos mais amplos;
Melhorar a interpretabilidade, um valor alto de `IQV` significa claramente melhores condições de vida, o que é mais intuitivo do que analisar cada variável negativa isoladamente.

No caso do IQV, as variáveis originais foram invertidas (porque valores altos representavam aspetos negativos), garantindo que um IQV maior corresponde sempre a uma melhor qualidade de vida. Esta transformação também contribui para tornar os modelos mais fáceis de explicar a utilizadores não técnicos.

#### Pergunta 2. Porque foi escolhido o _Random Forest_ e não o _XGBoost_, que é habitualmente mais preciso?
Foram testados quatro modelos de regressão: Regressão Linear, _Random Forest_, _XGBoost_ e SVR. O _Random Forest_ foi selecionado porque apresentou o melhor equilíbrio entre desempenho e generalização para este dataset específico.
Embora o _XGBoost_ seja frequentemente mais preciso em competições e conjunto de dados (_dataset_) de maior dimensão, neste caso o _Random Forest_ obteve resultados comparáveis com menor risco de overfitting, o que é relevante dado o tamanho reduzido do conjunto de dados (_dataset_) (506 observações). O modelo explicou cerca de 83% da variação dos preços (R² ≈ 0,83), com um RMSE aproximado de 3,59 mil dólares.
É importante reconhecer que o objetivo foi apenas parcialmente cumprido: o R² ultrapassou o valor mínimo definido, mas o `RMSE` ficou ligeiramente acima do limite pretendido.

#### Pergunta 3. Como foi decidido o número de aprupamentos (_clusters_) no Agglumerative Clustering o e porque dois grupos?
O número de agrupamentos (_clusters_) não foi definido à partida, o modelo _Agglomerative Clustering_ foi executado com os parâmetros por defeito e avaliado através de três métricas de clustering: _Silhouette Score_, _Calinski-Harabasz_ e _Davies-Bouldin_.
O modelo identificou consistentemente 2 agrupamentos (_clusters_), tanto no treino como no teste, sem qualquer ponto de ruído, o que demonstra estabilidade e robustez face a diferentes subconjuntos de dados.
O objetivo SMART definido (_Silhouette_ > 0,50) foi cumprido no conjunto de teste, com um valor de 0,5868. O índice de _Davies-Bouldin_, onde valores mais baixos indicam melhor separação, também melhorou do treino para o teste. Estes resultados em conjunto confirmam que a solução com 2 clusters é estável e adequada para os dados.
Os dois perfis identificados, Zona Urbana Desvalorizada e Zona Residencial Valorizada, são coerentes com a realidade imobiliária e oferecem valor prático para compradores, investidores e decisores públicos.
