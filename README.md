# 🚢 Análise de Impacto Climático em Operações Portuárias

## Unificação do projeto
**[aqui](./abtra-climate-impact.ipynb)**, unificamos o projeto para a entrega da tarefa de aula.


## 1. Sobre o projeto

Neste projeto, nosso objetivo foi simular o impacto real das condições climáticas nas operações portuárias de Santos/Bertioga. Utilizamos a base de dados da **ABTRA** (Associação Brasileira de Terminais e Recintos Alfandegários), disponibilizada pelo professor Luiz Guilherme, para sair da teoria e aplicar Data Science na prática.

A ideia central foi responder: **Quanto custa um dia de chuva ou vento forte para a eficiência do porto?** Investigamos desde o impacto no volume de carga movimentada (toneladas) até o tempo que a mercadoria fica parada aguardando liberação (lead time).

---

## 2. Estrutura do Repositório

Aqui você encontra o passo a passo do desenvolvimento, desde a limpeza até a previsão:

* **1. [Dados Brutos](./data)**
  * Contém os datasets originais da **ABTRA** e dados meteorológicos históricos do **INMET** (Instituto Nacional de Meteorologia). *Nota: Os dados de clima de 2020-2021 possuem lacunas que foram tratadas no código.*

* **2. [Engenharia de Dados (ETL)](./notebooks/data_abtra_climate.ipynb)**
  * Script responsável pela "faxina" dos dados.
  * **O que foi feito:** Correção de formatação numérica padrão BR (`1.000,00` para `float`), limpeza de headers e, crucialmente, a **separação dos datasets** em "Carga Descarregada" e "Tempo de DI" para evitar duplicatas e garantir a integridade da análise.

* **3. [Análise Exploratória (EDA)](./notebooks/EDA_ABTRA.ipynb)**
  * Onde os dados contam a história. Investigamos correlações e testamos hipóteses de negócio.
  * **Destaque:** Descoberta da sazonalidade cruzada (Vento forte coincide com época de Safra).

* **4. [Modelagem Preditiva](./notebooks/abtra_models.ipynb)**
  * Treinamento de algoritmos de **Regressão Linear Múltipla** para prever atrasos e volume.
  * Inclui validação de métricas (RMSE, R², MAPE) e análise de resíduos para checar overfitting.

---

## 3. Principais Resultados

O estudo revelou insights importantes para a logística portuária:

* **🌬️ O Mito do Vento:** Descobrimos que o volume de carga *aumenta* nos meses de vento forte. Isso não é causalidade, mas **sazonalidade**: a safra (pico de demanda) ocorre justamente no segundo semestre, quando venta mais em Bertioga.
* **⏱️ O Custo do Tempo:** Embora o volume se mantenha, a eficiência cai. Confirmamos estatisticamente que rajadas de vento aumentam o tempo de fila (`+0.08 dias` por m/s de vento).
* **🎯 Acurácia do Modelo:** Conseguimos criar um modelo preditivo para o **Volume de Carga** com uma acurácia estimada de **~94%** (MAPE de 5.8%), permitindo prever quebras de produtividade baseadas na previsão do tempo.

---

## 4. Tecnologias Utilizadas

* Python 3.x
* Pandas & Numpy (Manipulação de dados)
* Matplotlib & Seaborn (Visualização)
* Scikit-Learn (Machine Learning)
