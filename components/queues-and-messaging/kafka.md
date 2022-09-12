---
description: Conheça o componente e saiba como utilizá-lo.
---

# Kafka

O **Kafka** produz registros para os _broker_s Kafka configurados nele.

Dê uma olhada nos parâmetros de configuração do componente:

* **Kafka** **Authentication** **Account** (BASIC)**:** se o servidor Kafka precisar de autenticação, será necessário criar uma conta tipo BASIC para esse componente. Suportamos também autenticação via Kerberos.
* **Truststore:** caso seja necessário informar uma _truststore_ para realizar o SSL Handshake utilizando certificados privados, deve-se criar uma conta do tipo CERTIFICATE-CHAIN e informar os certificados concatenados. No campo “password” é opcional inserir a senha a ser cadastrada na criação da _truststore_.
* **Keystore:** caso seja necessário informar uma _keystore_ para realizar a autenticação SSL mútua, deve-se criar uma conta do tipo CERTIFICATE-CHAIN, informar a cadeia completa com os certificados concatenados e a chave privada a ser utilizada para a autenticação SSL mútua. Caso exista uma chave privada, é necessário informá-la no campo “password”.
* **Brokers:** _brokers_ do servidor (HOST: PORT) usados para o envio de registros. Para informar múltiplos HOSTS, você pode separá-los por vírgula. Exemplo: HOST1:PORT1,HOST2:PORT2,...,HOSTn:PORTn
* **Security Protocol:** forma que a conexão é estabelecida. Você pode ou não utilizar um canal de segurança (SSL) e de autenticação (SASL). A utilização de ambos (SASL\_SSL) também é possível.

