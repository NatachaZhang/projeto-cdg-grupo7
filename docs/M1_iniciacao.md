# Milestone 1: Iniciação e Definição do Projeto
## 1. Descrição Detalhada do Problema
Este projeto insere-se no setor imobiliário, onde o preço de um imóvel depende de múltiplos fatores tais como, localização, condições socioeconómicas da zona, qualidade do ambiente, acessos, e características físicas (ex.: número de divisões, idade do imóvel, etc.).
Atualmente entidades como agências imobiliárias, bancos (crédito habitação), seguradoras, investidores e plataformas digitais precisam de estimativas consistentes para suportar decisões rápidas e reduzir risco.
## 2. Objetivos SMART
*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível,
Relevante e Temporal):*
1. **Objetivo 1:** Criar um modelo de _Clustering_ para segmentar as habitações em perfis distintos com base nas suas características socioeconómicas, habitacionais e ambientais, validado pelo método do cotovelo e por um Coeficiente de Silhueta (>0.50), até ao Milestone 3.
2. **Objetivo 2:** Construir um modelo de previsão supervisionada do preço médio das habitações (`MEDV`), alcançando um R² superior a 0.80 e um RMSE inferior a 3.500 dólares, até ao Milestone 3.
### Perguntas de Investigação
1. De que forma o modelo de regressão revela qua as condições socioeconómicas do bairro (LSTAT) condicionam o valor habitacional mais do que as características físicas da habitação (RM), que padrão descreve essa relação?
2. O modelo consegue distinguir o efeito direto da criminalidade (CRIM) no valor habitacional do efeito mediado pelo estatuto socioeconómico (LSTAT), e em que medida a criminalidade constitui um preditor autónomo ou reflete as condições do bairro?
3. Como é que o modelo capta a relação entre a qualidade dos recursos educativos (PTRATIO) e o valor das habitações, e esse efeito é uniforme ao longo da distribuição de preços ou concentra-se em determinados segmentos do mercado?
4. O modelo identifica perfis distintos de outliers em MEDV, tanto nos valores extremamente elevados como nos mais baixos, e que combinação de variáveis explica esses casos atípicos, de acordo com o que o modelo aprendeu?
## 3. Metodologia de Gestão (PBL)
* **Divisão de Tarefas:**
 * **Diana Figueiredo:** Responsável pela Engenharia de Dados.
 * **Natacha Zhang:** Responsável pela Modelação Estatística.
 * **Sofia Tanganho:** Responsável pela Visualização e Documentação.
* **Ferramentas de Colaboração:** GitHub, Kaggle para partilha de código, reuniões semanais via Discord.
## 4. Análise de Viabilidade dos Dados
* **Disponibilidade:** Os dados encontram-se descarregados e armazenados numa base de dados em formato CSV.
* **Qualidade Inicial:** Todas as colunas apresentam valores preenchidos, ou seja, não existem valores nulos. Verificou-se que não existem observações duplicadas. O conjunto de dados (_dataset_) apenas possui variáveis numéricas.
* **Ética:** O conjunto de dados (_dataset_) não contém dados pessoais identificáveis e encontra-se anonimizado, cumprindo o RGPD.
## 5. Dicionário de Dados 
| **Variável** | **Tipo de Váriável** | **Valores** | **Descrição** |
| :--- | :--- | :--- | :--- |
|**CRIM**| Numéria Contínua | Valores decimais positivos | Taxa de criminalidade per capita por região |
|**ZN**| Numéria Contínua | Valores decimais entre [0, 100] | Proporção de terrenos residenciais com lotes acima de 25.000 pés quadrados |
|**INDUS**| Numéria Contínua | Valores decimais entre  [0, 27.74] | Proporção em hectares ocupados por zonas industriais que não são comércio por retalho, por região |
|**CHAS**| Categórica Binária | 0 = Não margem do rio; 1 = Margem do rio Charles | Variável binária indicadora da fronteira com o rio Charles |
|**NOX**| Numéria Contínua | Valores decimais entre [0.385, 0.871] | Concentração de óxidos de nitrogênio (partes por 10 milhões) |
|**RM**| Numéria Contínua | Valores decimais entre [3.561, 8.780] | Número médio de quartos por residência |
|**AGE**| Numéria Contínua | Valores decimais entre [2.9, 100] | Proporção de unidades ocupadas por proprietários com imovéis construídos antes de 1940 |
|**DIS**| Numéria Contínua | Valores decimais entre [1.130, 12.127] | Distâncias ponderadas até cinco centros de emprego de Boston |
|**RAD**| Numérica Discreta | Valores inteiros entre [1, 24] | Índice de acessibilidade a rodovias radiais |
|**TAX**| Numérica Discreta | Valores inteiros entre [187, 711] | Taxa de imposto predial integral por cada 10.000 dólares |
|**PTRATIO**| Numéria Contínua | Valores decimais entre [12.6, 22.0] | Proporção entre o número de alunos e professores por cidade |
|**B**| Numéria Contínua | Valores decimais entre [0.32, 396.90] | O resultado da equação B=1000(Bk - 0,63)^2, onde Bk é a proporção de negros por cidade |
|**LSTAT**| Numéria Contínua | Valores decimais entre [1.73, 37.97] | Percentagem da população com baixo rendimento |
|**MEDV**| Numéria Contínua | Valores decimais entre [5.0, 50.0] | Valor mediano de casas ocupadas pelos proprietários em milhares de dólares [k$] |
## 6. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. |
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. |
| M4: Finalização| [Data] | Pitch e Relatório Final. |  
## 7. Referências
* S. Puneeth, Md. Ammaar Quadri, M. Sahithi, Mohd. Arbas, & P.S. Jyothi. (2025). PREDICTING HOME PRICES: A BEGINNER’S JOURNEY WITH  REGRESSION ANALYSIS USING THE BOSTON HOUSING DATASET. Journal of Science Engineering Technology and Management Science , 02(06). https://www.jsetms.com/admin/uploads/Ugtw54.pdf
---
*Data de última atualização: [11/03/2026]* 
