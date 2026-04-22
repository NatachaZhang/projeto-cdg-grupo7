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
* **Disponibilidade:** O conjunto de dados encontra-se armazenado em formato CSV no kaggle. Os dados estão acessíveis e prontos para utilização em ambiente de análise. 
* **Características iniciais:** O conjunto de dados é composto por 560 observações e 14 variáveis, incluindo a variável preditiva. Todas as variáveis são de natureza numérica, o que facilita a aplicação de métodos estatísticos e de aprendizagem automática (_Machine Learning_).
* **Qualidade Inicial:** Todas as colunas apresentam valores preenchidos, não se verificou a existência de valores em falta. Foi igualmente confirmada a ausência de observações duplicadas. A estrutura dos dados encontra-se organizada em formato tabular, pois cada linha correspondente a uma observação e cada coluna a uma variável.
* **Ética:** O conjunto de dados (_dataset_) não contém dados pessoais identificáveis e encontra-se anonimizado, cumprindo o RGPD.
  
## 5. Dicionário de Dados 
| **Variável** | **Tipo de Váriável** | **Valores** | **Descrição** |
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
