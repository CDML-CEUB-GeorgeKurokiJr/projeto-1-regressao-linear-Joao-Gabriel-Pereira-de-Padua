[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/gIUcegNI)

Credit Card Fraud Detection com Regressão Linear

Este projeto explora a aplicação de um modelo de **Regressão Linear** em um cenário de **Classificação Binária altamente desbalanceada**, focado na detecção de fraudes em cartões de crédito.

Objetivo
Avaliar a capacidade geométrica e matemática da Regressão Linear Múltipla para distinguir transações legítimas de fraudulentas em um dataset do mundo real, onde as fraudes representam apenas **0.172%** das transações.

Sobre os Dados
* **Dataset:** European Credit Card Transactions (Setembro 2013).
* **Características:** 284.807 transações, contendo apenas variáveis numéricas resultantes de uma transformação **PCA** (V1 a V28), além de `Time` e `Amount`.
* **Validação do PCA:** Através do cálculo do Fator de Inflação da Variância (VIF), provamos que as variáveis originais são estritamente ortogonais (VIF = 1.000), garantindo ausência total de multicolinearidade.

Metodologia e Experimentos

O projeto exigiu a adaptação de um algoritmo de regressão contínua para um problema de classificação. As seguintes abordagens foram testadas empírica e matematicamente:

1. **Threshold Tuning (Ajuste de Limiar):** * Como a Regressão Linear prevê valores contínuos, aplicamos limiares de corte (Thresholds) para binarizar as saídas.
   * **Descoberta:** Reduzir o limiar de `0.5` para `0.2` dobrou a captura de fraudes reais (de 45 para 80), aumentando os falsos positivos de forma irrisória (apenas 7 cartões a mais bloqueados). Este se provou o modelo com maior viabilidade de negócio.

2. **Undersampling (Balanceamento Majoritário):**
   * Reduzimos as transações legítimas no treino para igualar o número de fraudes (50/50).
   * **Resultado:** O modelo sofreu um colapso geométrico. A reta de decisão perdeu o contexto da classe majoritária, resultando em uma anomalia de **900 falsos positivos**.

3. **SMOTE (Synthetic Minority Over-sampling Technique):**
   * Criamos dados sintéticos da classe minoritária para treinar o modelo.
   * **Resultado:** Redução dos falsos positivos para 794 (melhoria em relação ao Undersampling), mas ainda inviável para produção bancária.

Conclusão Científica
O projeto comprovou de forma prática o **limite geométrico da Regressão Linear**. 
A fronteira de decisão (uma linha reta/hiperplano) é insuficiente para separar classes complexas e intrincadas como as de fraude financeira. Apesar de técnicas avançadas de engenharia de dados (PCA) e balanceamento (SMOTE), a rigidez espacial do algoritmo linear inevitavelmente sacrifica transações legítimas (Falsos Positivos) ao tentar capturar anomalias. 

Para produção, o estudo recomenda a transição empírica para modelos baseados em probabilidade não-linear (Regressão Logística) ou árvores de decisão.
Link para base de dados: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud
