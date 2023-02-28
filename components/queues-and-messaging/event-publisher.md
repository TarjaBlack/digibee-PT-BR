---
description: Conheça o componente e saiba como utilizá-lo.
---

# Event Publisher

Um evento é uma mensagem que notifica outros componentes sobre uma mudança de estado, uma ação ou um fato ocorrido. O _**Event Publisher**_ publica um evento para que outros _pipelines_ configurados para escutá-lo possam reagir quando a publicação ocorrer.

Mais informações sobre Arquitetura Orientada a Eventos podem ser encontradas [aqui](../../tutoriais-e-melhores-praticas/arquitetura-orientada-a-eventos.md).

Dê uma olhada nos parâmetros de configuração do componente:

* **Evento:** nome do evento criado que será publicado para consumo por outros _pipelines_. Este parâmetro aceita _Double Braces_.
* **Body:** _payload_ a ser enviado com o evento. Este parâmetro aceita _Double Braces_.
* **Log Each Event Sent:** quando ativada, a opção irá gerar uma entrada de _log_ para cada evento enviado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso artigo clicando [aqui](broken-reference).

## Como o Event Publisher é utilizado? <a href="#como-o-event-publisher--utilizado" id="como-o-event-publisher--utilizado"></a>

Para implementar uma Arquitetura Orientada a Eventos é necessário definir:

* o _pipeline_ que publicará o evento (Publicador)
* um ou mais _pipelines_ que irão consumir o evento (Assinantes)

Para configurar o _pipeline_ que publicará o evento:

* arraste o _**Event Publisher**_ para o _canvas_ do _pipeline_ Publicador;
* configure o nome do evento na propriedade “Evento” do _**Event Publisher**_;
* caso deseje passar um _payload_ junto com o evento, defina o conteúdo da propriedade “Body”.

Para configurar o _pipeline_ que consumirá o evento:

* altere o tipo do _trigger_ para "Event" no _pipeline_ Assinante;
* abra as configurações do _trigger_ e informe o nome do evento a ser consumido na propriedade “Nome do Evento”. Esse valor deve ser idêntico ao informado no _**Event Publisher**_ do _pipeline_ Publicador.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Entrada** <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem válida em formato JSON. Não é esperado nenhum atributo específico. A mensagem de entrada poderá ser referenciada através de _Double Braces_ tanto para a configuração do atributo “Evento” quanto do atributo “Body”. Por exemplo, digamos que a mensagem abaixo fosse passada para o _**Event Publisher**_:

```
{
"eventName": "example",
"body": {
"id": "1",
"description": "Description of the case"
}
}
```

Você poderia definir uma expressão _Double Braces_ no atributo “Evento” para obter o valor do atributo _eventName_:

```
{{ message.eventName }}
```

O atributo _body_ também poderia ser configurado da mesma forma:

```
{{ message.body }}
```

### **Saída** <a href="#sada" id="sada"></a>

O componente repassa a mensagem recebida do componente anterior sem nenhuma alteração. No caso do exemplo acima, a mensagem repassada seria:

```
{
"eventName": "example",
"body": {
"id": "1",
"description": "Description of the case"
}
}
```
