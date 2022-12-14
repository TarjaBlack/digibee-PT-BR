---
description: Conheça o trigger e saiba como utilizá-lo.
---

# JMS Trigger

#### IMPORTANTE: O JMS Trigger precisa de uma infraestrutura dedicada. Por questões de segurança, é necessário entrar em contato com a nossa Equipe de Suporte para obter a liberação e usar este _trigger_.&#x20;

Digamos que você queira utilizar um _trigger_ para realizar a subscrição em uma fila de mensagens. Dessa maneira, você consegue disparar um _pipeline_ que habilita o consumo de uma mensagem por vez.

### **Commit com garantia de entrega**

Com a propriedade Auto Commit desabilitada, é possível dar o _ack_ da mensagem somente após a execução bem sucedida do _pipeline_. Para o _broker_ IBM MQ, é necessário manter esse campo sempre habilitado, pois não é suportado controlar o _ack_ ou o _reject_ da mensagem.

### Filas suportadas e parâmetros de configuração

As filas suportadas são:

* Oracle Advanced Queue
* Tibco EMS
* SQS
* IBM MQ

Dê uma olhada nos parâmetros de configuração do _trigger_:  &#x20;

* **Account:** define a conta que será usada pelo _trigger_.
* **Auto Commit**: quando ativada, a estratégia de _auto commit_ JMS será usada. Se não for ativada, o _commit_ manual será usado.
* **Destination:** define o parâmetro (_Queue_ ou _Topic_).
* **Name of the Queue or Topic:** nome único dado ao _Queue_ ou _Topic_ selecionado.
* &#x20;**Which JMS Provider Will Be Used:** seleciona a fila desejada (Oracle Advanced Queue, Tibco EMS, SQS ou IBM MQ). Dependendo da fila, parâmetros diferentes podem ser acessados:

### Oracle AQ <a href="#oracle-aq" id="oracle-aq"></a>

* **Hostname:** o nome do _host_ da conexão _string_ JMS.
* **SID - Oracle Site Identifier:** nome do banco de dados Oracle.&#x20;
* **Port:** número da porta de acesso ao servidor Oracle.
* **JDBC Type:** _driver_ **** Oracle jbdc(ex.: THIN ou OCI).
* **Durable Subscriber:** consumidor de mensagem que recebe todas as mensagens publicadas em um tópico, incluindo aquelas publicadas enquanto o _subscriber_ está inativo; quando essa opção estiver ativada, é necessário informar o nome específico do _subscriber_ no campo "_Subscriber Name"_.
* **Set Client ID:** propriedade utilizada especificamente por um provedor JMS para identificar a conexão JMS do cliente e permitir que ela seja durável
* **Message Selector:** se a sua aplicação precisa filtrar as mensagens recebidas, você pode utilizar um selecionador de mensagens JMS API, que permite ao consumidor de mensagens especificar quais delas interessam - o _message selector_ repassa a filtragem para o provedor JMS.
* **Maximum Timeout:** preencha o tempo máximo de execução do _trigger_.
* **Allow Redelivery of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_.&#x20;

### Tibco EMS <a href="#tibco-ems" id="tibco-ems"></a>

* **Connection String:** conexão string JMS no formato _tcp://{host}:{port}._
* **Durable Subscriber:** consumidor de mensagem que recebe todas as mensagens publicadas em um tópico, incluindo aquelas publicadas enquanto o _subscriber_ está inativo; quando essa opção estiver ativada, é necessário informar o nome específico do _subscriber_ no campo _**Subscriber Name**_.
* **Set Client ID:** propriedade utilizada especificamente por um provedor JMS para identificar a conexão JMS do cliente e permitir que ela seja durável.
* **Message Selector:** se a sua aplicação precisa filtrar as mensagens recebidas, você pode utilizar um selecionador de mensagens JMS API, que permite ao consumidor de mensagens especificar quais delas interessam - o _message selector_ repassa a filtragem para o provedor JMS. &#x20;
* **Maximum Timeout:** preencha o tempo máximo de execução do _trigger_.
* **Allow Redelivery of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_.&#x20;

