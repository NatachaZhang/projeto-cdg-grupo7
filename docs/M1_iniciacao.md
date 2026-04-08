# Milestone 1: Iniciação e Definição do Projeto
## 1. Descrição Detalhada do Problema
Este projeto insere-se no setor imobiliário, onde o preço de um imóvel depende de múltiplos fatores tais como, localização, condições socioeconómicas da zona, qualidade do ambiente, acessos, e características físicas (ex.: número de divisões, idade do imóvel, etc.).
Atualmente entidades como agências imobiliárias, bancos (crédito habitação), seguradoras, investidores e plataformas digitais precisam de estimativas consistentes para suportar decisões rápidas e reduzir risco.
## 2. Objetivos SMART
*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível,
Relevante e Temporal):*
1. **Objetivo 1:** Identificar as 3 variáveis que mais influenciam o preço mediano das habitações (MEDV) através de análise de correlação e variáveis importantes (_Feature Importance_), e segmentar as 506 habitações em grupos distintos com _K-Means_ validado por um Coeficiente de Silhueta superior a 0.50, até ao Milestone 2.
2. **Objetivo 2:** Comparar o desempenho de algoritmos de regressão na previsão do valor médio das habitações, selecionar o modelo com melhor RMSE e R² superior a 0.85, até ao Milestone 3.
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
## 5. Descrição das Variáveis 
* **CRIM:** Taxa de criminalidade per capita por região
* **ZN:** Proporção de terrenos residenciais com lotes acima de 25.000 pés quadrados
* **INDUS:** Proporção de hectares ocupados por zonas industriais que não são comércio por retalho por região
* **CHAS:** Variável binária indicadora da fronteira com o rio Charles
* **NOX:** Concentração de óxidos de nitrogênio (partes por 10 milhões)
* **RM:** Número médio de quartos por residência
* **AGE:** Proporção de unidades ocupadas por proprietários construídas antes de 1940
* **DIS:** Distâncias ponderadas até cinco centros de emprego de Boston
* **RAD:** Índice de acessibilidade a rodovias radiais
* **TAX:** Taxa de imposto predial integral por cada 10.000 dólares
* **PTRATIO:** Proporção entre o número de alunos e professores por cidade
* **B:** O resultado da equação B=1000(Bk - 0,63)^2, onde Bk é a proporção de negros por cidade
* **LSTAT:** Percentagem da população com baixo rendimento
* **MEDV:** Valor mediano de casas ocupadas pelos proprietários em milhares de dólares [k$]
## 6. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. |
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. |
| M4: Finalização| [Data] | Pitch e Relatório Final. |
---
*Data de última atualização: [11/03/2026]* 
