# Detecção de Fraude em Cartão de Crédito utilizando Inteligência Artificial

Este repositório contém o desenvolvimento prático do projeto final de Inteligência Artificial para detecção de transações fraudulentas em cartões de crédito. O objetivo principal do projeto é aplicar técnicas de processamento de dados e aprendizado de máquina para lidar com o desbalanceamento severo de classes e identificar de forma consistente e estável as atividades fraudulentas.

**Autora:** Tainara da Silva Santos (UNIFESP)

---

## Visão Geral do Projeto

Transações de fraude financeira são eventos raros e de alta criticidade. A base de dados utilizada registra transações ocorridas na Europa, onde as fraudes representam apenas **0,172%** do volume total de dados. Devido a esse desbalanceamento extremo, o projeto foca em:
1. **Pré-processamento e Balanceamento** utilizando a técnica de *Undersampling*.
2. **Visualização Espacial** do comportamento dos dados usando algoritmos de redução de dimensionalidade (*t-SNE* e *TruncatedSVD*).
3. **Avaliação Estatística Robusta** de 4 modelos de Machine Learning ao longo de 30 simulações aleatórias.
4. **Análise de Variáveis** e detalhamento do modelo campeão através de métricas específicas orientadas ao problema.

---

## Como Executar o Projeto

### Pré-requisitos
Certifique-se de possuir o Python instalado junto com as seguintes bibliotecas fundamentais listadas nas dependências do script:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost psutil
```

---

## Arquitetura e Estrutura do Código

O arquivo principal `projetoFinal_IA.ipynb` está estruturado de forma sequencial e lógica, dividido nas seguintes etapas:

### 1. Configuração e Monitoramento do Ambiente
* Coleta informações do ecossistema computacional utilizado (`platform`, `psutil`, `sys`) para garantir a reprodutibilidade técnica e o controle de consumo de memória física.

### 2. Pré-processamento e Balanceamento de Dados
* Identificação da minoria e aplicação de **Undersampling** aleatório fixado em 492 transações legítimas vs. 492 transações fraudulentas.
* Escalonamento e normalização das variáveis contínuas com o `MinMaxScaler` para o intervalo $[0, 1]$.
* Aplicação das técnicas **t-SNE** e **TruncatedSVD** para condensar as 30 variáveis preditivas em uma matriz bidimensional (2D), gerando gráficos comparativos de clusterização espacial.

### 3. Validação Estatística de Modelos (30 Rodadas)
Treinamento iterativo de quatro famílias distintas de algoritmos de Machine Learning com sementes de aleatoriedade aleatórias e dinâmicas:
1. **Regressão Logística** (Modelo Linear de Base)
2. **XGBoost Classifier** (Algoritmo Ensamble Baseado em Gradient Boosting)
3. **Random Forest Classifier** (Algoritmo de Ensamble Baseado em Bagging)
4. **K-Neighbors Classifier (KNN)** (Modelo Baseado em Instâncias e Distância)

Todas as 30 execuções coletam a métrica **F1-Score**, gerando ao fim o intervalo de confiança de 95% para cada modelo.

### 4. Análise e Métricas do Modelo Campeão
Treinamento final detalhado e extração de relatórios analíticos utilizando o **XGBoost**:
* Matriz de Confusão para contagem de falsos positivos/negativos.
* Curva ROC e cálculo exato da Área Sob a Curva (AUC).
* Extração das 10 características essenciais determinantes (*Feature Importance*).

---

## Visualizações e Resultados Gerados

O script é responsável por plotar automaticamente as seguintes visualizações cruciais:
* **Gráficos de Redução de Dimensionalidade:** Gráficos de dispersão (*scatterplots*) lado a lado comparando as assinaturas geométricas e agrupamentos do *t-SNE* e *TruncatedSVD*.
* **Distribuição do F1-Score (Boxplot):** Demonstração visual da estabilidade e variação do erro dos 4 classificadores.
* **Estabilidade das Distribuições (KDE Plot):** Gráfico de densidade para estimar visualmente qual modelo concentra os piores ou melhores picos de F1-Score.
* **Matriz de Confusão:** Diagnóstico sobre a taxa de falsos negativos (fraudes que passaram direto) do modelo selecionado.
* **Curva ROC e AUC:** Desempenho geral do limiar de probabilidade discriminatório.
* **Importância de Variáveis:** Classificação vertical com os 10 atributos mais impactantes que acionam o alerta do classificador.

---

## Principais Resultados

- Comparação entre Regressão Logística, KNN, Random Forest e XGBoost.
- XGBoost apresentou o melhor desempenho na detecção de fraudes.
- Avaliação baseada em F1-Score devido ao forte desbalanceamento dos dados.
- Validação estatística por meio de 30 execuções independentes e Teste T-Pareado.
