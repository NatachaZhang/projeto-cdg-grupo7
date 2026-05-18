# Milestone 2: Análise Exploratória e Engenharia de Atributos


## 1. Análise Exploratória de Dados (EDA)

### 1.1. Distribuição da Variável Alvo
A variável alvo `MEDV` apresenta uma distribuição com assimetria positiva, onde a maioria das habitações se concentra na faixa dos 20 a 25 mil dólares, existindo um conjunto reduzido de observações com valores significativamente elevados que originam uma cauda mais extensa no lado direito da distribuição.
Relativamente ao equilíbrio, a variável não pode ser considerada totalmente equilibrada. O histograma revela uma clara concentração de observações nos valores intermédios, com menor frequência nos extremos. O diagrama de extermos e quartis (boxplot) confirma ainda a presença de vários valores atípicos (_outliers_) no limite superior, visíveis como pontos acima dos 40 mil dólares.
No que diz respeito à normalidade, a distribuição de `MEDV` não segue uma distribuição normal perfeita. Embora apresente um pico central próximo dos 20 mil dólares, a cauda direita alongada afasta-a da simetria característica de uma distribuição normal, o que poderá influenciar o desempenho do modelo de regressão linear, uma vez que este pressupõe normalidade nos resíduos para garantir previsões fiáveis.

### 1.2. Correlações Relevantes
* **Atributo `LSTAT` vs. Alvo (`MEDV`):** A análise bivariada revela que a variável `LSTAT` apresenta a correlação negativa mais forte com a variável alvo `MEDV` (r = -0.74), evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_), onde se observa claramente que à medida que a percentagem (%) de população de baixa renda aumenta, o valor mediano das habitações diminui de forma consistente, confirmando que o perfil socioeconómico do bairro é o preditor mais determinante do preço das habitações no~conjunto de dados(_dataset_) de Boston. 
* **Atributo `RM` vs. Alvo (`MEDV`):** A variável `RM` apresenta a correlação positiva mais forte com o `MEDV` (r = 0.70), evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_), onde se observa claramente uma tendência linear positiva, quanto maior o número médio de quartos numa habitação, maior o seu valor mediano. 
* **Atributo `PTRATIO` vs. Alvo (`MEDV`):** A variável `PTRATIO` surge como o terceiro preditor com maior relação com a variável alvo `MEDV`, apresentando uma correlação negativa moderada de r = 0.51, evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_). Bairros com rácios mais elevados de alunos por professor, indicativos de menor qualidade no ensino público, estão associados a valores medianos de habitação mais reduzidos. Este resultado demonstra que o valor imobiliário no conjunto de daddos (_dataset_) de Boston é moldado em grande parte pelo perfil dos serviços e do ambiente do bairro, confirmando que fatores socioeconómicos e de qualidade urbana superam as características físicas da própria habitação na determinação do preço.

  
## 2. Qualidade dos Dados e Limpeza

### 2.1. Tratamento de Dados em Falta (_Missing Data_)
* **Colunas afetadas:** Nenhuma
* **Estratégia adotada:** A fase de preparação e limpeza de dados foi conduzida com base nas três verificações fundamentais definidas na metodologia CRISP-DM (_Cross-Industry Standard Process for Data Mining_). Em primeiro lugar, a verificação de valores nulos confirmou que nenhuma das 14 variáveis apresenta valores em falta, não sendo necessária qualquer imputação ou remoção de registos. Em segundo lugar, a verificação de duplicados confirmou a ausência de registos repetidos no conjunto de dados (_dataset_). Por fim, a inspeção visual dos valores através das estatísticas descritivas e da visualização das observações não revelou erros de inserção evidentes, como valores impossíveis ou fora dos intervalos esperados para cada variável. 
Conclui-se assim que o conjunto de dados (_dataset_) de Boston se encontra em boas condições de qualidade, estando pronto para avançar diretamente para a fase de modelação sem necessidade de transformações adicionais.

### 2.2. Outliers e Inconsistências
Realizou-se uma análise da distribuição das variáveis para identificar valores atípicos (_outliers_) e possíveis erros de registo, concluindo-se que não existem valores impossíveis ou incoerentes, tais como idades negativas ou preços nulos. Através da visualização dos digramas de caixa de bigodes (_boxplots_) de todas as variáveis do conjunto de dados (_dataset_), identificou-se que as variáveis `CRIM`, `ZN`, `RM`, `B`, `LSTAT` e `MEDV` apresentam valores atípicos (_outliers_). Em contrapartida, as variáveis `INDUS`, `NOX`, `AGE`, `RAD` e `TAX` não apresentam valores atípicos (_outliers_).
Decidimos manter os valores atípicos (_outliers_) identificados, uma vez que não se tratam de falhas de digitação, mas sim reflexos reais de disparidades sociais e económicas. 
Adicionalmente, a variável `RAD` foi removida do conjunto de preditores por apresentar uma correlação de 0.91 com a variável `TAX`, configurando um caso de multicolinearidade com potencial para comprometer a estabilidade do modelo. A opção  por manter `TAX` justifica-se pelo facto de esta apresentar uma correlação mais elevada com a variável alvo `MEDV` (r = -0.47 face a r = -0.38 do `RAD`), sendo por isso mais relevante para a capacidade preditiva.


