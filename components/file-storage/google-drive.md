---
description: Conheça o componente e saiba como utilizá-lo.
---

# Google Drive

O **Google Drive** se conecta ao seu _drive_ do Google e efetua as seguintes operações com arquivos: _List_, _Download_, _Upload_ e _Delete_.\
&#x20;      \
Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** define a conta a ser usada pelo componente.
* **Operation:** define a operação a ser executada (_List, Download, Upload, Delete_).
* **Folder ID:** o ID da pasta do Google. Ele é encontrado na parte superior da URL quando estiver no interior da pasta selecionada no seu Google Drive.
* **File Name:** nome do arquivo salvo localmente no _pipeline_. No caso da operação _Upload_, é o nome do arquivo já salvo; na operação _Download_, esse parâmetro define o nome e como o arquivo será salvo.
* **File Extension Type:** tipo de extensão do arquivo para efetuar _upload_. Ex.: text/csv, text/xml, image/png. Caso não seja especificado, o _upload_ será efetuado com o tipo _application/octet-stream_.
* **Mime Type On Upload:** se você quiser converter o arquivo em um arquivo do tipo Google Workspace, assim como um Google Doc ou Planilha, defina o _mime type_ e o componente fará a conversão durante o _upload_. O arquivo convertido para um tipo Google Workspace não poderá ser baixado.
* **Remote File Name:** este parâmetro está disponível para a operação _Upload_ e define o nome do arquivo remoto do qual será feito _upload_.
* **Query:** este parâmetro está disponível para a operação _List_ e define a _query language_ de filtros durante a operação. Para mais informações sobre essa linguagem, visite [a documentação oficial do Google](https://developers.google.com/drive/api/v3/ref-search-terms).
* **Page Size:** este parâmetro está disponível para a operação _List_ e se refere à quantidade de objetos retornados na busca.
* **Page Token:** este parâmetro está disponível para a operação _List_. Caso haja mais resultados após a listagem, o parâmetro será informado para que se possa continuar com a listagem paginada.
* **Field ID:** este parâmetro está disponível para as operações _Delete_ e _Download_ e informa o ID do arquivo.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

\
O Google Drive não segue o mesmo conceito de hierarquia de pastas. Portanto, não é possível efetuar buscas especificando um caminho de diretório. Exemplo:&#x20;

`dir1/dir2/dir3/fileName.extension`

Um outro detalhe sobre o Google Drive é que você pode salvar arquivos com o mesmo nome no mesmo diretório. Por isso que a API definida pelo Google utiliza o _fileId_ para fazer o download ou remoção de arquivos ao invés do próprio nome do arquivo.

{% hint style="info" %}
**IMPORTANTE:** para efetuar qualquer uma dessas operações, é necessário cadastrar uma ACCOUNT do tipo OAuth 2 com o escopo de `"`[`https://www.googleapis.com/auth/drive`](https://www.googleapis.com/auth/drive)`"`.
{% endhint %}

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### LIST <a href="#list" id="list"></a>

#### **Entrada**

```
{
    "query": "'11HMcyPhqH4OpAVv7p0Ip1uNu-vGk0nKV' in parents",
    "pageSize": 5,
    "pageToken": null,
    "operation": "list",
    "failOnError":false
}
```

#### **Saída**

```
[{
    "name": "REMOTE_FILE_NAME or REMOTE_FOLDER_NAME",
    isFolder: false,
    "fileId": "FILE_ID",
    "mimeType": "FOLDER OR FILE MIME_TYPE",
    "description": "FOLDER or FILE DESCRIPTION"
}]
```

### GOOGLE QUERY LANGUAGE <a href="#google-query-language" id="google-query-language"></a>

Veja alguns exemplos de _query_:&#x20;

#### Para buscar todos os arquivos/pastas dentro de uma pasta específica

```
"query": " 'FOLDER_ID' in parents "
```

#### Para fazer uma busca de arquivos que tenham o mesmo nome específico dentro de uma pasta

```
"query": " 'FOLDER_ID' in parents and name = 'FILE NAME' "
```

#### Para buscar um nome específico dentro de todo o seu Drive

```
"query": " name = 'FILE NAME' "
```

{% hint style="info" %}
**IMPORTANTE:** na _query_ acima, a busca vai ser feita em todo o seu Drive, incluindo na pasta Lixeira (_Trash_). Caso não queira pesquisar nada que esteja na pasta _Trash_, então utilize a seguinte _query_:
{% endhint %}

```
"query": " name = 'FILE NAME' and trashed = false "
```

#### Para buscar um arquivo específico em 2 diretórios

```
"query": "'FOLDER_ID_1' in parents or 'FOLDER_ID_2' in parents and name = 'FILE NAME'"
```

#### **Saída**

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

### UPLOAD <a href="#upload" id="upload"></a>

#### **Entrada**

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

#### **Saída**

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

#### **Entrada**

```
{
    "fileId": "FILE_ID",
    "operation": "download",              
    "fileName": "test",              
    "failOnError":false  
}
```

#### **Saída**

```
{              
    "fileId": "FILE_ID_UPLOADED",              
    "fileName": "test",              
    "success":true  
}
```

### DELETE <a href="#delete" id="delete"></a>

#### **Entrada**

```
{              
    "fileId": "FILE_ID",              
    "operation": "delete",              
    "failOnError":false  
}
```

#### **Saída**

```
{              
    "fileId": "FILE_ID_UPLOADED",              
    "success":true  
}
```
