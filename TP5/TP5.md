# Trabalho Prático 5 - Resolução

## 1. Blockchain

### Pergunta 1.1

Com o intuito de na criação do Genesis Block, o timestamp ser a data do dia de hoje e o dado incluído nesse Bloco ser "Bloco inicial da koreCoin", efetuaram-se algumas alterações no código disponibilizado. O código alterado encontra-se na diretoria P1_1.

### Pergunta 1.2

## 2. Proof of Work Consensus Model

### Pergunta 2.1

![Dificuldade2](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP5/P2_1/P2_1_dificuldade2.png)
*<center> Dificuldade 2 </center>*

![Dificuldade3](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP5/P2_1/P2_1_dificuldade3.png)
*<center> Dificuldade 3 </center>*

![Dificuldade4](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP5/P2_1/P2_1_dificuldade4.png)
<center> Dificuldade 4 </center>

![Dificuldade5](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP5/P2_1/P2_1_dificuldade5.png)
<center>* Dificuldade 5 *</center>

Analisando os resultados obtidos, conclui-se que à medida que se aumenta a dificuldade, o tempo de resolução do puzzle aumenta, o que era de esperar, uma vez que com o aumento da dificuldade, aumenta também a dificuldade de resolução do puzzle.

### Pergunta 2.2

1. Na experiência anterior, o algoritmo de "proof of work" utilizado é: dado o último valor que resolveu o puzzle incrementá-lo de modo a obter-se, simultaneamente, um múltiplo de 9 e desse mesmo número.

2. O algoritmo implementado não parece ser o mais adequado, uma vez que não é possível definir o grau de dificuldade da resolução do puzzle (tal como se pode fazer no código analisado na pergunta anterior), pois o número de prova para a resolução do puzzle vai sendo cada vez maior e, como tal, vai sendo cada vez mais difícil encontrar um número múltiplo de 9 que seja também múltiplo do número de prova. 
