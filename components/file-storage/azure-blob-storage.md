---
description: Conheça o componente e como utilizá-lo.
---

# Azure Blob Storage

O Blob Storage ( Azure ) + possibilita a manipulação de arquivos dentro de contêineres da Azure Blob Storage .

**Parâmetros de configuração**

Dê uma olhada nas opções de configuração do componente:

*   **Account:** conta a ser utilizada pelo componente (listar as _accounts_ suportadas pelo componente). As _accounts_ suportadas são: basic e _public key_. A _Basic_ é utilizada para se conectar via _ConnectionString_, deve ser passado o nome da _account_ do _storage_ no campo usuário e a _key1_ no campo _password_. A _public key_ é utilizada caso queira autenticar via _SAS token_, utilizar a _public-key_ no campo key, passar o _SAS token_ gerado pela Azure. Para saber mais sobre esses _accounts_ e os outros tipos existentes, clique no link.

    [Aqui](broken-reference).
* **Step Name:** Nome do passo que o componente é configurado.
* **Operation:** Qual operação o componente irá realizar, _list_, download, _upload_ ou delete (o preenchimento deste campo é obrigatório).
* **Container Name:** Nome do _container_ do _Blob Storage_ ( Azure ) que manipulará os arquivos (o preenchimento deste campo é obrigatório).
* **Container Account:** Nome da _account_ na Azure que o Blob Storage utiliza (o preenchimento deste campo é obrigatório).
* **Remote File Name:** Nome de destino do seu arquivo, o nome que o arquivo terá no Blob Storage (Azure) (o preenchimento deste campo é obrigatório apenas nas operações _upload_, _download_ e _delete_). Este parâmetro aceita _Double Braces_.
* **File Name:** Nome do arquivo que você deseja subir para o seu Blob Storage (Azure) (o preenchimento deste campo é obrigatório). Este parâmetro aceita _Double Braces_.
* **Show File Link:** Gera um _link_ de _download_ do arquivo quando está configurado como _true_ e a operação é _upload_.
* **Fail On Error:** Caso o parâmetro esteja configurado como _true_ ele lança a exceção para frente.
* **Page Size:** Quantidade de registros que deseja trazer por página (apenas quando a operação é _List_). Este parâmetro aceita _Double Braces_.
* **Next Page Token:** _NextToken_ que será usado para trazer os registros da próxima página (apenas quando a operação é _List_ ). Este parâmetro aceita _Double Braces_.
* **Next Page Type:** Tipo do próximo registro que será listado na próxima página (apenas quando a operação é _List_ ).
* **Overwrite File on Upload:** Sobrescreve o arquivo no momento do _upload_ (apenas quando a operação é _Upload_ ). Este parâmetro aceita _Double Braces_.

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso artigo clicando no link [Aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

### **Fluxo de mensagens** <a href="#h_721d00c487" id="h_721d00c487"></a>

### Exemplo de retorno quando operação é _list_: <a href="#h_f1ad5045a4" id="h_f1ad5045a4"></a>

{

"success": true,

"content": \[

{

"fileName": "my-remote-file.txt",

"containerName": "newcontainer",

"properties": {

"createdDate": "Fri May 20 13:41:12 UTC 2022",

"lastUpdated": "Wed May 25 14:59:26 UTC 2022",

"contentType": "application/octet-stream",

"length": 23

}

},

{

"fileName": "testeOverwrite.txt",

"containerName": "newcontainer",

"properties": {

"createdDate": "Tue Jun 14 18:11:35 UTC 2022",

"lastUpdated": "Tue Jun 14 18:11:47 UTC 2022",

"contentType": "application/octet-stream",

"length": 76952

}

}

],

"count": 2,

"containerName": "newcontainer"

}

#### Foram adicionados campos novos no componente para tornar possível filtrar por prefixo, e temos agora a opção de incluir alguns tipos de arquivo no retorno, como deletados, por exemplo:

**Prefix**: Filtra os resultados para retornar apenas blobs cujos nomes começam com o prefixo especificado na operação de lista: Allows _Double Braces_

**Snapshot**: Incluir Snapshots na resposta blob para operação list

**Metadata**: Incluir Metadata na resposta de blob para operação de lista

**Uncommited**: Incluir blob Uncommited na resposta para operação de lista

**Copy**: Incluir Copy blob na resposta para operação de lista

**Delete**: Incluir blob Delete na resposta para operação de lista

### Exemplo de retorno quando operação é _upload_: <a href="#h_adcada8305" id="h_adcada8305"></a>

{

"success": true,

"fileName": "teste-upload.jpeg",

"containerName": "teste",

"remoteFileName": "teste-upload.jpeg",

"urlGenerated": "[https://digibeeblobstorage.blob.core.windows.net/teste/teste-upload.jpeg](https://digibeeblobstorage.blob.core.windows.net/teste/teste-upload.jpeg)"

}

### Exemplo de retorno quando operação é _download_: <a href="#h_31719736bb" id="h_31719736bb"></a>

***

{% hint style="info" %}
**Importante:** Utilizar o componente _File Reader_ para manipular o base64 retornado.
{% endhint %}

### Exemplo de retorno quando operação é _delete_: <a href="#h_30beadc363" id="h_30beadc363"></a>

{

"success": true,

"containerName": "newcontainer",

"remoteFileName": "teste-upload.jpeg"

}
