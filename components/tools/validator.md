---
description: Conheça o componente e saiba como utilizá-lo.
---

# Validator

O _**Validator**_ tem a função de analisar um JSON de entrada e compará-lo ao _schema_ fornecido, para que seja criada uma validação dentro de seu _pipeline_ e interrompa o fluxo se a estrutura não estiver de acordo com o declarado.

_JSON Schema_ é um vocabulário bastante difundido no mercado, que permite validar documentos JSON. Para saber mais sobre esse vocabulário, clique [aqui](https://json-schema.org/).

Dê uma olhada nos parâmetro de configuração do _**Validator**_:

* **JSON Schema:** definição JSON Schema que valida o JSON

### Fluxo de mensagens <a href="#h_b973e0f591" id="h_b973e0f591"></a>

#### Entrada <a href="#h_0e8e92558e" id="h_0e8e92558e"></a>

O componente aceita mensagens de entrada do tipo JSON para realizar a validação.

```
{
   "data": [
       {
           "product": "Samsung 4k Q60T 55",
           "price": 3278.99
       },
       {
           "product": "Samsung galaxy S20 128GB",
           "price": 3698.99
       }
   ]
}
```

#### Saída <a href="#h_a5ce7d5374" id="h_a5ce7d5374"></a>

O componente não altera nenhuma informação da mensagem de entrada quando o _**JSON Validador**_ estiver de acordo com _JSON Schema_. Portanto, a mensagem é retornada para o componente seguinte ou é utilizada como resposta final se esse componente for o último passo do _pipeline_.

```
{
   "data": [
       {
           "product": "Samsung 4k Q60T 55",
           "price": 3278.99
       },
       {
           "product": "Samsung galaxy S20 128GB",
           "price": 3698.99
       }
   ]
}
```

### Validator em Ação <a href="#h_be2ba24eca" id="h_be2ba24eca"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

* **Informando um **_**schema**_** e enviando um JSON que não atende aos requisitos**

Configure o componente com o seguinte _schema_:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "price": {
      "type": "number"
    }
  },
  "required": [
    "name",
    "price"
  ]
}
```

Depois, envie o seguinte JSON para o componente:

**Entrada**

```
{
    "name": "Samsung galaxy S20 128GB",
    "price": 3698.99
}
```

**Saída**

```
{
  "timestamp": 1614186691087,
  "error": "Failed to validate message. #Validation: error: object has missing required properties ([\"product\"])\n    level: \"error\"\n    schema: {\"loadingURI\":\"#\",\"pointer\":\"\"}\n    instance: {\"pointer\":\"\"}\n    domain: \"validation\"\n    keyword: \"required\"\n    required: [\"price\",\"product\"]\n    missing: [\"product\"]\n",
  "code": 400
}
```

* **Informando um **_**schema**_** e enviando um JSON que atende aos requisitos**

Configure o componente com o seguinte _schema_:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "product": {
              "type": "string"
            },
            "price": {
              "type": "number"
            }
          },
          "required": [
            "product",
            "price"
          ]
        },
        {
          "type": "object",
          "properties": {
            "product": {
              "type": "string"
            },
            "price": {
              "type": "number"
            }
          },
          "required": [
            "product",
            "price"
          ]
        }
      ]
    }
  },
  "required": [
    "data"
  ]
}
```

Depois, envie o seguinte JSON para o componente:

#### Entrada <a href="#h_2772aafb26" id="h_2772aafb26"></a>

```
{    
    "product": "Samsung galaxy S20 128GB",    
    "price": 3698.99
}
```

#### Saída <a href="#h_38fea8cd86" id="h_38fea8cd86"></a>

```
{    
    "product": "Samsung galaxy S20 128GB",    
    "price": 3698.99
}
```

\
