---
description: Conheça o componente e saiba como utilizá-lo.
---

# JMS

O _**JMS**_ realiza operações em _brokers_ de mensageria que suportem API JMS. Atualmente suportamos ActiveMQ, IBM MQ, Oracle AQ e Tibco EMS.

Dê uma olhada nos parâmetros de configuração do componente, dependendo do tipo de barramento que se deseja utilizar:

* **Account:** conta do tipo BASIC que será utilizada para autenticação no _broker_ JMS configurado.
* **Message:** conteúdo da mensagem a ser enviada. Nesse campo pode ser informado qualquer valor de texto. Esse parâmetro suporta _Double Braces_.
* **Destination:** tipo de destino para onde a mensagem será enviada (QUEUE ou TOPIC).
* **Name:** nome da fila ou tópico.
* **JMS Provider:** provedor JMS que será utilizado. Opções disponíveis: ActiveMQ, IBM MQ, Oracle AQ e Tibco EMS.
* **Is Binary:** “true” se a mensagem recebida é um base64 dos _bytes_ que você precisa enviar; do contrário, a mensagem será enviada como texto.
* **Charset:** se a mensagem que você precisa enviar é binária, então você deve selecionar o _charset_ para a mensagem.
* **Raw Value:** “true” se a mensagem é um _raw value_ e precisa ser enviada como JSON (ex.: a palavra 'teste' será enviada como "teste").
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Advanced Configurations:**

**- Correlation ID:** um cliente de JMS pode utilizar o _header_ JMS Correlation ID para associar uma mensagem a outra (para solicitações de solicitação/resposta). Esse campo pode conter um valor de _string_ arbitrário. A utilização desse campo é opcional.

**- Expiration:** tempo de expiração da mensagem dentro da fila ou tópico (Time To Live). Em milissegundos.

**- Priority:** define a prioridade da mensagem. Um valor de 0 a 4 indica um intervalo de prioridade normal (sendo 4 o valor padrão); os valores de 5 a 9 indicam prioridade acentuada.

**- Type:** esse campo pode ser utilizado para definir algum valor no envio da mensagem, que poderá ser utilizado para filtrá-la.

**- JMS Object Properties:** define algumas propriedades JMSX da API JMS que poderão serem configuradas:

**-> JMSXUserID (**_**String**_**):** _string_ arbitrário que identifica o usuário que está enviando a mensagem. Ele deve ser definido pelo provedor durante a operação de envio.

**-> JMSXAppID (**_**String**_**):** identidade da aplicação de envio. Ela deve ser definida pelo provedor durante a operação de envio.

**-> JMSXDeliveryCount (int):** número de tentativas de envio da mensagem.

**-> JMSXGroupID (**_**String**_**)**: identidade do grupo de mensagem (definida pelo cliente) da qual a mensagem em questão faz parte. Ela deve ser usada pelos clientes que enviarem mensagens em lotes.

**-> JMSXGroupSeq (int)**: sequência numérica da mensagem (definida pelo cliente) dentro de um grupo.

**-> JMSXConsumerTXID (**_**String**_**):** identificador da transação dentro da qual a mensagem foi produzida.

**-> JMSXProducerTXID (**_**String**_**):** identificador da transação dentro da qual a mensagem foi consumida.

**-> JMSXRvcTimeStamp (long):** tempo levado para uma mensagem ser entregue ao seu consumidor final.

**-> JMSXState (int):** pode ser 1 (em espera), 2 (pronto), 3 (expirado) ou 4 (retido). Isso não é relevante para o aplicativo do cliente, sendo de uso interno do provedor.

Exemplo de uso no campo de algumas das propriedades:

```
{

"JMSXUserID": "123",

"JMSXState": 1,

"JMSXGroupID": "test"

}
```

Existem algumas propriedades específicas para cada _broker_:

### Activemq e Tibco EMS <a href="#h_7773f15b40" id="h_7773f15b40"></a>

* **Url:** conexão _string_ JMS no formato tcp://{host}:{port}

### Oracle AQ <a href="#h_839564ec9e" id="h_839564ec9e"></a>

* **Host Name:** nome do _host_ da conexão _string_ JMS
* **Port:** número da porta para Oracle
* **Sid:** Oracle database sid (identificador de site)
* **JBDC Driver:** Oracle JBDC _driver_ (ex.: THIN ou OCI)

**IBM MQ**

**Ainda não há suporte ainda para autenticação por meio do TLS.**

* **Host Name:** nome do _host_ da conexão _string_ JMS
* **Port:** número da porta do _broker_ IBM MQ
* **Channel Name:** nome do canal a ser utilizado na comunicação do _broker_
* **Queue Manager:** nome do gerenciador de filas do IBM MQ

## Fluxo de Mensagens <a href="#h_4fc6f61f33" id="h_4fc6f61f33"></a>

### Entrada <a href="#h_ad9662f11c" id="h_ad9662f11c"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela através de _Double Braces_.

### Saída <a href="#h_0cb81ab1a6" id="h_0cb81ab1a6"></a>

* **Sucesso**

```
{
"success": true,
"message": "MENSAGEM QUE FOI ENVIADA AO BROKER"
}
```

* **Erro**

```
{
"success": false,
"message": "Something went wrong while trying to produce the message to JMS service. Error: Error while attempting to add new Connection to the pool",
"error": "javax.jms.JMSException: Error while attempting to add new Connection to the pool"
}
```

## JMS em Ação <a href="#h_05715198d8" id="h_05715198d8"></a>

* **ActiveMQ e Tibco EM**

**Message**:

```
{
"message": "test"
}
```

**Destination**: QUEUE

**Name**: NAME.OF.THE.QUEUE

**JMS Provider**: ActiveMQ

**Connection string**: tcp://\<HOST>:\<PORT>

**Is Binary**: desabilitado

**Raw Value**: desabilitado

**Fail On Error**: desabilitado

**Resposta:**

```
{
"success": true,
"message": {
"message": "test"
}
}
```

* **Oracle AQ**

**Message**:

```
{
"message": "test"
}

```

**Destination**: QUEUE

**Name**: NAME.OF.THE.QUEUE

**JMS Provider**: Oracle AQ

**Hostname**: \<HOSTNAME> ou \<IP>

**Port**: \<PORT>

**SID**: \<ORACLE SID>

**JDBC Type**: thin

**Is Binary**: desabilitado

**Raw Value**: desabilitado

**Fail On Error**: desabilitado

**Resposta:**

```
{
"success": true,
"message": {
"message": "test"
}
}
```

* **IBM MQ**

**Message**:

```
{
"message": "test"
}
```

**Destination**: QUEUE

**Name**: NAME.OF.THE.QUEUE

**JMS Provider**: IBM MQ

**Hostname**: \<HOSTNAME> ou \<IP>

**Port**: \<PORT>

**Channel Name**: \<IBM MQ CHANNEL NAME>

**Queue Manager**: \<IBM MQ QUEUE MANAGER>

**Is Binary**: desabilitado

**Raw Value**: desabilitado

**Fail On Error**: desabilitado

**Resposta:**

```
{
"success": true,
"message": {
"message": "test"
}
}
```
