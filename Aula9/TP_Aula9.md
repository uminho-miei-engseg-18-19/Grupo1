# Aula TP - 1 de Abril - Resolução

## 1. Vulnerabilidades e codificação

### Pergunta P1.1

**1.**

Em relação ao número de bugs no código de um software, estima-se que este está entre 5 e 50 por cada 1000 linhas de código - _SLOC_ -, tendo em conta o tipo de software que é.

Ora, através do site citado no enunciado e fazendo os cálculos necessários, podemos concluir o que está na tabela abaixo:

| Software | Linhas de código | Estimativa do nº de bugs |
| :-----------: | :---------------: | :-----------------: |
| Facebook | 62.000.000 | 31.000 a 310.000 |
| Car Software | 100.000.000 | 50.000 e 500.000 |
| Linux 3.1 | 15.000.000 | 7.500 e 75.000 |
| Google Services | 2.000.000.000 | 1.000.000 e 10.000.000 |

**2.**

Não existe uma fórmula que calcule o número de vulnerabilidades a partir do número de bugs de um software, isto é, não é possível determinar quantos dos 5 a 50 bugs por cada 1000 linhas de código se vão manifestar como vulnerabilidades!


### Pergunta P1.2

[falta colocar links e explicar correções]

**Vulnerabilidades de Projecto**

- [Not using password aging](https://cwe.mitre.org/data/definitions/262.html). Apesar de maior parte das aplicações recomendar a atualização das passwords e a não utilização de passwords iguais em todos os sistemas, muitas vezes, não é incluído no desenho do software uma forma de prever que as passwords "passem o seu prazo de validade". Para melhorar esta característica de segurança podia ser incluído um sistema de notificação/aviso de password "velha" com a sugestão de que a substituíssem por uma forte, atualmente. Assim, seria algo corrigido com alguma facilidade.
- [Execution with unnecessary privileges](https://cwe.mitre.org/data/definitions/250.html). Esta vulnerabilidade remete-nos para um nível de permissões muito elevado em certas aplicações, permissões estas que podiam ser bem mais reduzidas. Assim sendo, é bastante plausível para um atacante ter acesso e explorar funcionalidades que não lhe deviam ser alcançáveis. Resolver isto passaria por criar utilizadores diferentes, com permissões limitadas para o propósito do utilizador ou para tarefas únicas. Elevar os privilégios quando necessário e reduzi-los assim que deixasse de ser aplicável também seria uma boa hipótese. Implementar isto pode não ser imediato, mas precaveria muitos ataques que são considerados fáceis. 

**Vulnerabilidades de Codificação**

- [Improper input validition](https://cwe.mitre.org/data/definitions/20.html). Se um input é mal lido, todo o fluxo de dados pode tornar-se confuso e ser mesmo afetado negativamente. Uma estratégia é implementar o código de forma a que aceite apenas determinados inputs, isto é, mais específicos ou incluir logo funções que convertam os inputs na forma que pretendemos.
- [Heap-based buffer overflow](https://cwe.mitre.org/data/definitions/122.html). A vulnerabilidade _heap overflow_ é como um _buffer overflow_, porém, o pedaço de memória onde o _buffer_ pode subscrever é no chamado _heap_ que funciona como uma alocação de memória dinâmica... que pode ocorrer em qualquer pedaço livre de memória. Ocorre o _buffer_ quando se usa um comando como _malloc()_. Explorar esta vulnerabilidade tem um nível elevado de possível sucesso, assim como não é imediato corrigir esta, uma vez que pode ser atacada na fase de projecto, assim como na fase de operações.

**Vulnerabilidades Operacionais**

- 
