# Trabalho Prático 9 - Resolução

## 1. Injection

#### Pergunta 1.1 String SQL Injection

1.
No sítio pedido no WebGoat, colocámos últimos nomes, como _Smith_, _Green_, _Snow_, etc, verificando se existiam ou não na base de dados. Exisitindo, obtivemos informações sobre _user_id_, _cc_type, cc_number_, etc.

2.
Utilizando a tautologia 1=1, exacutámos o ataque de _SQL injection_, obtendo, como pedido, informação sobre todos os cartões de crédito.
![pergunta 1.1](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP_9/pergunta1.1.png)

#### Pergunta 1.2 Numeric SQL Injection

Através da ferramenta **Inspector** no Firefox, procurámos as linhas onde estavam as diferentes _stations_, alterando o valor relativo a Columbia para "101 or 1=1".
![pergunta 1.2](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP_9/pergunta1.2.png)
