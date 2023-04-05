---
description: Conheça o componente e como utilizá-lo.
---

# Blob Storage (Azure)

O Blob Storage (Azure) possibilita que você trabalhe com arquivos armazenados em _containers_ da Azure Blob Storage.

Dê uma olhada nas opções de configuração do componente:

* **Account:** conta a ser utilizada pelo componente. As _accounts_ suportadas são: _Basic_ e _Public key_. A _Basic_ é utilizada para se conectar via _ConnectionString_; o nome da _storage account_ deve ser passado no campo _"user"_ e a _key1_ no campo "_password"_. A _Public key_ é utilizada caso queira autenticar via _SAS token_; use a _public-key_ no campo "_key_", e depois passe o _SAS token_ gerado pela Azure. Leia a documentação sobre [Contas (Accounts)](../../configurations/contas-accounts/) para saber mais sobre esses e outros tipos de contas existentes.
* **Operation:** define qual operação o componente irá realizar (_List_, _Download_, _Upload_ ou _Delete)._ O preenchimento deste campo é obrigatório.
* **Container Name:** nome do _container_ do Blob Storage (Azure) que manipulará os arquivos. O preenchimento deste campo é obrigatório.
* **Container Account:** nome da _account_ Azure que o Blob Storage utiliza. (O preenchimento deste campo é obrigatório.
* **Remote File Name:** nome de destino do seu arquivo, o mesmo nome que o arquivo terá no Blob Storage (Azure). O preenchimento deste campo é obrigatório apenas quando as operações _Upload_, _Download_ ou _Delete_ estiverem selecionadas. Este parâmetro aceita _Double Braces_.
* **File Name:** nome do arquivo que você deseja subir para o seu Blob Storage (Azure). O preenchimento deste campo é obrigatório. Este parâmetro aceita _Double Braces_.
* **Generate a Download Link:** se a opção é habilitada, você poderá gerar um link para download do arquivo. Este parâmetro é mostrado somente quando a operação _Upload_ é selecionada.
* **Page Size:** quantidade de registros que deseja trazer por página. Este parâmetro aceita _Double Braces_ e é mostrado somente quando a operação _List_ é selecionada.
* **Prefix**: filtra os resultados para retornar apenas _blobs_ cujos nomes começam com o prefixo especificado. Este parâmetro aceita _Double Braces_ e é mostrado somente quando a operação _List_ é selecionada.
* **Next Page Token:** _NextToken_ que será usado para trazer os registros da próxima página. Este parâmetro aceita _Double Braces_ e é mostrado somente quando a operação _List_ é selecionada.
* **Next Token Type:** Tipo do próximo registro que será listado na próxima página. Este parâmetro é mostrado somente quando a operação _List_ é selecionada.
* **Overwrite File on Upload:** sobrescreve o arquivo no momento do upload. Este parâmetro aceita _Double Braces_ e é mostrado somente quando a operação _Upload_ é selecionada.
* **Snapshot**: se a opção for ativada, irá incluir _snapshots_ na resposta dos _blobs_. Disponível somente para a operação _List_.
* **Metadata**: se a opção for ativada, irá incluir metadados (_metadata_) na resposta dos _blobs_. Disponível somente para a operação _List_.
* **Uncommited**: se a opção for ativada, irá incluir _uncommited blobs_ na resposta. Disponível somente para a operação _List_.
* **Copy**: se a opção for ativada, irá incluir _copy blobs_ na resposta. Disponível somente para a operação _List_.
* **Delete**: se a opção for ativada, irá incluir _delete blobs_ na resposta. Disponível somente para a operação _List_.
* **Fail On Error:**  se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

Alguns dos parâmetros acima aceitam _Double Braces_. Leia o artigo [Como referenciar dados usando Double Braces](../../build/double-braces/como-referenciar-dados-usando-double-braces.md) para entender melhor como funciona essa linguagem.

## **Fluxo de mensagens** <a href="#h_721d00c487" id="h_721d00c487"></a>

### Operação _List_ <a href="#h_f1ad5045a4" id="h_f1ad5045a4"></a>

```
{
"success": true,
"content": [
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
```

### Operação _Upload_ <a href="#h_adcada8305" id="h_adcada8305"></a>

```
{
"success": true,
"fileName": "teste-upload.jpeg",
"containerName": "teste",
"remoteFileName": "teste-upload.jpeg",
"urlGenerated": "
https://digibeeblobstorage.blob.core.windows.net/teste/teste-upload.jpeg
"
}
```

### Operação _Download_ <a href="#h_31719736bb" id="h_31719736bb"></a>

{% hint style="info" %}
**IMPORTANTE:** Utilizar o componente [_**File Reader**_](../files/file-reader.md) para manipular o base64 retornado.
{% endhint %}

### Operação _Delete_ <a href="#h_30beadc363" id="h_30beadc363"></a>

```
{
"success": true,
"containerName": "newcontainer",
"remoteFileName": "teste-upload.jpeg"
}
```
