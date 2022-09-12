---
description: Saiba como ocorre a comunicação entre os componentes de um pipeline.
---

# Processamento de mensagens

De forma simplificada, é possível dizer que o _pipeline_ é uma sequência de componentes conectados que fazem processamentos e se comunicam por meio de mensagens.

O processamento de um componente dentro um _pipeline_ ocorre em 3 passos:

* recebimento de uma mensagem do componente anterior (mensagem “in”);
* execução de algum processamento, que pode ou não usar as informações da mensagem recebida;
* envio de uma mensagem ao próximo componente (mensagem “out”)

Essas mensagens estão sempre no formato JSON.

Veja o exemplo abaixo. Um _pipeline_ configurado com um _trigger_ REST foi chamado e passou o parâmetro recebido ("type": "revenue") para o componente seguinte - no caso um _Object Store_ chamado _Delete all_. De forma sucessiva, cada componente termina a sua execução e aciona o próximo, passando a mensagem resultante do seu processamento.

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/244528649/5b257029f216933afba465d1/OQCcMsP2xo1vRG-q7RfDuG26IQVvunz-ez5a2ZszOwJeLCdcsdHlCVVFsFvlbmA9eNMCcWMGeebWUK5VRNGnVuZf09Yx6d7SokjAJjm3mYiPhASmOMUNLqsKj1gemoXX1tlYGsXW)

Quando você opta por trafegar somente mensagens no formato JSON, a manipulação e transformação delas fica muito mais fácil tanto se você recorre aos componentes de transformação quanto às expressões em _Double Braces_. Essas expressões precisam fazer referência a elementos da mensagem de entrada para produzir uma mensagem de saída. Para saber mais, leia o artigo [Double Braces e Entrada de Dados](../funcoes-double-braces/double-braces-e-entrada-de-dados.md).
