---
description: Conheça o trigger e saiba como utilizá-lo.
---

# Kafka Trigger

O **Kafka Trigger** é responsável pelo consumo das mensagens de um _broker_ Kafka.

#### &#x20;Para utilizar esse _trigger_, é necessário entrar em contato com a nossa Equipe de Suporte para obter a liberação. <a href="#para-utilizar-esse-trigger--necessrio-entrar-em-contato-com-a-nossa-equipe-de-suporte-para-obter-a-l" id="para-utilizar-esse-trigger--necessrio-entrar-em-contato-com-a-nossa-equipe-de-suporte-para-obter-a-l"></a>

\
Esse _trigger_ possui 2 estratégias de _offsets commit_ configuráveis:

**1.** **Commit sem garantia de entrega**

Todas as mensagens recebidas pelo _trigger_ são enviadas ao _pipeline_ de forma mais rápida, porém sem garantia de entrega (ou seja, não será esperado o retorno do _pipeline_ para que o processamento da mensagem seja confirmado). Com o _auto commit_ ativado, utilizaremos o _commit default_ implementado pelo Kafka. O envio de mensagem pode ser configurado por:

* **Envio batch**

Todas as mensagens recebidas pelo polling do consumidor serão enviadas juntas em um _array_. Por exemplo, se durante esse _poll_ forem retornadas 10 mensagens, então o _trigger_ enviará um _array_ com essas 10 mensagens.

* **Envio de mensagem uma a uma**

Será feito um envio ao _pipeline_ ao invés do _array_ total (apenas 1 mensagem por vez). Por exemplo, se durante esse _poll_ forem retornadas 10 mensagens, então o _trigger_ enviará somente 1 mensagem por vez. No total, serão feitos 10 envios de mensagens ao _pipeline_.

\
**2. Commit com garantia de entrega**

O _trigger_ ficará responsável por realizar o _offsets commit_, que será feito após o recebimento de uma resposta de sucesso do _pipeline_. Somente o envio _batch_ das mensagens é possível, através do qual todas as mensagens recebidas pelo polling do consumidor serão enviadas juntas em um _array_.

Por exemplo: se durante esse _poll_ forem retornadas 10 mensagens, então o _trigger_ enviará um _array_ com essas 10 mensagens.

{% hint style="info" %}
**IMPORTANTE:** poderá ocorrer um rebalanceamento dos consumidores e/ou das partições do Kafka. Caso isso ocorra entre o retorno da resposta do _pipeline_ ao _trigger_, os _offsets_ vão receber o _commit_. Isso pode acarretar em perdas ou mensagens duplicadas.
{% endhint %}

**Autocommit "false" e Batch Mode "true"**\
Nessa opção, o _poll_ realizado pode trazer um _array_ de mensagens e o seu tamanho máximo é estipulado pelo _Max Poll Records_. As mensagens passam por _commit_ somente depois que o _pipeline_ retornar a transação com sucesso. Se ocorrer _timeout_ durante o processamento do _pipeline_, as mensagens não vão passar por _commit_.

\
**Autocommit "false" e Batch Mode "false"**\
Nessa opção, o _poll_ vai enviar apenas 1 mensagem e não um _array_ de mensagens. Assim, o _throughput_ de envio/recebimento de mensagens é diminuído, mas a garantia do processamento bem sucedido é maior - ou seja, não há perda de mensagens.

