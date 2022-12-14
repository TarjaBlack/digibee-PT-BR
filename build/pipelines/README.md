---
description: Entenda como um pipeline é construído.
---

# Pipeline

A Digibee Integration Platform tem como peça central o _pipeline_, que é uma sequência de componentes que permite conectar sistemas e estabelecer fluxos de dados entre eles.

Um _pipeline_ é composto por:

* um _trigger_;
* pelo menos um componente.

{% hint style="info" %}
**IMPORTANTE:** _trigger_ e componentes precisam estar interconectados.
{% endhint %}

<figure><img src="../../.gitbook/assets/image2.png" alt=""><figcaption></figcaption></figure>

O _trigger_ é a condição de disparo do _pipeline_, ou seja, é um elemento que define como a execução do _pipeline_ será iniciada - por exemplo, através de uma chamada externa, em resposta a um evento ou via agendamento. Para saber mais, leia a [documentação dos _Triggers_ aqui](https://docs.digibee.com/documentation/v/pt-br/components/triggers).

Um componente é um elemento que recebe uma mensagem, podendo interagir ou utilizar as informações contidas nela para executar uma das seguintes atividades:

* chamar serviços externos (por exemplo, uma chamada a um _endpoint_ [REST](../../components/web-protocols/rest-v2.md));
* processar mensagens (por exemplo, transformar o conteúdo da mensagem);
* alterar o fluxo de execução (por exemplo, uma bifurcação que permite direcionar o fluxo do _pipeline_ com base em uma condição, como o componente [Choice](../../components/logic/choice.md) faz);
* percorrer coleções (por exemplo, [For Each](../../components/logic/for-each/)).

Este último caso é um pouco mais sofisticado e, para entendê-lo, precisamos examiná-lo mais de perto.

<figure><img src="../../.gitbook/assets/image3 (2).png" alt=""><figcaption></figcaption></figure>

Quando você utiliza um componente que itera em coleções, cada item da coleção é processado em um fluxo separado chamado _subpipeline_. Veja a imagem abaixo:

<figure><img src="../../.gitbook/assets/image1.png" alt=""><figcaption></figcaption></figure>

1. a execução do fluxo principal acontece até chegar ao componente onde o _subpipeline_ é criado (no exemplo acima, o componente é o For Each **Processa registros**);
2. a execução passa para o _subpipeline_, onde cada item da coleção será tratado individualmente;
   1. ao término da execução deste item, o controle volta ao início do _subpipeline_, que inicia o processamento do próximo item e assim sucessivamente, até que a coleção seja totalmente processada;
3. uma vez que toda a coleção tenha sido processada, o controle retorna ao componente For Each, que direciona o fluxo para o próximo componente do fluxo principal (no caso, o componente **Lê todos os dados**).

Para saber mais, leia o artigo [_Subpipeline_](subpipelines.md).
