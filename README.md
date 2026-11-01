# Detecção de Fraude em Cartão de Crédito com Machine Learning 💳🛑

( <img width="768" height="940" alt="Variavel_fraude" src="https://github.com/user-attachments/assets/2fd0bfff-83fa-4db6-8f15-45e7302df85b" />
)

Este projeto foi desenvolvido como um **Desafio de Projeto** prático guiado pela Expert Isadora Garcia Ferrão. O objetivo central é construir um pipeline completo de Ciência de Dados em Python para identificar transações fraudulentas de cartão de crédito, lidando com o desafio extremo de dados altamente desbalanceados.

## 🎯 O Problema do Desbalanceamento
Em cenários reais de fraude bancária, os eventos criminosos são raros. Neste dataset, apenas **0,17%** das transações são fraudes, enquanto **99,83%** são normais. 

Se utilizássemos a métrica de **Acurácia**, um modelo ingênuo que classificasse todas as transações como "normais" teria 99,83% de acerto, mas deixaria passar 100% dos golpes. Por essa razão, este projeto foca nas métricas corretas para o negócio:
*   **Recall (Revogação):** Para garantir que o maior número possível de fraudes seja detectado.
*   **Precision (Precisão):** Para monitorar a taxa de alarmes falsos enviados aos clientes.
*   **F1-Score & AUPRC:** Para avaliar o equilíbrio do modelo na classe minoritária.

---

## 🛠️ Estrutura do Pipeline Desenvolvido

O projeto foi construído do zero seguindo rigorosamente as 5 etapas do pipeline profissional de Machine Learning:

1. **Explore (Análise Exploratória):** Carregamento dos dados brutos e mapeamento estatístico do desbalanceamento severo da variável alvo `Class`.
2. **Prepare (Pré-processamento):** 
   * Engenharia de Features aplicando a transformação matemática de Logaritmo (`np.log1p`) na variável `Amount` para suavizar o impacto de outliers.
   * Padronização das variáveis `Time` e `Amount` utilizando o `StandardScaler`.
   * Separação dos conjuntos de treino e teste de forma estratificada (`stratify=y`) para preservar a proporção exata de 0,17% de fraudes em ambas as partições.
3. **Treine (Modelagem Avançada):** Treinamento comparativo de três algoritmos robustos:
   * **Regressão Logística** (usada como Baseline com `class_weight='balanced'`).
   * **Random Forest** (com subamostragem e ajuste de limiar).
   * **XGBoost** (utilizando `scale_pos_weight` e técnicas de Oversampling via SMOTE).
4. **Avalie (Métricas de Performance):** Geração de relatórios de classificação completos, plotagem e análise da **Curva ROC (AUROC)** e da **Curva de Precisão-Recall (AUPRC)**.
5. **Explique (Explicabilidade de IA - XAI):** Implementação do framework **SHAP (SHapley Additive exPlanations)** para abrir a caixa-preta do modelo campeão, demonstrando quais variáveis latentes (V1 a V28 vindas do PCA) mais impactaram na pontuação de risco de cada transação.

---

## 📊 Tecnologias e Ferramentas Utilizadas

*   **Linguagem:** Python
*   **Manipulação e Análise de Dados:** Pandas, NumPy
*   **Machine Learning:** Scikit-Learn, XGBoost
*   **Tratamento de Desbalanceamento:** Imbalanced-Learn (SMOTE, RandomUnderSampler)
*   **Visualização de Dados:** Matplotlib, Seaborn
*   **Explicabilidade de Modelos:** SHAP

---

## 🚀 Como Executar o Projeto

1. Clone este repositório:
   ```bash
   git clone https://github.com
   ```
2. Instale as dependências necessárias:
   ```bash
   pip install pandas numpy scikit-learn xgboost imbalanced-learn matplotlib seaborn shap
   ```
3. Abra e execute o arquivo Jupyter Notebook (`.ipynb`) no seu ambiente de preferência (Google Colab ou Jupyter Lab).

---

## 📈 Conclusões Técnicas

O modelo final demonstrou que, ao ajustar estrategicamente o **limiar de decisão (Threshold Tuning)** de 0.50 para patamares mais sensíveis (como 0.30), conseguimos alavancar dramaticamente o **Recall da classe de Fraude**, minimizando o risco financeiro da instituição, mantendo uma precisão comercialmente aceitável para evitar fricção excessiva com bons clientes.
