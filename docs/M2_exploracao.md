# Milestone 2: Análise Exploratória e Engenharia de Atributos
> **Nota de Revisão:** Este documento pressupõe que o conjunto de dados (_dataset_) já foi identificado e descrito no
ficheiro `docs/M1_iniciacao.md`. Caso precise de consultar o significado original das variáveis,
deve consultar essa Milestone.
## 1. Análise Exploratória de Dados (EDA)
### 1.1. Distribuição da Variável Alvo
*Descrevam como se comporta a variável que querem prever. Está equilibrada? Segue uma distribuição
normal?*
> **Factos importantes:** A nossa variável alvo 'MEDV' não segue uma distribuição normal
### 1.2. Correlações Relevantes
*Quais as variáveis que têm maior relação com o problema? Incluam referências a gráficos que
geraram no Kaggle.*
* **Atributo LSTAT vs. Alvo (MEDV):** A análise bivariada revela que a variável LSTAT apresenta a correlação negativa mais forte com a variável alvo MEDV (r = -0.74), evidenciada tanto na matriz de correlação (_heatmap_) como no gráfico de dispersão (_scatter plot_), onde se observa claramente que à medida que a % de população de baixa renda aumenta, o valor mediano das habitações diminui de forma consistente, confirmando que o perfil socioeconómico do bairro é o preditor mais determinante do preço das habitações no dataset de Boston. Estes resultados respondem à Pergunta de Investigação 1, confirmando que o LSTAT supera variáveis físicas como o número de divisões (RM, r = 0.70), provando que o contexto socioeconómico do bairro tem maior influência no preço das habitações do que as características físicas da própria casa."
* **Atributo RM vs. Alvo (MEDV):** A variável RM apresenta a correlação positiva mais forte com o MEDV (r = 0.70), evidenciada tanto no heatmap de correlação como no scatter plot, onde se observa claramente uma tendência linear positiva, quanto maior o número médio de quartos numa habitação, maior o seu valor mediano. Estes resultados reforçam a resposta à Pergunta de Investigação 1, confirmando que embora o RM seja a característica física com maior influência no preço, é ainda assim superado pelo fator socioeconómico do bairro (LSTAT, r = -0.74), provando que o contexto do bairro pesa mais no valor das habitações do que o tamanho da própria casa.
* **Atributo C vs. Alvo (MEDV):**
## 2. Qualidade dos Dados e Limpeza
### 2.1. Tratamento de Dados em Falta (Missing Data)
* **Colunas afetadas:** Nenhuma
* **Estratégia adotada:** A fase de preparação e limpeza de dados foi conduzida com base nas três verificações fundamentais definidas na metodologia CRISP-DM (_Cross-Industry Standard Process for Data Mining_). Em primeiro lugar, a verificação de valores nulos através do comando "df.isnull().sum()" confirmou que nenhuma das 14 variáveis apresenta valores em falta, não sendo necessária qualquer imputação ou remoção de registos. Em segundo lugar, a verificação de duplicados através do comando "df.duplicated().sum()" confirmou a ausência de registos repetidos no dataset. Por fim, a inspeção visual dos valores através do "df.describe()" e "df.head()" não revelou erros de inserção evidentes, como valores impossíveis ou fora dos intervalos esperados para cada variável. Conclui-se assim que o dataset de Boston se encontra em boas condições de qualidade, estando pronto para avançar diretamente para a fase de modelação sem necessidade de transformações adicionais.
### 2.2. Outliers e Inconsistências
Realizou-se uma análise da distribuição das variáveis para identificar valores atípicos (_outliers_) e possíveis erros de registo, concluindo-se que não existem valores impossíveis ou incoerentes, tais como idades negativas ou preços nulos. Através da visualização dos boxplots de todas as variáveis do dataset, identificou-se que as variáveis CRIM, ZN,RM,B,LSTAT e MEDV apresentam outliers. Em contrapartida, as variáveis INDUS,NOX,AGE,RAD e TAX não apresentam qualquer outlier.
Decidimos manter os valores atípicos (_outliers_) identificados, uma vez que não se tratam de falhas de digitação, mas sim reflexos reais de disparidades sociais e económicas. 
## 3. Engenharia de Atributos (Feature Engineering)
### 3.1. Transformações Realizadas
* **Encoding:** Não se revelou necessária a aplicação de técnicas de codificação (_encoding_), dado que todas as variáveis do conjunto de dados (_dataset_) se encontram em formato numérico.
* **Escalonamento:** Procedeu-se à normalização (_Min-Max_) das variáveis que não apresentam outliers, de forma a garantir a comparabilidade entre os valores. Por outro lado, aplicou-se a standardização(_Z-score_) às variáveis que apresentam outliers, uma vez que esta técnica é menos sensível à presença de valores extremos, de forma a reduzir o seu impacto sem remover informação relevante
### 3.2. Criação de Novos Atributos
* **Índice de Qualidade de Vida (IQV):** agrega três variáveis CRIM , NOX e PTRATIO numa única métrica. Como as três são de natureza negativa, ou seja, valores altos representam condições desfavoráveis, foi aplicado o inverso (1/variável) a cada uma antes de as somar, garantindo que valores altos do IQV correspondam a boas condições de vida. A soma assegura que cada fator contribui de forma independente e equilibrada para o índice final. Após a criação do IQV, as variáveis originais foram removidas do dataset para evitar redundância na fase de modelação.
* **Outra variável:**
## 4. Dicionário de Dados Final (Pós-Processamento)
*Listagem final das variáveis que serão entregues ao modelo na Fase 3.*
| Atributo | Tipo | Descrição | Método |
| :--- | :--- | :--- |:--- |
| `IQV` | Float | Índice de Qualidade de Vida (Nova variável) | Feature Engineering (criação manual — inversão e soma) |
| `IAH` | Float | Índice de Atratividade Habitacional (Nova variável) | Feature Engineering (divisão e multiplicação) |
| `CRIM_stand` | Float | CRIM após padronização | StandardScaler |
| `RM_stand` | Float | RM após padronização | StandardScaler |
| `LSTAT_stand` | Float | LSTAT após padronização | StandardScaler |
| `DIS_stand` | Float | DIS após padronização | StandardScaler |
| `PTRATIO_stand` | Float | PTRATIO após padronização | StandardScaler |
| `B_stand` | Float | B após padronização | StandardScaler |
| `ZN_stand` | Float | ZN após padronização | StandardScaler |
| `INDUS_norm` | Float | INDUS após normalização | MinMaxScaler |
| `NOX_norm` | Float | NOX após normalização | MinMaxScaler |
| `AGE_norm` | Float | AGE após normalização | MinMaxScaler |
| `RAD_norm` | Int | RAD após normalização | MinMaxScaler |
| `TAX_norm` | Float | TAX após normalização | MinMaxScaler |

## 5. Conclusões da Fase de Exploração

A análise exploratória revelou que o preço das habitações (MEDV) é fortemente influenciado por fatores socioeconómicos, destacando-se a variável LSTAT como o principal preditor. Verificou-se também que o conjunto de dados apresenta boa qualidade, sem valores em falta, duplicados ou erros de inserção. Os outliers identificados foram considerados plausíveis e tratados através de técnicas de escalonamento. Conclui-se que os dados são adequados e suficientes para avançar para a fase de modelação.  

---
*Data de última atualização: [24/03/2026]* 
