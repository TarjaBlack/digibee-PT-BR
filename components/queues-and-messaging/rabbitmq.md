---
description: Conheça o componente e saiba como utilizá-lo.
---

# RabbitMQ

O **RabbitMQ** permite a publicação de mensagens em um _broker_ RabbitMQ.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** credencial utilizada para autenticação no RabbitMQ.
* **Hostname:** nome do _host_ que executa o RabbitMQ.
* **Port:** porta de conexão do RabbitMQ (padrão: 5672).
* **Connection Timeout**: tempo máximo para conexão ao RabbitMQ.
* **Virtual Host:** nome do grupo lógico dentro do RabbitMQ ao qual se deseja conectar (padrão /).
* **Exchange Name:** nome do _exchange_ definido no RabbitMQ ao qual se deseja enviar mensagens.
* **Binary Message:** se a opção estiver ativada, a mensagem será considerada binária e o campo _**Message Body**_ deverá informar uma _string_ contendo a representação base64 do conjunto de _bytes_ a enviar; do contrário, a mensagem será considerada como texto.
* **Message Body:** conteúdo da mensagem a ser enviada.
* **Routing Key:** _string_ representando a chave de relacionamento entre o Exchange e a(s) Fila(s).
* **Headers:** conjunto de entradas "chave": "valor" contendo cabeçalhos que serão enviados na mensagem (campo opcional).
* **Message Type:** _string_ representando o tipo de mensagem (campo opcional).
* **Message Content Type:** _string_ representando o tipo de conteúdo da mensagem (ex.: application/json) (campo opcional).
* **Message Content Encoding:** _string_ representando a codificação do conteúdo (ex.: UTF-8) (campo opcional).
* **Priority:** número indicando a prioridade da mensagem (campo opcional).
* **Correlation ID:** _string_ representando o ID de correlação da mensagem (campo opcional).
* **Message ID:** _string_ representando o ID da mensagem (campo opcional).
* **Delivery Mode:** se "Persistent Message", então a mensagem é enviada com a _flag_ persistente e o _broker_ tentará mantê-la em disco assim que possível; se "Transient Message", então o _broker_ tentará manter a mensagem em memória.
* **Reply To:** _string_ representando o endereço de retorno da mensagem (campo opcional).
* **Message Expiration:** número representando o tempo de duração da mensagem em fila (também conhecido como TTL) (campo opcional).
* **Message Timestamp:** número representando o _timestamp_ da mensagem (campo opcional).
* **Application Name:** _string_ representando o nome da aplicação (campo opcional).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Wait for a Publish Acknowledgement**: se a opção estiver ativada, o componente aguardará por uma confirmação de publicação da mensagem; do contrário, o componente enviará a mensagem e não aguardará confirmação.
* **Publisher Acknowledgement Timeout**: tempo máximo que o componente aguardará por uma confirmação de publicação da mensagem.
* **Mandatory Message**: se a opção estiver ativada, então a mensagem é marcada como obrigatória e um erro será lançado caso ela não possa ser roteada; do contrário, então nenhuma verificação de roteamento será feita (é necessário que a opção "Wait for a Publish Acknowledgement" seja habilitada).

{% hint style="info" %}
**IMPORTANTE:** todos os parâmetros de configuração opcionais não serão definidos na mensagem caso os seus valores sejam deixados em branco.
{% endhint %}

### Exemplo de resposta de requisição ao RabbitMQ <a href="#exemplo-de-resposta-de-requisio-ao-rabbitmq" id="exemplo-de-resposta-de-requisio-ao-rabbitmq"></a>

```
<MESMA MENSAGEM QUE FOI INFORMADA NA ENTRADA>
```

{% hint style="info" %}
**IMPORTANTE:** o _**RabbitMQ**_ não altera a mensagem apresentada na sua entrada, exceto em caso de erro.
{% endhint %}

### Exemplo de resposta de requisição ao RabbitMQ contendo erro <a href="#exemplo-de-resposta-de-requisio-ao-rabbitmq-contendo-erro" id="exemplo-de-resposta-de-requisio-ao-rabbitmq-contendo-erro"></a>

```
{
"success": false,
"message": "Could not publish message to RabbitMQ due to an error",
"error": "java.net.SocketTimeoutException: connect timed out"
}
```

* **success:** “false” quando a operação falha
* **message:** mensagem sobre o erro
* **exception:** informação sobre o tipo de erro ocorrido

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada, podendo utilizá-la por meio de _Double Braces_.

### &#x20;<a href="#h_c8a4396fb8" id="h_c8a4396fb8"></a>

### Saída <a href="#sada" id="sada"></a>

* **sem erro**

```
<A MESMA MENSAGEM INFORMADA NA ENTRADA>
```

* **com erro**

```
{
"success": false,
"message": "Could not publish message to RabbitMQ due to an error",
"error": "java.net.SocketTimeoutException: connect timed out"
}
```

## RabbitMQ em Ação <a href="#h_80645f3395" id="h_80645f3395"></a>

Uma mensagem é sempre enviada através desse componente a partir do _**Exchange**_ e do _**Routing Key**_. O Exchange possui um _bind_ com um tópico ou uma fila e direciona a mensagem a partir do Routing Key.

### Enviando uma mensagem simples <a href="#h_6588bee0be" id="h_6588bee0be"></a>

**Mensagem de entrada**:

```
{"message": "test"}
```

**Configurações:**

**Hostname:** \<RABBITMQ HOSTNAME>

**Port:** \<PORT> (porta padrão: 5672)

**Virtual Host:** /

**Exchange Name:** \<EXCHANGE NAME>

**Binary Message**: desabilitado

**Message:** \{{ message.$ \}}

**Routing key:** \<ROUTING KEY>

**Fail On Error:** desabilitado

**Resultado:**

```
{"message": "test"}
```

### Enviando uma mensagem binária simples <a href="#h_fdefc82d1f" id="h_fdefc82d1f"></a>

**Mensagem de entrada:**

```
{"message": "ewoJIm1lc3NhZ2UiOiAidGVzdCIKfQo="}
```

**Configurações:**

**Hostname:** \<RABBITMQ HOSTNAME>

**Port:** \<PORT> (porta padrão: 5672)

**Virtual Host:** /

**Exchange Name:** \<EXCHANGE NAME>

**Binary Message:** habilitado

**Message:** \{{ message.message \}}

**Routing key:** \<ROUTING KEY>

**Fail On Error:** desabilitado

**Resultado:**

```
{"message": "ewoJIm1lc3NhZ2UiOiAidGVzdCIKfQo="}
```

### Enviando uma mensagem para uma fila e a resposta será devolvida para uma outra especificada (Direct Reply-To) <a href="#h_1e95f3c10e" id="h_1e95f3c10e"></a>

**Mensagem de entrada**:

```
{"message": "test"}
```

**Configurações:**

**Hostname:** \<RABBITMQ HOSTNAME>

**Port:** \<PORT> (porta padrão: 5672)

**Virtual Host:** /

**Exchange Name:** \<EXCHANGE NAME>

**Binary Message:** desabilitado

**Message:** \{{ message.$ \}}

**Routing key:** \<ROUTING KEY>

**Reply To:** \<REPLY TO>

**Fail On Error:** desabilitado

**Resultado:**

```
{"message": "test"}
```
