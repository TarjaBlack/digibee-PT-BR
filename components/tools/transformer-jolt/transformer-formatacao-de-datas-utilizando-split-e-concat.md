---
description: Exemplo da utilização de split e join para formatação de datas.
---

# Transformer - Formatação de datas utilizando split e concat

**Entrada json:**

```
{
  "data": {
    "PAC_DATA_NASCTO": "18/09/1974"
  }
}
```

**Transformer Spec:**

```
[
  {
    "operation": "modify-overwrite-beta",
    "spec": {
      "data": {
        "array_aux": "=split('/',@(1,PAC_DATA_NASCTO))",
        "PAC_DATA_NASCTO": "=concat(@(1,array_aux[2]),@(1,array_aux[1]),@(1,array_aux[0]))"
      }
    }
    },
  {
    "operation": "shift",
    "spec": {
      "data": {
        "PAC_DATA_NASCTO": "&"
      }
    }
  }
  ]
```

\
Para esta formatação foi utilizado o "operation": "**modify-overwrite-beta**" que possibilita a alteração do json.\
Comando =split para separar a data pelo carácter '/' e  criar um array de 3 posições. Também é possível utilizar **regex** no split. Veja mais exemplos em:&#x20;

[Github - Split Functions](https://github.com/bazaarvoice/jolt/blob/7812399d1c955742d81eae363244a2d0ef86cf3b/jolt-core/src/test/resources/json/modifier/functions/stringsSplitTest.json)

Após o Split, o comando =concat nos dá a possibilidade de concatenar os itens do array de acordo com o index.

**Saída** &#x20;

```
{  
    "PAC_DATA_NASCTO" : "19740918"
}
```

\
