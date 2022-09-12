---
description: Conheça o componente e saiba como utilizá-lo.
---

# Block Execution

O _**Block Execution**_ declara um trecho de _pipeline_ para um fim específico. Ele pode ser usado para:

* separar logicamente trechos de um _pipeline_ extenso de maneira que o seu comportamento se torne mais fácil de entender;
* permitir que os diferentes caminhos criados por componentes de desvio de fluxo possam se unir ao final do trecho declarado (mais detalhes adiante);
* declarar um trecho de _pipeline_ para tratamento de erros específicos.

O _**Block Execution**_ faz parte de um conjunto de componentes que trabalham com _subpipelines_ para executar as suas funções.

Para trabalhar com este tipo de componente, você precisa levar em consideração 2 conceitos importantes:

* _**Subpipeline**_** definido no bloco "onProcess":** o _pipeline_ definido nesse bloco é o trecho de execução do componente.
* _**Subpipeline**_** definido no bloco "onException":** o _pipeline_ definido nesse bloco é executado sempre que ocorrer uma falha no bloco “onProcess”. Veja mais detalhes abaixo.

O _**Block Execution**_ não possui nenhuma configuração específica para o seu funcionamento, bastando apenas construir os _subpipelines_ “onProcess” e “onException”.

### Definindo o _subpipeline_ executado como parte do bloco <a href="#definindo-o-subpipeline-executado-como-parte-do-bloco" id="definindo-o-subpipeline-executado-como-parte-do-bloco"></a>

Para definir o _subpipeline_ a ser executado, basta clicar no ícone “onProcess” do componente:

![](<../../.gitbook/assets/block execution.png>)



Ao clicar nesse ícone, um _subpipeline_ será criado (ou exibido, caso já exista). Então basta construir o fluxo desejado conforme a necessidade de execução.

**IMPORTANTE:** a entrada desse _subpipeline_ será alimentada com a mensagem imediatamente anterior ao _**Block Execution**_.

### Utilizando o Block Execution para unir caminhos diferentes de um componente de desvio de fluxo <a href="#utilizando-o-block-execution-para-unir-caminhos-diferentes-de-um-componente-de-desvio-de-fluxo" id="utilizando-o-block-execution-para-unir-caminhos-diferentes-de-um-componente-de-desvio-de-fluxo"></a>

Quando um componente de desvio de fluxo é utilizado, assim como o Choice, múltiplos caminhos são criados no _pipeline_ para atender ao desvio de fluxo desejado. Por exemplo:

![](<../../.gitbook/assets/block execution1.png>)



No caso acima, você pode ver 2 desvios de fluxo: _path1_ e _path2_, que levam a caminhos completamente diferentes no _pipeline_. Suponha que seja necessário unir esses caminhos para continuar a execução do _pipeline_. O componente _**Block Execution**_ tem a função de realizar esse agrupamento de caminhos diferentes em um bloco de execução separado. Quando um dos caminhos terminar, o controle volta para o _**Block Execution**_ que, por sua vez, é seguido pelo próximo componente. Veja:

![](<../../.gitbook/assets/block execution2.png>)



Nesse outro exemplo acima, o _**Block Execution**_ é seguido pelo JSON Generator. Dentro do _subpipeline_ “onProcess” do _**Block Execution**_, foi utilizado um componente Choice com desvios.

Quando os desvios chegam ao final, eles encerram o _**Block Execution**_, que retorna ao _pipeline_ principal e executa o componente seguinte - nesse caso, o JSON Generator.

Dessa forma, é possível unir e organizar _subpipelines_ que contenham fluxos com ramificações.

### Tratamento de erros <a href="#tratamento-de-erros" id="tratamento-de-erros"></a>

Assim como todos os outros componentes que possuem os _subpipelines_ “onProcess” e “onException”, o _**Block Execution**_ também faz o tratamento de erros por meio da execução do _subpipeline_ “onException”.

Um erro pode ser ocasionado por outros componentes quando eles identificam situações adversas. Geralmente os componentes possuem uma propriedade de configuração denominada “failOnError”, que controla se você deseja ou não gerar um erro que possa ser tratado em fluxos “onException”.

Assim, quando um componente "lança" um erro e está com a propriedade “failOnError” habilitada, o _**Block Execution**_ intercepta o erro e o envia para tratamento no _subpipeline_ “onException”.

Estas são as situações especiais que você deve levar em consideração:

* se um fluxo “onException” não for definido, o _**Block Execution**_ simplesmente repassa o erro adiante para que outro componente com execução por _subpipeline_ o trate. Por outro lado, se o fluxo principal do _pipeline_ for utilizado, então o _pipeline_ é encerrado com o erro;
* se um novo erro ocorre durante o _subpipeline_ “onException”, o _**Block Execution**_ também repassa o erro adiante para que outro componente com execução por _subpipeline_ o trate. Mas se o fluxo principal do _pipeline_ for utilizado, o _pipeline_ é igualmente encerrado com o erro.

Para entender melhor o conceito de _subpipelines_, clique [aqui](../../build/pipelines/subpipelines.md).
