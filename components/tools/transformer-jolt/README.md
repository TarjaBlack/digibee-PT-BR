---
description: Conheça o componente e saiba como utilizá-lo.
---

# Transformer (JOLT)

O _**Transformer (JOLT)**_ permite a manipulação de um JSON através da tecnologia JOLT.

O componente é útil para:

* modificar a estrutura de um JSON mantendo seus valores;
* adicionar, extrair e remover dados de um JSON;
* ordenar a estrutura de um JSON;
* modificar os valores contidos em um JSON através de funções, como manipular textos, realizar cálculos matemáticos, conversão entre tipos de dados, entre outros;
* acessar e manipular dados de _arrays_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Type Properties**: área para inclusão das transformações JOLT.

Exemplo de _**Transformer (JOLT)**_ configurado:

![](<../../../.gitbook/assets/transformer jolt.png>)

{% hint style="info" %}
**IMPORTANTE**: o JSON configurado em _**Type Properties**_ não representa o JSON a ser manipulado e sim a transformação via JOLT em si. O próprio JOLT utiliza uma estrutura JSON para a construção das transformações, que interpretarão o JSON recebido pelo componente _**Transformer (JOLT)**_.
{% endhint %}

## Operações JOLT <a href="#h_529946f6d7" id="h_529946f6d7"></a>

### _**Shift**_

Utilizada para alterar a estrutura de um JSON, mantendo os valores contidos nesse mesmo JSON.

**Exemplo:**

Entrada

```
{  
    "body": {    
        "userName": "John"  
    }
}
```

Transformação

```
[
  {
    "operation": "shift",
    "spec": {
      "body": {
        "userName": "dados.nomeUsuario"
      }
    }
  }
]
```

Saída

```
{
  "dados" : {
    "nomeUsuario" : "John"
  }
}
```

### _**Default**_

Utilizada para adicionar novos campos ou objetos em um JSON, caso esses não existam previamente.

**Exemplo:**

Entrada

```
{
  "body": {
    "userName": "John"
  }
}
```

Transformação

```
[
  {
    "operation": "default",
    "spec": {
      "body": {
        "email": "default@email.com"
      }
    }
  }
]
```

Saída

```
{
  "body": {
    "userName": "John",
    "email": "default@email.com"
  }
}
```

### _**Remove**_

Utilizada para remover campos ou objetos de um JSON.

**Exemplo:**

Entrada

```
{
  "body": {
    "userName": "John",
    "email": "default@email.com"
  }
}
```

Transformação

```
[
  {
    "operation": "remove",
    "spec": {
      "body": {
        "email": ""
      }
    }
  }
]
```

Saída

```
{
  "body" : {
    "userName" : "John"
  }
}
```

### _**Sort**_&#x20;

Utilizada para ordenar campos ou objetos de um JSON em ordem alfabética.

**Exemplo:**

Entrada

```
{
  "funcionario": {
    "telefone": "9 9999-9999",
    "nome": "Funcionario Sort",
    "dataNascimento": "01/01/1980",
    "cargo": "Analista"
  }
}
```

Transformação

```
[
  {
    "operation": "sort"
  }
]
```

Saída

```
{
  "funcionario" : {
    "cargo" : "Analista",
    "dataNascimento" : "01/01/1980",
    "nome" : "Funcionario Sort",
    "telefone" : "9 9999-9999"
  }
}
```

### _**Cardinality**_

Utilizada para transformar campos e objetos simples em _arrays_ e vice-versa.

**Exemplo:**

Entrada

```
{
  "produtos": {
    "nome": "Produto A",
    "id": "123-A",
    "valor": 10
  }
}
```

Transformação

```
[
  {
    "operation": "cardinality",
    "spec": {
      "produtos": "MANY"
    }
  }
]
```

Saída

```
{
  "produtos" : [ {
    "nome" : "Produto A",
    "id" : "123-A",
    "valor" : 10
  } ]
}
```

### **Modify-default-beta**

Utilizada para incluir valores e aplicar funções em um JSON.

**Exemplo:**

Entrada

```
{
  "produto": [
    {
      "nome": "Produto A",
      "preco": 10
    },
    {
      "nome": "Produto B",
      "preco": 20
    }
  ]
}

```

Transformação

```
[
  {
    "operation": "modify-default-beta",
    "spec": {
      "produto": {
        "*": {
          "fabricante": "Fabricante default"
        }
      }
    }
  }
]
```

Saída

```
{
  "produto" : [ {
    "nome" : "Produto A",
    "preco" : 10,
    "fabricante" : "Fabricante default"
  }, {
    "nome" : "Produto B",
    "preco" : 20,
    "fabricante" : "Fabricante default"
  } ]
}{
  "data": {
    "firstName": "John",
    "lastName": "Smith"
  }
}
```

### **Modify-overwrite-beta**

Utilizada para sobrescrever valores e aplicar funções em um JSON.

**Exemplo:**

Entrada

```
{
  "data": {
    "firstName": "John",
    "lastName": "Smith"
  }
}
```

Transformação

```
[
  {
    "operation": "modify-overwrite-beta",
    "spec": {
      "data": {
        "fullName": "=concat(@(1,firstName),' ',@(1,lastName))"
      }
    }
  }
]
```

Saída

```
{
  "data" : {
    "firstName" : "John",
    "lastName" : "Smith",
    "fullName" : "John Smith"
  }
}
```

[Clique aqui para ler o artigo detalhado sobre o _Transformer (JOLT)_.](https://docs.digibee.com/documentation/v/pt-br/components/tools/transformer-jolt/transformer-conhecendo-o-jolt)

\
