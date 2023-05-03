# Stroke-Classification


Este projeto tem como base a realização de uma classificação binária utilizando um conjunto de dados que contém diversos pacientes indicando se eles tiveram ou não AVC. Para realizar a classificação foram utilizados alguns algoritmos
de aprendizado de máquina supervisionado e também foi utilizado técnicas de pré-processamento de dados para a obtenção de resultados melhores.

# Introdução

O AVC ou Acidente Vascular Cerebral é o entupimento dos vasos que levam sangue ao cérebro, e provoca a paralisia da região afetada no cérebro.

Segundo dados do Ministério da Saúde de 2018, a cada 5 minutos um brasileiro vem a óbito em decorrência do AVC. O que resulta em aproximadamente 100 mil mortes por ano. Também segundos dados do Ministério da Saúde o AVC é a segunda principal causa de mortes no Brasil, atrás apenas do infarto.

Esta doença, normalmente, tem como alvo pessoas mais idosas, entretanto no período entre 2019 e 2021 houve um crescimento de 3% no número de óbitos em decorrência do AVC, na faixa etária de 20 à 59 anos, segundo a Central Nacional de Informações do Registro Civil (CRC Nacional).

É possível identificar sinais, que possam sugerir a ocorrência de um AVC, entre eles estão a fraqueza, formigamento na face, alteração na fala, etc... Esse acidente pode ser evitado, caso seja feito um acompanhamento médico que evite a ocorrencia do próprio. Segundo o Ministério da Saúde, em 90% dos casos, o AVC, pode ser evitado com a prevenção. Assim é importante classificar pacientes de acordo com seus hábitos se estes são ou não propícios a terem um AVC.

