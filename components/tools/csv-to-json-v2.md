---
description: Conheça o componente e saiba como utilizá-lo.
---

# CSV to JSON V2

O **CSV to JSON V2** transforma um CSV em um objeto JSON.

Dê uma olhada nos parâmetros de configuração do componente:

* **Headers:** lista de _headers_ CSV a serem lidos - cada CSV _header_ é convertido em uma propriedade JSON. Ele será exibido somente se a opção _CSV Has Reader_ estiver desativada.
* **Delimiter:** delimitador no qual o CSV é configurado.
* **CSV Has Reader:** mantenha a opção ativada caso o CSV a ser transformado tenha _headers_ no início do _array,_ da _string_ ou do arquivo.
* _**CSV as File:**_ se a opção estiver ativada, o componente esperará um arquivo para gerar o JSON de saída; do contrário, será necessário parar um CSV como _array_ ou como uma _string_.
* **File Name:** quando a opção _CSV as File_ estiver ativada, esse campo será exibido e deverá receber o nome do arquivo CSV.
* _**Body:**_ quando a opção CSV as File estiver desativada, esse campo será exibido e um CSV em forma de JSON (_array_ ou _string_) deverá ser passado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

### Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem com a propriedade. Você pode passar os dados CSV como um _array_ de _strings_:

```
{    
    "data": ["HEADER1,HEADER2,HEADER3", "LINE1,LINE1,LINE1", ...]
}
```

como um _string_ único:

```
{    
    "data": "HEADER1,HEADER2,HEADER3\nLINE1,LINE1,LINE1\nLINE2,LINE2,LINE2"
}
```

ou como arquivo:

```
File Name: arquivo.csv
```



#### Saída <a href="#sada" id="sada"></a>

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
    "data": [{"HEADER1": "LINE1",
        "HEADER2": "LINE1",
        "HEADER3": "LINE1" 
        },
        {"HEADER1": "LINE2",
            "HEADER2": "LINE2",
            "HEADER3": "LINE2"
    }]         
}
```

\
