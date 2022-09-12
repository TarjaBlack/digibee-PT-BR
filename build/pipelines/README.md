---
description: Entenda como um pipeline é construído.
---

# Pipeline

A Plataforma tem como peça central o _pipeline_, que é uma sequência de componentes que permite conectar sistemas e estabelecer fluxos de dados entre eles.

Um _pipeline_ é composto por:

* 1 _trigger_
* pelo menos mais 1 componente

{% hint style="info" %}
**IMPORTANTE:** _trigger_ e componentes precisam estar conectados entre si.
{% endhint %}

![](<../../.gitbook/assets/01 (8).png>)

_Trigger_ é a condição de disparo do _pipeline_, ou seja, é um elemento que define como a execução do _pipeline_ será iniciada - por exemplo, através de uma chamada externa, em resposta a um evento ou via agendamento.

Um componente é um elemento que recebe uma mensagem, podendo interagir ou utilizar as informações dela para executar uma das seguintes atividades:

* chamar serviços externos (por exemplo, uma chamada a um _endpoint_ REST);
* processar mensagens (por exemplo, transformar o conteúdo da mensagem);
* alterar o fluxo de execução (por exemplo, uma bifurcação que permite direcionar o fluxo do pipeline com base em uma condição, como o componente Choice faz);
* percorre coleções (por exemplo, For Each).

Este último caso é um pouco mais sofisticado e para entendê-lo precisamos examiná-lo mais detalhadamente.

![](<../../.gitbook/assets/02 (1).png>)

Quando você utiliza um componente que itera em coleções, a estrutura de pipeline torna-se um pouco cada elemento da coleção que é processado/tratado em um fluxo separado, que chamamos de subpipelines. Veja a imagem abaixo:

![](<../../.gitbook/assets/03 (15).png>)

1. a execução do processo principal vai acontecendo até chegar ao componente onde o _subpipeline_ é criado (no exemplo acima, o componente é o For Each - Processa Registros);
2. a execução passa para o _subpipeline_, onde um item da coleção será tratado individualmente;
3. ao término da execução desse item, o controle volta ao início do _subpipeline_, que inicia o processamento do item seguinte e assim sucessivamente, até que a coleção seja totalmente processada;
4. uma vez que toda a coleção tenha sido processada, o controle volta para o componente For Each que, com a sua execução finalizada, passa o processamento ao próximo componente do processo principal (no caso, o componente “_Lê todos os Dados”_).

Para saber mais, leia o artigo [Subpipeline](subpipelines.md).
