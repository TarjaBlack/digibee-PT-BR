---
description: Conheça o componente e saiba como utilizá-lo.
---

# Log

O **Log** permite criar registros de _logs_ dentro do fluxo de um _pipeline_. Ele auxilia na geração da rastreabilidade do passos quando você desejar.&#x20;

Os _logs_ gerados ficam disponíveis no Dashboard -> Logs.

Além disso, quando você está construindo um _pipeline_ e realiza testes na área _test-mode,_ os resultados ficam disponíveis também na aba LOGS, ao lado de MENSAGENS.\


Dê uma olhada nos parâmetros de configuração do componente:

* **Step Name:** define o nome do componente no _canvas_.
* **Log Level:** define como será classificado o _log_ gerado (possui as opções INFO, ERROR e WARN).
* **Message:** define a mensagem que será registrada no _log_ - é possível utilizar a funcionalidade de _Double Braces,_ que permite compor a mensagem com dados do fluxo do _pipeline_.

**Exemplo:**\
Ocorreu um erro ao tentar registrar o cliente código \{{ message.id \}}&#x20;

{% hint style="info" %}
**IMPORTANTE:** todos os caracteres de quebra de linha (\n ou \r\n) serão removidos na exibição dos logs.
{% endhint %}

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela através de _Double Braces_.

### Saída <a href="#sada" id="sada"></a>

O componente não altera nenhuma informação da mensagem de entrada. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se este componente for o último passo do _pipeline_.

## Campos sensíveis <a href="#h_9296d1d973" id="h_9296d1d973"></a>

Quando configurado campos sensíveis no pipeline ou em seu _realm_, esses campos aparecerão na saída do conector ofuscados com o conjunto de caracteres **"\*\*\*"**.

**Exemplo:**

Imagine que o campo sensível _**email**_ esteja definido no _pipeline_ e a mensagem do componente Log esteja configurada conforme abaixo:

```
Ocorreu um erro ao enviar email para {{ message.email }} no dia {{ message.dateTime }}
```

O _log_ será apresentado da seguinte forma:

```
Ocorreu um erro ao enviar email para *** no dia 07/05/2021 10:11:33:5120  
```

{% hint style="info" %}
**IMPORTANTE:** a ofuscação dos campos sensíveis necessita de mais recursos de processamento e memória do _pipeline_. Esses recursos adicionais são afetados tanto pela quantidade de campos sensíveis configurados quanto pelo tamanho da mensagem.
{% endhint %}

\
