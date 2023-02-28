---
description: Conheça o componente e saiba como utilizá-lo.
---

# Base64

O _**Base64**_ realiza a codificação e a decodificação de/para campos, _payloads_ e arquivos no formato base64 _string_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** define qual operação será executada (_Encode Fields, Encode Payload, Encode File, Decode Fields, Decode Payload, Decode File_).
* **JSON Fields:** caminho do JSON a ser codificado ou decodificado. Os campos precisam ser separados por vírgula (ex.: field1,field2). Essa opção é válida somente para as operações _Encode Fields_ e _Decode Fields_.
* **Preserve Original:** se habilitada, a opção preserva campos originais e modifica prefixos adicionando o caractere _underline_ `(_)`.
* **Payload:** campo para informar diretamente o _payload_ que terá o seu conteúdo codificado/decodificado (ex: body, data, \{{ message.payload \}}). Essa opção é válida somente para as operações _Encode Payload_ e _Decode Payload_.
* **Result As File:** se habilitada, a opção salva o resultado da codificação ou da decodificação em um arquivo. Essa opção é válida somente para as operações _Encode Payload_ e _Decode Payload_.
* **File Name:** nome do arquivo a ser comprimido.
* **Output File Name:** nome do arquivo de saída após a codificação/decodificação de um arquivo. Essa opção é válida somente para as operações _Encode File_ e _Decode File_.
* **Is Binary:** se habilitada, a opção irá esperar o _payload_ como um arquivo binário. Essa opção é válida somente para a operação _Decode Payload_.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado mostrará um valor falso para a propriedade _"success"_.

{% hint style="info" %}
**IMPORTANTE**: Os campos **File Name** e **Output File Name** devem receber valores diferentes. Caso os valores sejam iguais, um erro será produzido (uma exceção).
{% endhint %}

Alguns dos parâmetros acima aceitam _Double Braces_. Leia o artigo [Double Braces](../../build/double-braces/) para saber mais sobre como essa linguagem funciona.

## Fluxo de mensagens <a href="#h_65727873d4" id="h_65727873d4"></a>

### Entrada <a href="#h_b75d443fee" id="h_b75d443fee"></a>

Para as operações _Encode Fields_ e _Decode Fields_, o componente espera receber um JSON contendo os campos configurados na propriedade **JSON Fields**.

**Exemplo:**

**Configuração**

```
JSON Field = field1,field2
```

O JSON esperado deve conter pelo menos:

```
{    
    "field1": "SOMETHING",    
    "field2": "SOMETHING"
}
```

Para as operações _Encode Payload_ e _Decode Payload_, você deve configurar o campo **Payload** para poder codificar/decodificar.

**Exemplo:**

**Configuração**

```
Payload = {{ message.field1 }}
```

O JSON esperado deve conter pelo menos:

```
{    
    "field1": "SOMETHING"
}
```

Para as operações _Encode File_ e _Decode File_, você deve configurar o arquivo que será codificado/decodificado e o arquivo resultante dessa operação.

**Exemplo:**

```
File Name = input.csv
Output File Name = outputfile.csv
```

### Saída <a href="#h_71a1f1a542" id="h_71a1f1a542"></a>

Para as operações _Encode Fields_ e _Decode Fields_:

```
{    
    "field1": "SOMETHING ENCODED/DECODED",    
    "field2": "SOMETHING ENCODED/DECODED",    
    "_field1": "ORIGINAL VALUE",    
    "_field2": "ORIGINAL VALUE"
}
```

Para as operações _Encode Fields_ e _Decode Fields_, caso a mensagem de entrada seja preservada:

```
{    
    "field1": "SOMETHING ENCODED/DECODED",    
    "field2": "SOMETHING ENCODED/DECODED",    
    "_field1": "ORIGINAL VALUE",    
    "_field2": "ORIGINAL VALUE",
}
```

Para as operações _Encode Payload_ e _Decode Payload_, caso a saída seja um arquivo:

```
{    
    "success": "true",    
    "fileName": "file.csv"
}
```

Para as operações _Encode Payload_ e _Decode Payload_, caso a saída seja uma _string_:

```
{    
    "success": "true",    
    "result": "SOMETHING ENCODED/DECODED"
}
```

Para as operações _Encode File_ e _Decode File_:

```
{    
    "success": "true",    
    "fileName": "file.csv",    
    "outputFileName": "file.csv"
}
```

\
