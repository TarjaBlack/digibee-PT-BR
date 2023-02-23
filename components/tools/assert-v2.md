---
description: Conheça o componente e saiba como utilizá-lo.
---

# Assert V2

O **Assert V2** permite que você crie a interrupção da execução do seu _pipeline_ quando uma condição definida não for atendida. Essa condição será avaliada de acordo com itens da mensagem do _pipeline_, sendo que _Double Braces_ são utilizados para isso.

**Dica:** utilize o Assert para garantir uma condição ou interromper o fluxo.

Dê uma olhada nos parâmetros de configuração do componente:

* **Condition:** quando essa condição não for verdadeira, a execução do _pipeline_ será interrompida (expressões em _Double Braces_ devem ser utilizadas nesse campo).
* **Error Message:** define a mensagem de erro que é retornada pelo _pipeline_ quando a condição não for verdadeira.
* **Internal Error Message:** campo onde você define a mensagem de erro interna quando a condição não for verdadeira (é uma mensagem apenas para fins internos).
* **HTTP Status Code:** status de retorno do componente.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela através de D_ouble Braces_.

#### **Saída** <a href="#sada" id="sada"></a>

O componente não altera nenhuma informação da mensagem de entrada quando a condição é verdadeira. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se o _**Assert V2**_ for o último passo do _pipeline._

Quando a condição for falsa e a propriedade _**Fail On Error**_ for “true”, a saída do componente segue a estrutura padrão:

```
{  
    "timestamp": 1587151050249,  
    "error": "<message declares in the config errorMessage>",  
    "code": <errorCode>
}
```

Se _**Fail On Error**_ for “false”:

```
{
  "error": "<message declares in the config errorMessage>",
  "internalErrorMessage": "<message declares in the config internalErrorMessage>",
  "code": <errorCode>,
  "success": false
}
```

Conforme visto, você deve utilizar expressões em _Double Braces_ no campo CONDIÇÃO.

Para ler o nosso artigo sobre _Double Braces_, clique [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

### Assert V2 em Ação <a href="#assert-v2-em-ao" id="assert-v2-em-ao"></a>

* \{{ AND( EQUALTO(message.name, "Arthur"), LESSTHAN( message.number, 40)) \}}

Recebendo uma mensagem:

```
{  
    "name": "Jimmy",  
    "number": 39
}
```

A condição resultará “false”.

* \{{ AND( EQUALTO(message.name, "Arthur"), LESSTHAN( message.number, 40)) \}}

Recebendo uma mensagem:

```
{  
    "name": "Arthur",  
    "number": 39
}
```

A condição resultará “true”.

\
