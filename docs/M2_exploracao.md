# Milestone 2: Análise Exploratória e Engenharia de Atributos
> **Nota de Revisão:** relembrar que o conjunto de dados (_dataset_) já foi identificado e descrito no ficheiro `docs/M1_iniciacao.md`. Caso precise de consultar o significado original das variáveis,
deve consultar essa Milestone.
## 1. Análise Exploratória de Dados (EDA)
### 1.1. Distribuição da Variável Alvo
A variável alvo `MEDV` apresenta uma distribuição com assimetria positiva, onde a maioria das habitações se concentra na faixa dos 20 a 25 mil dólares, existindo um conjunto reduzido de observações com valores significativamente elevados que originam uma cauda mais extensa no lado direito da distribuição.
Relativamente ao equilíbrio, a variável não pode ser considerada totalmente equilibrada. O histograma revela uma clara concentração de observações nos valores intermédios, com menor frequência nos extremos. O diagrama de extermos e quartis (boxplot) confirma ainda a presença de vários valores atípicos (_outliers_) no limite superior, visíveis como pontos acima dos 40 mil dólares.
No que diz respeito à normalidade, a distribuição de `MEDV` não segue uma distribuição normal perfeita. Embora apresente um pico central próximo dos 20 mil dólares, a cauda direita alongada afasta-a da simetria característica de uma distribuição normal, o que poderá influenciar o desempenho do modelo de regressão linear, uma vez que este pressupõe normalidade nos resíduos para garantir previsões fiáveis.

### 1.2. Correlações Relevantes