## 3. Engenharia de Atributos (Feature Engineering)

### 3.1. Transformações Realizadas
* **Encoding:** Não se revelou necessária a aplicação de técnicas de codificação (_encoding_), dado que todas as variáveis do conjunto de dados (_dataset_) se encontram em formato numérico.
* **Escalonamento:** Procedeu-se à normalização (_MinMaxScaler_) das variáveis que não apresentam outliers, de forma a garantir a comparabilidade entre os valores. Por outro lado, aplicou-se a padronização (_StandardScaler_) às variáveis que apresentam valores atípicos (_outliers_), uma vez que esta técnica é menos sensível à presença de valores extremos, de forma a reduzir o seu impacto sem remover informação relevante.
  
### 3.2. Criação de Novos Atributos
* **Índice de Qualidade de Vida (IQV):** Agrega três variáveis `CRIM` , `NOX` e `PTRATIO` numa única métrica. Como as três são de natureza negativa, ou seja, valores altos representam condições desfavoráveis, foi aplicado o inverso (1/variável) a cada uma antes de as somar, garantindo que valores altos do `IQV` correspondam a boas condições de vida. A soma assegura que cada fator contribui de forma independente e equilibrada para o índice final. Após a criação do `IQV`, as variáveis originais foram removidas do conjunto de dados (_dataset_) para evitar redundância na fase de modelação.
* **Índice de Atratividade Habitacional (IAH):** Foi criado para capturar numa única métrica o equilíbrio entre as características físicas da habitação e o contexto socioeconómico e urbano do bairro. A fórmula IAH = RM / (LSTAT × DIS) coloca no numerador o RM e no denominador o `LSTAT` e o `DIS`, garantido que habitações com mais números de quartos em bairros com menor proporção de população de baixo estatuto e mais próximos dos centros de emprego produzem valores `IAH` mais altos, e vice-versa. O `IAH` não partilha variáveis com o `IQV`, assegurando que ambos os índices contribuem com informação complementar para a modelação. Após a sua criação, as variáveis originais `RM`, `LSTAT` e `DIS` foram removidas do conjunto de dados (_dataset_).
 
### 3.3. Escalonamento das Novas Variáveis
Após a criação de novos atributos procedeu-se ao escalonamento das novas variáveis. Dado que tanto `IQV` como o `IAH` apresentam valores atípicos (_outliers_), foi aplicada a padronização (_StandardScaler_) a ambas as variáveis.


## 4. Dicionário de Dados Final (Pós-Processamento)
| Atributo | Tipo Estatístico dos Dados | Intervalo de Valores | Descrição | Método |
| :--- | :--- | :--- |:--- |:--- |
| `IQV` | Numérica Contínua | [1.45, 160.15] | Índice de Qualidade de Vida (Nova variável) | Engenharia de Atributos(criação manual - inversão e soma) |
| `IAH` | Numérica Contínua | [0.03, 2.20] | Índice de Atratividade Habitacional (Nova variável) | Engenharia de Atributos (criação manual - divisão e multiplicação) |
| `B_stand` | Numérica Contínua | [-3.91, 0.44] | B após padronização | StandardScaler |
| `ZN_stand` | Numérica Contínua | [-0.49, 3.80] | ZN após padronização | StandardScaler |
| `INDUS_norm` | Numérica Contínua | [0, 1] | INDUS após normalização | MinMaxScaler |
| `AGE_norm` | Numérica Contínua | [0, 1] | AGE após normalização | MinMaxScaler |
| `TAX_norm` | Numérica Contínua | [0, 1] | TAX após normalização | MinMaxScaler |
| `IQV_stand` | Numérica Contínua | [-0.63, 9.15] | IQV após padronização | StandardScaler |
| `IAH_stand` | Numérica Contínua | [-0.9, 9.2] | IAH após padronização | StandardScaler |


## 5. Conclusões da Fase de Exploração
A fase de análise exploratória e engenharia de atributos foi conduzida de forma estruturada e coerente com o processo CRISP-DM, permitindo transformar o conjunto de dados (_dataset_) de _Boston Housing_ num _input_ sólido e bem fundamentado para a fase de modelação.

