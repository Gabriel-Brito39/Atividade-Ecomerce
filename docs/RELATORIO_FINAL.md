# Relatório Final: Previsão de Vendas de E-commerce

**Grupo:** 
Marcos José da Silva - 01184654
José Carlos Sabino Xavier - 01706924
Gabriel Heitor Santos Duarte Brito - 01735986
Shleydson Radackson Henrique da Silva - 01697937
Alexandre Cesar Pereira de Barros Filho- 01684888
**Disciplina:** Machine Learning
**Data:** 25/11/2025

---

## 1. Resumo Executivo
Neste projeto, desenvolvemos um pipeline completo de Machine Learning para prever o volume mensal de vendas de um E-commerce. O objetivo era criar um modelo preditivo capaz de auxiliar na gestão de estoque e planejamento financeiro.

Após identificar e corrigir um problema crítico de **Vazamento de Dados (Data Leakage)** nas primeiras iterações, desenvolvemos um modelo final utilizando **Ridge Regression** otimizado via Grid Search. O modelo final obteve um **R² de 0.2545** (nos dados de validação), representando uma estimativa realista e honesta do comportamento das vendas, livre de overfitting artificial.

## 2. Introdução e Definição do Problema
O problema abordado é de **Regressão**, visando estimar um valor contínuo (`monthly_sales`) com base em características operacionais e de marketing.

**Contexto:**
Prever vendas é desafiador devido à volatilidade do mercado. Um modelo ajustado permite que a empresa evite custos com estoque parado ou perdas por falta de produtos.

## 3. Análise Exploratória de Dados (EDA)
Durante a Etapa 1, exploramos o dataset `ecommerce-sales.csv` e identificamos:
* **Variável Alvo:** As vendas mensais apresentam distribuição assimétrica.
* **Correlações:** Identificamos que variáveis relacionadas a gastos de marketing e tráfego possuem correlação positiva com as vendas.
* **Qualidade dos Dados:** Detectamos a presença de valores nulos e outliers que exigiram tratamento na etapa seguinte.

## 4. Pré-processamento de Dados (A Correção Crítica)
Esta foi a etapa mais importante do projeto. Aplicamos as seguintes técnicas:

1.  **Limpeza Básica:** Remoção de duplicatas e imputação de valores nulos (Mediana para numéricos, Moda para categóricos).
2.  **Tratamento de Outliers:** Aplicação do método IQR (Capping) para suavizar valores extremos sem perder dados.
3.  **🔴 Correção de Data Leakage (Ponto Chave):**
    * Nas primeiras versões, o modelo atingiu um R² artificial de 1.0 (100%).
    * Investigamos e descobrimos que as colunas de identificação (`sale_id`) estavam sendo usadas como features.
    * **Ação:** Removemos todas as colunas de ID antes do treinamento para garantir que o modelo aprendesse padrões reais e não apenas memorizasse identificadores.
4.  **Engenharia:** Normalização com `StandardScaler` e codificação One-Hot para variáveis categóricas.

## 5. Modelagem e Otimização

### 5.1 Modelo Baseline (Regressão Linear)
Estabelecemos um modelo simples de Regressão Linear como linha de base para comparação.
* **Algoritmo:** LinearRegression (Scikit-Learn)
* **Objetivo:** Servir como referência mínima de desempenho.

### 5.2 Modelo Otimizado (Ridge Regression)
Na Etapa 4, buscamos melhorar a generalização usando um modelo linear com regularização (Ridge).
* **Técnica de Otimização:** `GridSearchCV` (Validação Cruzada com 5 folds).
* **Hiperparâmetros Testados:** Variações de `alpha` (força da regularização) e `solver`.
* **Melhor Configuração:** Alpha=100.0, Solver='svd'. A escolha de um Alpha alto indica que o modelo precisou simplificar a equação para lidar com o ruído dos dados.

## 6. Resultados Finais
Abaixo, a comparação de desempenho nos dados de Validação (nunca vistos durante o treino):

| Modelo | R² (Coeficiente de Determinação) | Status |
| :--- | :--- | :--- |
| **Baseline (Linear)** | 0.2388 | Referência |
| **Final (Ridge)** | **0.2545** | **Campeão 🏆** |

**Interpretação:**
O modelo final consegue explicar aproximadamente **25,45%** da variação nas vendas. Embora o número pareça modesto, ele é estatisticamente robusto. A diferença entre o Baseline e o Ridge mostra que a regularização ajudou a estabilizar as previsões.

## 7. Conclusão e Próximos Passos
O projeto foi bem-sucedido em construir um fluxo de trabalho honesto de Data Science, diagnosticando erros graves (leakage) e implementando correções.

**Limitações:**
O R² de ~0.25 sugere que o volume de vendas depende fortemente de fatores externos não presentes neste dataset (como sazonalidade anual, economia macro, ações da concorrência, etc.).

**Próximos Passos:**
1.  **Novos Algoritmos:** Testar modelos de árvore (Random Forest, XGBoost) para capturar relações não-lineares.
2.  **Enriquecimento de Dados:** Adicionar dados de datas comemorativas e feriados.
3.  **Deployment:** Colocar o modelo em produção para monitorar sua performance com dados reais mês a mês.