{% hint style="info" %}
**IMPORTANTE:** se houver rebalanceamento do Tópico no Broker do Kafka durante o processamento das mensagens e os consumidores tiverem que assumir outras partições, as mensagens vão passar por _commit_ caso ocorra erro no término da execução do _pipeline_. Dessa maneira, as mensagens não vão ser processadas no _poll_ seguinte. Para contornar esse problema, recorra às configurações _**Autocommit "false"**_ e _**Batch Mode "false**_".
{% endhint %}

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Account:** nome da conta que será utilizada.
* **Truststore:** caso seja necessário informar uma _truststore_ para realizar o SSL Handshake usando certificados privados, crie uma conta do tipo _CERTIFICATE-CHAIN_ e informe os certificados concatenados. No campo _“password”_ é opcional inserir a senha a ser cadastrada na criação da _truststore_.
* **Keystore:** caso seja necessário informar uma _keystore_ para realizar a autenticação SSL mútua, crie uma conta do tipo _CERTIFICATE-CHAIN_, informe a cadeia completa com os certificados concatenados e a chave privada a ser utilizada para a autenticação SSL mútua. Caso exista uma chave privada, é necessário informá-la no campo _“password”_.
* **Brokers:** _brokers_ do servidor (HOST: PORT) usados para o envio de registros. Para informar múltiplos HOSTS, você pode separá-los por vírgula. Exemplo: HOST1:PORT1,HOST2:PORT2,...,HOSTn:PORTn
* **Topic:** nome do tópico que recupera os registros.
* **Protocol:** protocolo utilizado para se comunicar com os _brokers_.
* **Consumer Group Name:** um _string_ único que identifica o grupo de consumidor ao qual esse consumidor pertence.
* **Auto Commit:** se “true”, a mensagem passará automaticamente por _commit_ assim que for recebida pelo _trigger_; do contrário, o _trigger_ vai efetuar o _commit_ manualmente após a confirmação de processamento do _pipeline_.
* **Send Batch:** só pode ser utilizado com _autoCommit_ - se “true”, um _poll_ de mais de 1 mensagem será enviado como _array_; do contrário, será enviada 1 mensagem por vez.
* **Key As Avro:** se "true", as keys dos registros recebidos serão interpretadas no formato Avro, do contrário, serão interpretadas como String
* **Payload As Avro:** se "true", os payloads (values) dos registros recebidos serão interpretados no formato Avro, do contrário, serão interpretados como String&#x20;
* **Schema Registry URL:** caso ao menos uma das opções Key As Avro e Payload As Avro for ativada, o campo será exibido para que seja informada a URL do Schema Registry.&#x20;
* **Schema Registry Account:** account para autenticação com o Schema Registry (account Basic ou Oauth-Bearer).&#x20;
* **Schema Registry Truststore:** caso seja necessário informar uma truststore para realizar o SSL Handshake utilizando certificados privados, deve-se criar uma conta do tipo CERTIFICATE-CHAIN e informar os certificados concatenados. No campo “password” é opcional inserir a senha a ser cadastrada na criação da truststore.&#x20;
* **Schema Registry Keystore:** caso seja necessário informar uma keystore para realizar a autenticação SSL mútua, deve-se criar uma conta do tipo CERTIFICATE-CHAIN, informar a cadeia completa com os certificados concatenados e a chave privada a ser utilizada para a autenticação SSL mútua. Caso exista uma chave privada, é necessário informá-la no campo “password”.
* **Max Poll Records:** número máximo de registros recuperados por um _long poll_.
* **Include Headers:** se a opção estiver ativada, os cabeçalhos da mensagem serão incluídos no _payload_ de entrada do _pipeline._
* **Binary Headers:** se a opção estiver ativada, os valores dos cabeçalhos de entrada serão considerados como binários e apresentados como uma representação base64. Essa opção será apresentada apenas quando _Include Headers_ estiver ativado também.
* **Headers Charset:** nome do código de caracteres para a codificação dos valores dos cabeçalhos (padrão UTF-8). Essa opção será apresentada apenas quando _Include Headers_ estiver ativada também.
* **Maximum Timeout:** por quanto tempo um _pipeline_ pode ser executado (em milissegundos).
* **Kerberos Service Name:** valor definido na propriedade _**sasl.kerberos.service.name**_ configurado no lado _server_ do _broker_ Kafka.
* **Partition Numbers**: especifica os números das partições em que o **Kafka Trigger** consumirá mensagens. Pode-se configurar mais de uma partição e, caso essa propriedade não seja configurada, o _**Kafka Trigger**_ irá consumir de todas as partições do tópico.

