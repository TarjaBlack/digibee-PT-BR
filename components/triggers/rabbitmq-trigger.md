---
description: Conheça o trigger e saiba como utilizá-lo.
---

# RabbitMQ Trigger

O _**RabbitMQ Trigger**_ é responsável pelo consumo das mensagens de um _broker_ RabbitMQ.

Esse _trigger_ possui 2 estratégias de _acknowledge_ (confirmação de recebimento) __ de mensagens:

**1. Acknowledge automático**

A confirmação de cada mensagem recebida pelo _trigger_ acontece de forma automática e imediata no recebimento e o _broker_ entende que ela foi entregue. Por um lado, o _acknowledge_ automático garante um grande desempenho, mas por outro não impede a perda da mensagem caso o _pipeline_ associado não a processe ou a processe com falha.

**2. Acknowledge manual**

Cada mensagem recebida pelo _trigger_ permanece em "unchecked", um estado de não confirmação, enquanto estiverem sendo processadas pelo _pipeline_. No _acknowledge_ manual, o _broker_ RabbitMQ entende que a mensagem está pendente e, caso haja qualquer problema na infraestrutura do _trigger_ ou o _pipeline_ responda com erro, a mensagem em questão pode ser reprocessada. O número de _consumers_ configurados para o _pipeline_ dita quantas mensagens podem ser processadas ao mesmo tempo. Para isso, o tamanho de _prefetch_ do RabbitMQ é configurado com o mesmo valor de _consumers_ do _pipeline_.

Dê uma olhada nos parâmetros de configuração desse _trigger_:

* **Account:** nome da conta que será utilizada (a conta deve ser do tipo _basic_)
* **Hostname:** endereço do host do RabbitMQ
* **Port:** porta onde o RabbitMQ está escutando
* **Virtual Host:** configuração de _host_ virtual que define o _tenant_ do RabbitMQ que se deseja acessar
* **Auto Acknowledge:** se “true”, a mensagem será confirmada assim que chegar ao trigger e não esperará um retorno do pipeline associado; se "false", a mensagem ficará pendente enquanto o pipeline a estiver processando
* **Binary Message:** se "true", define que a mensagem recebida será binária e, portanto, seu conteúdo será apresentado como base64; se "false", a mensagem será apresentada como texto
* **Maximum Timeout:** por quanto tempo um _pipeline_ pode ser executado (em milissegundos)
* **Expiration**: tempo máximo de espera da mensagem numa fila de _pipeline_
* **Allow Redelivery of Messages**: se "true", uma execução de pipeline será re-executada em caso de erro; se "false", não haverá re-execução em caso de erro

{% hint style="info" %}
**IMPORTANTE**: o cliente RabbitMQ não permite a limitação do tamanho de mensagens. Caso mensagens muito grandes sejam enviadas, a infraestrutura de _triggers_ da Digibee poderá recusá-las. Não aconselhamos o envio de mensagens grandes através de um barramento de mensagens.
{% endhint %}

### Consumers <a href="#consumers" id="consumers"></a>

A configuração de consumidores feita no momento de implantação de um _pipeline_ impacta diretamente no _throughput_ de recebimento e saída de mensagens quando o _**RabbitMQ Trigger**_ é ativado. Caso o auto acknowledge esteja desabilitado, a preocupação com o número de consumidores se torna ainda mais importante. Isso acontece porque o número de mensagens simultâneas sendo processadas é igual ao número de consumidores configurados.

### Declaração de filas, routing keys e exchanges <a href="#declarao-de-filas-routing-keys-e-exchanges" id="declarao-de-filas-routing-keys-e-exchanges"></a>

O _**RabbitMQ Trigger**_ não declara parâmetros de configuração de filas, _routing keys_ e _exchanges_ no _broker_ RabbitMQ. É esperado que toda a configuração já esteja feita para que o _trigger_ possa consumir mensagens de filas.

### Formato de mensagem na entrada do pipeline <a href="#formato-de-mensagem-na-entrada-do-pipeline" id="formato-de-mensagem-na-entrada-do-pipeline"></a>

_Pipelines_ associados com o _**RabbitMQ Trigger**_ recebem a seguinte mensagem como entrada:

```
{
  "body": <STRING message content; if binary, then Base64>,
  "properties": {
    "appId": <STRING application id>,
    "classId": <STRING class id>,
    "clusterId": <STRING cluster id>,
    "contentEncoding": <STRING content encoding>,
    "contentType": <STRING message content type>,
    "correlationId": <STRING correlation id>,
    "deliveryMode": <INT delivery mode>,
    "expiration": <STRING message expiration in ms>,
    "messageId": <STRING message id>,
    "priority": <INT message priority>,
    "replyTo": <STRING reply to queue>,
    "type": <STRING message type>,
    "userId": <STRING user id>,
    "timestamp": <LONG message timestamp>
  }
  "headers": {
    "header1": "value1", ...
  },
  "envelope": {
    "deliveryTag": <LONG message delivery tag>
    "exchange": <STRING exchange that processed the message>
    "routingKey": <STRING routing key used to route message>
  }
}
```

