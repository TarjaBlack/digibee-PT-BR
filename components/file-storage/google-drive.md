---
description: Conheça o componente e saiba como utilizá-lo.
---

# Google Drive

O **Google Drive** se conecta ao seu _drive_ do Google e efetua as seguintes operações com arquivos: _list_, _download_, _upload_ e _delete_.\
&#x20;      \
Dê uma olhada nos parâmetros de configuração do componente:

![](<../../.gitbook/assets/ezgif.com-gif-maker (13).gif>)

* **File Name:** nome do arquivo salvo localmente no _pipeline_. No caso da operação _upload_, é o nome do arquivo já salvo; na operação _download_, esse parâmetro define o nome e como o arquivo será salvo.
* **Folder ID:** o ID da pasta do Google. Ele é encontrado na parte superior da URL quando estiver no interior da pasta selecionada no seu Google Drive.
* **File Type:** tipo de extensão do arquivo para efetuar _upload_. Ex.: text/csv, text/xml, image/png. Caso não seja especificado, o _upload_ será efetuado com o tipo _application/octet-stream_.
* **Mime Type On Upload:** se você quiser converter o arquivo em um arquivo do tipo Google Workspace, assim como um Google Doc ou Planilha, defina o _mime type_ e o componente fará a conversão durante o _upload_. O arquivo convertido para um tipo Google Workspace não poderá ser baixado.
* **Remote File Name:** utilizado apenas na operação _upload_. Esse parâmetro define o nome do arquivo remoto do qual será feito _upload_.
* **Operation:** _list_, download, upload, _delete_.
* **Query:** utilizado na operação _list_. Esse parâmetro define a _query language_ de filtros durante a operação _list_. Para saber mais sobre essa linguagem, clique [aqui](https://developers.google.com/drive/api/v3/ref-search-terms).
* **Page Size:** utilizado na operação _list_, se refere à quantidade de objetos retornados na busca.
* **Page Token:** utilizado na operação _list_. Caso haja mais resultados após a listagem, esse parâmetro será informado para que se possa continuar com a listagem paginada.
* **Field ID:** utilizado nas operações _delete_ e _download_, esse é o ID do arquivo.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

&#x20;    \
O Google Drive não segue o mesmo conceito de hierarquia de pastas. Portanto, não é possível efetuar buscas especificando um caminho de diretório.

**Exemplo:** dir1/dir2/dir3/fileName.extension

&#x20;      \
Um outro detalhe sobre o Google Drive é que você pode salvar arquivos com o mesmo nome no mesmo diretório. Por isso que a API definida pelo Google utiliza o _fileId_ para fazer o download ou remoção de arquivos ao invés do próprio nome do arquivo.

**IMPORTANTE:** para efetuar qualquer uma dessas operações, é necessário cadastrar uma ACCOUNT do tipo OAuth 2 com o escopo de "[https://www.googleapis.com/auth/drive](https://www.googleapis.com/auth/drive)"

\
&#x20;        &#x20;

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### LIST <a href="#list" id="list"></a>

* **Entrada**

```
{
    "query": "'11HMcyPhqH4OpAVv7p0Ip1uNu-vGk0nKV' in parents",
    "pageSize": 5,
    "pageToken": null,
    "operation": "list",
    "failOnError":false
}
```

&#x20;        &#x20;

**Saída**

```
[{
    "name": "REMOTE_FILE_NAME or REMOTE_FOLDER_NAME",
    isFolder: false,
    "fileId": "FILE_ID",
    "mimeType": "FOLDER OR FILE MIME_TYPE",
    "description": "FOLDER or FILE DESCRIPTION"
}]
```

&#x20;   &#x20;

### GOOGLE QUERY LANGUAGE <a href="#google-query-language" id="google-query-language"></a>

Veja alguns exemplos de _query_:&#x20;

* Para buscar todos os arquivos/pastas dentro de uma pasta específica:

```
"query": " 'FOLDER_ID' in parents "
```

&#x20;       &#x20;

* Para fazer uma busca de arquivos que tenham o mesmo nome específico dentro de uma pasta:

```
"query": " 'FOLDER_ID' in parents and name = 'FILE NAME' "
```

&#x20;      &#x20;

* Para buscar um nome específico dentro de todo o seu Drive:

```
"query": " name = 'FILE NAME' "
```

\
**IMPORTANTE:** na _query_ acima, a busca vai ser feita em todo o seu Drive, incluindo na pasta Lixeira (_Trash_). Caso não queira pesquisar nada que esteja na pasta _Trash_, então utilize a seguinte _query_:

```
"query": " name = 'FILE NAME' and trashed = false "
```

&#x20;      &#x20;

* Para buscar um arquivo específico em 2 diretórios:

```
"query": "'FOLDER_ID_1' in parents or 'FOLDER_ID_2' in parents and name = 'FILE NAME'"
```

&#x20;       &#x20;

* **Saída**

```
{
    "data": [{
        "name": "REMOTE_FILE_NAME or REMOTE_FOLDER_NAME",
        isFolder: false,
        "fileId": "FILE_ID",
        "mimeType": "FOLDER OR FILE MIME_TYPE",
        "description": "FOLDER or FILE DESCRIPTION"
    }],
    "pageToken": "PAGE_TOKEN",
    "success":true
}
```

&#x20;      \
&#x20;      &#x20;

### UPLOAD <a href="#upload" id="upload"></a>

* **Entrada**

```
{
    "folderId": "11HMcyPhqH4OpAVv7p0Ip1uNu-vGk0nKV",
    "fileType": "text/csv",
    "remoteFileName": "test",
    "operation": "upload",
    "fileName": "test",
    "failOnError":false
}
```

&#x20;     &#x20;

* **Saída**

```
{
    "folderId": "11HMcyPhqH4OpAVv7p0Ip1uNu-vGk0nKV",
    "fileId": "FILE_ID_UPLOADED",
    "remoteFileName": "test",
    "fileName": "test",
    "success":true
}
```

### DOWNLOAD <a href="#download" id="download"></a>

* **Entrada**

```
{
    "fileId": "FILE_ID",
    "operation": "download",              
    "fileName": "test",              
    "failOnError":false  
}
```

* **Saída**

```
{              
    "fileId": "FILE_ID_UPLOADED",              
    "fileName": "test",              
    "success":true  
}
```

### DELETE <a href="#delete" id="delete"></a>

* **Entrada**

```
{              
    "fileId": "FILE_ID",              
    "operation": "delete",              
    "failOnError":false  
}
```

&#x20; &#x20;

&#x20;****&#x20;

* **Saída**

```
{              
    "fileId": "FILE_ID_UPLOADED",              
    "success":true  
}
```
