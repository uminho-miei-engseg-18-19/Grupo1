# Trabalho Prático 8 - Resolução

## 1. Buffer Overflow

#### Pergunta P1.1

Executando o mesmo programa escrito em Java (LOverflow2.java), Python (LOverflow2.py) e C++ (LOverflow2.cpp), obtêm-se os seguintes resultados:

![Java](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP8/P1_1/javaP1.png)

<p align="center">
  Java
</p>

![Python](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP8/P1_1/pythonP1.png)

<p align="center">
  Python
</p>


![C++](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP8/P1_1/cP1.png)

<p align="center">
  C++
</p>

Analisando o programa verifica-se que este começa por criar um *buffer* de tamanho 10 e recebe como input o número de números que queremos inserir nesse *buffer*. No entanto, ao executar o programa nas diferentes linguagens este comporta-se de forma distinta.

Note-se que quando executado em Java ou em Python, o comportamento do programa é análogo, pelo que a descrição do que acontece serve para ambas as linguagens. Tanto em Java como em Python, quando se insere um input que seja superior a 10, por exemplo 12, ao tentar escrever o 11º número no *buffer*, o programa dá erro uma vez que se está a tentar escrever numa posição da memória que não pertence ao *buffer*.

Por outro lado, quando executamos o programa em C++ o mesmo não se verifica. Verifica-se que ao se inserir o valor 12 como input, o programa permite que sejam inseridos 12 números, sendo que os primeiros 10 números são escritos no *buffer* e os restantes subrescrevem a memória adjacente ao *buffer*.
