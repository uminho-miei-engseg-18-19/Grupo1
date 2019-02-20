# TP2 - Resolução

### 1\. Assinaturas cegas (_Blind signatures_) baseadas no Elliptic Curve Discrete Logarithm Problem (ECDLP)

#### Pergunta P1.1

Os ficheiros com as respetivas alterações encontram-se guardados na pasta TP2.

### 2\. Protocolo SSL/TLS

#### Pergunta P2.1



### 3\. Protocolo SSH

#### Pergunta P3.1

*Universidade de Aveiro*

1. *[Resultados](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP2/Pergunta3/mmlog.fis.ua.pt.md)*
2. *Software e versão utilizada:* OpenSSH 7.2p2

*Universidade do Minho*

1. *[Resultados](https://github.com/uminho-miei-engseg-18-19/Grupo1/blob/master/TP2/Pergunta3/193.137.11.59.md)*
2. *Software e versão utilizada:* OpenSSH 6.7p1

**Discussão dos resultados obtidos**

Avaliando as versões de software relativas aos sites utilizados, conclui-se que a versão *OpenSSH 7.2p2* é a que apresenta maiores vulnerabilidades. Esta versão apresenta 6 vulnerabilidades, enquanto a versão *OpenSSH 6.7p1* apresenta apenas 6.

Analisando o CVSS score de ambos os softwares em análise, conclui-se que a versão *OpenSSH 7.2p2* é a que apresenta a vulnerabilidade mais grave, apresentando uma vulnerabilidade com *CVSS score* de 7.8.

A vulnerabilidade apresentada consiste no facto da função *auth_password* contida em *auth_passwd.c* não limitar o tamanho da *password* autenticada, o que pode levar à negação de serviço (crypt CPU consumption).