{% hint style="info" %}
**IMPORTANTE:** devido a necessidade de uma grande alocação de memória, não suportamos os seguintes tipos de Security Protocol: **PLAINTEXT** e **SASL\_PLAINTEXT**. Para entender melhor, clique [aqui](https://cwiki.apache.org/confluence/display/KAFKA/KIP-498%3A+Add+client-side+configuration+for+maximum+response+size+to+protect+against+OOM).
{% endhint %}

* **Schema Registry URL:** se pelo menos uma das opções **Headers By Avro,** **Payload As Avro e Partition Key As Avro** estiver ativada, o campo será mostrado para configurar o Schema Registry's URL.
* **Schema Registry Account:** conta para autenticar com o Schema Registry.  &#x20;
* **Schema Registry Truststore:** se for necessário informar um truststore para fazer o SSL Handshake utilizando certificados privados, deve-se criar uma conta do tipo **CERTIFICATE-CHAIN** e informar os certificados concatenados. É opcional informar, no campo “senha”, a senha a ser cadastrada na criação do truststore.
* **Schema Registry Keystore:** se for necessário informar um keystore para fazer a autenticação mútua SSL, deve-se criar uma conta do tipo **CERTIFICATE-CHAIN**, informar a cadeia completa com os certificados concatenados e a chave privada a ser utilizada para a autenticação mútua SSL. Se houver chave privada, é necessário informá-la no campo “senha”.
* **Headers:** conjunto de entradas "chave": "valor", contendo cabeçalhos a serem enviados na mensagem (campo opcional).
* **Binary Headers:** se a opção estiver ativada, os valores dos cabeçalhos são considerados binários e são interpretados como uma _string_ com a representação base64; do contrário, os valores dos cabeçalhos são interpretados como texto.
* **Headers By Avro Schema:** se a opção estiver habilitada, o componente validará os cabeçalhos com base em um esquema Avro antes de enviar os cabeçalhos.
* **Headers Schema:** se a opção Headers By Avro Schema estiver habilitada, será exibido o campo para definir os Headers Schemas a serem validados.
* **Headers Charset:** nome do código de caracteres para a codificação dos valores dos cabeçalhos (padrão UTF-8).
* **Payload:** _payload_ que será despachado.
* **Payload As Avro**: se a opção estiver ativada, o componente enviará o payload no formato Avro.
* **Payload Schema:** se a opção **Payload As Avro** estiver habilitada, o campo será mostrado para informar o Payload Schema a ser validado.
* **Request Timeout:** configuração que controla o tempo máximo (em milissegundos) que o cliente aguarda pela resposta de uma solicitação. Se a resposta não for recebida antes que o tempo limite se esgote, a solicitação é reenviada automaticamente. Do contrário, haverá uma falha se as tentativas se esgotarem.
* **Retries:** se for estabelecido um valor diferente de 0 (zero), qualquer registro cujo envio falhar será reenviado. Esses registros podem ser reenviados com um provável erro transitório.
* **Metadata Timeout:** tempo máximo para o envio do registro ao Kafka.
* **Key Strategy:** caso a opção **Partition Key As Avro** for ativada, o campo será exibido para configuração da estratégia de _subject_ a ser utilizada para construir o _subject name_ para as keys das mensagens.
* **Value Strategy:** caso a opção **Payload as Avro** for ativada, o campo será exibido para configuração da estratégia de _subject_ a ser utilizada para construir o _subject name_ para os values das mensagens.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Kerberos Service Name:** valor definido na propriedade _**sasl.kerberos.service.name**_ configurado no lado _server_ do _broker_ Kafka.
* **Partition Number**: especifica os números da partição para os quais o _**Kafka Trigger**_ enviará mensagens. Caso essa propriedade não seja configurada, o servidor do Kafka ficará responsável por decidir para qual partição do tópico a mensagem será enviada.
* **Partition Key:** uma chave de partição pode ser especificada para indicar a partição de destino da mensagem. Caso esse campo não seja preenchido, um particionador baseado em _hashing_ é utilizado para determinar a _id_ de partição dada a chave.
* **Partition Key As Avro:** se a opção estiver ativada, o componente fará o envio do _partition key_ no formato Avro.
* **Partition Key Schema:** caso a opção **Partition Key As Avro** for ativada, o campo será exibido para que seja informado o _Schema_ da _partition key_ a ser validada.
* **Producer Client Name:** identificador de origem dos pedidos (opcional)
* **Acks:** configuração para reconhecer o recebimento da mensagem pelo broker Kafka (valores: 0, 1 ou ALL).

{% hint style="info" %}
**IMPORTANTE**: As mensagens trafegadas no formato Avro deverão ser do tamanho máximo suportado por Pipelines SMALL, MEDIUM ou LARGE. O componente não suporta cenários extremos de leitura de dezenas de mega/giga/tera/peta bytes.

O suporte para o formato Avro está na fase Beta.
{% endhint %}

&#x20;     &#x20;

### Exemplo de resposta de requisição ao Kafka <a href="#exemplo-de-resposta-de-requisio-ao-kafka" id="exemplo-de-resposta-de-requisio-ao-kafka"></a>

```
{
  "message": "{}",
  "offset": 201,
  "timestamp": 1585168528773,
  "serializedKeySize": -1,
  "serializedValueSize": 2,
  "topic": "Welcome-Kafka",
  "partition": 1,
  "success": verdadeiro
}
```

&#x20;   &#x20;

* **message:** mensagem enviada
* **offset:** _offset_ do registro no tópico/partição
* **timestamp:** horário/data do registro no tópico/partição
* **serializedKeySize:** tamanho da chave serializada, com valor descomprimido em bytes. Se o valor é nulo, o tamanho devolvido é -1
* **serializedValueSize:** tamanho do valor serializado, com valor descomprimido em bytes. Se o valor é nulo, o tamanho devolvido é -1
* **topic:** nome do tópico
* **partition:** partição para onde o registro foi enviado
* **success:** se "verdadeiro", o envio foi realizado com sucesso

&#x20;     &#x20;

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela através de _Double Braces_.\
&#x20;     &#x20;

### Saída <a href="#sada" id="sada"></a>

O componente não altera nenhuma informação da mensagem de entrada. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se este componente for o último passo do _pipeline_.\
&#x20;          &#x20;

## Kafka em Ação <a href="#kafka-em-ao" id="kafka-em-ao"></a>

### Autenticação utilizando SSL ou SASL <a href="#autenticao-utilizando-ssl-ou-sasl" id="autenticao-utilizando-ssl-ou-sasl"></a>

Isso permite a autenticação dos seus produtores e clientes ao _cluster_ do Kafka (verificação de identidade). Essa também é uma forma segura de permitir que os seus clientes confirmem a identidade.

### Autenticação usando Kerberos <a href="#autenticao-usando-kerberos" id="autenticao-usando-kerberos"></a>

Para utilizar a autenticação via Kerberos no _**Kafka**_ é necessário ter cadastrado o arquivo de configuração “krb5.conf” no parâmetro de _Realm_. Caso não tenha feito isso, acione o nosso suporte via _chat_. Após concluir esse passo, basta configurar corretamente uma conta do tipo Kerberos e utilizá-la no componente.
