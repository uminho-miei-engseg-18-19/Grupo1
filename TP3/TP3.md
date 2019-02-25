# Trabalho Prático 3 - Resolução

## 1\. TOR (The Onion Router)

### Pergunta P1.1

#### 1.
Ao efetuar o comando ``sudo anonsurf start`` não conseguimos garantir que estamos nos EUA.

#### 2.
Ao estabelecer uma comunicação TOR, o OP salta de circuito para circuito em intervalos de 1 minuto, que estão pré-estabelicidos. Para este circuito, o OP necessita de, por norma, 3 OR acordando uma chave simétrica com cada um deles, sendo que o OP não tem poder de escolha em relação a estes OR, que são fornecidos por um Directory Server. Assim sendo, sabemos quais as localizações que os circuitos abragem, mas não podemos escolher estar numa.
