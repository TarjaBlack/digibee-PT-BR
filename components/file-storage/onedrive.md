---
description: Conheça o componente e saiba como utilizá-lo.
---

# OneDrive

O _**OneDrive**_ permite estabelecer uma conexão com o serviço OneDrive da Microsoft e habilita as seguintes operações: _list_, _list search_, _pagination_, _download_, _download by file ID_, _upload_ e _delete_.

Dê uma olhada nos parâmetros de configuração do componente:

![](<../../.gitbook/assets/ezgif.com-gif-maker (9).gif>)

* **Account:** para o componente fazer a autenticação ao serviço do OneDrive é necessário usar uma _account_ do tipo Oath 2 de provedor Microsoft com ao menos o escopo de "offline\_access" e "Files.ReadWrite.All".
* **Operation:** _list_, _list search_, _pagination_, _download_, _download by file ID_, _upload_ e _delete_.
* **Remote Directory:** diretório remoto base, que pode ser relativo (ex.: _pub/tmp_) ou absoluto (ex.: _/root/pub_). Este parâmetro aceita _Double Braces_.
* **Page Size:** utilizado na operação _list_ e _list search_, se refere à quantidade de objetos retornados na busca.
* **Query:** presente na operação _list search_. Esse parâmetro define o tipo de busca que será feito nos diretórios do OneDrive. Para saber mais sobre esse filtro, clique [aqui](https://docs.microsoft.com/pt-br/onedrive/developer/rest-api/api/driveitem\_search?view=odsp-graph-online).
* **Next Page:** presente na operação _pagination_.

**IMPORTANTE:** se um componente OneDrive que estiver executando a operação _list_ ou _list search_ gerar mais resultados do que o _Page Size_, então um segundo componente OneDrive ligado pode usar a operação _pagination_ e o parâmetro _Next Page_. Isso pode ocorrer manualmente ou por meio de _Double Braces_. Exemplo: com _\{{ message. nextPage \}}_), mais resultados da operação anterior são carregados.

* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: tmp/file.txt) para o arquivo remoto. Este parâmetro aceita _Double Braces_.
* **File ID:** identificador único de um arquivo.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Saída <a href="#sada" id="sada"></a>

Ao executar um componente _**OneDrive**_ utilizando as operações _**list**_** ** e _ **list search**_, a seguinte estrutura de JSON será gerada:

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

* **value\[name]:** nome da pasta ou arquivo
* **value\[size]:** tamanho em _bytes_
* **nextPage:** _url_ para carregar mais resultados (ver operação “pagination”)

Operação _**download**_:

```
{
  "remoteDirectory": "REMOTE_DIRECTORY",
  "remoteFileName": "remoteFileName"
  "fileName": "file.ext",
  "success": true
}

```

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto
* **fileName:** nome do arquivo local
* **success:** "true" se a operação sucedeu, "false" caso contrário

Operação _**download by file Id**_:

```
{
  "fileId": "FILE_ID"
  "fileName": "file.ext",
  "success": true
}
```

* **fileId:** identificador único do arquivo
* **fileName:** nome do arquivo local
* **success:** "true" se a operação sucedeu, "false" caso contrário

Operação _**upload**_:

```
{
    "remoteFileName": "remote_file.ext",
    "remoteDirectory": "Documents""fileName": "file.ext",
    "success": true
}
```

* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **fileName:** nome do arquivo local
* **success:** "true" se a operação sucedeu, "false" caso contrário

Operação _**delete**_:

```
{
    "fileId": "FILE_ID""success": true
}
```

* **fileId:** identificador único do arquivo
* **success:** "true" se a operação sucedeu, "false" caso contrário

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](../../build/pipelines/processamento-de-mensagens.md) e leia o nosso artigo.
