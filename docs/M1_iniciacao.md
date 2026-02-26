# Milestone 1: Iniciação e Definição do Projeto
## 1. Descrição Detalhada do Problema
Este projeto insere-se no setor imobiliário, onde o preço de um imóvel depende de múltiplos fatores tais como, localização, condições socioeconómicas da zona, qualidade do ambiente, acessos, e características físicas (ex.: número de divisões, idade do imóvel, etc.).
Atualmente entidades como agências imobiliárias, bancos (crédito habitação), seguradoras, investidores e plataformas digitais precisam de estimativas consistentes para suportar decisões rápidas e reduzir risco.
## 2. Objetivos SMART
*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível,
Relevante e Temporal):*
1. **Objetivo 1:** Identificar as 3 variáveis que mais influenciam o preço mediano das habitações (MEDV) através de análise de correlação e Feature Importance, e segmentar as 506 habitações em grupos distintos com K-Means validado por um Coeficiente de Silhueta superior a 0.50, até ao Milestone 2.
2. **Objetivo 2:** Comparar o desempenho de algoritmos de regressão na previsão do valor médio das habitações, selecionar o modelo com melhor RMSE e R^2 superior a 0.85, até ao Milestone 3.
### Perguntas de Investigação
1. A percentagem da população de estatuto socioeconómico mais baixo (LSTAT) é o preditor mais forte do valor mediano das habitações (MEDV), superando variáveis físicas como o número de divisões (RM)?
2. As zonas com maior taxa de criminalidade per capita (CRIM) estão associadas a valores de habitação significativamente mais baixos, independentemente de outras variáveis socioeconómicas?
3. Qual é o impacto do rácio aluno/professor (PTRATIO) no preço das habitações, e se bairros com melhores recursos educativos tendem a apresentar habitações mais valorizadas?
4. Quais as habitações consideradas outliers no valor mediano de mercado (MEDV) e que características as diferenciam das restantes? 
## 3. Metodologia de Gestão (PBL)
* **Divisão de Tarefas:**
 * **Diana Figueiredo:** Responsável pela Engenharia de Dados.
 * **Natacha Zhang:** Responsável pela Modelação Estatística.
 * **Sofia Tanganho:** Responsável pela Visualização e Documentação.
* **Ferramentas de Colaboração:** GitHub, Kaggle para partilha de código, reuniões semanais via Discord.
## 4. Análise de Viabilidade dos Dados
* **Disponibilidade:** Os dados encontram-se descarregados e armazenados numa base de dados em formato CSV.
* **Qualidade Inicial:** Todas as colunas apresentam valores preenchidos, ou seja, não existem valores nulos. Verificou-se que não existem observações duplicadas. O dataset apenas possui variáveis numéricas.
* **Ética:** O dataset não contém dados pessoais identificáveis e encontra-se anonimizado, cumprindo o RGPD.
## 5. Descrição das Variáveis 
* **CRIM:** Taxa de criminalidade per capita por cidade
* **ZN:** Proporção de terrenos residenciais com lotes acima de 25.000 pés quadrados
* **INDUS:** Proporção de hectares de comércio não varejista por cidade
* **CHAS:** ??
* **NOX:** Concentração de óxidos de nitrogênio (partes por 10 milhões
* **RM:** Número médio de quartos por residência
* **AGE:** Proporção de unidades ocupadas por proprietários construídas antes de 1940
* **DIS:** Distâncias ponderadas até cinco centros de emprego de Boston
* **RAD:** Índice de acessibilidade a rodovias radiais
* **TAX:** ??
* **PTRATIO:** ??
* **B:** O resultado da equação B=1000(Bk - 0,63)^2, onde Bk é a proporção de negros por cidade
* **LSTAT:** % da população de baixa renda
* **MEDV:** Valor mediano de casas ocupadas pelos proprietários em milhares de dólares [k$]
## 6. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. |
| M3: Modelação | [Data] | Comparação de algoritmos e métricas. |
| M4: Finalização| [Data] | Pitch e Relatório Final. |
---
*Data de última atualização: [DD/MM/AAAA]* 