{% hint style="info" %}
**IMPORTANTE:** aceitamos no máximo 5MB de mensagem de envio por _poll_. Não faz parte do padrão utilizar o Kafka para trafegar mensagens grandes. Recomendamos que você configure a propriedade (message.max.bytes) no broker para 1MB no máximo. . A capacidade de tráfego de dados no formato Avro também está inclusa nesta limitação de tamanho. As configurações de key e payload do Kafka Trigger devem estar de acordo com as configurações dos tópicos a serem consumidos pelo Trigger. Se Key As Avro for habilitada, todas as keys dos registros a serem consumidos devem estar no formato Avro. Se Payload As Avro for habilitada, todos os payloads (values) dos registros a serem consumidos devem estar no formato Avro.&#x20;

**Atualmente o suporte ao formato Avro está em fase Beta.**
{% endhint %}

### &#x20;Consumers

A configuração de consumidores impacta diretamente no _throughput_ de recebimento e saída de mensagens quando o Kafka Trigger é ativado. O cenário ideal de utilização é ter a mesma quantidade de _consumers_ configurados e partições em determinado tópico.

Caso haja mais _consumers_ do que partições, os _consumers_ excedentes ficarão _idle_ até ocorra um aumento de partições. E, se esse aumento ocorrer, Kafka vai iniciar o processo de rebalanceamento de _consumers_.

### Consumer Group <a href="#consumer-group" id="consumer-group"></a>

É o grupo de consumidores ao qual o seu _pipeline_ vai fazer a subscrição no tópico do Kafka. Um tópico pode ter “n” _Consumer Groups_ e cada um deles vai ter “n” consumidores que consomem os registros do tópico.

* **Cenário 1**

Digamos que exista um tópico chamado _kafka-topic_, um _pipeline_ que utilize um _trigger_ configurado com o _consumer group_ (groupId) nomeado _digibee_ e um segundo _pipeline_ que utilize um _trigger_ configurado com o mesmo tópico, mas com um _consumer group_ (groupId) nomeado digibee-2. Nesse caso, ambos os _pipelines_ receberão as mesmas mensagens.\


* **Cenário 2**

Digamos que exista um tópico chamado _kafka-topic_, um _pipeline_ que utilize um _trigger_ configurado com o _consumer group_ (groupId) nomeado _digibee_ e um segundo _pipeline_ que utilize um _trigger_ configurado com o mesmo tópico e _consumer group_ (digibee). Ambos os _pipelines_ vão receber as mensagens passadas por esse tópico. No entanto, o Kafka fica encarregado de fazer o balanceamento das partições entre os _consumers_ cadastrados nos dois _triggers_. Nesse caso, ambos os _pipelines_ vão receber mensagens de forma intercalada, de acordo com a distribuição das partições.

### Tecnologia <a href="#tecnologia" id="tecnologia"></a>

#### **Autenticação usando Kerberos** <a href="#autenticao-usando-kerberos" id="autenticao-usando-kerberos"></a>

Para utilizar a autenticação via Kerberos no _**Kafka Trigger**_ é necessário ter cadastrado o arquivo de configuração “krb5.conf” no parâmetro de _Realm_. Caso não tenha feito isso, acione o nosso suporte via _chat_. Após concluir esse passo, basta configurar corretamente uma conta do tipo Kerberos e utilizá-la no componente.

### Formato de mensagem na entrada do pipeline <a href="#h_7510e36b4b" id="h_7510e36b4b"></a>

_Pipelines_ associados ao Kafka Trigger recebem a seguinte mensagem como entrada:

```
{
  "data": [
    {
      "data": <STRING conteúdo da mensagem>,
      "topic": <STRING O tópico do qual o registro é recebido>,
      "offset": <LONG A posição do registro na partição Kafka correspondente>,
      "partition": <INT A partição da qual o registro é recebido>,
      "success": <BOOLEAN Indica se a mensagem individual foi consumida com sucesso ou não>,
      "headers": {
          "header1": "value1", … (quando incluídos)
      }
    }
  ],
  "success": <BOOLEAN Indica se todas as mensagens foram consumidas com sucesso ou não>
}
```

\
