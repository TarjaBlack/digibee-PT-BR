---
description: Conheça o componente e saiba como utilizá-lo.
---

# SQS

Para fazer o envio para uma fila, você pode invocar um JSON Generator que indique as mensagens. Dessa forma, você consegue enviar uma mensagem por vez.

**IMPORTANTE:** além das permissões para publicar uma mensagem na fila SQS, você também precisa ter a permissão sqs:GetQueueUrl.\
&#x20;    &#x20;

### O significado de SQS <a href="#o-significado-de-sqs" id="o-significado-de-sqs"></a>

_**Simple Queue Service**_ é um serviço de distribuição da Amazon que faz o enfileiramento de mensagens. Com ele, você pode programar o envio para se comunicar por meio da Internet.

&#x20;

&#x20;

## Como usar o componente <a href="#como-usar-o-componente" id="como-usar-o-componente"></a>

Digamos que você queira utilizar um componente para realizar a subscrição em uma fila de mensagens do SQS. Dessa maneira, você consegue disparar um _pipeline_ que habilita o consumo de uma mensagem por vez.&#x20;

&#x20;  \
**Exemplo 1 (com JMS Trigger):**

**1.** Selecione o JMS Trigger para criar o seu _pipeline._

\
**2.** Abra as configurações do _trigger_ e especifique os valores dos campos:

**- Destination:** selecione _**queue**_&#x20;

**- JMS provider:** escolha _**SQS**_

**- Connection string:** URL de conexão da Amazon

**- REGION:** região em que está instalado o Broker SQS\
&#x20; &#x20;

**3.** Clique em "Confirmar".\
\
**4.** Continue a construção do _pipeline_.\
\
**5.** Conecte os seus componentes.\
\
**6.** Faça o _deploy_ do _pipeline_:

\- Clique em "Run", localizado na parte superior da tela.\
\- Selecione o ambiente, que pode ser _**test**_ ou _**prod**_.\
\- Clique em "Criar uma nova implantação".\
\- Selecione o _pipeline_ com a sua versão e capacidade.\
\- Clique em "Confirmar".\
&#x20;  &#x20;

**7.** Quando for disparado, o _pipeline_ receberá um _payload_ similar ao seguinte:

```
{  "data":"mensagem"}
```

&#x20;&#x20;

* **data:** conteúdo da mensagem recebida

&#x20;       &#x20;

**Exemplo 2 (com JSON Generator):**

**1.** Crie um _pipeline_ e adicione um JSON Generator.

**2.** Abra as configurações do componente e envie os JSONs desejados.\
\
**3.** Clique em “Confirmar”.\
\
**4.** Adicione um _**SQS**_.\
\
**5.** Abra as configurações e escolha uma ACCOUNT.\
\
**6.** Configure os outros campos do componente:

**- Name of the QUEUE:** nome da fila SQS

**- Connection string:** URL de conexão da Amazon

**- REGION:** região em que está instalado o Broker SQS\


**7.**  Clique em “Confirmar”.\
\
**8.** Conecte todos os componentes do _pipeline_.\
\
**9.** Abra o Test-Mode e execute um teste do _pipeline_. Você pode utilizar o comando CTRL + ENTER para isso.\
\
**10.** Aparecerá o resultado do teste executado, conforme demonstrado abaixo:

```
{

"messageId": "6d95f5c5-08c4-4327-a2d6-950b54d44601",

"messageBodyMD5": "65319b689ece655dd519e5cb0082291b",

"sequenceNumber": null,

"success": true,

"requestId": "4eed2d9e-63cd-5a8e-8d31-7b4c48182c94"

}
```

* **messageId:** ID da mensagem enviada.
* **messageBodyMD5:** MD5 da mensagem enviada.
* **sequenceNumber:** número sequencial da mensagem (se existir).
* **requestId:** request ID da mensagem enviada.
* **success:** “true” se a mensagem é enviada com sucesso; “false” se não é enviada com sucesso.&#x20;
