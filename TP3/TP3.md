# Trabalho Prático 3 - Resolução

## 1\. TOR (The Onion Router)

### Pergunta P1.1

#### 1.
Ao efetuar o comando ``sudo anonsurf start`` não conseguimos garantir que estamos nos EUA.

#### 2.
Ao estabelecer uma comunicação TOR, o OP salta de circuito para circuito em intervalos de 1 minuto. Para este circuito, o OP necessita de, por norma, 3 OR acordando uma chave simétrica com cada um deles. Note-se que o OP não tem poder de escolha em relação a estes OR, uma vez que estes são fornecidos, de forma aleatória, por um Directory Server. Assim sendo, sabemos quais as localizações que os circuitos abragem, mas não podemos escolher estar numa, isto porque o TOR garante anonimato ponto a ponto, ou seja, quando o OP estabelece os circuitos não tem controlo sobre os OR que formarão esse circuito, pelo que é impossível saber, após estabelecimento de um circuito, qual o OR ao qual o OP se vai ligar.

### Pergunta P1.2

#### 1. Acedendo a https://www.facebookcorewwwi.onion/ obteve-se o seguinte circuito:

![circuito](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP3/pergunta1_2.png)

#### 2.

Os seis saltos servem para existir anonimato tanto do lado do utilizador como do servidor, os primeiros três servem para garantir o anonimato do utilizador, para tal faz uso de três OR que são proporcionados pelo Directory Server para o utilizador se conectar ao servidor. Os ultimos três são aos OR atribuídos pelo OP de destino.

#### 2. Analisando a imagem acima, observa-se que existem 6 "saltos" até ao site Onion, sendo que 3 deles são "relay". Isto deve-se ao facto de se estabelecerem pontos *rendezvous*, estes pontos servem de suporte à disponibilização de serviços anónimos. Permitindo que tanto o OP que acede ao serviço como o OP que é acedido sejam anónimos.

Deste modo, a existência destes 6 "saltos" devem-se a: (suponhamos que a Alice é a entidade que pretende aceder a um determinado serviço web e a Bob é esse mesmo serviço)

> Bob gera um par de chaves de longo tempo para identificar o seu serviço Web, sendo a chave pública o identificador do serviço;

> Bob escolhe alguns pontos de introdução e anuncia-os no Directory Server, assinando o anuncio com a sua chave privada;

> Bob cria um circuito TOR para cada um dos pontos de introdução e pede-lhes para esperarem por pedidos.

Depois de criado o circuito TOR, acontece o seguinte:

> Alice sabe da existência do serviço XYZ.onion e acede aos seus detalhes (chave pública e pontos de introdução) no TOR através do Directory Server;

> Alice escolhe um OR como ponto de rendezvous (RP) para a conexão com o serviço ao qual o Bob quer aceder;

> Alice constrói um circuito TOR até ao RP e fornece-lhe um “rendezvous cookie” (segredo aleatório único) para posterior reconhecimento do serviço web;

> Alice abre um stream anónimo até um dos pontos de introdução e fornece-lhe uma mensagem (cifrada com a chave pública do serviço web) com informação sobre o RP, o “rendezvous cookie” e o inicio de troca de chaves Diffie-Hellman. O ponto de introdução reencaminha a mensagem para o serviço web através do circuito TOR criado nos passos anteriores.

Por fim,

> Se o Bob pretender falar com a Alice (OP), este cria um circuito TOR até ao RP e envia o “rendezvous cookie”, a segunda parte da troca de chaves Diffie-Hellman e um hash da chave de sessão que agora partilha com a Alice;

> O RP conecta o circuito da Alice com o circuito do Bob (normalmente o circuito consiste de 6 OR: 3 escolhidos por Alice sendo o terceiro o RP e, outros 3 escolhidos por Bob). Note-se que o RP não consegue reconhecer Alice, Bob nem os dados que transmitem;

> Alice envia uma célula de relay begin através do circuito que, ao chegar ao OP de Bob, conecta com o serviço disponibilizado pelo Bob;

> Um stream anónimo foi estabelecido e Alice e Bob comunicam da forma normal num stream TOR.
