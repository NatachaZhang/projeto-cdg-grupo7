# Milestone 2: Análise Exploratória e Engenharia de Atributos
> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no
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
* **Atributo LSTAT vs. Alvo (MEDV):** A análise bivariada revela que a variável LSTAT apresenta a correlação negativa mais forte com a variável alvo MEDV (r = -0.74), evidenciada tanto no heatmap de correlação como no scatter plot, onde se observa claramente que à medida que a % de população de baixa renda aumenta, o valor mediano das habitações diminui de forma consistente, confirmando que o perfil socioeconómico do bairro é o preditor mais determinante do preço das habitações no dataset de Boston. Estes resultados respondem à Pergunta de Investigação 1, confirmando que o LSTAT supera variáveis físicas como o número de divisões (RM, r = 0.70), provando que o contexto socioeconómico do bairro tem maior influência no preço das habitações do que as características físicas da própria casa."
* **Atributo RM vs. Alvo (MEDV):**
* **Atributo C vs. Alvo (MEDV):**
## 2. Qualidade dos Dados e Limpeza
### 2.1. Tratamento de Dados em Falta (Missing Data)
* **Colunas afetadas:** [Lista de colunas]
* **Estratégia adotada:** (Ex: "Substituímos os nulos da coluna 'Salário' pela mediana para
evitar o impacto de outliers.")
### 2.2. Outliers e Inconsistências
*Descrevam se encontraram valores impossíveis (ex: idade = 200) e como os resolveram.*
## 3. Engenharia de Atributos (Feature Engineering)
### 3.1. Transformações Realizadas
* **Encoding:** (Ex: "Convertemos a variável 'Género' em numérica usando One-Hot Encoding.")
* **Escalonamento:** (Ex: "Aplicámos o StandardScaler nas variáveis numéricas para que todas
fiquem na mesma escala.")
### 3.2. Criação de Novos Atributos
*Descrevam as variáveis que criaram para ajudar o modelo.*
* **Nova Variável [Nome]:** (Ex: "Criámos a 'Tenure_Per_Year' que divide o tempo de contrato
pela idade do cliente.")
## 4. Dicionário de Dados Final (Pós-Processamento)
*Listagem final das variáveis que serão entregues ao modelo na Fase 3.*
| Atributo | Tipo | Descrição |
| :--- | :--- | :--- |
| `cliente_id` | ID | Removido (não preditivo) |
| `idade_norm` | Float | Idade após normalização |
| `is_premium` | Binary | 1 para clientes com plano superior |
## 5. Conclusões da Fase de Exploração
*O que aprenderam sobre o dataset que não sabiam no final do Milestone 1? Os dados são suficientes
para avançar para a modelação?*
---
*Data de última atualização: [DD/MM/AAAA]* 
