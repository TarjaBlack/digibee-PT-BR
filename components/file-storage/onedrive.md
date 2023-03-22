---
description: Conheça o componente e saiba como utilizá-lo.
---

# OneDrive

O _**OneDrive**_ permite estabelecer uma conexão com o serviço OneDrive da Microsoft e habilita as seguintes operações: _List, List Search, Pagination, Download, Download by File ID, Upload_ ou _Delete_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** para o componente fazer a autenticação ao serviço do OneDrive é necessário usar uma _account_ do tipo Oath 2 de provedor Microsoft com ao menos o escopo de "offline\_access" e "Files.ReadWrite.All".
* **Operation:** operação a ser executada (_List, List Search, Pagination, Download, Download by File ID, Upload_ ou _Delete)_.
* **Remote Directory:** diretório remoto base, que pode ser relativo (ex.: pub/tmp) ou absoluto (ex.: __ /root/pub). Este parâmetro aceita _Double Braces_.
* **Page Size:** utilizado na operação _List_ e _List Search_, se refere à quantidade de objetos retornados na busca.
* **Query:** presente na operação _List Search_. Esse parâmetro define o tipo de busca que será feito nos diretórios do OneDrive. Para saber mais sobre esse filtro, visite a [documentação oficial Microsoft](https://docs.microsoft.com/pt-br/onedrive/developer/rest-api/api/driveitem\_search?view=odsp-graph-online).
* **Next Page:** presente na operação _Pagination_.

{% hint style="info" %}
**IMPORTANTE:** se um componente _**OneDrive**_ que estiver executando a operação _List_ ou _List Search_ gerar mais resultados do que o **Page Size**, então um segundo componente _**OneDrive**_ ligado pode usar a operação _pagination_ e o parâmetro **Next Page**. Isso pode ocorrer manualmente ou por meio de _Double Braces_. Exemplo: com _\{{ message. nextPage \}}_), mais resultados da operação anterior são carregados.
{% endhint %}

* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: tmp/file.txt) para o arquivo remoto. Este parâmetro aceita _Double Braces_.
* **File ID:** identificador único de um arquivo.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

Alguns dos parâmetros acima suportam Double Braces. Para entender como essa linguagem funciona, leia a [documentação sobre Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/double-braces).

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

## Saída <a href="#sada" id="sada"></a>

### Operações List e List Search

Ao executar um componente _**OneDrive**_ utilizando as operações **List** e __ **List Search**, a seguinte estrutura de JSON será gerada:

```
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('user%40hotmail.com')/drive/root/children",
    "count": 5,
    "nextPage": "https://microsoft.graph/nextPage?token=Md",
    "value": [
        {
            "createdDateTime": "2010-10-07T23:25:28.99Z",
            "cTag": "adDpEOUMxOTZEMzdEMkQxNT42MzcyODc4NjU2Nzg0MDAwMUHDA",
            "eTag": "aRDlfdseMTk2RDRfdfDJEMTU5RSExEuMA",
            "id": "DXCC196D37D2D159E!161",
            "lastModifiedDateTime": "2020-06-26T16:42:47.84Z",
            "name": "Documentos",
            "size": 49378390,
            "webUrl": "https://1drv.ms/f/s!AGG4VLX3T6sHZgSE",
            "reactions": {
                "commentCount": 0
            },
            "createdBy": {
                "user": {
                    "displayName": "NAME",
                    "id": "d9c196d37d2d159e"
                }
            },
            "lastModifiedBy": {
                "user": {
                    "displayName": "NAME",
                    "id": "d9de396d37d2d159e"
                }
            },
            "parentReference": {
                "driveId": "d9c196d37d2d159e",
                "driveType": "personal",
                "id": "XCC196D37D2D159E!160",
                "path": "/drive/root:a_folder"
            },
            "fileSystemInfo": {
                "createdDateTime": "2010-10-07T23:25:28.99Z",
                "lastModifiedDateTime": "2010-10-07T23:25:28.99Z"
            },
            "folder": {
                "childCount": 6,
                "view": {
                    "viewType": "thumbnails",
                    "sortBy": "name",
                    "sortOrder": "ascending"
                }
            },
            "specialFolder": {
                "name": "documents"
            }
        }
    ]
}
```

* **value\[name]:** nome da pasta ou arquivo.
* **value\[size]:** tamanho em _bytes._
* **nextPage:** _url_ para carregar mais resultados (ver operação _Pagination_).

### Operação **Download**

```
{
  "remoteDirectory": "REMOTE_DIRECTORY",
  "remoteFileName": "remoteFileName"
  "fileName": "file.ext",
  "success": true
}

```

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto.
* **fileName:** nome do arquivo local.
* **success:** "true" se a operação sucedeu, "false" caso contrário.

### Operação **Download **_****_** by File ID**

```
{
  "fileId": "FILE_ID"
  "fileName": "file.ext",
  "success": true
}
```

* **fileId:** identificador único do arquivo.
* **fileName:** nome do arquivo local.
* **success:** "true" se a operação sucedeu, "false" caso contrário.

### Operação **Upload**

```
{
    "remoteFileName": "remote_file.ext",
    "remoteDirectory": "Documents""fileName": "file.ext",
    "success": true
}
```

* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto.
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **fileName:** nome do arquivo local.
* **success:** "true" se a operação sucedeu, "false" caso contrário.

### Operação **Delete**

```
{
    "fileId": "FILE_ID""success": true
}
```

* **fileId:** identificador único do arquivo.
* **success:** "true" se a operação sucedeu, "false" caso contrário.

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.
{% endhint %}

Leia o artigo [Processamento de mensagens](https://docs.digibee.com/documentation/v/pt-br/build/pipelines/processamento-de-mensagens) para entender como esse conceito funciona na Digibee Integration Platform.
