# Trabalho Prático 5 - Resolução

## 1. Blockchain

### Pergunta 1.1

Com o intuito de na criação do Genesis Block, o timestamp ser a data do dia de hoje e o dado incluído nesse Bloco ser "Bloco inicial da koreCoin", efetuaram-se algumas alterações no código disponibilizado. O código alterado encontra-se na diretoria P1_1.

### Pergunta 1.2

## 2. Proof of Work Consensus Model

### Pergunta 2.1

### Pergunta 2.2

1. Na experiência anterior, o algoritmo de "proof of work" utilizado é: dado o último valor que resolveu o puzzle incrementá-lo de modo a obter-se, simultaneamente, um múltiplo de 9 e desse mesmo número.

2. O algoritmo implementado não parece ser o mais adequado, uma vez que não é possível definir o grau de dificuldade da resolução do puzzle (tal como se pode fazer no código analisado na pergunta anterior), pois o número de prova para a resolução do puzzle vai sendo cada vez maior e, como tal, vai sendo cada vez mais difícil encontrar um número múltiplo de 9 que seja também múltiplo do número de prova. 
