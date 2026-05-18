# Relatório de Conclusão e Entrega de Valor (Milestone 4)
## 1. Síntese de Resultados e Impacto
## Problema SMART 1
* **O Problema Resolvido:** O Objetivo 1 consistiu em criar um modelo capaz de estimar automaticamente o preço de uma habitação em Boston, com um nível de precisão previamente definido, até ao final do Milestone 3. Este objetivo foi parcialmente alcançado: o modelo atingiu o nível de precisão exigido em termos de capacidade explicativa (acerta na faixa de preço correta em mais de 82% dos casos), mas a margem de erro média ficou ligeiramente acima do pretendido, cerca de 3.594 dólares por estimativa, face ao objetivo de 3.500 dólares.

* **Interpretação dos Resultados:** O modelo demostra uma boa capacidade explicativa, pois consegue explicar 82.7% da variação do preço médio das casas. Contudo, o RMSE de 3.594 dólares, significa que, em média, as previsões do modelo erram cerca de 3.594 dólares face ao preço real das habitações.

* **Valor para o Utilizador/Negócio:** Com esta solução, agentes imobiliários, investidores e avaliadores podem obter uma estimativa automatizada e fundamentada do preço de uma habitação, com base em diversas características da habitação. Isto permite agilizar avaliações, identificar habitações subvalorizadas no mercado e apoiar decisões de compra ou venda com maior rigor quantitativo.

### Problema SMART 2
* **O Problema Resolvido:** O Objetivo 2 consistie em segmentar os bairros de Boston em perfis distintos, com base nas características das habitações e do meio envvolvente, atingindo um nível mínimo de separação entre grupos até ao final do Milestone 3. Este objetivo foi integralmente alcançado, com uma separação entre grupos muito superior ao mínimo.
* **Interpretação dos Resultados:** A análise identificou dois perfis de bairros claramente distintos. O primeiro, denominado "Zona Urbana Desvalorizada", engloba a grande maioria dos bairros (487 em 506), caracterizados por habitações mais antigas, maior presença industrial e menor qualidade de vida. O segundo, denominado "Zona Residencial Valorizada", é composto por apenas 19 em 506, com habitações mais recentes, zonas mais amplas, menos industrialização e melhor qualidade de vida.
* **Valor para o Utilizador/Negócio:**  Esta segmentação permite perceber, de forma simples e automática, em que tipo de bairro se insere uma habitação. Para um comprador, ajuda a perceber se está a adquirir uma casa numa zona mais valorizada ou numa zona com menor qualidade de vida. Para um investidor, permite identificar zonas com potencial de valorização. Para um município, apoia a definição de prioridades em políticas de habitação e requalificação urbana, direcionando recursos para as zonas que mais necessitam de intervenção.
## 2. Análise Crítica e Limitações
* **Limitações dos Dados:** *  O conjunto de dados (_dataset_) é composto por apenas 506 observações recolhidas em 1978, o que limita a representatividade dos dados face ao mercado imobiliário atual.
### Problema 1:
* **Limitações do Modelo:** Random Forest apresentou sinais evidentes de sobreajustamento (_overfitting_). Apesar da sintonização fina de hiperparâmetros via GridSearchCV (realizando testes de diferentes valores de n_estimators, max_depth e min_samples_split), o modelo convergiu consistentemente para os parâmetros por omissão (100 árvores, sem limitação de profundidade), sem melhorias adicionais de desempenho. A validação cruzada K-Fold (k=10) confirmou um RMSE médio de 4.026, ligeiramente acima do objetivo de 3.500 dólares, sugerindo que o desempenho obtido na divisão 70/30 pode ser parcialmente otimista.
* **Contextos de Falha:** O modelo não é recomendado para a previsão de habitações de valor muito elevado, uma vez que os dados de treino contêm poucos exemplos nessa gama de preços, resultando numa maior imprecisão das previsões para esse segmento,como evidenciado pela maior dispersão nos valores extremos de MEDV.
### Problema 2:
* **Limitações do Modelo:**  modelo dividiu as zonas em apenas 2 grupos, sendo que um deles é muito pequeno, com apenas 19 zonas num total de 506. Isto significa que as conclusões retiradas sobre esse grupo devem ser interpretadas com cautela, uma vez que um número tão reduzido de casos pode não ser suficiente para representar de forma fiável esse tipo de zona. 
* **Contextos de Falha:**
## 3. Considerações Éticas e de Viés
* **Privacidade:** O conjunto de dados (_dataset_) não contém qualquer identificador pessoal, sendo composto exclusivamente por características agregadas de zonas geográficas de Boston. Não existe qualquer risco de exposição de dados individuais ou violação de privacidade.
* **Transparência:** A análise de importância de variáveis (_Feature Importance_) aplicada ao _Random Forest_ permitiu identificar que o Índice de Atratividade Habitacional, que combina a dimensão das habitações, o estatuto socioeconómico da população e a proximidade ao emprego,é a variável com maior peso nas previsões (59%), tornando o processo de decisão do modelo compreensível e justificável. No Problema 2, a caracterização dos dois segmentos com base nos valores médios das variáveis permite perceber de forma clara o que distingue cada grupo, sem necessidade de conhecimentos técnicos aprofundados.
## 4. Roadmap e Trabalhos Futuros
1. **Melhoria Técnica:** A distribuição desigual entre os dois grupos de bairros reflete a realidade dos dados disponíveis. Uma análise mais equilibrada exigiria um conjunto de dados mais diversificado, com maior representação de zonas residenciais valorizadas.
2. **Novas Variáveis:** (Ex: "Integrar dados meteorológicos ou sazonais para refinar as previsões
de venda.")
3. **Escalabilidade (Deployment):** (Ex: "Desenvolver uma interface web (Streamlit) para que o
modelo possa ser utilizado por utilizadores não-técnicos em tempo real.")
---
**Data de Conclusão:** 18/05/2026
**Versão do Projeto:** v4.0 Final--- 
