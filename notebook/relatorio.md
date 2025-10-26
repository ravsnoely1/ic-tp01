# 📄 **Relatório Final - Spaceship Titanic (Kaggle)**

## 1. **Introdução**

O **Spaceship Titanic** é uma competição fictícia hospedada no [Kaggle](https://www.kaggle.com/competitions/spaceship-titanic), inspirada no famoso dataset Titanic, mas ambientada em uma nave espacial. 
Essa nave espacial, viajava com destino a três exoplanetas recém-habitáveis que orbitam estrelas próximas ao nosso sistema solar. Mas houve um acidente e que levou a metade dos 13.000 passageiros serem transportados para uma dimensão alternativa. Para ajudar a equipe de resgate a recuperar os passageiros perdidos, temos o objetivo de prever qual passageiro foi **transportado para outra dimensão** (`Transported = True/False`) após um acidente, usando informações demográficas e de viagem.

- **Tipo de problema:** Classificação binária.
- **Métrica oficial:** **Accuracy**  
  
  $Accuracy = \frac{\text{Previsões corretas}}{\text{Total de previsões}}$
 
- **Formato de entrega:** Arquivo `submission.csv` com colunas `PassengerId` e `Transported`.

---

## 2. **Descrição dos Dados**

O dataset contém informações como:

- **Variáveis numéricas:** `Age`, `RoomService`, `FoodCourt`, `ShoppingMall`, `Spa`, `VRDeck`.
- **Variáveis categóricas:** `HomePlanet`, `CryoSleep`, `Cabin`, `Destination`, `VIP`.
- **Target:** `Transported` (booleano).

**Tamanho do dataset:**
- **Treino:** 8.693 linhas × 14 colunas.
- **Teste:** 4.277 linhas × 13 colunas.

**Valores ausentes:**
| Variável       | % Missing |
|----------------|-----------|
| Cabin          | 20%       |
| HomePlanet     | 2%        |
| Destination    | 2%        |
| Age            | 5%        |
| RoomService    | 7%        |
| FoodCourt      | 7%        |
| ShoppingMall   | 7%        |
| Spa            | 7%        |
| VRDeck         | 7%        |

---

## 3. **Análise Exploratória (EDA)**

### 3.1 Distribuição das variáveis numéricas
- **Idade:** maioria entre 20 e 40 anos.
- **Gastos (RoomService, FoodCourt, etc.):** altamente assimétricos, com muitos passageiros gastando pouco ou nada.

*(Inserir aqui histogramas gerados no notebook)*

### 3.2 Distribuição das variáveis categóricas
- **HomePlanet:** maioria de passageiros vem de `Earth`.
- **Destination:** destino mais comum é `TRAPPIST-1e`.
- **CryoSleep:** cerca de 30% dos passageiros estavam em sono criogênico.

*(Inserir aqui countplots gerados no notebook)*

### 3.3 Correlação
- Gastos em serviços (`Spa`, `VRDeck`) têm correlação positiva moderada entre si.
- Idade não apresenta correlação forte com o target.

*(Inserir aqui heatmap gerado no notebook)*

### 3.4 Relação com o Target
- Passageiros em **CryoSleep** têm maior probabilidade de serem transportados.
- Passageiros que gastaram mais em `VRDeck` tendem a não ser transportados.

*(Inserir aqui boxplots gerados no notebook)*

---

## 4. **Pré-processamento**

- **Imputação de valores ausentes:**
  - Numéricos → **mediana**.
  - Categóricos → **moda**.
- **Codificação:** `LabelEncoder` para variáveis categóricas.
- **Escalonamento:** `StandardScaler` para variáveis numéricas.
- **Split:** 80% treino / 20% validação.

---

## 5. **Modelos e Resultados**

### 5.1 Modelos semelhantes
Os autores ZHUCUI JING e XIAOLI YIN, em seu o artigo: “Neural Network-Based Prediction Model for Passenger Flow in a Large Passenger Station: An Exploratory Study” apresenta a aplicação de redes neurais para prevê a entrada e saída de passageiros de uma estação, com objetivo de fornecer a garantia de segurança da estação, alocação de recursos e distribuição de pessoal.
Neste modelo como entrada da rede neural, eles utilizaram os principais fatores que afetam a mudança do fluxo de passageiros. Durante o processo de aprendizagem, era atualizado a taxa de tamanho de passos para estimar o número de pessoas que entram na estação durante um determinado intervalo de tempo. O resultado é avaliado com os dados históricos para derivar a previsão do fluxo de passageiros durante o próximo intervalo de tempo. (Veja em: https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8985339 )

No artigo “Prospects and challenges of Metaverse application in data-driven intelligent transportation systems”, de acordo com os autores Judith Nkechinyere Njoku, Cosmas Ifeanyi Nwakanma, Gabriel Chukwunonso Amaizu, Dong-Seong Kim, o Metaverso é um conceito usado para referir a um mundo virtual que existe paralelamente ao mundo físico. Por exemplo a aplicação de metaverso em jogos de realidades virtuais. Neste artigo, os autores realizam um estudo de caso que analisa os conceitos de recursos de Metaverso em sistemas de transportes inteligentes baseado em dados. (Veja em: https://ietresearch.onlinelibrary.wiley.com/doi/epdf/10.1049/itr2.12252 )

### 5.2 Baseline
- **DummyClassifier (most_frequent)** → Accuracy: **0.50**  
  *(serve como referência mínima)*

### 5.3 Modelos testados
| Modelo         | Accuracy (CV) |
|----------------|---------------|
| RandomForest   | 0.78          |
| XGBoost        | 0.79          |
| KNN            | 0.74          |

### 5.4 Meta-learning
- **VotingClassifier (soft voting)** → Accuracy: **0.80**  
  *(ganho pequeno, mas consistente)*

---

## 6. **Otimização de Hiperparâmetros**

Usando **Optuna** no RandomForest:
- **Melhores parâmetros:**
  ```json
  {
    "n_estimators": 420,
    "max_depth": 12
  }
  ```
- **Accuracy após tuning:** **0.81**

*(Inserir gráfico de importância de parâmetros do Optuna)*

---

## 7. **Comparação Final**

| Modelo               | Accuracy (CV) | Melhor Parâmetro | Observações |
|----------------------|---------------|------------------|-------------|
| Baseline             | 0.50          | -                | Referência mínima |
| RandomForest         | 0.78          | -                | Bom desempenho |
| XGBoost              | 0.79          | -                | Estável |
| KNN                  | 0.74          | -                | Sensível ao escalonamento |
| VotingClassifier     | 0.80          | -                | Ensemble de 3 modelos |
| RandomForest Tunado  | **0.81**      | Optuna params    | Melhor resultado |

---

## 8. **Conclusão**

- O **RandomForest Tunado** apresentou o melhor desempenho (Accuracy = 0.81).
- O **VotingClassifier** também foi competitivo, mostrando que ensembles podem ajudar.
- **Possíveis melhorias futuras:**
  - Engenharia de atributos (ex.: extrair número e lado da cabine).
  - Testar LightGBM e CatBoost.
  - Imputação mais sofisticada (KNNImputer).
  - Feature selection para reduzir ruído.

