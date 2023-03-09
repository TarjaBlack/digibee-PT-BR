---
description: Conheça o componente e saiba como utilizá-lo.
---

# CSV to JSON V1 (Descontinuado)

O **CSV to JSON V1** transforma um CSV em um objeto JSON.

Dê uma olhada nos parâmetros de configuração do componente:

* **Headers:** lista de _headers_ CSV a serem lidos - cada CSV _header_ é convertido em uma propriedade JSON.
* **Delimiter:** delimitador no qual o CSV é configurado.
* **CSV Has Reader:** manter a opção ativada caso o CSV a ser transformado tenha _headers_ no início do _array_.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem com a propriedade. Você pode passar os dados CSV como um _array_ de _strings_:

```
{    
    "data": ["HEADER1,HEADER2,HEADER3", "LINE1,LINE1,LINE1", ...]
}
```

ou passar os dados CSV como um _string_ único:

```
{    
    "data": "LINE1,LINE1,LINE1"
}
```

### Saída <a href="#sada" id="sada"></a>

```
{
    "data": [{"HEADER1": "LINE1",
        "HEADER2": "LINE1",
        "HEADER3": "LINE1"
        },
        {"HEADER1": "LINE2",
        "HEADER2": "LINE2",
        "HEADER3": "LINE2"
        }, ....]
}
```

Caso você receba um _string_ único:

```
{        
    "data": {"HEADER1": "LINE1",
        "HEADER2": "LINE1",
        "HEADER3": "LINE1"
    }              
}
```

\
