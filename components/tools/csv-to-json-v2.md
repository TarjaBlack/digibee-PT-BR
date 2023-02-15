---
description: Conheça o componente e saiba como utilizá-lo.
---

# CSV to JSON V2

O **CSV to JSON V2** transforma um CSV em um objeto JSON.

Dê uma olhada nos parâmetros de configuração do componente:

* _**CSV as File:**_ se a opção estiver ativada, o componente esperará um arquivo para gerar o JSON de saída; do contrário, será necessário parar um CSV como _array_ ou como uma _string_.
* **Charset:** se a opção _CSV As File_ estiver habilitada, este campo será mostrado e deverá ser especificado o nome do código dos caracteres para a leitura do arquivo (padrão UTF-8).
* **File Name:** quando a opção _CSV as File_ estiver ativada, esse campo será exibido e deverá receber o nome do arquivo CSV.
* _**CSV:**_ quando a opção _CSV As File_ estiver desativada, este campo será mostrado e um CSV no formato JSON (array ou string) deve ser fornecido.
* _**CSV**_** Has Header:** mantenha a opção ativada caso o CSV a ser transformado tenha _headers_ no início do _array,_ da _string_ ou do arquivo.
* **Headers:** lista de _headers_ CSV a serem lidos - cada CSV _header_ é convertido em uma propriedade JSON. Ele será exibido somente se a opção _CSV Has Header_ estiver desativada.
* **Delimiter:** delimitador no qual o CSV é configurado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline será interrompida em caso de erro. Caso contrário, a execução do pipeline continuará, mas o resultado mostrará um valor falso para a propriedade _"sucess"._

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

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
