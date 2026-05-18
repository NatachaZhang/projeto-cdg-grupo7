# Relatório de Conclusão e Entrega de Valor (Milestone 4)
## 1. Síntese de Resultados e Impacto

Este projeto teve como objetivo aplicar técnicas de Ciência de Dados ao mercado imobiliário de Boston, combinando modelos preditivos e técnicas de segmentação para apoiar decisões de compra, venda e análise urbana.
Através da utilização de Machine Learning, foi possível estimar preços de habitações com elevada capacidade explicativa e identificar diferentes perfis de bairros com base em características socioeconómicas e ambientais.
O projeto demonstra como dados históricos podem ser transformados em informação útil para investidores, agentes imobiliários e entidades públicas.

## Problema SMART 1
* **O Problema Resolvido:** O Objetivo 1 consistiu em desenvolver um modelo capaz de estimar automaticamente o preço de uma habitação em Boston, com um nível de precisão previamente definido, até ao final do Milestone 3. Este objetivo foi maioritariamente alcançado: o modelo atingiu o nível de capacidade explicativa pretendido, embora a margem de erro média tenha ficado ligeiramente acima da meta inicialmente estabelecida, registando cerca de 3.594 dólares por estimativa face ao objetivo de 3.500 dólares.

* **Interpretação dos Resultados:** O modelo revelou elevada capacidade de previsão, conseguindo explicar aproximadamente 83% da variação dos preços das habitações. Contudo, o RMSE de 3.594 dólares, significa que, em média, as previsões do modelo erram cerca de 3.594 dólares face ao preço real das habitações.

* **Valor para o Utilizador/Negócio:** Com esta solução, agentes imobiliários, investidores e avaliadores podem obter uma estimativa automatizada e fundamentada do preço de uma habitação, com base em diversas características da habitação. Isto permite agilizar avaliações, identificar habitações subvalorizadas no mercado e apoiar decisões de compra ou venda com maior rigor quantitativo.

### Problema SMART 2
* **O Problema Resolvido:** O Objetivo 2 consistiu em segmentar as habitações de Boston em perfis distintos, com base nas suas características socioeconómicas, habitacionais e ambientais, atingindo um nível mínimo de separação entre grupos até ao final do Milestone 3. Este objetivo foi integralmente alcançado, com uma separação entre grupos muito superior ao mínimo.
  
* **Interpretação dos Resultados:** A análise identificou dois perfis de bairros claramente distintos. O primeiro, denominado "Zona Urbana Desvalorizada", engloba a grande maioria dos bairros (487 em 506), caracterizados por habitações mais antigas, maior presença industrial e menor qualidade de vida. O segundo, denominado "Zona Residencial Valorizada", é composto por apenas 19 em 506 habitações, com habitações mais recentes, zonas mais amplas, menos industrialização e melhor qualidade de vida.

* **Valor para o Utilizador/Negócio:**  Esta segmentação permite perceber, de forma simples e automática, em que tipo de bairro se insere uma habitação. Para um comprador, ajuda a perceber se está a adquirir uma casa numa zona mais valorizada ou numa zona com menor qualidade de vida. Para um investidor, permite identificar zonas com potencial de valorização. Para um município, apoia a definição de prioridades em políticas de habitação e requalificação urbana, direcionando recursos para as zonas que mais necessitam de intervenção.

