# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema

A previsão do valor mediano das habitações na área metropolitana de Boston constitui um problema de regressão supervisionada, no qual se pretende estimar uma variável contínua (`MEDV`) com base num conjunto de variáveis explicativas de natureza diversa. Estas variáveis incluem indicadores socioeconómicos (como a taxa de criminalidade ou o nível de rendimento), características estruturais das habitações (como o número médio de divisões) e fatores ambientais (como a proximidade a infraestruturas ou qualidade do ar), cuja relação com o preço não é linear nem uniforme. Um dos principais desafios deste problema reside na complexidade das relações entre as variáveis independentes e a variável alvo.
Em particular, podem existir fenómenos como multicolinearidade entre variáveis explicativas, heterogeneidade dos dados e presença de outliers, que dificultam a identificação de padrões robustos e comprometem o desempenho dos modelos preditivos. Adicionalmente, a distribuição da variável `MEDV` pode apresentar assimetrias ou limites (como valores máximos censurados), o que exige cuidados adicionais na escolha e avaliação dos modelos.Outro aspeto relevante prende-se com a necessidade de equilibrar capacidade preditiva e interpretabilidade. Enquanto modelos mais complexos podem oferecer maior precisão, nem sempre permitem compreender claramente o contributo de cada variável para o preço final, o que é fundamental no contexto imobiliário, onde a transparência é valorizada pelos diferentes intervenientes.
Assim, o problema consiste não apenas em prever com exatidão o valor mediano das habitações, mas também em compreender quais os fatores que mais influenciam esse valor e de que forma o fazem. Para tal, torna-se necessário aplicar e comparar diferentes técnicas de modelação, avaliando o seu desempenho através de métricas adequadas e garantindo a robustez dos resultados obtidos.

## 2. Objetivos SMART
*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível,
Relevante e Temporal):*
1. **Objetivo 1:** Construir um modelo de previsão supervisionada do preço médio das habitações (`MEDV`), alcançando um R² superior a 0.80 e um RMSE inferior a 3.500 dólares, até ao Milestone 3.
2. **Objetivo 2:** Criar um modelo de _Clustering_ para segmentar as habitações em perfis distintos com base nas suas características socioeconómicas, habitacionais e ambientais, validado pelo método do cotovelo e por um Coeficiente de Silhueta (>0.50), até ao Milestone 3.
### Perguntas de Investigação

As perguntas de investigação estruturam o enquadramento científico do estudo, orientando a análise empírica dos dados com o objetivo de identificar os principais determinantes do preço mediano das habitações (`MEDV`), avaliar a sua relevância estatística e preditiva e verificar a capacidade dos modelos desenvolvidos em captar os padrões que explicam as variações no valor habitacional.

1. Que perfis distintos de habitações identifica o modelo de clustering, e de que forma diferem entre si nas variáveis socioeconómicas, habitacionais e ambientais?
2. Qual é a relação entre o estatuto socioeconómico do bairro (`LSTAT`) e o preço mediano das habitações (`MEDV`) no modelo de regressão?
3. A taxa de criminalidade (`CRIM`) é um preditor relevante do preço das habitações (`MEDV`) quando considerada em conjunto com outras variáveis do bairro?
4. Que variáveis caracterizam as habitações com os preços mais elevados e mais baixos identificadas pelo modelo?
   
## 3. Metodologia de Gestão (PBL)
* **Divisão de Tarefas:**
 * **Diana Figueiredo:** Responsável pela Engenharia de Dados.
 * **Natacha Zhang:** Responsável pela Modelação Estatística.
 * **Sofia Tanganho:** Responsável pela Visualização e Documentação.
* **Ferramentas de Colaboração:** GitHub, Kaggle para partilha de código, reuniões semanais via Discord.
  
