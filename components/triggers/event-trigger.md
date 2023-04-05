---
description: Conheça o trigger e saiba como utilizá-lo.
---

# Event Trigger

Um evento é uma mensagem que notifica outros componentes sobre uma mudança de estado, uma ação ou um fato ocorrido. O _**Event Trigger**_ responde a um evento específico gerado por outro _pipeline_ por meio do _Event Publisher_. Para ler sobre esse componente, clique [aqui](../queues-and-messaging/event-publisher.md).

Mais informações sobre Arquitetura Orientada a Eventos podem ser encontradas [aqui](../../tutoriais-e-melhores-praticas/arquitetura-orientada-a-eventos.md).

Os parâmetros de configuração do _trigger_ são os seguintes:

* **Event Name:** nome do evento ao qual o _trigger_ responde.
* **Expiration:** tempo de permanência do evento em fila (em milissegundos). Se o _expiration_ for = 0 ou um valor maior que 6h, então o _expiration_ será 1/4 do valor _**Maximum timeout**_ especificado.
* **Maximum Timeout:** tempo máximo de execução do _pipeline_ iniciado pelo _**Event Trigger**_ (em milissegundos).
* **Allow Redelivery of Messages:** se ativada, a opção permite que mensagens sejam entregues novamente caso o _Pipeline Engine_ falhe.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Entrada** <a href="#entrada" id="entrada"></a>

O _trigger_ espera uma mensagem válida em formato JSON. A mensagem recebida é exatamente aquela que foi definida no atributo _**body**_ do componente _Event Publisher_.

```
{    
    "id": "1",    
    "description": "Description of the case"
}
```

### **Saída** <a href="#sada" id="sada"></a>

O componente repassa a mensagem recebida do componente anterior sem nenhuma alteração. No caso do exemplo acima, a mensagem repassada seria:

```
{    
    "id": "1",    
    "description": "Description of the case"
}
```

## Event Trigger em Ação <a href="#event-trigger-em-ao" id="event-trigger-em-ao"></a>

#### Para implementar uma Arquitetura Orientada a Eventos é necessário definir:

* o _pipeline_ que publicará o evento (Publicador)
* um ou mais _pipelines_ que irão consumir o evento (Assinantes)

#### Para configurar o _pipeline_ que publicará o evento:

* arraste o _Event Publisher_ para o _canvas_ do _pipeline_ Publicador;
* configure o nome do evento na propriedade “Evento” do _Event Publisher_;
* caso deseje passar um _payload_ junto com o evento, defina o conteúdo da propriedade “Body”.

#### Para configurar o _pipeline_ que consumirá o evento:

* altere o tipo do _trigger_ para _**Event**_ no _pipeline_ Assinante;
* abra as configurações do _trigger_ e informe o nome do evento a ser consumido na propriedade “Nome do Evento”. Esse valor deve ser idêntico ao informado no _Event Publisher_ do _pipeline_ Publicador.

\
