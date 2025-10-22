# ic-tp01

# Planejamento - Competição Kaggle: Spaceship Titanic

## 1. Objetivo da Competição
Prever quais passageiros foram transportados para outra dimensão durante a viagem da Spaceship Titanic, usando dados fornecidos sobre características pessoais e de viagem.

**Tipo de problema:** Classificação binária (`Transported` = True/False).

---

## 2. Etapas do Planejamento

### 2.1. Entendimento do Problema e Dados
- Ler a descrição completa da competição no Kaggle.
- Baixar os arquivos `train.csv` e `test.csv`.
- Identificar:
  - Variáveis numéricas e categóricas.
  - Possíveis valores ausentes.
  - Variável alvo: `Transported`.

---

### 2.2. Análise Exploratória de Dados (EDA)
- **Objetivo:** entender padrões, distribuições e relações entre variáveis.
- Passos:
  1. Verificar valores nulos e propor estratégias de imputação.
  2. Analisar distribuição da variável alvo.
  3. Explorar correlações entre variáveis numéricas.
  4. Criar gráficos para variáveis categóricas vs. alvo.
  5. Detectar outliers e inconsistências.

Ferramentas sugeridas: `pandas`, `matplotlib`, `seaborn`.

---

### 2.3. Pré-processamento
- **Tratamento de valores ausentes**:
  - Numéricos: média, mediana ou modelos de imputação.
  - Categóricos: valor padrão ou imputação baseada em frequência.
- **Codificação de variáveis categóricas**:
  - One-Hot Encoding ou Label Encoding.
- **Normalização/Escalonamento**:
  - `StandardScaler` ou `MinMaxScaler` para variáveis numéricas.
- **Feature Engineering**:
  - Criar novas variáveis a partir de colunas existentes (ex.: extrair deck da coluna `Cabin`).
  - Agrupar variáveis relacionadas (ex.: gastos totais a bordo).

---

### 2.4. Modelagem
- **Modelo escolhido:** `RandomForestClassifier` (Scikit-learn).
- **Validação:**  
  - Usar **validação cruzada K-Fold** (ex.: `KFold` ou `StratifiedKFold` com `n_splits=5`).
  - Métrica principal: `accuracy` (conforme competição), mas também avaliar `F1-score` para balanceamento.
- **Passos:**
  1. Definir hiperparâmetros iniciais do RandomForest.
  2. Treinar e avaliar usando K-Fold.
  3. Registrar resultados médios e variância entre folds.

---

### 2.5. Otimização de Hiperparâmetros
- Usar `GridSearchCV` ou `RandomizedSearchCV` com validação cruzada.
- Testar parâmetros como:
  - `n_estimators`
  - `max_depth`
  - `min_samples_split`
  - `min_samples_leaf`
  - `max_features`
- Avaliar impacto no score médio da validação cruzada.

---

### 2.6. Avaliação Final
- Treinar o modelo final com todos os dados de treino usando os melhores hiperparâmetros.
- Gerar previsões para o conjunto `test.csv`.

---

### 2.7. Submissão no Kaggle
- Criar arquivo `submission.csv` com:
  - `PassengerId`
  - `Transported` (True/False)
- Submeter no Kaggle e registrar score.
- Documentar resultados e insights.

---

## 3. Cronograma Sugerido

| Dia | Tarefa |
|-----|--------|
| 1   | Entendimento do problema e download dos dados |
| 2-3 | EDA e tratamento inicial de dados |
| 4   | Pré-processamento e feature engineering |
| 5   | Treinamento inicial com RandomForest e K-Fold |
| 6   | Otimização de hiperparâmetros |
| 7   | Avaliação final e submissão |
| 8+  | Iterações para melhorar score |

---

## 4. Recursos Úteis
- [Documentação Pandas](https://pandas.pydata.org/docs/)
- [Seaborn](https://seaborn.pydata.org/)
- [Scikit-learn - RandomForestClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
- [Scikit-learn - KFold](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html)

---

## 5. Observações
- Sempre versionar o código (Git).
- Registrar experimentos e resultados.
- Testar diferentes abordagens de imputação e codificação.
- Participar do fórum da competição para trocar ideias.
