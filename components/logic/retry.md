---
description: Conheça o componente e saiba como utilizá-lo.
---

# Retry

O _**Retry**_ permite novas tentativas de execução de passos definidos em um _subpipeline_**.**

Dê uma olhada nos parâmetros de configuração do componente:

* **Maximum Number of Retries:** número máximo de tentativas. A primeira tentativa também conta, então se o passo falhar na primeira execução e você deseja que seja feita uma nova tentativa, o valor nesse parâmetro deve ser igual a 2.
* **Timeout Of The Whole Retry Operation:** duração máxima de cada tentativa, incluindo a primeira (em milissegundos).
* **Fail On Error:** se a opção for ativada, a execução do _**Retry**_ que atingir o número máximo de tentativas ou a duração máxima, terminará com erro e será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado da última tentativa será entregue ao próximo componente.

## Definindo o subpipeline que é executado a cada tentativa <a href="#h_4da0771299" id="h_4da0771299"></a>

Para trabalhar com esse tipo de componente, é importante levar em consideração:

* **Subpipeline definido em "onProcess":** _subpipeline_ a ser executado a cada nova tentativa.
* **Subpipeline definido em "onException":** _subpipeline_ a ser executado sempre que uma tentativa resultar em falha.

Para entender melhor o funcionamento de _subpipelines_, leia a [documentação Subpipelines](https://docs.digibee.com/documentation/v/pt-br/build/pipelines/subpipelines).

{% hint style="warning" %}
**IMPORTANTE:** a cada nova tentativa, o primeiro passo do _subpipeline_ definido em _onProcess_ recebe a mensagem de saída do último passo processado. Portanto, dados a serem reutilizados nas novas tentativas devem ser devidamente tratados para que possam ser acessíveis durante as novas tentativas (exemplo.: manipulação dos dados através de componentes _**Session**_).
{% endhint %}

### Informando sucesso para uma execução do componente Retry <a href="#h_9121c6196f" id="h_9121c6196f"></a>

O _**Retry**_ espera que uma propriedade "success" com o valor _**true**_ seja informada no último passo do _subpipeline_ para que a execução seja considerada bem sucedida. Se um erro ocorrer ou se a propriedade “success” for informada com o valor _**false**_ ou for inexistente, o _**Retry**_ entenderá que uma nova tentativa deverá ser executada.

## Fluxo de mensagens <a href="#h_81aedec92e" id="h_81aedec92e"></a>

### Entrada <a href="#h_8d4b07ca16" id="h_8d4b07ca16"></a>

Qualquer estrutura é aceita.

### Saída <a href="#h_04df5cd8db" id="h_04df5cd8db"></a>

Mensagem de saída do último passo processado.

## Tratamento de Erros <a href="#h_a3bc434e27" id="h_a3bc434e27"></a>

Quando um erro ocorre durante o processamento do _subpipeline_ em _onProcess_, o _subpipeline_ em onException será invocado se estiver definido.

No _onException_, é possível:

* ter acesso aos detalhes do erro que ocorreu durante o processamento da última tentativa.
* definir se o _**Retry**_ continua as tentativas, informando uma propriedade “success” com o valor _**false**_ ou não a definindo. Caso a propriedade “success” seja especificada com o valor _**true**_, então o _**Retry**_ será finalizado com sucesso e nenhuma outra tentativa será executada.

## Cenários de utilização do componente Retry com tratamento de erros <a href="#h_a1cba176b1" id="h_a1cba176b1"></a>

### Propriedade "Fail on Error" habilitada e nenhum subpipeline definido em onException <a href="#h_200edda8f2" id="h_200edda8f2"></a>

* o _pipeline_ será interrompido após todas as tentativas
* um erro será emitido a partir do componente _**Retry**_
* nenhum outro componente será invocado após o _**Retry**_

### Propriedade "Fail on Error" habilitada e um subpipeline definido em onException <a href="#h_389b2ed99a" id="h_389b2ed99a"></a>

* o _pipeline_ será interrompido após todas as tentativas
* o _subpipeline_ definido em _onException_ será executado após cada tentativa
* um erro será emitido a partir do componente _**Retry**_
* nenhum outro componente será invocado após o _**Retry**_

### Propriedade "Fail on Error" desabilitada e nenhum subpipeline definido em onException <a href="#h_a006162471" id="h_a006162471"></a>

* o _pipeline_ não será interrompido após todas as tentativas
* nenhum erro será emitido a partir do componente _**Retry**_
* o próximo componente será invocado recebendo a mensagem de saída do _**Retry**_

### Propriedade "Fail on Error" desabilitada e um subpipeline definido em onException <a href="#h_aad3137ee2" id="h_aad3137ee2"></a>

* o _pipeline_ não será interrompido após todas as tentativas
* o _subpipeline_ definido em _onException_ será executado após cada tentativa
* nenhum erro será emitido a partir do componente _**Retry**_
* o próximo componente será invocado recebendo a mensagem de saída do _**Retry**_

{% hint style="warning" %}
**IMPORTANTE:** caso um componente de erro, como o _Throw Error_ ou _Assert_, seja utilizado dentro do _subpipeline_ em _onProcess_ ou um erro ocorra, então o _**Retry**_ será finalizado e o erro será propagado para o _pipeline_. Além disso, sempre que a propriedade "success" for definida com valor _**true**_ no último passo do _subpipeline_ em _onException_, a execução do componente _**Retry**_ também será concluída, independentemente da propriedade _**Fail on Error**_ estar ativa.
{% endhint %}
