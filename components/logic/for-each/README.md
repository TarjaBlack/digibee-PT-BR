---
description: Conheça o componente e saiba como utilizá-lo.
---

# For Each

O _**For Each**_ realiza um _loop_ dentro de uma estrutura JSON, processando cada elemento do _array_ em um _subpipeline_.

Dê uma olhada nos parâmetros de configuração do componente:

* **JSON Path Expression:** expressão que é aplicada à estrutura JSON recebida pelo componente _**For Each**_, filtrando-a. O _**For Each**_ pode receber um objeto que possua vários elementos e a expressão _JSON Path_ permite obter apenas aqueles que atenderem a uma condição específica.
* **Element Identifier:** elemento único que identifica a linha em processamento (ex.: elemento "id").
* **Parallel Execution:** quando habilitada, a opção faz com que elementos do _array_ recebido pelo _**For Each**_ sejam processados em paralelo, com um limite de até 10 execuções concorrentes - ou seja, caso o _array_ recebido pelo componente _**For Each**_ tenha 20 elementos, os 10 primeiros terão seu processamento iniciado imediatamente. Assim que um desses processamentos terminar, o próximo elemento do _array_ será processado e assim por diante, até que todo o _array_ tenha sido processado. Caso a opção _Parallel Execution_ esteja desabilitada, os elementos do _array_ recebido pelo _**For Each**_ são processados em série - é preciso que o primeiro tenha sido processado para que o processamento do segundo elemento possa começar.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do _pipeline_ apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro "Fail On Error" não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines_ (onProcess e onException). Se você quiser que a execução seja interrompida para qualquer tipo de ocorrência de erro, avalie a utilização do componente _**Do While**_. Clique [aqui](../do-while.md) para ler sobre esse componente e validar se ele se aplica ao seu cenário.

**Exemplos de Expressões **_**JSON Path**_

```
$.[?(@.status == 'EXPIRED')]
```

A expressão acima mostra como a mensagem recebida pelo componente pode ser filtrada: neste exemplo, o _array_ é a raiz do objeto e somente os elementos cujo atributo status seja EXPIRED serão processados pelo componente _**For Each**_.

```
$.body
```

Obtém todo o conteúdo do _body_ da mensagem recebida.

```
$.body.products
```

Obtém o conteúdo de um _array_ _products_ que está dentro do _body_ da mensagem recebida.

## Definindo o _subpipeline_ que é executado a cada iteração <a href="#definindo-o-subpipeline-que--executado-a-cada-iterao" id="definindo-o-subpipeline-que--executado-a-cada-iterao"></a>

Para definir o _subpipeline_ que será executado a cada iteração, basta clicar no ícone _onProcess_ do componente _**For Each**_**.**

![](<../../../.gitbook/assets/for each.png>)

Ao clicar nesse ícone, um _subpipeline_ será criado (ou exibido, caso já exista). Então basta construir o fluxo desejado conforme a necessidade de execução de cada iteração.

**IMPORTANTE:** caso sejam utilizados componentes _**Session**_ para manipular dados de cada elemento do _array_ no _subpipeline_ do _**For Each**_ e a opção _**Parallel Execution**_ esteja ativa, é necessário que a opção _**Scoped**_ do _Session_ esteja ativa para que cada execução em paralelo acesse os seus respectivos dados.

### Tratando erros no _loop_ <a href="#tratando-erros-no-loop" id="tratando-erros-no-loop"></a>

O comportamento padrão do _**For Each**_ é interromper a execução caso algum erro seja encontrado. Erros são situações atípicas na execução de um pipeline que incorrem em uma parada. Por exemplo, o uso de um componente _Assert_ causa um erro no _pipeline_ quando a condição de asserção não for satisfeita. Outras situações de erro ocorrem quando são utilizados componentes com a configuração _"Fail on Error"_ habilitada.

Conforme explicado anteriormente, é possível definir um _subpipeline_ para tratamento de erros. A definição desse _subpipeline_ é feita através do ícone _onException_ do componente _**For Each**_:

