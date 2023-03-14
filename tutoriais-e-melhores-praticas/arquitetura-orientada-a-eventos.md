# Arquitetura orientada a eventos

Usar um único pipeline para realizar todas as tarefas do seu fluxo de integração pode parecer uma solução simples e eficiente, mas esse método pode trazer problemas a longo prazo. Aqui, vamos falar sobre arquitetura orientada a eventos, um modelo mais eficiente que divide seu fluxo de integração em vários pipelines.

## O padrão publisher-subscriber

Suponha que você fez uma compra com seu cartão de crédito. Após você fazer a transação, você recebe uma notificação do seu aplicativo do banco confirmando a compra e um e-mail da loja contendo a nota fiscal.

Vamos usar esse exemplo para ilustrar um conceito importante na arquitetura de pipelines : a arquitetura orientada a eventos. Alguns conceitos importantes desse modelo são:

* **Evento**: uma ação de interesse de um sistema. No nosso exemplo, sua compra é um evento
* **Publisher (publicadores)**: a parte do sistema que informa quais eventos ocorreram. No nosso exemplo, a empresa de cartão de crédito é um publisher. Na Digibee Integration Platform, você pode publicar eventos com o componente Event Publisher
* **Subscriber ou consumer (inscrito ou consumidor)**: a parte do sistema que recebe informações acerca de certos eventos. No nosso exemplo, o aplicativo do banco e o e-mail da loja são subscribers. Na Digibee Integration Platform, você pode criar um subscriber com um Event Trigger

No padrão publisher-subscriber, registros de eventos não são comunicados a subscribers específicos. Eles são enviados a um log administrado por um event broker, como o Apache Kafka ou o RabbitMQ. Consumers inscritos nesses eventos são informados quando eles ocorrem.

Note que um único evento pode ser comunicado a vários subscribers. No nosso exemplo, o evento da compra foi comunicado tanto ao aplicativo do banco quanto ao e-mail da loja.

Note também que publishers e subscribers não estão “cientes” uns dos outros e existem independentemente. Suponha que a loja não tenha e-mail e que o aplicativo do banco esteja fora do ar. Mesmo não havendo subscribers para o evento da compra, a empresa de cartão de crédito o publicaria de qualquer maneira.

<figure><img src="https://lh5.googleusercontent.com/bzYVFk5CVCKUNKdSCzEJl7B1WROonVQAOf4WNLh0Ip8kD4mV4JDHM_ygym35zbg_shXg1ktyTnP7_OG-eC7cMleLnN8XQ2qOXoMbJJtWeCLLOdmT0fpSq9snu30ZjvV2_taZpPQ1D5YGSIHWlZ9fEMKhtL76-UwNLW7uJPSFmC0I1cOLmgIp7v1Ywg" alt=""><figcaption><p>Padrão publisher-subscriber</p></figcaption></figure>

Na Digibee Integration Platform, você pode usar a arquitetura orientada a eventos para dividir seu fluxo de integração em mais de um pipeline e usar cada pipeline para um propósito específico. Esse modelo oferece várias vantagens, como:

* **Evitar retrabalho**: suponha que você está construindo dez pipelines. Em cada pipeline, você quer fazer uma chamada a uma REST API de uma ferramenta ITSM sempre que um erro ocorre. Em vez de configurar o request em cada um dos dez pipelines, você pode criar um pipeline que faz essa chamada e usar Event Publishers nos outros pipelines para ativá-lo.
* **Facilitar manutenção**: suponha que você queira fazer um ajuste a essa parte do fluxo de integração responsável por enviar uma mensagem de erro a uma ferramenta ITSM. Em vez de ajustar dez pipelines, você pode ajustar somente a que faz a chamada API
* **Evitar erros**: usando um pipeline para cada tarefa, você reduz a chance de erros Out of Memory ou Timeout, causados por sobrecarga no pipeline
* **Escalar de acordo com sua necessidade**: usando a arquitetura orientada a eventos, você pode aumentar o tamanho de implementação somente dos pipelines do seu fluxo de integração que requerem mais memória, em vez de aumentar o de todos eles

## Modelo síncrono

Um dos modelos que usam arquitetura orientada a eventos na Digibee Integration Platform é o modelo síncrono. Nesse modelo, dividimos nosso fluxo de integração em dois tipos de pipelines: os pipelines de regra de negócio e os pipelines de tratamento de erros.

Os pipelines de regra de negócio realizam todos os passos necessários para fazer sua integração de dados. Quando um erro ocorre nesses processos, um componente Log os registra e um componente Event Publisher publica o evento de erro.

O pipeline de tratamento de erro é um único pipeline que possui um trigger de evento. Ele “escuta” os eventos de erro que são publicados pelos pipelines de regra de negócio. Esse pipeline pode enviar alertas de erro ou reprocessar dados.

Note que o mesmo evento de erro pode ser publicado por vários pipelines e enviado para o mesmo pipeline de tratamento de erro.

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption><p><strong>Modelo síncrono</strong></p></figcaption></figure>

{% hint style="success" %}
Use o modelo síncrono para integrações que exigem confirmação imediata
{% endhint %}

{% hint style="danger" %}
Não use o modelo síncrono para integrações que:&#x20;

* Manipulem grandes quantidades de dados&#x20;
* Insiram, modifiquem ou deletem dados em um banco de dados&#x20;
* Façam chamadas POST para serviços que não suportam grandes listas de dados
* Demorem pra processar
{% endhint %}

## O modelo assíncrono

Outro modelo que usa a arquitetura orientada a eventos é o modelo assíncrono. Para construir um fluxo de integração usando um modelo assíncrono, você deve construir quatro pipelines.

**O primeiro pipeline** busca dados de um banco de dados ou de uma API e publica um evento para cada registro de dados. Se um erro ocorrer nesse processo, esse pipeline publica um evento de erro.

**O segundo pipeline** é inscrito nos eventos publicados pelo primeiro pipeline. Ele recebe os registros de dados que foram buscados do banco de dados e os processa de acordo com a regra de negócio. Se um erro ocorrer durante esse processo, esse pipeline registra o erro, assim como o payload de input em um Object Store.

**O terceiro pipeline** periodicamente acessa o Object Store mencionado anteriormente e busca registros de erros. Depois, ele checa quantas tentativas de reprocessamento já foram feitas para um determinado registro. Se o número de tentativas ainda não alcançou um limite definido anteriormente, o pipeline publica um evento de reprocessamento que será recebido pelo segundo pipeline. Se o número de tentativas de reprocessamento atingir o limite ou se um erro acontecer durante a execução desse pipeline, ele publica um evento de erro.

**O quarto pipeline** é inscrito nos eventos de erro que foram enviados pelos três pipelines anteriores. Depois de receber esses eventos de erro, ele os armazena em um banco de dados e envia esses registros a uma ferramenta de ITSM ou por email.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p><strong>Modelo assíncrono</strong></p></figcaption></figure>

{% hint style="success" %}
Use o modelo assíncrono para integrações que:&#x20;

* Insiram dados em um banco de dados&#x20;
* Manipulem grandes quantidades de dados
* Façam chamadas POST a serviços que não suportem grandes listas de dados
* Demorem para processar
{% endhint %}

{% hint style="danger" %}
Não use o modelo assíncrono para integrações que exigem confirmação imediata
{% endhint %}
