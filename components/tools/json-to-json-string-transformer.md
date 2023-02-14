---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON to JSON String Transformer

O **JSON to JSON String Transformer** transforma objetos JSON em JSON _strings_.

Dê uma olhada nos parâmetros de configuração do componente:

* **JSON Field Path:** JSON como caminho do campo _string_ em notação com pontos.
* **Preserve Original:** se ativada, a opção preserva os campos originais.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Entrada** <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem em qualquer formato, mas vai procurar procurar por um caminho dentro da propriedade de configuração _**JSON Field Path**_.

### **Saída** <a href="#sada" id="sada"></a>

A estrutura será igual a de entrada, porém com outra propriedade de JSON _string_ e a sua representação de objeto JSON. Em caso de erro, a propriedade "error" será criada no mesmo nível da propriedade original.

A notação com pontos de JSON vai procurar pelo elemento raiz que está sendo processado pelo _pipeline_ e realizar um cruzamento de acordo com as especificações passadas na propriedade _**JSON Field Path**_.

#### **Exemplo:**

Em uma representação do _**JSON Field Path**_ contendo a.b.c.d, "a" será procurado no elemento raiz. Em seguida será o "b", depois o "c" e finalmente o "d". Se um _array_ for encontrado durante o cruzamento, então o algoritmo vai gerar um caminho de cruzamento para cada elemento no _array_.&#x20;

O algoritmo substitui todas as ocorrências do caminho definido em _**JSON Field Path**_.

## JSON to JSON String Transformer em Ação <a href="#json-to-json-string-transformer-em-ao" id="json-to-json-string-transformer-em-ao"></a>

### Config <a href="#config" id="config"></a>

```
{
"type": "transformer",
"stepName": "prepare-transformer",
"transformSpec": [
    {
    "operation": "default",
        "spec": {
            "payload": {
                "a": "a",
                    "b": [
                        {
                            "c": 2,
                            "d": 3
                        }
                    ]
                }
            }
        }
    ]
},
{
    "type": "json-to-json-string-transformer",
    "stepName": "json-to-json-string-transformer",
    "jsonFieldPath": "payload",
    "preserveOriginal": true
}
```

### Resultado <a href="#resultado" id="resultado"></a>

```
{
"payload": "{\"a\":\"a\",\"b\":[{\"c\":2,\"d\":3}]}",
    "_payload": {
    "a": "a",
        "b": [
            {
                "c": 2,
                "d": 3
            }
        ]
    }
}
```

\
