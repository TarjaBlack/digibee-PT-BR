---
description: Conheça o componente e saiba como utilizá-lo.
---

# Base64

O _**Base64**_ realiza a codificação e a decodificação de/para campos, _payloads_ e arquivos no formato base64 _string_.

### Dê uma olhada nos parâmetros de configuração do componente:

* **Operações:**

**- Encode Fields:** codifica os campos de JSON.

**- Decode Fields:** decodifica os campos de JSON.

**- Encode Payload:** codifica o _payload_ recebido.

**- Decode Payload:** decodifica o _payload_ recebido.

**- Encode File:** codifica o arquivo recebido.

**- Decode File:** decodifica o arquivo recebido.

* **JSON Field:** caminho do JSON a ser codificado ou decodificado. Os campos precisam ser separados por vírgula (ex.: field1,field2).
* **Preserve Original:** se habilitada, a opção preserva campos originais e modifica prefixos adicionando o caractere _underline_ (\_).
* **Payload:** campo para informar diretamente o _payload_ que terá o seu conteúdo codificado/decodificado (ex: body, data, \{{ message.payload \}}).
* **Result As File:** se habilitada, a opção salva o resultado da codificação ou da decodificação em um arquivo (válido somente para as operações “encode\_payload” e “decode\_payload”).
* **File Name:** nome do arquivo a ser comprimido.
* **Output File Name:** nome do arquivo de saída após a codificação/decodificação de um arquivo (válido somente para as operações “encode\_file” e “decode\_file").
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado mostrará um valor falso para a propriedade "success".

{% hint style="info" %}
**Importante**: Os campos 'File Name' e 'Output File Name', devem receber valores diferentes, caso os valores sejam iguais, produzirá um erro (uma exceção).
{% endhint %}

Alguns dos parâmetros acima aceitam _Double Braces_. Para compreender melhor como funciona essa linguagem, leia o nosso artigo clicando [aqui](broken-reference).

### Fluxo de mensagens <a href="#h_65727873d4" id="h_65727873d4"></a>

#### Entrada <a href="#h_b75d443fee" id="h_b75d443fee"></a>

Para as operações “encode\_fields” e “decode\_fields”, o componente espera receber um JSON contendo os campos configurados na propriedade _JSON Field_.

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

Para as operações “encode\_payload” e “decode\_payload”, você deve configurar o campo “Payload” para poder codificar/decodificar.

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

Para as operações “encode\_file” e “decode\_file”, você deve configurar o arquivo que será codificado/decodificado e o arquivo resultante dessa operação.

**Exemplo:**

```
File Name = input.csv
Output File Name = outputfile.csv
```



#### Saída <a href="#h_71a1f1a542" id="h_71a1f1a542"></a>

Para as operações “encode\_fields” e “decode\_fields”:

```
{    
    "field1": "SOMETHING ENCODED/DECODED",    
    "field2": "SOMETHING ENCODED/DECODED",    
    "_field1": "ORIGINAL VALUE",    
    "_field2": "ORIGINAL VALUE"
}
```

Para as operações “encode\_fields” e “decode\_fields”, caso a mensagem de entrada seja preservada:

```
{    
    "field1": "SOMETHING ENCODED/DECODED",    
    "field2": "SOMETHING ENCODED/DECODED",    
    "_field1": "ORIGINAL VALUE",    
    "_field2": "ORIGINAL VALUE",
}
```

Para as operações “encode\_payload” e “decode\_payload”, caso a saída seja um arquivo:

```
{    
    "success": "true",    
    "fileName": "file.csv"
}
```

Para as operações “encode\_payload” e “decode\_payload”, caso a saída seja uma _string_:

```
{    
    "success": "true",    
    "result": "SOMETHING ENCODED/DECODED"
}
```

Para as operações “encode\_file” e “decode\_file”:

```
{    
    "success": "true",    
    "fileName": "file.csv",    
    "outputFileName": "file.csv"
}
```

\
