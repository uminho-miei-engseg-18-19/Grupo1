## Exercícios

### 1\. Números aleatórios/pseudoaleatórios

#### Pergunta P1.1

Para a resolução desta pergunta é necessário começar por definir a diferença entre `/dev/random` e `/dev/urandom`.


Executando os diferentes comandos no terminal observamos que quando executamos as 3 primeiras instruções o tempo de resposta aumenta consoante o número de _bytes_ que pretendemos gerar. Isto acontece, uma vez que a entropia necessária para gerar 1024 _bytes_ pseudoaleatórios é superior à entropia necessária para se gerarem 32 ou 64 _bytes_ pseudoaleatórios. É também de notar que enquanto não existir entropia suficiente para gerar o _output_, o mesmo fica a aguardar até que seja gerada entropia suficiente para concluír o mesmo.

Relativamente ao comando: `head -c 1024 /dev/urandom | openssl enc -base64`, este permite-nos obter de modo quase instantâneo 1024 _bytes_ pseudoaleatórios, isto deve-se ao facto de quando o `/dev/urandom` não tem entropia suficiente para gerar o _output_ de tamanho pretendido, ele gera uma _seed_ com a entropia disponível, e a partir da mesma usa um **PRNG** para gerar o restante output.

Na seguinte tabela são apresentados os tempos que cada comando demorou até ser concluído

| Comando  | Tempo execução |
| ------------- | ------------- |
| head -c 32 /dev/random \| openssl enc -base64 | 0.005s
| head -c 64 /dev/random \| openssl enc -base64 | 0.006s
| head -c 1024 /dev/random \| openssl enc -base64 |
| head -c 1024 /dev/urandom \| openssl enc -base64 | 0.006s


#### Pergunta P1.2

A package _haveged_ é um gerador de números pseudoaleatórios, tendo sido criada com o objetivo de colmatar as condições de baixa entropia no dispositivo aleatório do _Linux_. Deste modo, após a instalação da package _haveged_ e executando os comandos propostos, observou-se que a geração de 1024 _bytes_ aleatórios recorrendo aos comandos:

- `head -c 1024 /dev/random | openssl enc -base64`
- `head -c 1024 /dev/urandom | openssl enc -base64`

ocorre em tempos muito semelhantes e no caso de `/dev/random` o tempo de execução é bastante mais baixo.


| Comando  | Tempo execução |
| ------------- | ------------- |
|head -c 1024 /dev/random \| openssl enc -base64 | 0.007s
|head -c 1024 /dev/urandom \| openssl enc -base64 | 0.006s


#### Pergunta P1.3

**1.**
Analisando o ficheiro *generateSecret-app.py* baseado no módulo _eVotUM.Cripto_ observa-se que este para gerar os _bytes_ pseudoaleatórios recorre ao módulo *shamirsecret.py*.

```python
def generateSecret(secretLength):
    """
    This function generates a random string with secretLength characters (ascii_letters and digits).
    Args:
        secretLength (int): number of characters of the string
    Returns:
        Random string with secretLength characters (ascii_letters and digits)
    """
    l = 0
    secret = ""
    while (l < secretLength):
        s = utils.generateRandomData(secretLength - l)
        for c in s:
            if (c in (string.ascii_letters + string.digits) and l < secretLength): # printable character
                l += 1
                secret += c
    return secret
```
Analisando o código relativo ao método _generateSecret()_ observa-se que para gerar a sequência de _bytes_ este inicia um ciclo que será executado enquanto o número de _bytes_ não for atingido. Neste ciclo é criada uma variável _s_ que é construída apartir do módulo _utils_, que faz uso do comando _urandom_. A variável _s_ contém caracteres imprimíveis e caracteres não imprimíveis. Assim, o _output_ do programa _generateSecret-app.py_ contém apenas letras e dígitos, uma vez que os únicos caracteres aceites para a contrução do _output_ têm de pertencer a `string.ascii_letters` ou `string.digits`.


Executando o programa obtém-se o seguinte _output_:

