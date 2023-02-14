---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON to XML Transformer

O **JSON To XML Transformer** gera um XML baseado em um JSON recebido na sua mensagem de entrada.

Dê uma olhada nos parâmetros de configuração do componente:

* **JSON Field Path:** JSON como caminho do campo _string_ em notação com pontos (_dotted notation_).
* **Root Element Name:** elemento raiz do XML gerado.
* **Preserve Original:** se ativada, a opção preserva os campos originais.
* **Header:** XML _header_ a ser incluído antes do XML _payload_.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem em qualquer formato, mas vai procurar procurar por um caminho dentro da propriedade de configuração _JSON Field Path_.

Alguns exemplos válidos de entrada:

#### **Exemplo 1**

```
{
     "orders": {
      "order": [
        {
          "a": 1,
  "b": 1
        },
        {
          "a": 2,
          "b": 2
        },
        {
          "a": 3,
          "b": 3
        }
    ]
    }
  }
```

#### **Exemplo 2**

```
{
  "payload": {
    "test": {
      "a": 1,
      "b": 1
    }
  }
}
```

### Saída <a href="#sada" id="sada"></a>

A estrutura será igual a de entrada, porém com outra propriedade de JSON _string_ e a sua representação de objeto JSON. Em caso de erro, a propriedade "error" será criada no mesmo nível da propriedade original.

A notação com pontos (_dotted notation_) de JSON vai procurar pelo elemento raiz que está sendo processado pelo _pipeline_ e realizar um cruzamento de acordo com as especificações passadas na propriedade _JSON Field Path_.

#### **Exemplo**

Em uma representação do _JSON Field Path_ contendo a.b.c.d, "a" será procurado no elemento raiz. Em seguida será o "b", depois o "c" e finalmente o "d". Se um _array_ for encontrado durante o cruzamento, então o algoritmo vai gerar um caminho de cruzamento para cada elemento no _array_. O algoritmo substitui todas as ocorrências do caminho definido em _JSON Field Path_.

#### **Sem erro**

```
{
 "XPTO": "TEMPLATE TRANSFORMADO"
"_body": {}
}
```

* **\_body:** se a opção **Preserve Original** estiver habilitada, a propriedade será exibida na saída contendo o JSON de entrada
* **XPTO:** nome dinâmico baseado na configuração do _JSON Field Path_ nas propriedades do componente

#### **Com erro**

```
{
  "body": null,
  "_error": "Can not construct instance of java.util.LinkedHashMap: no String-argument constructor/factory method to deserialize from String value ('')\n at [Source: N/A; line: -1, column: -1]",
  "_body": ""
}
```

* **\_body:** se a opção **Preserve Original** estiver habilitada, a propriedade será exibida na saída contendo o JSON de entrada
* **\_error:** descrição do erro que ocorreu na execução
* **XPTO:** nome dinâmico baseado na configuração do _JSON Field Path_ nas propriedades do componente

## JSON to XML Transformer em Ação <a href="#json-to-xml-transformer-em-ao" id="json-to-xml-transformer-em-ao"></a>

#### **Exemplo 1**

* **JSON Field Path:** orders
* **Root Element Name:** doc
* **Preserve Original:** habilitado
* **Header:** \<?xml version='1.0' encoding='UTF-8' standalone='no' ?>

#### **Entrada**

```
{
     "orders": {
      "order": [
        {
          "a": 1,
          "b": 1
        },
        {
          "a": 2,
          "b": 2
        },
        {
          "a": 3,
          "b": 3
        }
      ]
    }
 }

```

#### **Saída**

```
{
  "orders": "<?xml version='1.0' encoding='UTF-8' standalone='no' ?><doc><order><a>1</a><b>1</b></order><order><a>2</a><b>2</b></order><order><a>3</a><b>3</b></order></doc>",
  "_orders": {
    "order": [
      {
        "a": 1,
        "b": 1
      },
      {
        "a": 2,
        "b": 2
      },
      {
        "a": 3,
        "b": 3
     }
    ]
  }
}
```

#### **Exemplo 2**

* **JSON Field Path:** payload
* **Root Element Name:** xpto
* **Preserve Original:** desabilitado

#### **Entrada**

```
{
  "payload": {
    "test": {
      "a": 1,
      "b": 1
    }
  }
}

```

#### **Saída**

```
{  
    "payload": "<xpto><test><a>1</a><b>1</b></test></xpto>"
}
```

\