## 2. Análise Crítica e Limitações
* **Limitações dos Dados:** *  O conjunto de dados (_dataset_) é composto por apenas 506 observações recolhidas em 1978, o que limita a representatividade dos dados face ao mercado imobiliário atual.
### Problema 1:
* **Limitações do Modelo:** O modelo _Random Forest_ apresentou sinais evidentes de sobreajustamento (_overfitting_), demonstrando melhor desempenho nos dados de treino do que em novos subconjuntos de validação.  Apesar da realização de testes automáticos de otimização de hiperparâmetros através de _GridSearchCV_, não se verificaram melhorias significativas no desempenho do modelo. A validação cruzada _K-Fold_ (k=10) confirmou um RMSE médio de 4.026, ligeiramente acima do objetivo de 3.500 dólares, sugerindo que o desempenho obtido na divisão inicial dos dados pode ser parcialmente otimista.
* **Contextos de Falha:** O modelo não é recomendado para a previsão de habitações de valor muito elevado, uma vez que os dados de treino contêm poucos exemplos nessa gama de preços. Como consequência, as previsões tornam-se menos precisas para imóveis com valores extremos, onde se observou maior dispersão entre os valores reais e os valores estimados.
### Problema 2:
* **Limitações do Modelo:** O modelo dividiu as zonas em apenas 2 grupos, sendo que um deles é muito pequeno, com apenas 19 habitações num total de 506. Isto significa que as conclusões retiradas sobre esse grupo devem ser interpretadas com cautela, uma vez que um número tão reduzido de casos pode não ser suficiente para representar de forma fiável esse tipo de zona. 
* **Contextos de Falha:** O modelo não é adequado para segmentar habitações com características intermédias, uma vez que a segmentação em apenas dois grupos não captura a eventual existência de perfis de transição entre a Zona Urbana Desvalorizada e a Zona Residencial Valorizada. Em contextos onde seja necessária uma segmentação mais granular do mercado, o modelo poderá revelar-se insuficiente.
## 3. Considerações Éticas e de Viés
* **Privacidade:** O conjunto de dados (_dataset_) não contém qualquer identificador pessoal, sendo composto exclusivamente por características agregadas de zonas geográficas de Boston. Não existe qualquer risco de exposição de dados individuais ou violação de privacidade.
* **Transparência:** A análise de importância de variáveis (_Feature Importance_) aplicada ao _Random Forest_ permitiu identificar que o Índice de Atratividade Habitacional, que combina a dimensão das habitações, o estatuto socioeconómico da população e a proximidade ao emprego, é a variável com maior peso nas previsões (59%), tornando o processo de decisão do modelo compreensível e justificável. No Problema 2, a caracterização dos dois segmentos com base nos valores médios das variáveis permite perceber de forma clara o que distingue cada grupo, sem necessidade de conhecimentos técnicos aprofundados.
Importa ainda reconhecer que o dataset Boston Housing apresenta limitações históricas e potenciais enviesamentos socioeconómicos, uma vez que foi construído com base em dados urbanos recolhidos nos anos 70. Desta forma, os resultados obtidos devem ser interpretados com cautela quando aplicados a contextos sociais atuais.

## 4. Roadmap e Trabalhos Futuros

Numa perspetiva futura, a solução poderá evoluir para uma plataforma interativa de apoio ao mercado imobiliário, integrando dados em tempo real, mapas geográficos e previsões dinâmicas ajustadas às condições atuais do mercado.

1. **Melhoria Técnica:** A distribuição desigual entre os dois grupos de bairros reflete a realidade dos dados disponíveis. Uma análise mais equilibrada exigiria um conjunto de dados mais diversificado, com maior representação de zonas residenciais valorizadas.
2. **Novas Variáveis:** Integrar informação adicional sobre cada zona, como proximidade a transportes públicos, escolas e espaços verdes, para tornar tanto a estimativa de preços como a classificação de bairros mais completa e representativa.
3. **Escalabilidade (Deployment):** Integrar as duas ferramentas numa solução única, onde ao inserir as características de uma habitação o utilizador recebe simultaneamente a estimativa de preço e o perfil do bairro correspondente, tornando a análise mais completa e acessível a qualquer pessoa.

## 5. Conclusão Final 

O desenvolvimento deste projeto permitiu demonstrar como técnicas de Ciência de Dados e do Machine Learning podem ser aplicadas ao mercado imobiliário para extrair conhecimento relevante a partir de dados urbanos e habitacionais. A utilização de modelos preditivos e técnicas de segmentação possibilitou não apenas estimar preços de habitações com elevada capacidade explicativa, mas também identificar diferentes perfis de bairros com características socioeconómicas e ambientais distintas.

Os resultados obtidos evidenciam que modelos preditivos podem apoiar avaliações imobiliárias de forma consistente e fundamentada, enquanto as técnicas de segmentação permitem compreender melhor as diferenças entre zonas urbanas e identificar padrões associados à valorização habitacional e à qualidade de vida. Apesar das limitações identificadas, nomeadamente a reduzida dimensão e antiguidade do conjunto de dados, o projeto conseguiu atingir os principais objetivos definidos e demonstrar valor prático na interpretação e utilização dos resultados.

Numa perspetiva futura, a integração destas soluções em plataformas interativas, alimentadas por dados atualizados em tempo real, poderá contribuir para análises imobiliárias mais acessíveis, transparentes e orientadas para apoio à decisão, reforçando o papel da Ciência de Dados na compreensão e planeamento do espaço urbano

---
**Data de Conclusão:** 18/05/2026
**Versão do Projeto:** v4.0 Final--- 
