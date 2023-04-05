---
description: Conheça o componente e saiba como utilizá-lo.
---

# Script

O componente _**Script**_ permite executar trechos de código _javascript_, também conhecido como _ECMAScript_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Code:** onde o código em _javascript_ pode ser escrito.
* **Script Timeout:** tempo para que o _script_ expire (em milissegundos).

## Fluxo de mensagens <a href="#h_4fb1281253" id="h_4fb1281253"></a>

### Entrada <a href="#h_dca97c2937" id="h_dca97c2937"></a>

O componente _**Script**_ pode receber parâmetros de componentes prévios através do objeto "body" - ou seja, caso a saída do componente anterior ao _**Script**_ tiver uma saída que inclui um objeto chamado "body", é possível acessá-lo diretamente no código do _Script_.

* **body:** objeto importado para o escopo do código do _**Script**_.

Por exemplo, caso a entrada seja:

```
{
    "body": {
        "company": "Digibee"
    }
}
```

Então no campo _code_ será possível fazer algo como:

```
var x = body.company;
```

### Saída <a href="#h_7f5258bc68" id="h_7f5258bc68"></a>

O código executado no componente pode produzir uma saída, desde que ela seja atribuída a variável global chamada _output_.

* **success:** "true" se a execução do código foi bem sucedida, "false" caso contrário.
* **output:** saída personalizável do componente.

Por exemplo, se você quiser que a saída do componente _**Script**_ seja 'Hello world' basta atribuí-lo à variável _output_:

```
output = 'Hello world';
```

O resultado após executar o _pipeline_ será:

```
{
    "success": true,
    "output": "Hello world"
}
```

Também é possível construir um objeto JSON como saída:

```
output = { "company": "Digibee" }
```

O resultado após executar o _pipeline_ será:

```
{
    "success": true,
    "output": { 
        "company": "Digibee" 
    }
}
```

Caso algum erro ocorra durante a execução do _script_, a seguinte saída é apresentada após a execução do _pipeline_:

```
{
    "success": false,
    "error": "Error message"
}
```

{% hint style="info" %}
**IMPORTANTE:** por questões de segurança, não é possível executar nenhuma função que faça uma chamada externa a partir do componente _Script_, como por exemplo _fetch()_ ou _XMLHttpRequest()_. Também não é possível importar Bibliotecas usando _require_.&#x20;
{% endhint %}

No entanto, as seguintes Bibliotecas já estão disponíveis e podem ser utilizadas:

* Lodash (variável global para utilizar lodash lib: 'lodash')
* Moment Timezone (variável global para utilizar moment-timezone: 'moment')