* **Atributo `LSTAT` vs. Alvo (`MEDV`):** A análise bivariada revela que a variável `LSTAT` apresenta a correlação negativa mais forte com a variável alvo `MEDV` (r = -0.74), evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_), onde se observa claramente que à medida que a % de população de baixa renda aumenta, o valor mediano das habitações diminui de forma consistente, confirmando que o perfil socioeconómico do bairro é o preditor mais determinante do preço das habitações no dataset de Boston. Estes resultados respondem à Pergunta de Investigação 1, confirmando que o `LSTAT` supera variáveis físicas como o número de divisões (`RM`, r = 0.70), provando que o contexto socioeconómico do bairro tem maior influência no preço das habitações do que as características físicas da própria casa.
* **Atributo `RM` vs. Alvo (`MEDV`):** A variável `RM` apresenta a correlação positiva mais forte com o `MEDV` (r = 0.70), evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_), onde se observa claramente uma tendência linear positiva, quanto maior o número médio de quartos numa habitação, maior o seu valor mediano. Estes resultados reforçam a resposta à Pergunta de Investigação 1, confirmando que embora o RM seja a característica física com maior influência no preço, é ainda assim superado pelo fator socioeconómico do bairro (`LSTAT`, r = -0.74), provando que o contexto do bairro pesa mais no valor das habitações do que o tamanho da própria casa.
* **Atributo `PTRATIO` vs. Alvo (`MEDV`):** A variável `PTRATIO` surge como o terceiro preditor com maior relação com a variável alvo `MEDV`, apresentando uma correlação negativa moderada de r = 0.51, evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_). Bairros com rácios mais elevados de alunos por professor, indicativos de menor qualidade no ensino público, estão associados a valores medianos de habitação mais reduzidos. Este resultado demonstra que o valor imobiliário no conjunto de daddos (_dataset_) de Boston é moldado em grande parte pelo perfil dos serviços e do ambiente do bairro, confirmando que fatores socioeconómicos e de qualidade urbana superam as características físicas da própria habitação na determinação do preço.
## 2. Qualidade dos Dados e Limpeza
### 2.1. Tratamento de Dados em Falta (_Missing Data_)
* **Colunas afetadas:** Nenhuma
* **Estratégia adotada:** A fase de preparação e limpeza de dados foi conduzida com base nas três verificações fundamentais definidas na metodologia CRISP-DM (_Cross-Industry Standard Process for Data Mining_). Em primeiro lugar, a verificação de valores nulos através do comando "df.isnull().sum()" confirmou que nenhuma das 14 variáveis apresenta valores em falta, não sendo necessária qualquer imputação ou remoção de registos. Em segundo lugar, a verificação de duplicados através do comando "df.duplicated().sum()" confirmou a ausência de registos repetidos no dataset. Por fim, a inspeção visual dos valores através do "df.describe()" e "df.head()" não revelou erros de inserção evidentes, como valores impossíveis ou fora dos intervalos esperados para cada variável. Conclui-se assim que o conjunto de dados (_dataset_) de Boston se encontra em boas condições de qualidade, estando pronto para avançar diretamente para a fase de modelação sem necessidade de transformações adicionais.
### 2.2. Outliers e Inconsistências
Realizou-se uma análise da distribuição das variáveis para identificar valores atípicos (_outliers_) e possíveis erros de registo, concluindo-se que não existem valores impossíveis ou incoerentes, tais como idades negativas ou preços nulos. Através da visualização dos boxplots de todas as variáveis do dataset, identificou-se que as variáveis `CRIM`, `ZN`, `RM`, `B`, `LSTAT` e `MEDV` apresentam valores atípicos (_outliers_). Em contrapartida, as variáveis `INDUS`, `NOX`, `AGE`, `RAD` e `TAX` não apresentam valores atípicos (_outliers_).
Decidimos manter os valores atípicos (_outliers_) identificados, uma vez que não se tratam de falhas de digitação, mas sim reflexos reais de disparidades sociais e económicas. 
## 3. Engenharia de Atributos (Feature Engineering)
### 3.1. Transformações Realizadas
* **Encoding:** Não se revelou necessária a aplicação de técnicas de codificação (_encoding_), dado que todas as variáveis do conjunto de dados (_dataset_) se encontram em formato numérico.
* **Escalonamento:** Procedeu-se à normalização (_MinMaxScaler_) das variáveis que não apresentam outliers, de forma a garantir a comparabilidade entre os valores. Por outro lado, aplicou-se a padronização (_StandardScaler_) às variáveis que apresentam valores atípicos (_outliers_), uma vez que esta técnica é menos sensível à presença de valores extremos, de forma a reduzir o seu impacto sem remover informação relevante
### 3.2. Criação de Novos Atributos
* **Índice de Qualidade de Vida (IQV):** agrega três variáveis `CRIM` , `NOX` e `PTRATIO` numa única métrica. Como as três são de natureza negativa, ou seja, valores altos representam condições desfavoráveis, foi aplicado o inverso (1/variável) a cada uma antes de as somar, garantindo que valores altos do `IQV` correspondam a boas condições de vida. A soma assegura que cada fator contribui de forma independente e equilibrada para o índice final. Após a criação do `IQV`, as variáveis originais foram removidas do conjunto de dados (_dataset_) para evitar redundância na fase de modelação.
* **Índice de Atratividade Habitacional (IAH):** foi criado para capturar numa única métrica o equilíbrio entre as características físicas da habitação e o contexto socioeconómico e urbano do bairro. A fórmula IAH = RM / (LSTAT × DIS) coloca no numerador o RM e no denominador o `LSTAT` e o `DIS`, garantindo que habitações maiores em bairros ricos e bem localizados produzam valores altos e vice-versa. O `IAH` não partilha variáveis com o `IQV`, assegurando que ambos os índices contribuem com informação complementar para a modelação. Após a sua criação, as variáveis originais `RM`, `LSTAT` e `DIS` foram removidas do conjunto de dados (_dataset_).
## 4. Dicionário de Dados Final (Pós-Processamento)
*Listagem final das variáveis que serão entregues ao modelo na Fase 3.*
| Atributo | Tipo Estatístico dos Dados | Intrevalo de Valores | Descrição | Método |
| :--- | :--- | :--- |:--- |:--- |
| `IQV` | Numérica Contínua | [4.45, 160.15] | Índice de Qualidade de Vida (Nova variável) | Engenharia de Atributos(criação manual - inversão e soma) |
| `IAH` | Numérica Contínua | [0.03, 2.20] | Índice de Atratividade Habitacional (Nova variável) | Engenharia de Atributos (criação manual - divisão e multiplicação) |
| `B_stand` | Numérica Contínua | [] | B após padronização | StandardScaler |
| `ZN_stand` | Numérica Contínua | [] | ZN após padronização | StandardScaler |
| `INDUS_norm` | Numérica Contínua | [0, 1] | INDUS após normalização | MinMaxScaler |
| `AGE_norm` | Numérica Contínua | [0, 1] | AGE após normalização | MinMaxScaler |
| `TAX_norm` | Numérica Contínua | [0, 1] | TAX após normalização | MinMaxScaler |
| `IQV_stand` | Numérica Contínua | [] | IQV após padronização | StandardScaler |
| `IAH_stand` | Numérica Contínua | [] | IAH após padronização | StandardScaler |

## 5. Conclusões da Fase de Exploração

A análise exploratória revelou que o preço das habitações (`MEDV`) é fortemente influenciado por fatores socioeconómicos, destacando-se a variável `LSTAT` como o principal preditor. Verificou-se também que o conjunto de dados apresenta boa qualidade, sem valores em falta, duplicados ou erros de inserção. Os outliers identificados foram considerados plausíveis e tratados através de técnicas de escalonamento. Conclui-se que os dados são adequados e suficientes para avançar para a fase de modelação.  

---
*Data de última atualização: [03/04/2026]* 
