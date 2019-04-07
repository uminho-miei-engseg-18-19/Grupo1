# Trabalho Prático 4 - Resolução

## 1\. RGPD (Regulamento Geral de Proteção de Dados)

#### Pergunta P1.1

Quando falamos em princípios relativos ao tratamento de dados pessoais temos que ter alguns aspetos em conta. Sempre que se procede a uma recolha de dados, estes devem ter uma causa definida e efetiva para o qual são recolhidos, ou seja, não é permitido que sejam recolhidos dados sem uma razão de causa, para além disso, estes devem ser tratados de forma lícita, coerente e transparente no que diz respeito ao titular dos mesmos.

Os dados devem ser conservados apenas durante o tempo necessário para o intuito ao quais foram recolhidos. Por exemplo, uma empresa não deve guardar dados de clientes que já não têm qualquer relação com a mesma, ocorrendo exceções em caso de interesse público, fins de investigação científica ou histórica, ou também para possíveis fins estatísticos. 

Quem quiser realizar um tratamento de dados deve garantir que existem medidas para realizar tal tratamento de forma segura, incluindo tanto a proteção contra tratamentos não autorizados como contra uma possível perda dos mesmos, destruição ou danificação acidental, para tal devem ser adotadas medidas técnicas adequadas afim de garantir a integridade e confidencialidade dos mesmos.

Deve sempre ter-se em conta o aspeto de minimizar os dados quando os recolhemos, ou seja, quem planear realizar um tratamento de dados tem de assegurar que só registam e tratam os dados pessoais estritamente necessários para cada fim estipulado.

Devem também ser garantidas formas de verificar a veracidade dos dados e que eles se encontram atualizados devendo ser tomadas sempre medidas pertinentes no âmbito de evitar dados imprecisos. Por exemplo, se uma empresa realizar um tratamento de dados, a mesma deve periodicamente garantir a atualização dos mesmos.


#### Pergunta P1.2

A pseudonimização é uma técnica para codificar dados pessoais e diminuir algumas das obrigações do RGPD. Deste modo, os data controller podem estabelecer os seguintes objetivos:

D1: a partir do pseudónimo não deve ser possível, para um terceiro, reidentificar o indivíduo ao qual aquele pseudónimo diz respeito;

D2: não deve ser trivial, para qualquer terceiro, reproduzir os pseudónimos.

Analisemos algumas técnicas utilizadas na pseudonimização. Comece-se pelas técnicas baseadas em funções de hash: hashing without key, hashing with key e hashing with salt.

As duas últimas técnicas baseiam-se na técnica hashing without key. Apesar das desvantagens desta técnica, note-se que o hashing pode ser uma ferramenta útil para suportar a precisão dos dados, uma vez que as funções de hash permitem verificar a integridade dos dados e autenticar uma dada entidade.

No entanto, criar pseudónimos recorrendo ao hashing simples de dados identificativos tem grandes desvantagens, uma vez que inputs iguais originam o mesmo output, não se verificando as propriedades D1 e D2.

Por outro lado, no hashing with key ou salt, inputs iguais já não originam os mesmos outputs, pelo que as propriedades D1 e D2 são verificadas. Isto deve-se ao facto de se usar uma chave ou um salt. Esta técnica é, normalmente, aplicada quando o data controller precisa de rastrear os indivíduos sem, no entanto, armazenar os seus identificadores iniciais.

Na técnica hashing com “salt”,, a utilização de “salts” para a proteção das funções de hash apresenta algumas desvantagens, uma vez que os “salts” são armazenados em conjunto com os valores de hash correspondentes.

A aplicação da criptografia simétrica aos dados identificadores de um dado indivíduo é também uma técnica eficiente na derivação de pseudónimos. Esta técnica é geralmente utilizada nos casos em que um data controller precisa de rastrear os dados e conhecer os identificadores iniciais.

É também possível recorrer a criptografia assimétrica para derivar pseudónimos, no caso em que o data controler pretende que a entidade autorizada a executar a pseudonimização não seja a mesma que está autorizada a realizar a reidentificação e quando pretende gerar pseudónimos diferentes para o mesmo indíviduo.

Uma outra abordagem interessante é permitir que os utilizadores participantes gerem os seus próprios pseudónimos, mantendo-os na sua posse. No entanto, trata-se de uma técnica que não é trivial e que tem alguns problemas associados. 

A tokenização é outra técnica de pseudonimização. Trata-se de um processo em que os identificadores dos titulares de dados são substituídos por valores gerados aleatoriamente. É, no entanto, uma técnica difícil de implementar e, portanto, as técnicas baseadas em funções de hash e as técnicas criptográficas podem ser preferíveis, relativamente à redução da complexidade e do armazenamento.

Por fim, existem ainda outras abordagens para a criação de pseudónimos, nomeadamente, o masking, o scrambling e o blurring.

O masking refere-se ao processo de ocultar parte do identificador de um indivíduo com caracteres aleatórios ou outros dados. Por outro lado, o scrambling refere-se a técnicas gerais para misturar ou ofuscar as identidades. No entanto, ambas as técnicas são fracas na derivação de pseudónimos, pelo que o seu uso não é recomendado como uma boa prática no processamento de dados pessoais.

Relativamente ao blurring trata-se de uma técnica que visa utilizar uma aproximação dos valores dos dados, de modo a reduzir a precisão dos mesmos, reduzindo a possibilidade de identificação dos indivíduos.


#### Pergunta P1.3

1. Para avaliar se um processamento de dados pessoais vai ou não resultar num risco elevado são usados os 9 critérios listados abaixo:
- Evaluation/Scoring - Inclui avaliação dos perfis e definição de cada um dos aspectos relacionados com os perfis.
- Automated-decision making with legal or similar significant effect - toma decisões automáticas perante determinadas características do perfil
- Systematic monitoring - 
- Sensitive data or data of highly personal nature
- Data processed on a large scale
- Matching or combining datasets
- Data concerning vulnerable data subjects
- Innovative use or applying new techonological or organisational solutions
- Improvement recommendations

[ver](http://www.sec-geral.mec.pt/sites/default/files/recomendacao_003_sgec.pdf)

#### Pergunta P1.4
