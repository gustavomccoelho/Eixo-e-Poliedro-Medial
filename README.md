# Eixo e Poliedro Medial

Criação de um algoritmo para definição do Eixo Medial de um polígono convexo

## Objetivo

O objetivo deste trabalho é detalhar os procedimentos teóricos e práticos para a definição do eixo medial de um polígono convexo. Em seguida, o conceito será estendido para a definição do poliedro medial. Além do detalhamento do processo de construção, ao final também será feita uma análise do tempo de execução do algoritmo. 

## Método e implementação
O algoritmo de definição do eixo medial de um polígono convexo se inicia calculando a bissetriz de cada um dos vértices do polígono. Isso é feito considerando o vértice em questão (v), o vértice à esquerda (v-1) e o vértice à direita (v+1), como mostrado abaixo:

![Bissetriz](/pictures/Bissetriz.png)

Ou seja, a bissetriz é calculada a partir da soma dos vetores unitários formados pelos vértices adjacentes.  

Em seguida, calculamos, para cada vértice, a intersecção entre sua bissetriz e a bissetriz do vértice seguinte. Para isso consideramos o problema de intersecção entre duas retas definidas pelas bissetrizes. A primeira bissetriz é formada pelos pontos p_11  e p_12, enquanto a segunda, pelos pontos p_21   e p_22. Definindo as equações das respectivas bissetrizes, temos: 

![Calculo_1](/pictures/Calculo_1.PNG)

Ou seja, o problema se resume a duas equações de duas incógnitas que é facilmente resolvida usando o Teorema de Laplace. É importante enfatizar que, como o polígono é convexo, a intersecção certamente ocorrerá dentro do polígono. 

Definida a intersecção, o próximo passo se resume em calcular a distância da intersecção para a aresta formada pelos vértices usados na intersecção. Esse é um problema análogo ao problema da definição entre um ponto e uma reta. Consideramos o ponto p e uma reta formada pelos pontos A e B, como ilustrado abaixo.

![Distancia](/pictures/Distancia.png)

Se considerarmos o vetor (V)=(O-P), a distância a ser definida é igual ao seu módulo. Portanto, a solução do problema se resume em definir o ponto O. Sabemos que O pertence à reta formada por A e B e sabemos que o vetor V é ortogonal à reta. Portanto, temos as seguintes relações:

![Calculo_2](/pictures/Calculo_2.PNG)

O ponto O é então definido desenvolvendo as duas equações de duas incógnitas, e a distância definida através do módulo de (O-P). O algoritmo realiza este cálculo para cada vértice e encontra o vértice que define o menor valor para esta distância. 

O vértice escolhido então forma a primeira aresta do eixo medial, usando o segmento de reta definido pelo próprio vértice e o ponto de intersecção calculado anteriormente. O mesmo é feito para o vértice adjacente, definindo a segunda aresta do eixo medial. Em seguida, a aresta do polígono original formada pelos vértices adjacentes em questão é removida e os vértices são estendidos, formando um novo vértice virtual. A definição do ponto virtual é feita de forma análoga ao problema de definição da intersecção entre duas retas, como já feito no caso da intersecção entre bissetrizes. Neste caso, mais uma vez nos aproveitamos da característica convexa do polígono para garantir que a intersecção irá ocorrer fora do polígono original. 

Esses passos são repetidos até que o polígono tenha apenas 3 vértices, como ilustrado na figura abaixo. 

![Eixo_Medial](/pictures/Eixo_Medial.png)

O poliedro medial é feito de maneira análoga ao eixo medial. Porém, o valor da terceira dimensão para os pontos de intersecção é definido como suas distâncias até a aresta definida pelos vértices adjacentes. O resultado é mostrado na figura abaixo.

![Poliedro_Medial](/pictures/Poliedro_Medial.png)

Em relação ao tempo de execução, espera-se que o algoritmo seja da ordem O(n^2), onde n é o número de vértices do polígono original. Isso porque o cálculo das bissetrizes, intersecções e distâncias da arestas às intersecções é feito para todos os vértices em cada iteração, que é também proporcional ao número de vértices. O tempo real de execução para vários tamanhos de entrada é mostrado no gráfico abaixo.  

![Runtime](/pictures/Runtime.png)

Como visto, o tempo de execução se aproxima do esperado. Uma possível forma de diminuir o tempo de execução seria no uso de uma lista de prioridade, reduzindo a complexidade para a ordem deO(n log⁡n). 