![](<../../../.gitbook/assets/for each1.png>)

Clique [aqui](https://intercom.help/godigibee/pt-BR/articles/4484877-subpipelines) para entender melhor o funcionamento dos _subpipelines_.

## Cenários de utilização do componente _For Each_ com tratamento de erros <a href="#cenrios-de-utilizao-do-componente-for-each-com-tratamento-de-erros" id="cenrios-de-utilizao-do-componente-for-each-com-tratamento-de-erros"></a>

### Propriedade "Fail on Error" habilitada e nenhum _subpipeline_ definido em _onException_ <a href="#propriedade-fail-on-error-habilitada-e-nenhum-subpipeline-definido-em-onexception" id="propriedade-fail-on-error-habilitada-e-nenhum-subpipeline-definido-em-onexception"></a>

* o _pipeline_ será interrompido imediatamente
* um erro será emitido a partir do componente _**For Each**_
* nenhum outro componente será invocado após o _**For Each**_

### Propriedade "Fail on Error" habilitada e um _subpipeline_ definido em _onException_ <a href="#propriedade-fail-on-error-habilitada-e-um-subpipeline-definido-em-onexception" id="propriedade-fail-on-error-habilitada-e-um-subpipeline-definido-em-onexception"></a>

* o _pipeline_ será interrompido imediatamente
* o _subpipeline_ definido em _onException_ será executado e a saída dele alimentará o próximo componente após o _**For Each**_
* o componente após o _For Each_ será invocado

### Propriedade "Fail on Error" desabilitada e nenhum _subpipeline_ definido em onException <a href="#propriedade-fail-on-error-desabilitada-e-nenhum-subpipeline-definido-em-onexception" id="propriedade-fail-on-error-desabilitada-e-nenhum-subpipeline-definido-em-onexception"></a>

* a iteração onde ocorreu o erro será interrompida
* uma mensagem de erro padrão será informada na entrada da próxima iteração e o _loop_ continuará a ser executado normalmente

### Propriedade "Fail on Error" desabilitada e um _subpipeline_ definido em onException <a href="#propriedade-fail-on-error-desabilitada-e-um-subpipeline-definido-em-onexception" id="propriedade-fail-on-error-desabilitada-e-um-subpipeline-definido-em-onexception"></a>

* a iteração onde ocorreu o erro será interrompida
* o _subpipeline_ definido em _onException_ será executado e a saída dele alimentará a próxima iteração
* o _loop_ continuará a ser executado normalmente

## Erro durante o _subpipeline_ onException <a href="#erro-durante-o-subpipeline-onexception" id="erro-durante-o-subpipeline-onexception"></a>

* o _loop_ será interrompido
* o erro será lançado para o próximo componente ao qual o componente _**For Each**_ esteja associado
* caso o _**For Each**_ esteja no fluxo principal do _pipeline_, então o _pipeline_ será interrompido
* se o _**For Each**_ estiver dentro de um componente que possui _subpipeline_, então o _subpipeline_ “onException” será invocado e o erro será informado na entrada desse _subpipeline_

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O _**For Each**_ aceita qualquer estrutura de JSON que contenha um _array_. Se o _array_ não for a raiz do objeto, então uma expressão JSON Path deve ser definida para localizar e filtrar o _array_. Caso o componente _**For Each**_** ** não receba um _array_, nenhum processamento será executado.

### Saída <a href="#sada" id="sada"></a>

```
{
    "total": 0,
    "success": 0,
    "failed": 0
}
```

* **total:** número total de elementos processados
* **success:** número total de elementos processados com sucesso
* **failed:** número total de elementos que não puderam ser processados

**IMPORTANTE:** para informar que uma linha foi processada corretamente e iterar o valor do campo "success", cada execução do _subpipeline_ _onProcess_ deve responder com { "success": true } ao seu término. Somente desta forma a mensagem de saída representará corretamente o resultado dos processamentos.&#x20;
