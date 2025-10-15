# ic-tp01

### 🔍 1. Análise Exploratória de Dados (EDA)

* **Carregamento e visualização dos dados**: Inspecionaria as primeiras linhas dos dados para entender sua estrutura e identificar tipos de variáveis.
* **Verificação de valores ausentes**: Identificaria e trataria valores ausentes, seja por imputação ou remoção de registros.
* **Análise de distribuições**: Avaliaria a distribuição das variáveis numéricas e categóricas para identificar padrões ou outliers.
* **Correlação entre variáveis**: Verificaria a correlação entre variáveis para entender relações e possíveis redundâncias.

---

### 🧹 2. Pré-processamento de Dados

* **Codificação de variáveis categóricas**: Utilizaria técnicas como One-Hot Encoding ou Label Encoding para converter variáveis categóricas em formatos numéricos.
* **Normalização ou padronização**: Aplicaria técnicas de normalização ou padronização em variáveis numéricas para garantir que todas as variáveis tenham a mesma escala.
* **Divisão dos dados**: Separaria os dados em conjuntos de treino e teste, garantindo que a divisão seja estratificada para manter a proporção das classes.

---

### ⚙️ 3. Construção e Treinamento do Modelo

* **Seleção de modelos**: Experimentaria com diferentes algoritmos de aprendizado de máquina, como:

  * Regressão logística
  * Árvores de decisão
  * Random Forest
  * Gradient Boosting (ex: XGBoost, LightGBM)
  * Redes neurais (se apropriado)
* **Validação cruzada**: Utilizaria validação cruzada para avaliar a performance dos modelos e evitar overfitting.
* **Ajuste de hiperparâmetros**: Aplicaria técnicas como Grid Search ou Random Search para otimizar os hiperparâmetros dos modelos.

---

### 📊 4. Avaliação e Seleção do Modelo

* **Métricas de avaliação**: Utilizaria métricas como AUC-ROC, precisão, recall e F1-score para avaliar a performance dos modelos.
* **Matriz de confusão**: Analisaria a matriz de confusão para entender os tipos de erros cometidos pelo modelo.
* **Interpretação do modelo**: Utilizaria ferramentas como SHAP ou LIME para interpretar as decisões do modelo e entender quais variáveis são mais influentes.

---

### 🚀 5. Submissão e Iteração

* **Preparação da submissão**: Geraria as previsões no formato exigido pela competição e as submeteria.
* **Análise dos resultados**: Avaliaria o feedback recebido para identificar áreas de melhoria.
* **Iteração**: Com base nos resultados, faria ajustes no modelo, no pré-processamento ou na engenharia de features para melhorar a performance.