## 4. Análise de Viabilidade dos Dados
* **Disponibilidade:** O conjunto de dados encontra-se armazenado em formato CSV no [Kaggle](https://www.kaggle.com/datasets/fedesoriano/the-boston-houseprice-data). Os dados estão acessíveis e prontos para utilização em ambiente de análise. 
* **Características iniciais:** O conjunto de dados (_dataset_) é composto por 506 observações e 14 variáveis, incluindo a variável preditiva. Todas as variáveis são de natureza numérica, o que facilita a aplicação de métodos estatísticos e de aprendizagem automática (_Machine Learning_).
* **Qualidade Inicial:** Todas as colunas apresentam valores preenchidos, não se verificou a existência de valores em falta. Foi igualmente confirmada a ausência de observações duplicadas. A estrutura dos dados encontra-se organizada em formato tabular, pois cada linha correspondente a uma observação e cada coluna a uma variável.
* **Ética:** O conjunto de dados (_dataset_) não contém dados pessoais identificáveis e encontra-se anonimizado, cumprindo o RGPD.
  
## 5. Dicionário de Dados 
| **Variável** | **Tipo estatístico de dados** | **Valores** | **Descrição** |
| :--- | :--- | :--- | :--- |
|**`CRIM`**| Numéria Contínua | Valores decimais entre [0.006320, 88.9762] | Taxa de criminalidade per capita por região |
|**`ZN`**| Numéria Contínua | Valores decimais entre [0, 100] | Proporção de terrenos residenciais com lotes acima de 25.000 pés quadrados |
|**`INDUS`**| Numéria Contínua | Valores decimais entre  [0.46, 27.74] | Proporção em hectares ocupados por zonas industriais que não são comércio por retalho, por região |
|**`CHAS`**| Categórica Binária | 0 = Não margem do rio; 1 = Margem do rio Charles | Variável binária indicadora da fronteira com o rio Charles |
|**`NOX`**| Numéria Contínua | Valores decimais entre [0.385, 0.871] | Concentração de óxidos de nitrogênio (partes por 10 milhões) |
|**`RM`**| Numéria Contínua | Valores decimais entre [3.561, 8.780] | Número médio de quartos por residência |
|**`AGE`**| Numéria Contínua | Valores decimais entre [2.9, 100] | Proporção de unidades ocupadas por proprietários com imovéis construídos antes de 1940 |
|**`DIS`**| Numéria Contínua | Valores decimais entre [1.1296, 12.1265] | Distâncias ponderadas até cinco centros de emprego de Boston |
|**`RAD`**| Numérica Discreta | Valores inteiros entre [1, 24] | Índice de acessibilidade a rodovias radiais |
|**`TAX`**| Numérica Discreta | Valores inteiros entre [187, 711] | Taxa de imposto predial integral por cada 10.000 dólares |
|**`PTRATIO`**| Numéria Contínua | Valores decimais entre [12.6, 22.0] | Proporção entre o número de alunos e professores por cidade |
|**`B`**| Numéria Contínua | Valores decimais entre [0.32, 396.90] | O resultado da equação B=1000(Bk - 0,63)^2, onde Bk é a proporção de negros por cidade |
|**`LSTAT`**| Numéria Contínua | Valores decimais entre [1.73, 37.97] | Percentagem da população com baixo rendimento |
|**`MEDV`**| Numéria Contínua | Valores decimais entre [5.0, 50.0] | Valor mediano de casas ocupadas pelos proprietários em milhares de dólares [k$] |
## 6. Síntese da Análise Inicial
A fase da compreensão dos dados (_Data Understanding_) do processo CRISP-DM (_Cross-Industry Standard Process for Data Mining_) teve como objetivo caracterizar formalmente o conjunto de dados (_dataset_), avaliar a sua qualidade e integridade, e identificar propriedades relevantes para as fases subsequentes de preparação dos dados e modelação.  
O dataset é composto por 506 observações e 14 variáveis, todas de natureza numérica, o que elimina a necessidade de codificação de variáveis categóricas e facilita a aplicação direta de algoritmos de aprendizagem automática (_Machine Learning_). Cada observação corresponde a um imóvel da região de Boston, descrita por um conjunto de características socioeconómicas, habitacionais e ambientais, e pela variável alvo (`MEDV`) , que representa o valor mediano das habitações em milhares de dólares.  
A verificação da integridade do conjunto de dados (_dataset_) confirmou a ausência total de valores em falta em todas as variáveis, bem como a inexistência de observações duplicadas. Estas propriedades garantem a completude e unicidade do dataset e eliminam a necessidade de recorrer a técnicas de imputação, reduzindo o risco de introdução de viés no processo de modelação.  
A análise estatística revelou diferenças consideráveis na escala e dispersão das variáveis. A título de exemplo, a taxa de criminalidade (`CRIM`) varia entre valores próximos de zero e cerca de 89, enquanto a concentração de óxidos de nitrogênio (`NOX`) se concentra num intervalo estreito entre 0,385 e 0,871. Esta heterogeneidade de escalas é relevante para a fase de modelação, uma vez que algoritmos sensíveis à magnitude das variáveis, como _K-Means_ e regressão com regularização, requerem normalização ou padronização prévia dos dados. Todas as variáveis apresentam variabilidade suficiente para suportar o processo de aprendizagem.
No que respeita à variável alvo, (`MEDV`) apresenta uma distribuição com valores entre 5 e 50 milhares de dólares,a existência de um limite superior fixado nos 50 milhares dólares sugere uma possível censura dos dados nos valores mais elevados.
Em síntese, o conjunto de dados (_dataset_) apresenta uma dimensão razoável para a análise e encontra-se pronto para as fases de preparação e modelação, sem necessidade de intervenções corretivas de fundo. As principais implicações identificadas nesta fase, nomeadamente a heterogeneidade de escalas e a possível censura da variável-alvo, serão devidamente consideradas nas etapas seguintes do processo CRISP-DM (_Cross-Industry Standard Process for Data Mining_).
## 7. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. |
| M3: Modelação | 23/04/2026 | Comparação de algoritmos e métricas. |
| M4: Finalização| [Data] | Pitch e Relatório Final. |  

## 8. Referências
* S. Puneeth, Md. Ammaar Quadri, M. Sahithi, Mohd. Arbas, & P.S. Jyothi. (2025). PREDICTING HOME PRICES: A BEGINNER’S JOURNEY WITH  REGRESSION ANALYSIS USING THE BOSTON HOUSING DATASET. Journal of Science Engineering Technology and Management Science , 02(06). https://www.jsetms.com/admin/uploads/Ugtw54.pdf
* Wirth, R., & Hipp, J. (n.d.). CRISP-DM: Towards a Standard Process Model for Data Mining. Retrieved April 22, 2026, from https://www.cs.unibo.it/~danilo.montesi/CBD/Beatriz/10.1.1.198.5133.pdf
---
*Data de última atualização: [22/04/2026]* 
