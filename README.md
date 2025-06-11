# ✍🏽 Classificação de algarismos escritos à mão com SGDClassifier, SupportVectorClassifier, K-nearest-neighbors e RandomForests

## 🎯 Objetivo

Este projeto tem como objetivo desenvolver e avaliar modelos de machine learning para classificar algarismos escritos à mão utilizando o conjunto de dados MNIST. O foco é explorar diferentes abordagens de classificação, incluindo classificação binária, multiclasse, multirrótulo e multioutput, e analisar o desempenho dos modelos utilizando métricas como Validação Cruzada, Precisão, Revocação, F1 Score e ROC AUC.

## 💾 Dataset

O conjunto de dados utilizado é o MNIST (Modified National Institute of Standards and Technology), que consiste em aproximadamente 70.000 imagens em tons de cinza de 28x28 pixels de dígitos escritos à mão por estudantes e funcionários do US Census Bureau. Cada imagem representa um dígito de 0 a 9. O dataset já vem pré-dividido em 60.000 imagens para treinamento e 10.000 para teste.

## 🔎Análise Exploratória de Dados (EDA)

Foi realizada uma análise inicial do dataset para entender sua estrutura e visualizar exemplos dos dígitos escritos à mão. Cada imagem é representada por um vetor de 784 características, correspondendo à intensidade de cada pixel.

## ✌🏽 Classificação Binária

Inicialmente, foi abordado o problema como uma classificação binária, focando em identificar se uma imagem representava o dígito '5' ou não. Para isso, foi utilizado o classificador Gradiente Descendente Estocástico (SGDClassifier), conhecido por sua eficiência com grandes datasets.

O desempenho do classificador binário foi avaliado utilizando validação cruzada k-fold. Observou-se que a acurácia, por si só, pode ser enganosa em datasets assimétricos como o MNIST (onde a classe '5' representa apenas cerca de 10% dos dados).

Para uma avaliação mais detalhada, foram utilizadas a matriz de confusão, precisão, revocação (recall) e o F1-score. A análise revelou que o classificador obteve uma precisão razoável, mas com uma revocação menor, indicando que ele era bom em identificar corretamente os 5s que ele classificava, mas falhava em detectar uma parte significativa dos 5s reais.

Explorou-se o trade-off entre precisão e revocação, ajustando o limiar de decisão do SGDClassifier. Foi demonstrado como escolher um limiar que atenda a um requisito específico de precisão (por exemplo, 90%) e o impacto disso na revocação.

Por fim, a curva ROC (Receiver Operating Characteristic) e a Área sob a Curva (AUC) foram utilizadas para avaliar o desempenho geral do classificador binário, especialmente em diferenciar as classes positiva e negativa.

## 🔢 Classificação Multiclasse

Expandindo para a classificação de todos os 10 dígitos, foram explorados classificadores multiclasse. Alguns algoritmos (como SGD e RandomForest) lidam com múltiplas classes nativamente, enquanto outros (como SVMs) são binários e requerem estratégias como One-vs-Rest (OvR) ou One-vs-One (OvO).

Foi demonstrado o uso de um classificador SVM, que automaticamente utilizou a estratégia OvO no scikit-learn. Também foi forçado o uso da estratégia OvR com um classificador SVM.

O SGDClassifier também foi aplicado à tarefa multiclasse. A avaliação inicial com validação cruzada mostrou uma acurácia acima de 85%. A aplicação da padronização dos dados (StandardScaler) resultou em uma melhora notável na acurácia do modelo.

## ❌ Análise de Erro

Para entender melhor onde o modelo multiclasse comete erros, foi analisada a matriz de confusão. Uma representação visual da matriz de confusão normalizada ajudou a identificar quais classes são mais frequentemente confundidas. Por exemplo, observou-se que muitos dígitos de outras classes foram erroneamente classificados como '8'.

A análise de erros individuais, visualizando exemplos de dígitos classificados incorretamente, forneceu insights sobre as causas dos erros, como a semelhança visual entre dígitos (por exemplo, 3 e 5) e a sensibilidade do classificador linear a variações na escrita e rotação.

## 🏷️ Classificação Multirrótulo (Extra)

Foi apresentado um exemplo de classificação multirrótulo, onde cada instância pode ter múltiplos rótulos associados. O exemplo consistiu em classificar os dígitos com base em duas propriedades: ser grande (>= 7) e ser ímpar. Foi utilizado um classificador KNeighborsClassifier para esta tarefa e avaliado com o F1-score médio (macro average).

## 📤 Classificação Multioutput (Extra)

Como uma generalização da classificação multirrótulo, foi demonstrada a classificação multioutput. Um sistema de remoção de ruído de imagens foi criado. Ruído aleatório foi adicionado às imagens do dataset, e um KNeighborsClassifier foi treinado para prever a imagem original (sem ruído) a partir da imagem ruidosa. Cada pixel da imagem de saída é um rótulo com múltiplos valores possíveis (intensiade do pixel).

## 💿 Como Rodar o Código

Para executar este projeto, siga os passos abaixo:

1. Clone o repositório para sua máquina local.
2. Certifique-se de ter as bibliotecas Python necessárias instaladas (numpy, matplotlib, scikit-learn). Você pode instalá-las usando pip: `pip install numpy matplotlib scikit-learn`.
3. O dataset MNIST será baixado automaticamente pelo scikit-learn na primeira execução.
4. Execute o notebook Python (`.ipynb`) em um ambiente como Jupyter Notebook ou Google Colab.

## ✅ Conclusão

Este projeto explorou diversas técnicas de classificação de machine learning aplicadas ao dataset MNIST. Foi possível demonstrar a implementação e avaliação de classificadores binários e multiclasse, entender a importância de métricas de avaliação apropriadas para datasets assimétricos, analisar erros para identificar áreas de melhoria e explorar conceitos mais avançados como classificação multirrótulo e multioutput. O SGDClassifier demonstrou um desempenho razoável, que pode ser melhorado com pré-processamento como a padronização dos dados. A análise de erros destacou a importância de considerar as características dos dados e do modelo para otimizar o desempenho.