```python
python generateSecret-app.py 1024
JR2uivKXiFjQ4raZfCnRrugxL0CuJYcXAL3hRXWUK4OAebG3ySH1sRHjIpAKFpvHg9cgbNojw4FxOSfhcacFPup7QTMeys0UJR8pUNM3I1JIQghol7UhRg6o7HU0e1fsUcJ98E9FCbKaPGymvinyvIMCyGFwXhSvR0AfMOHCCrKzQ1UtSsP4o3vuw0jg8et1J0W5U7ofCDIw5owzeLFzcaJ7Q0EhP8DoKQyHlGd5P9Uj50W4w5BBZAQU7D31WPAH0EQbYjuRKsqX1KT1ajtvqAYpXob4EYZRfVz6A4d7S6yVk72OZChYS2QVmQjiyjOC27wfFi1YxhkEBe1k8lV5VA0pSBoasMsxwpxMXNgO5NdVvlImZNZyi4U2YncYGUTH4CB6VcF1GjQP5ab4GiAPsTlQBUzwWZzPIj1yAcWIyjCqT3dsN3YCXOBqx6KPSxYmfcQaGDgp5xBDbkyKtATkakT2MwwXStQGkf2sQktEHCJAqNDuy09C2xNBUZFQeElOpFXH0fDCFtIA7saZzCE6DDhThl4t5BNDq3Xmv6ERep7sxAwikabSlNJASepy90qA9b8GUQOnsbYBXdGSu96CRz9S8B876ZzD4fETH3csQc1h7bBxH8sO44iRAWoiAslwuh2OxJoEXgM724DI6OdJjSb19RBbP7D9LfCgLUUslSr2GDG4k9d405TJZtdNBEUqzYXmcYBsGH4PiG5hZrO1bZ6eDYPsWXJ9nG8PWX7qbkBWCyI3f19cRx0oqG85Is2V1olW3y65xQRRqIzhZMIgK2ROG6eo2NoWXLb3WA3ZH9QjfZjZwqfnJ3ZudpswX90SHiRewAJ8oNGqmUDPwNd5gtex2nX71NUDH4fSNirDNZOsDWjDXMYU9btCa6SL7EXju35TChV9EOe0B6m7GOtuv40g186jEWLCyYz8VhgLRBgJXxOVJUwPz8r5I0mUASWaeRbje3xNSXSOhLj33FOR5e8XhZxkUhhuu6X2ita08jwLeOw5FVs2N4OS96wFtrXJ
```

**2.**
Para não limitar o _output_ a letras e dígitos é necessário fazer uma alteração ao código, por exemplo basta adicionar `string.punctuation` de maneira a que c possa também ler símbolos de pontuação. Ou seja o código passa a ser o seguinte:

```python
def generateSecret(secretLength):
    """
    This function generates a random string with secretLength characters (ascii_letters and digits).
    Args:
        secretLength (int): number of characters of the string
    Returns:
        Random string with secretLength characters (ascii_letters and digits)
    """
    l = 0
    secret = ""
    while (l < secretLength):
        s = utils.generateRandomData(secretLength - l)
        for c in s:
            if (c in (string.ascii_letters + string.digits + string.punctuation) and l < secretLength): # printable character
                l += 1
                secret += c
    return secret
```

Executando de novo programa com as alterações realizados obtém-se o seguinte _output_:

