# 📊 Relatório da Etapa 3: Modelo Baseline

## 1. Resumo de Desempenho
O modelo baseline de Regressão Linear foi treinado e avaliado na base de validação (20% dos dados).

### Métricas Principais (Validação)
* **R² (R-Quadrado):** 0.3945
  > Interpretação: O modelo explica cerca de **39.5%** da variação das vendas.
* **MAE (Erro Médio):** 0.62
* **RMSE (Erro Quadrático):** 0.80

## 2. Análise de Overfitting
Comparação de estabilidade entre Treino e Validação:
* **R² Treino:** 0.4537
* **R² Validação:** 0.3945
* **Diferença:** 0.0592

**Conclusão:** A diferença é pequena (< 0.10), indicando que o modelo **NÃO sofreu overfitting**, embora sofra de underfitting (simples demais para os dados).

## 3. Diagnóstico Crítico (Storytelling)
Apesar do R² de 0.39, a análise de importância das features revelou um problema grave de qualidade nos dados que limitou o desempenho.

A variável **Frete Grátis** (uma das mais importantes) apareceu fragmentada em múltiplas categorias devido a erros de digitação no dataset original:
* `free_shipping_YES`
* `free_shipping_No`
* `free_shipping_Yes`
* ... e outras variações.

**Plano para a Etapa 4:**
Essa "sujeira" nos dados diluiu a capacidade preditiva do modelo. Na próxima etapa (Otimização), a prioridade será limpar essas colunas categóricas para unificar a informação e, consequentemente, aumentar o R².