![image](https://user-images.githubusercontent.com/91696970/236003272-7b58f357-1802-49d3-941c-fbce44849274.png)


Para isto, foi utilizado um conjunto de dados do Kaggle, que contém estas informações, o conjunto de dados pode ser obtido no seguinte link:


https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset?resource=download


# Conjunto de dados

O conjunto de dados analisado contém 12 atributos, e 5110 instâncias. Desses 12 atributos, 11 são atributos preditivos e um é o atributo classe, que identifica se o paciente teve ou não AVC.

Com isso, pode-se realizar o entendimento dos atributos e a definição se eles são categóricos ou númericos.

Neste conjunto possuímos 10 atributos Categóricos Nominais, 4 Numéricos Binários e 3 atributos Numéricos Contínuos.

# Análise do conjunto

COmo se trata de uma tarefa de classificação é necessário verificar se o conjunto de dados está balanceado ou não, para não gerar um overfitting do classificador, que é quando o modelo se adapta tantos aos dados de treino que não
é capaz de generalizar, fazendo com que não seja um classificador tão eficiente.

Desta maneira, foi constatado que o conjunto de dados estava incrivelmente desbalanceado, que era o esperado, visto que existem muito mais pessoas que não tiveram AVC no mundo do que pessoas que tiveram. Esta proporção era de 
95% para a classe negativa (sem AVC) e 5% para a classe positva (com AVC). Desta maneira o conjunto de dados foi balanceado, deixando em uma proporção não tão desbalanceada, 75% para a classe negativa e 25% para a classe positiva.

Após isso, iniciou o pré-processamento dos dados.

# Pŕe-Processamento

Como um dos algoritmos que se iria utilizar neste projeto era o kNN era necessário que os atributos categóricos fossem transformados em valores numéricos, para que fosse possível a execução do algoritmo. Assim, realizou-se o processo de One-Hot-Encoding. Além disso, os atributos binários que eram representados por valores em string, foram transformados em 0 e 1. Felizmente o conjunto de dados não possuia valores NULOS nas instâncias.

## One-Hot-Encoding

O processo de One-Hot-Encoding consiste em transformar todos os valores do atributo em atributos do conjunto de dados. Ou seja, se um atributo possui 3 valores serão criados 3 novos atributos, e o atributo original será removido. Estes novos atributos serão binários, e indicarão a presença ou não do valor para aquela instância.

![image](https://user-images.githubusercontent.com/91696970/236005248-b3335c2b-63d8-4948-9be6-93718f02fded.png)

## Normalização dos dados

Como estamos utilizando um algoritmo que utilizaria o cálculo da distância dos pontos (kNN) era necessário padronizar os atributos para evitar que um atributo se torne dominante na hora da classificação, assim utilizou-se a padronização por média e desvio padrão usual para padronizar os valores do conjunto de dados.

# Classificação

Na classificação foram utilizados 2 algoritmos que puderam ser comparados, o kNN e a Árvore de Decisão. 

## kNN


O algoritmo de classificação utilizado foi o KNN. Este algoritmo faz a classificação das novas instâncias com base na distância entre seus atributos.
O KNN calcula os k vizinhos mais próximos de uma instância, com base em seus atributos, e com estes vizinhos descobre a classe que o exemplo pertence.

Como mostra a imagem abaixo:

![image](https://user-images.githubusercontent.com/91696970/236006355-69924ea5-0bc5-4fee-95fd-bedcccbd15ed.png)

Nesta imagem podemos observar várias coisas interessantes:
O funcionamento do algoritmo, que leva em conta a classe dos k exemplos mais próximos à nova instância, utiliza a contagem das classes para definir a classe do novo exemplo. Ou seja, se o número k é igual a 3, e à um ponto verde existem 2 pontos da classe vermelha e 1 ponto da classe azul, então o algoritmo irá classificar o novo ponto como pertencente à classe vermelha.

Além disso, pode-se notar que caso o hiperparâmetro do algoritmo, o valor de k, não esteja corretamente configurado, o algoritmo pode classificar erroneamente.
Neste exemplo, suponha-se que o ponto verde pertence à classe azul.

Ao aplicar o algoritmo, caso o valor de k fosse 3 o algoritmo classificaria o ponto verde como sendo da classe vermelha, entretanto este ponto é da classe azul.
Logo, é de suma importância definir o valor de k


## Árvores de decisão

Uma árvore de decisão é utilizada para classificação de um data-frame e esta é separada em raiz, nós internos, ramos e folhas.

A árvore vai se ramificando de acordo com condições, testadas a cada camada, até chegar nas folhas (nós finais), que mostram qual classe se encaixa nas condições testadas.

A parte mais difícil na montagem de uma árvore de decisão é encontrar os nós que se encaixam em cada posição e para isso, deve se calcular o gini, a entropia, a profundidade e o número de amostras mínimas para dividir a folha.

Exemplo de árvore de decisão:

![image](https://user-images.githubusercontent.com/91696970/236006549-c03785bd-b0af-4540-b6c7-896dfa4bcb59.png)


## Treinamento dos modelos

O Aprendizado de Máquina Supervisionado consiste em treinar o modelo com dados do conjunto de dados para que este consiga aprender e então, com esse aprendizado, classificar novas instâncias da forma mais correta possível.

Entretanto, existem dois tipos de problemas que podem ser gerados na hora do treinamento do modelo.

OverFiting: Quando o modelo está tão ajustado aos exemplos do conjunto de treino que quando tenta classificar instâncias do conjunto de testes acaba classificando errado

UnderFiting: Isto ocorre quando o modelo não é capaz de encontrar meios para relacionar as variáveis, e dessa forma o treinamento não ocorre. Caso isto aconteça, ou o conjunto de dados não é informativo ou o modelo foi projetado de forma incorreta

Dessa forma, é importante particionar os dados em treinamento e teste, para que o modelo possa ser construído de forma que este consiga classificar corretamente as novas instâncias.

A técnica empregada para testagem foi a Cross-Validation

### Cross-Validation





O Cross-Validation é uma técnica utilizada para realizar o treinamento do modelo, e testar se este treinamento gerou um modelo que prediz corretamente as instâncias.

Este processo consiste em dividir o conjunto de dados em dois subconjuntos: treinamento e teste, como é feito na maioria das técnicas de testagem. Entretanto, esta técnica particiona os dados de treinamento em k folds, este valor representa que k-1 folds serão usados para treinamento e 1 fold será usado para testagem

Este processo se repete k vezes, em cada iteração 1 fold diferente é utilizado para testagem. Com a realização desta técnica é possível obter k métricas diferentes do modelo construído.

Ao final, o conjunto de testes inicial é utilizado para validar o modelo que já foi apurado

![image](https://user-images.githubusercontent.com/91696970/236006723-f90b5efe-7d05-49cf-958b-ab6790ccc476.png)

Após isso foi realizado a busca pelos hiperparâmetros dos algoritmos

### Grid-Search

No algoritmo utilizado, o valor de k é um hiperparâmetro do algoritmo

Dessa forma, é necessário definir este valor de forma cuidadosa, para que o não haja erro no funcionamento do algoritmo.

Uma maneira de realizar isto, para problemas de pequena escala, é realizar uma busca exaustiva, para encontrar o melhor hiperparâmetro.

Abaixo, esta busca é realizada, entretanto, além de se comparar diversos valores de k, também é levado em conta 4 distâncias diferentes:

Euclidiana
Manhattan
Chebyshev
Minkowski


Desta maneira, pode-se construir os gráficos que representam a acurácia obtida com a cross-validation para cada distância, abaixo, podemos ver para a distãncia Euclidiana e a Manhattan para difierentes valores de _k_



![Screenshot from 2023-05-03 12-13-36](https://user-images.githubusercontent.com/91696970/236007146-9cc8080b-22ca-4b3d-9f4d-2a1119731ff9.png)
![Screenshot from 2023-05-03 12-13-49](https://user-images.githubusercontent.com/91696970/236007149-11c41e22-d1b0-45e1-a338-57f580212e83.png)


## Treinamento modelo final

Após a definição dos hiperparâmetros foi realizado o treinamento final segudia da predição para ambos algoritmos utilizando os parâmetros encontrados e dessa maneira, pode-se realizar a visualização dos resultados.


# Resultados

Para realizar a avaliação do modelo, decidimos utilizar a matriz de confusão
A matriz de confusão consiste numa tabela que mostra as frequências de classificação para cada classe do modelo, conforme a imagem abaixo



![image](https://user-images.githubusercontent.com/91696970/236007575-4701ffb5-2147-4cbc-9c52-aa89e3518987.png)


Com isso, os seguintes resultados foram obtidas:

## kNN

Para o kNN o modelo funcionou muito bem para prever a classe negativa (96% de acerto) mas para a classse negativa não conseguiu desempenhar tão bem (36% de acerto). Isso provavelmente se da pelo fato da presença de outliers que não foram tratados neste projeto, e que deveriam ter sido verificados para evitar este tipo de problema.

![image](https://user-images.githubusercontent.com/91696970/236007694-6dcdf48a-2012-467e-95ab-79bebcda60d8.png)


## Árvore de Decisão

Para a Árvore de decisão o modelo funcionou melhor para prever a classe positiva embora ainda não foi tão eficiente, obtendo um pouco mais de 50% e acerto para esta classe, enquanto os acertos para a classe negativa continuaram altos.

![image](https://user-images.githubusercontent.com/91696970/236007722-afc80685-fc09-4994-b8e9-0d6e2ab45e32.png)

# Conclusão

Ao fim da análise, encontrou-se dois valores de acurácia para os modelos testados (KNN e Árvore de Decisão).

Para o modelo do KNN, a acurácia encontrada foi de aproximadamente 77.16%.

Para o modelo da Árvore de Decisão, a acurácia encontrada foi de aproximadamente 82.10%.

A matriz de confusão do KNN mostrou que o modelo não se mostrou um modelo tão eficiente para lidar com este conjunto de dados.

Já a Árvore de Decisão, se mostrou um modelo mais eficiente para lidar com o conjunto de dados selecionado, visto que alcançou melhores resultados, e previu mais resultados corretamente.

Dessa forma, conclui-se que a Árvore de Decisão é um modelo melhor para ser utilizado neste conjunto de dados.

# Colaboradores

Augusto Luchesi Matos
Carlos Eduardo Nascimento dos Santos
Gabriel Meirelles Carvalho Orlando