```python
python generateSecret-app.py 1024
:1`3/nb2;ITKrBIEi*A{4UEl,1u"@xiifR,%NSkEH{WDOVjIpJ![o36{dOe5rx&N[nmKwi=|R^l4=_IO*Fc[}1D1v6[0G)K*zOLb<~Vud-Y2g9x<KA2,rV;O2>#amkBK909rd:C)XXQ"Wljog[xGgll2JUk#`9KXeXC`N*)(QVX`qdAd[3P&RlyH!vmzl?yZf<%oq6",}WhXb%N4p8F/.Eejh2^]B/Oo,j70K'`QPl$Sp{;oU^!eE01JYchGE*tE<Y/>H<2JUy"Jj6^kzZ}"1Ob8qBJp\W-q[f<V?Gslq7*)MbPt7=GmhSD7^Yrr,M|~>H('anH6jUb5"0S<^~A?^EUioB\a5,1"ovG6Q),.tM-M'mnc)gWr!-hml/E%9HXdo<8R-t90)!ej>{fJ])0~q1UjtwUQ]e/n"lXLI5MB802]<1%b@m.G_T7#L\Hn~K+mpi0[NFcw@>;f_*kSI|zJx!ObW}cfqIo_.Y6i[4_|n~YZ^^m?a]/^dR+Q>oKH8G]2~D`U5AqN:W/JGQU(H9Zko?re]cY|$BlveX\+dJFB\=u}JD|=1A|r=W.Ol.F>&M<J^+OYkY<JaV!zt9@=}..PRMF)\p>JIS5LgRG_z]pOVcB6b?A[DVBNPdPF+}e[Kh&j+,&6B6:g)h>A/]oroRR5:I|8N3]Fl{X:')K,O-8PWNR7.4SI\^;BC(f6b]mzX~IA1k6u?/L@6S<4IX1)9{IJBkbNZ05KZpHf|De1j[[cnfEn0t}01%%+>ZKL_0\#6wC/$A8v)|\ii1Y7.<jsEsN)bvn+MCYbgk_83W{mrU,7M?Gg?CJ$Z2x-rEC8Exx&^Ze)MN,!)1_U(_*i".7PD2,&<0];lS8%[yV%^,*SHAF?<To)`&ls5]$kPx!:"QlEt{;!9f[vUtZVkt.[+=}HI"y=kq1mYu({1E(U#eC!=Ed-F-[,VT1cCo~Ht2qq393C3MU+:SS"gg6Ua3?J6.6<^B_^E@2E5FJzu#=?S[-<Q0zA4[)A|c1ILJt!uV/"tDe%#d]F

```

Deste modo podemos ver que, o nosso _output_ já não se limita só a digítos e letras



### 2\. Partilha/Divisão de segredo (Secret Sharing/Splitting)

#### Pergunta P2.1

A

Para dividir o segredo *"Agora temos um segredo extremamente confidencial"* em 8 partes, com quorom de 5 começou-se por gerar a chave privada, usando o seguinte comando:

```
openssl genrsa -aes128 -out key.pem 1024
```
```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,A22B0DBE3DF7602DC4D7BF5C1CA06BE2

Kl4tqhGsD2zyU1SBRTzPN80LRHNiakebnZnpKd/RsZDGY3T6B+DDvFAaaWnD1px0
QzO+nTWU/qsaW5Cs8bj/4gmyhzwnF1qMSN9j+2LBOGa+Vy/nIYtJVsfcU/11oH+X
qWz6SuZM3udGuuzU2TDhnEmkvHywpOP80WXgmCIkjgI2pIP+t8CvZ08HHl5i+4Os
gbFBcpM9SMOAG5gn2J38AZnLpFZxBu6RwYAR9dBOVyMsKlIAUp66QniShO0nNJdg
wBcyYWv1BFre/F35+jWz08WQj/GseJso2BuBgoj3teCYx3R/tRWu+RNlEDNBtWWo
UAiixD1D1KWa/1npUCdD5pEfWY6ZKDY8MYdveVopc+GnSLSExxZhldFwGSCHPx+x
CpjbyqxZiMRfwAahFtEKStSNvzJgiuYK/ncb+fFxfVYRtfLBvlQnwClAQKkXBdIe
vSzaeY8qpv7cZ2ojSvuOySjoMZdOx7iCVqvU6oGkC+Mxcob5AxVThiiVxbP0YqIu
bIp2RI7Z/aqsqWrz8QYsgP3/OHwLqvw37ZDJzRPqnv4XQ8fGqKzkoJUNA5VYZ1iE
oGTQ3vaRVySLBFOS1a/WTBlnHCehuI+CtVa7DP6mkvAPhSXyplGBbJhN2xQsc+K3
WBy0DH0OWVVt2WkI93r/vc0AvBURwW0Apdksahl2lDgVZpMUy6kuZ+eBJtbu/Bp8
OJiqYJILQDeNc3V5m+sqmZRK+n5GuF5c2h35Ry+7I9SVtK3knF3NXoT6PqsPs7ds
CdEkvnWjq/49fyKd4vbEY3NcViWsT3fce5Vhh3TzOI5trZ1r4XTlRaKKfqef11sP
-----END RSA PRIVATE KEY-----
```

Uma vez gerada a chave, procedeu-se à divisão do segredo:

```
user@CSI:~/Aulas/Aula2/ShamirSharing$ python createSharedSecret-app.py 8 5 1 key.pem
Private key passphrase: olaola
Secret: Agora temos um segredo extremamente confidencial
Component: 1
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjEtZDVkYTdjMGQzN2UwNGJlM2ViNTQzMTAwY2ZlNWVlNWJjNzQ5MGZlNjU4NDI4YmQ1M2NiNzkzMWNmMzM5NDNmYTg2ZWMwZDE3ZGZkNTUzYWY3Nzg2NzI4NWUyOWJhZWVmIiwgIjEiLCA1LCA4LCAiNWE1YjhiNWRmNTNhMWIyOGQ3YTRlYmUxNjc4NWRiMjZmMWFmNjZmOWFmNWJmMjIyM2FkZWU2MzQ5YTA0ODAzZSJdfQ.PeZ-hregcV8jPnahkeS__hi_neUk-xelVs8WcrVoQkDx0wXIGcCZtWFbVjbLqeYaKMmm1Xog7qDzmSZWbXDkqi1Po-5yrKuccNE2LHqu0sts5mcMX2JqLsix3D0FD1RUAd_zc82aDg9HoIpVqxDhlyQQRdyC6PrJLT9AK2svddk
Component: 2
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjItMmZhZGI5ZjU5NzMxNGM0NDZhMDFiOGYxOWJkMjJmNjhhMDA3YjA5YzBlNTMyYjQ4YTAwMzRiYzQ4ZDNlMGFhYWY3NTkwMDJiZjE0MTA2MWM5NTdkZjIxZmUyZDY5MzQ0IiwgIjEiLCA1LCA4LCAiNmZkZDFkNGRlN2YxOTc3MGRiYTg5ZTE2ZmFiOTU0OTY1MGY0NWFlMWQyYTFmYTczMWNlMGRlNWYxYzNhODY4NSJdfQ.YHUZMfuK57vgr8Q_O7iztOnVjyLnhS2DM1KElA4mHb1SmCEtMdlSD55GLuL8XBOvMDb75rQSMpPG7p9kp8oqhlysk2de4JSsvpxDgJmOO547pT8P-UOQAV_rj2SwDRrXBsQjvAqXpFGNnJQgjEtCqx_8qga8FJftDnyFL2Pyhls
Component: 3
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjMtYTZiOTRmNTIxOWUxZDZlZTczZDUxMmJjZmE5YjdlMjYxZDdiOWNmNzEzNGQwNzFlYTRkNTQ1ZmNkOTJiMmI5YTVkYmVmYmUyZDY1NTVjZmJhMDMwZjE3OWY0N2RhOWFiIiwgIjEiLCA1LCA4LCAiMDVlNDM2MjE1MTY2N2E5NDFhNGNiMjYwNTljMWFkNjgwZGJjOTZkZmZhYTNlZDhkMzBhZGY3NDRkMmVkNThlYyJdfQ.O6wq9bF6BVeEE4iGG76CoglSjEFNAjeT6ZG3AnBMXV05opP9E-FevayCnT97h21V09LHjV-OI9ZtUMoNHF8IazM7Fuxho-0A3XX17cR49dv3sxSg_mKM4WiHpARiVW-2ovQT9L3mGFVO0A-l5SnCsBT12SeuvC-pxs27MFFEkMc
Component: 4
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjQtZGI4MGY0Zjc1ZDI2ODlmM2NlZjA2OGExNTQwOWQ3YjgzODZmMDY4NzMxMGJkOTk3NzRmMWU0YmIyN2NiNzY2YTM1YmJjZWU2YWI3Y2QzNDllMDhkMDkwZmYxY2ExMzU3IiwgIjEiLCA1LCA4LCAiYWQyNWRkNWIyYTgyZTBjZjQ4ZTY0YzQzNzg0MjdmNzQ5N2QzYTM2YmM3M2I0ZjExNDM3YmVlMmI5OGNiOGZlNiJdfQ.gXHDyHvFWmXMlghPnFoLdHeFVOzITotnhUqsydY26jGs3-1IlM5yXeNshGJGG18OdZV13PhHCGRhxU_S3R1y1h0CThpeA89pEroobS5G1_dPoGR3fhfUHiV3GcNtj2X902R2EO3AL8kY61OeW4rMVlko4FxjjtXxG8-m22DG-00
Component: 5
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjUtYjczM2Y2NjgwMDlhNDAxMDdkM2IwNzUxNTY0MzliZGFiNDllMDdmYjZlOWIwZWQ0NjE2NDQ0NDk3Y2Y5MjAzOWQ4ODc1OTA1NmFlOTg3YjQwYjg3NWM5YmZlY2E3YmYxIiwgIjEiLCA1LCA4LCAiYTVjYWY0ZDIxNmM2M2NkOTZhNTE2NzlkNjg5ZDkzMDY0Y2QwMzhjMTE4MjY5NzY3NTJhMDQ3YzYyMTVkOTU1MSJdfQ.EPhHSinkN_XpzgTLl0q57Ty8dMPdgYU7Z1RwANYJQnskcdVgqyow7ubtCD3eO-ty_iKt3TGjGAoHliW2ZTe7ir4ZPqRtETQ158wD4cPtr9og-WU8g8CRuwzPJ7xGZmnncGYr4oTeodZagYnlRCWWQZA0PWasMOzL2G8UQLo6Jgs
Component: 6
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjYtNmJhZDMxZDRhNjNlMTBhYWJjNjE1ZGYzZjVjZDhjZTEyMGI2YTUyMjEwMzVjNGQ3ZTI3ZTNhNDY4ZjlkYzNhNjdjZjM4YjMwZWM5NTNjOTY0MjFjOWIxNjg5NjMxOGIxIiwgIjEiLCA1LCA4LCAiZjgwOGRlYmMxMzJjNGFhNjMwMWZiYWExNDFjOGE0MGFlMjcwOTU1YTY2OWQyN2I1MjJjYWNlOGFhZDljOTA4OSJdfQ.hk8wcqCB9QpI0en9FYZc6fu3sRCPjzsqOgNQ_i3T9ZNpr79Jm9fK4rWYCEZRXWm13Og199tAMAqjDTXaaZti6ToYZLdNYTTfIgS-DC7WBTtRaHhPJ7e5flrFvP0mffXJ7LsUK1kwn0_9ZfsyfbHSO8Kd_KAAy6Sfwkg8fgZzTNE
Component: 7
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjctNzM3MzE4MWJmMjc5NGZkMzA1ZDRmZTI0NmQ4YWNmYjZkNjU4Y2FlODk3NDZjYjg1OTdkODU1YTVjOWIyNjBjYjM3NmM2NzdlZTY0MTU3ZmMxMTUwZmViNjQ5NGRhODVlIiwgIjEiLCA1LCA4LCAiYzY1NDFlNzRiMzg4NTM4Nzc0YjRiOWMwMWZlMTNmMzU4ZWJlNmM0NTE2MDE5MjdhMTU3ZjBkOGMwOWNkMDY0YyJdfQ.ldvYUcQ9mEhEnaxYfKm-xnmnWgTvIDCAQBkzsC0oWw9tTlKCTU20qS9pSUUl7xMdYXQHkKjEDtF-rGkTvYoLz0vR44uzRSJ9zdjRDOs5l0LoZYx7uQtLTsrKN_Kee4qinGtdiIAuNUoRdFprcEaDSWnsbNE2krxsrRIS9GmQvMw
Component: 8
eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjgtOTFiN2FjY2E4YzE5OGU0NDBlY2M5YmYyM2ViY2ViZGVmYTE2NGY1YmMyNjhhNGEyNDg1MWRlYWY0ODNmNWQ0MGY5ZjgwMTI4ZWI3NmUzYTA3MjMwNGNmMDQwMTk3MjY3IiwgIjEiLCA1LCA4LCAiYmY1N2FlMzNlYjg1ZWY5YWNlY2QzMDQ0MDZkZmE4OGJjZDQ5YWU5YzM3YzljN2I2Y2E5NTM5ZjhkMWFkMWZkYyJdfQ.XyXI85O-DbdF5ID1WiZmnKBB-952wbbm9impvtLsIb2LPPTs49IbMtZcjhsZXdzdXaOBi6pc6pgbjp8zMpaDPRnOgkxU3emzYK_wQl9x2dU_sMn1zBmEZG3A58_ARvDnCWduGATBi8Q7p7u56K0tEanGlfqCa3hnvj72UsgV938
```

B

Para recuperar o segredo houve a necessidade de construir o certificado associado à chave gerada, para isso efetuou-se o seguinte comando:

```
openssl req -key key.pem -new -x509 -days 365 -out key.cert
```
```
-----BEGIN CERTIFICATE-----
MIICezCCAeSgAwIBAgIJAPWz726Bg47zMA0GCSqGSIb3DQEBCwUAMFUxCzAJBgNV
BAYTAlBUMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5ldCBX
aWRnaXRzIFB0eSBMdGQxDjAMBgNVBAMMBUNoYXZlMB4XDTE5MDIxMzE4MjIwMFoX
DTIwMDIxMzE4MjIwMFowVTELMAkGA1UEBhMCUFQxEzARBgNVBAgMClNvbWUtU3Rh
dGUxITAfBgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDEOMAwGA1UEAwwF
Q2hhdmUwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAKndWGTZSVMy7A06gAUH
iR52a0k6PpgSfwO+h076PWyVYmjVLpS61LJn2AHaTLvUHX1AGiye4bNpfAQskKz7
l4/h6VIv82HRPsU3tr/BjunRw40KoO14f0n5McgGeGrEYnJMYd428hMlrZiJh713
G4z50cz5M6DWlK9uVm5Z76F7AgMBAAGjUzBRMB0GA1UdDgQWBBSkgvq4Ycc3xSUl
017X4614gQxMrTAfBgNVHSMEGDAWgBSkgvq4Ycc3xSUl017X4614gQxMrTAPBgNV
HRMBAf8EBTADAQH/MA0GCSqGSIb3DQEBCwUAA4GBABkiylGdUi6fxRhhyvmoUY3C
vx3y7Pxe/s5YzcaKYtgPo094tjilKkty/NYR/S8vc9Al6I03OJfJNA2eh8RHMaU0
xujoWMDja1UdyPB9HSbpGJfbvMxMmnwlOVNUYQpQXSLHEfPBJqNoEz3u2ZMQMjmA
rEt+dCBwm2NL8ga8peTS
-----END CERTIFICATE-----
```

Vejamos agora a diferença entre utilizar o programa *recoverSecretFromAllComponents-app.py* e o *recoverSecretFromComponents-app.py*.

Usando o *recoverSecretFromComponents-app.py*, obteve-se:

```
user@CSI:~/Aulas/Aula2/ShamirSharing$ python recoverSecretFromComponents-app.py 5 1 key.cert
Component 1: eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjQtZGI4MGY0Zjc1ZDI2ODlmM2NlZjA2OGExNTQwOWQ3YjgzODZmMDY4NzMxMGJkOTk3NzRmMWU0YmIyN2NiNzY2YTM1YmJjZWU2YWI3Y2QzNDllMDhkMDkwZmYxY2ExMzU3IiwgIjEiLCA1LCA4LCAiYWQyNWRkNWIyYTgyZTBjZjQ4ZTY0YzQzNzg0MjdmNzQ5N2QzYTM2YmM3M2I0ZjExNDM3YmVlMmI5OGNiOGZlNiJdfQ.gXHDyHvFWmXMlghPnFoLdHeFVOzITotnhUqsydY26jGs3-1IlM5yXeNshGJGG18OdZV13PhHCGRhxU_S3R1y1h0CThpeA89pEroobS5G1_dPoGR3fhfUHiV3GcNtj2X902R2EO3AL8kY61OeW4rMVlko4FxjjtXxG8-m22DG-00
Component 2: eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjUtYjczM2Y2NjgwMDlhNDAxMDdkM2IwNzUxNTY0MzliZGFiNDllMDdmYjZlOWIwZWQ0NjE2NDQ0NDk3Y2Y5MjAzOWQ4ODc1OTA1NmFlOTg3YjQwYjg3NWM5YmZlY2E3YmYxIiwgIjEiLCA1LCA4LCAiYTVjYWY0ZDIxNmM2M2NkOTZhNTE2NzlkNjg5ZDkzMDY0Y2QwMzhjMTE4MjY5NzY3NTJhMDQ3YzYyMTVkOTU1MSJdfQ.EPhHSinkN_XpzgTLl0q57Ty8dMPdgYU7Z1RwANYJQnskcdVgqyow7ubtCD3eO-ty_iKt3TGjGAoHliW2ZTe7ir4ZPqRtETQ158wD4cPtr9og-WU8g8CRuwzPJ7xGZmnncGYr4oTeodZagYnlRCWWQZA0PWasMOzL2G8UQLo6Jgs
Component 3: eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjYtNmJhZDMxZDRhNjNlMTBhYWJjNjE1ZGYzZjVjZDhjZTEyMGI2YTUyMjEwMzVjNGQ3ZTI3ZTNhNDY4ZjlkYzNhNjdjZjM4YjMwZWM5NTNjOTY0MjFjOWIxNjg5NjMxOGIxIiwgIjEiLCA1LCA4LCAiZjgwOGRlYmMxMzJjNGFhNjMwMWZiYWExNDFjOGE0MGFlMjcwOTU1YTY2OWQyN2I1MjJjYWNlOGFhZDljOTA4OSJdfQ.hk8wcqCB9QpI0en9FYZc6fu3sRCPjzsqOgNQ_i3T9ZNpr79Jm9fK4rWYCEZRXWm13Og199tAMAqjDTXaaZti6ToYZLdNYTTfIgS-DC7WBTtRaHhPJ7e5flrFvP0mffXJ7LsUK1kwn0_9ZfsyfbHSO8Kd_KAAy6Sfwkg8fgZzTNE
Component 4: eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjctNzM3MzE4MWJmMjc5NGZkMzA1ZDRmZTI0NmQ4YWNmYjZkNjU4Y2FlODk3NDZjYjg1OTdkODU1YTVjOWIyNjBjYjM3NmM2NzdlZTY0MTU3ZmMxMTUwZmViNjQ5NGRhODVlIiwgIjEiLCA1LCA4LCAiYzY1NDFlNzRiMzg4NTM4Nzc0YjRiOWMwMWZlMTNmMzU4ZWJlNmM0NTE2MDE5MjdhMTU3ZjBkOGMwOWNkMDY0YyJdfQ.ldvYUcQ9mEhEnaxYfKm-xnmnWgTvIDCAQBkzsC0oWw9tTlKCTU20qS9pSUUl7xMdYXQHkKjEDtF-rGkTvYoLz0vR44uzRSJ9zdjRDOs5l0LoZYx7uQtLTsrKN_Kee4qinGtdiIAuNUoRdFprcEaDSWnsbNE2krxsrRIS9GmQvMw
Component 5: eyJhbGciOiAiUlMyNTYifQ.eyJvYmplY3QiOiBbIjgtOTFiN2FjY2E4YzE5OGU0NDBlY2M5YmYyM2ViY2ViZGVmYTE2NGY1YmMyNjhhNGEyNDg1MWRlYWY0ODNmNWQ0MGY5ZjgwMTI4ZWI3NmUzYTA3MjMwNGNmMDQwMTk3MjY3IiwgIjEiLCA1LCA4LCAiYmY1N2FlMzNlYjg1ZWY5YWNlY2QzMDQ0MDZkZmE4OGJjZDQ5YWU5YzM3YzljN2I2Y2E5NTM5ZjhkMWFkMWZkYyJdfQ.XyXI85O-DbdF5ID1WiZmnKBB-952wbbm9impvtLsIb2LPPTs49IbMtZcjhsZXdzdXaOBi6pc6pgbjp8zMpaDPRnOgkxU3emzYK_wQl9x2dU_sMn1zBmEZG3A58_ARvDnCWduGATBi8Q7p7u56K0tEanGlfqCa3hnvj72UsgV938
Recovered secret: Agora temos um segredo extremamente confidencialuser@CSI:~/Aulas/Aula2/ShamirSharing$
```
Analisando os programas *recoverSecretFromComponents-app.py* e *recoverSecretFromAllComponents-app.py* são notórias algumas diferenças. Enquanto o programa *recoverSecretFromComponents-app.py* para reconstruir o segredo necessita exatamente(**pelo menos**) da quantidade definida como sendo o *quorum*, o programa *recoverSecretFromAllComponents-app.py* para reconstruir o segredo necessita de todas as partes.
Deste modo, recorre-se a cada um dos programas, dependendo do objetivo. Ou seja, recorre-se ao *recoverSecretFromAllComponents-app.py* quando se pretende uma maior segurança, uma vez que, neste caso, é necessário a junção de todas as partes para reconstruir o segredo.


### 3\. Authenticated Encryption

#### Pergunta P3.1

PrimeSign GmbH
CRYPTAS-PrimeSign Qualified Root CA

| Algoritmo de Assinatura | Tamanho da Chave Pública |
| ------------- | ------------- |
| Sha256 with RSA encryption | 4096 bits |



Encrypt-then-MAC

### Referências
<http://www.issihosts.com/haveged/index.html>
