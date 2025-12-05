# 1. **Health Insurance Cross-Sell Prediction**

## Desenvolvimento de um sistema para priorizar clientes com maior propensão à contratação de seguros automotivos

Os dados utilizados neste projeto foram obtidos no Kaggle, a partir do desafio **“Health Insurance Cross Sell Prediction”**.

Embora o contexto seja simulado, toda a concepção, implementação e avaliação seguem o mesmo rigor aplicado em projetos reais no ambiente corporativo.

---

# 1.2 **Objetivo**

Desenvolver um sistema de priorização que, a partir de **304 mil clientes**, identifique e ranqueie os que possuem a  maior **probabilidade de contratar seguro automotivo**, organizando-os por ordem de propensão de compra.

---

# 2. **Planejamento da Solução**

## 2.1 **Produto Final**

Entrega de um **modelo de Machine Learning** capaz de **ranquear clientes por probabilidade de contratação**, possibilitando ao time comercial priorizar aqueles com maior chance de conversão.

## 2.2 **Processo**

Este é um projeto do tipo **Learning to Rank (LTR)**.

A metodologia adotada segue o framework **CRISP-DS**:

---

### **01. Data Description**

- Leitura e análise inicial dos dados
- Compreensão dos atributos
- Padronização de nomes e tipos
- Identificação e tratamento de valores ausentes
- Estatística descritiva dos principais campos

---

### **02. Feature Engineering**

- Construção de novas variáveis relevantes
- Transformações necessárias para testar hipóteses

---

### **03. Exploratory Data Analysis**

- Análise univariada para entendimento individual dos atributos
- Análise bivariada para investigar relações com a variável-alvo

---

### **04. Data Preparation**

- Padronização de variáveis numéricas com distribuição normal
- Escalonamento de variáveis com distribuição não normal
- Codificação de atributos categóricos
- Aplicação das transformações ao conjunto de teste

---

### **05. Feature Selection**

- Ranking das variáveis por importância
- Seleção das features mais relevantes
- Remoção de atributos com baixo poder preditivo

---

### **06. Machine Learning Modelling**

Modelos utilizados:

- **KNN Classifier**
- **Logistic Regression**
- **Extra Trees Classifier**

Além disso, foram geradas as curvas de **Cumulative Gain** para avaliar a capacidade de priorização de cada modelo.

---

### **07. Model Performance**

As principais métricas avaliadas foram:

- **precision@k**: quantos dos K clientes priorizados são realmente interessados
- **recall@k**: percentual de todos os interessados capturados entre os primeiros K
- Ordenação dos clientes por score
- Avaliação das métricas em diferentes valores de K
- Validação nos dados de teste

**Exemplo (valores fictícios):**

- **Precision@50:** 34%

→ Entre os 50 clientes com maior score, 34% realmente demonstraram interesse.

- **Recall@50:** 0,18%

→ Os 50 primeiros clientes representam apenas 0,18% de todos os clientes interessados da base.

Essa abordagem permite otimizar a operação do call center, ajustando K conforme a capacidade de atendimento disponível.

---

# 3.0 **Avaliação dos Modelos**

## **Cumulative Gain**

Para comparar o desempenho dos algoritmos, foram analisadas as curvas de **Cumulative Gain**, que medem a capacidade do modelo em **priorizar corretamente a classe positiva (interessados)**.

Quanto mais a curva da classe 1 (positivos) se distancia da linha aleatória, melhor é o ranqueamento.

---

### **3.1 Analise de resultados**

### **KNN**

- Curva aceitável, porém instável.
- Captura parte dos interessados nos primeiros percentis.
- Necessita de uma parcela maior da base para atingir todos os positivos.

---

### **Regressão Logística**

- Curva crescente, suave e consistente.
- Recupera rapidamente grande parte dos interessados.
- Bom nível de calibração e ranqueamento.

---

### **Extra Trees (melhor modelo)**

- Melhor performance entre os algoritmos.
- A curva sobe rapidamente e captura quase todos os clientes interessados com menos de **40%** da amostra.
- Forte separação entre as classes e excelente poder preditivo.

| **Modelo** | **Ganho Acumulado** | **Capacidade de Priorizar Positivos** | **Comentário** |
| --- | --- | --- | --- |
| KNN | Razoável | Moderada | Curva instável; desempenho mediano. |
| Regressão Logística | Boa | Alta | Modelo bem calibrado e consistente. |
| Extra Trees | Excelente | Muito alta | Melhor modelo para o problema. |

# Conclusões

O modelo **Extra Trees** apresentou o melhor desempenho, demonstrando alta capacidade de priorizar os clientes com maior probabilidade de contratação do seguro automotivo.

Com base nos resultados, é possível direcionar o esforço do call center de forma muito mais eficiente: uma fração relativamente pequena da base já contempla a maior parte dos clientes interessados.

Este projeto mostra como técnicas de **Learning to Rank**, combinadas com análises de ganho cumulativo, podem gerar valor imediato para operações comerciais, reduzindo custos, aumentando conversão e tornando o processo de prospecção mais estratégico e orientado por dados.

## Próximos passos

- **Aprimorar os modelos** com otimização de hiperparâmetros e testar algoritmos mais robustos (XGBoost, LightGBM, CatBoost).
- **Adicionar novas métricas** de avaliação, como Lift Curve, ROC AUC e Brier Score.
- **Testar o modelo em ambiente real**, aplicando A/B tests e monitorando performance ao longo do tempo.
- **Criar uma API e um dashboard** para disponibilização do ranking ao time comercial.