### SQS <a href="#sqs" id="sqs"></a>

* **Connection String:** conexão string JMS no formato _https://{REGION\_ENDPOINT}/queue.|api-domain|/{YOUR\_ACCOUNT\_NUMBER}/{YOUR\_QUEUE\_NAME}_
* **Region:** região da AWS onde a fila está instalada.
* **Set Client ID:** propriedade utilizada especificamente por um provedor JMS para identificar a conexão JMS do cliente e permitir que ela seja durável.
* **Maximum Timeout:** preencha o tempo máximo de execução do _trigger_.
* **Allow Redelivery of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_.&#x20;

{% hint style="info" %}
**IMPORTANTE:**  o Visibility Timeout no Broker SQS deve ter um valor maior ou igual que o _timeout_ do _pipeline_. Isso é necessário, porque o Broker SQS é um sistema distribuído e não remove a mensagem após o seu consumo, já que não há garantia de que ela foi realmente consumida. Se o Visibility Timeout não é configurado dentro das condições mencionadas, pode ocorrer o reenvio de uma mensagem em processamento. O Broker SQS envia a mensagem novamente caso ela não receba ACK ou REJECT dentro do tempo configurado em Visibility Timeout. Para entender melhor, clique [aqui](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html).
{% endhint %}

### **IBM MQ**

**Não há suporte ainda para autenticação usando TLS.**

* **Hostname:** nome do _host_ da conexão _string_ JMS.
* **Channel Name:** nome do canal a ser utilizado na comunicação do _broker_.
* **Queue Manager:** nome do gerenciador de filas do IBM MQ.
* **Port:** número da porta de acesso ao servidor Oracle.
* **Durable Subscriber:** consumidor de mensagem que recebe todas as mensagens publicadas em um tópico, incluindo aquelas publicadas enquanto o _subscriber_ está inativo; quando essa opção estiver ativada, é necessário informar o nome específico do _subscriber_ no campo _Subscriber Name._
* **Set Client ID:** propriedade utilizada especificamente por um provedor JMS para identificar a conexão JMS do cliente e permitir que ela seja durável.
* **Message Selector:** se a sua aplicação precisa filtrar as mensagens recebidas, você pode utilizar um selecionador de mensagens JMS API, que permite ao consumidor de mensagens especificar quais delas interessam - o _message selector_ repassa a filtragem para o provedor JMS.
* **Maximum Timeout:** tempo máximo de execução do _trigger_.
* **Allow Redelivery of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_.

### JMS Trigger em ação

Se você deseja disparar o _trigger_, será necessário publicar o _pipeline_.

Veja como realizar o _deploy_:

* Clique em "Run", localizado na parte superior da tela.
* Selecione o ambiente, que pode ser _**test**_ ou _**prod**_.
* Clique em "Criar uma nova implantação".
* Selecione o _pipeline_ com a sua versão e capacidade.
* Clique em "Confirmar".

Quando for disparado, o _pipeline_ receberá um _payload_ similar ao seguinte:

```
{  
    "data":"mensagem"
}
```

&#x20;            &#x20;

* **data:** conteúdo da mensagem recebida

&#x20;  \
O **JMS Trigger** suporta o consumo de mensagens de forma paralela - o número de _consumers_ configurado na hora do _deploy_ de um _pipeline_ será exatamente o mesmo para a fila/tópico JMS.

Portanto, se forem configurados 10 _consumers_ no deploy, 10 _consumers_ serão criados de tópico/fila JMS.

Isso aumenta o _throughput_ de consumo das mensagens, além de permitir ao usuário ter controle de quantos consumidores simultâneos ele poderá criar.

Antigamente havia apenas um _consumer_ por _trigger_.\
&#x20;            &#x20;

{% hint style="info" %}
**IMPORTANTE:** caso você realize o _deploy_ de um _pipeline_ com o trigger JMS atrelado a um tópico, é preciso configurar apenas 1 _consumer_ na hora de realizar o _deploy_.
{% endhint %}