**Qualidade dos dados e robustez da base de partida**  
A verificação sistemática de valores nulos e de duplicados confirmou a ausência de qualquer problema de completude ou redundância. Este resultado elimina a necessidade de imputação uma fonte frequente de enviesamento em modelos preditivos quando mal aplicada (Little & Rubin, 2002), permitindo-nos avançar diretamente para a análise exploratória.

**Distribuição da variável alvo `MEDV` e implicações para a modelação**  
A análise não se limitou ao histograma: calculámos as três medidas de tendência central (média = 22.53 > mediana = 21.20, com a moda deslocada para 50.000 dólares) e aplicámos o teste de _Kolmogorov-Smirnov_ (p-valor < 0.05), rejeitando formalmente a hipótese de normalidade de `MEDV`. A discrepância entre as três medidas confirma que a distribuição se afasta claramente da simetria característica de uma distribuição normal, o que poderá influenciar o desempenho do modelo de regressão linear.

**Outliers: decisão de retenção fundamentada**  
A detecção sistemática por IQR identificou `B` (77 outliers), `ZN` (68) e `CRIM` (66) como as variáveis com maior concentração de valores atípicos. A análise dos _scatter plots_ segmentados por _outlier_ revelou padrões interpretáveis: os _outliers_ de `CRIM` concentram-se em valores baixos de `MEDV`, os de `RM` em valores altos, e os de `LSTAT` em valores baixos de `MEDV` mas altos de `LSTAT`. Concluímos que estes padrões não constituem erros de registo, mas sim reflexos de disparidades socioeconómicas reais, pelo que optámos pela sua retenção. A sua remoção eliminaria informação genuína sobre os extremos do mercado imobiliário.

**Multicolinearidade: tratamento cirúrgico**   
A matriz de correlação identificou dois pares críticos: `RAD` e `TAX` com r = 0.91 e `NOX `e `DIS` com r = −0.77. Removemos `RAD` por apresentar uma correlação inferior com `MEDV` (r = −0.38) face a `TAX` (r = −0.47), mantendo a variável com maior poder preditivo. O par `NOX`e `DIS` foi resolvido indirectamente pela incorporação de `NOX` no `IQV` e de `DIS` no `IAH`, eliminando ambas as variáveis originais do conjunto de dados (_dataset_) final. Esta abordagem permitiu tratar a multicolinearidade sem perda de informação, transferindo-a para índices compostos.

**Escalonamento diferenciado e coerente**   
Aplicámos StandardScaler às variáveis com _outliers_ (`CRIM`, `RM`, `LSTAT`, `DIS`, `PTRATIO`, `B`, `ZN`) e MinMaxScaler às restantes (`INDUS`, `NOX`, `AGE`, `RAD`, `TAX`). O _StandardScaler_ centra e escala pela variância, sendo mais robusto à presença de extremos; o _MinMaxScaler_ comprime para [0,1] e é adequado para distribuições mais uniformes (Géron, 2019). Esta distinção evita a aplicação cega de um único método e garante que o escalonamento respeita as características de cada variável.

**Engenharia de atributos (IQV e IAH)**  
Criámos duas novas variáveis para enriquecer a capacidade preditiva do modelo. O `IQV` foi construído por inversão e soma de `CRIM`, `NOX` e `PTRATIO`, garantindo que valores altos do índice correspondem a condições de vida favoráveis. A sua correlação com `MEDV` é moderada (r = 0.31), mas o índice agrega de forma coerente três variáveis com correlações individuais de −0.39 (`CRIM`), −0.43 (`NOX`) e −0.51 (`PTRATIO`), produzindo um indicador interpretável de qualidade urbana. O `IAH = RM / (LSTAT × DIS)` captura o rácio entre a atractividade física da habitação e a penalização socioeconómica e locacional, alinhando-se com a teoria de valor locacional em economia urbana (Alonso, 1964), obtendo uma correlação de 0.65 com `MEDV`. Este valor deve ser interpretado com cautela, dado que o índice incorpora `RM` (r = 0.70) e `LSTAT` (r = −0.74), variáveis que individualmente já apresentavam correlações elevadas com a variável alvo. Ambos os índices apresentam _outliers_ confirmados pelos _boxplots_, pelo que foram padronizados com _StandardScaler_, em coerência com as escolhas anteriores. O conjunto de dados  (_dataset_) final ficou com 9 variáveis preditoras e a variável alvo `MEDV`, exportado para `boston_processed.csv`.


## 6. Referências

Alonso, W. (1964). Location and Land Use: Toward a General Theory of Land Rent. Harvard University Press  
Géron, A. (2019). Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow (2nd ed.). O'Reilly Media  
Little, R. J. A., & Rubin, D. B. (2002). Statistical Analysis with Missing Data (2nd ed.). Wiley  

---
*Data de última atualização: [18/05/2026]* 
