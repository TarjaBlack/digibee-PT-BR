---
description: Conheça o componente e saiba como utilizá-lo.
---

# S3 Storage



O _**S3 Storage**_ se conecta ao AWS S3 Storage e realiza as seguintes operações no _storage_: _List, Download, Upload, Delete_ ou _Move_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente - obrigatório, o tipo de _account_ deve ser BASIC. É necessário especificar o ID do cliente e a _secret key_ fornecida pelo console da AWS.
* **Operation:** operação a ser executada (_List, Download, Upload, Delete_ ou _Move_).
* **Region:** região onde o S3 está localizado.
* **Bucket Name:** nome do Bucket S3.
* **Bucket Name - Move:** somente para operação _Move_. Nome do _bucket_ do qual será movido o arquivo.
* **File Name:** nome do arquivo local a passar por _download_ ou _upload_ (a função _Delete_ não se aplica).
* **Remote File Name:** nome do arquivo do Google a passar por _Download_, _Upload_, _List_ ou _Delete_.
* **Remote File Name - Move:** somente para operação _Move_. Novo nome do arquivo remoto após ser movido.
* **Remote Directory:** diretório remoto do Google Storage a passar por _Download_, _Upload_ ou _Delete_.
* **Remote Directory - Move:** somente para operação _Move_. Nome do diretório remoto cujo o arquivo será movido.
* **Generate Download Link:** quando selecionada, a opção gera um _link_ público para _download_ do arquivo.
* **Expiration Timestamp (in ms):** tempo para expiração do link (em milissegundos). Nesse campo devem ser passados o _timestamp_ atual + o _timestamp_ de expiração. Exemplo: TIMESTAMP ATUAL + 600000 (600000 = 10 minutos informados em milisegundos). Caso o valor não seja informado, será assumido o valor padrão de 15 minutos após _timestamp_ corrente.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.
* **Custom Endpoint:** Se esta opção estiver ativada, você pode inserir um _endpoint_ customizado via URL no _pipeline_. Se esta opção estiver desativada, a URL não poderá ser inserida.&#x20;
* **Endpoint URL:** a URL do _endpoint_ customizado. Este campo aceita expressões _Double Braces_.

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.
{% endhint %}

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

## **Entrada** <a href="#entrada" id="entrada"></a>

Será necessário passar alguma mensagem de entrada apenas se o componente tenha algum campo configurado com expressões em _Double Braces_. Do contrário, o componente não espera nenhuma mensagem de entrada específica - basta configurar os campos exibidos em cada operação selecionada.

## **Saída** <a href="#sada" id="sada"></a>

### **Cenário da operação LIST**

```
{
    "success": true,
    "content": [{
        "bucketName": "digibee-amazon-s3-connector-test",
        "key": "list/test.csv","size": 9,
        "lastModified": 1596139663000,
        "storageClass": "STANDARD",
        "owner": null,
        "etag": "59587d0fd956dee6905d423bfda2acaf"
    }],
    "count": 1,"nextToken": "1kWwy…..."
}
```

* **success:** caso a chamada ocorra com sucesso, o resultado será “true”; do contrário, será “false”.
* **content:** _array_ contendo informações do arquivo.
* **bucketName:** nome do _bucket._
* **key:** nome do diretório + nome do arquivo.
* **size:** tamanho do arquivo.
* **lastModified:** data da última modificação do arquivo.
* **storageClass:** tipo do armazenamento configurado no S3.
* **owner:** nome do proprietário do arquivo.
* **etag:** _entity tag_, um _hash_ gerado pelo S3 do arquivo.
* **count:** número de objetos retornados.
* **nextToken:** se houver mais de um objeto a ser listado, essa propriedade é exibida para que ocorra a paginação dos itens remanescentes.

### **Cenário da operação DOWNLOAD**

```
{
    "success": true,
    "fileName": "test.file",
    "remoteDirectory": "pagination_folder/",
    "remoteFileName": "c4b88b6b-83bb-42b0-9de6-0371389db585.csv",
    "bucketName": "digibee-amazon-s3-connector-test"
}
```

* **success:** caso a chamada ocorra com sucesso, o resultado será “true”; do contrário, será “false”.
* **fileName:** nome do arquivo baixado no diretório do _pipeline._
* **remoteDirectory:** nome do diretório remoto do S3.
* **remoteFileName:** nome do arquivo remoto baixado do S3.
* **bucketName:** nome do _bucket_ do S3.

### **Cenário da operação UPLOAD**

```
{
    "success": true,
    "fileName": "test.file",
    "remoteDirectory": "pagination_folder/",
    "remoteFileName": "test.file",
    "urlGenerated": "https://digibee-amazon-s3-connector-test.s3.sa-east-1.amazonaws.com/pagination_folder/test.file?....",
    "bucketName": "digibee-amazon-s3-connector-test"
}
```

* **success:** caso a chamada ocorra com sucesso, o resultado será “true”; do contrário, será “false”.
* **fileName:** nome do arquivo no diretório do _pipeline._
* **remoteDirectory:** nome do diretório remoto do S3.
* **remoteFileName:** nome do arquivo remoto do S3 do qual foi feito _upload._
* **bucketName**: nome do _bucket_ do S3.
* **urlGenerated:** link de _download_ do arquivo caso a opção **Generate Download Link** esteja habilitada.

### **Cenário da operação MOVE**

```
{
    "success": true,"remoteDirectory": "pagination_folder/",
    "remoteFileName": "c4b88b6b-83bb-42b0-9de6-0371389db585.csv",
    "remoteFileNameMove": "abc.file",
    "remoteDirectoryMove": "list/",
    "bucketName": "digibee-amazon-s3-connector-test",
    "bucketNameMove": "digibee-amazon-s3-connector-test"
}
```

* **success:** caso a chamada ocorra com sucesso, o resultado será “true”; do contrário, será “false”.
* **remoteDirectory:** nome do diretório remoto do S3.
* **remoteFileName:** nome do arquivo remoto movido do S3.
* **bucketName:** nome do _bucket_ do S3.
* **bucketNameMove:** nome do _bucket_ do arquivo movido.
* **remoteDirectoryMove:** nome do diretório remoto do arquivo foi movido.
* **remoteFileNameMove:** novo nome do arquivo remoto a ser movido.

### **Cenário da operação DELETE**

```
{
    "success": true,
    "remoteDirectory": "list/",
    "remoteFileName": "abc.file",
    "bucketName": "digibee-amazon-s3-connector-test"
}
```

* **success:** caso a chamada ocorra com sucesso, o resultado será “true”; do contrário, será “false”.
* **remoteDirectory:** nome do diretório remoto do S3.
* **remoteFileName:** nome do arquivo remoto deletado do S3.

### **Saída com erro**

```
{
  "success": false,
  "message": "Could no issue the operation: download in the AWS S3 Storage",
  "error": "com.amazonaws.services.s3.model.AmazonS3Exception: The specified key does not exist. (Service: Amazon S3; Status Code: 404; Error Code: NoSuchKey; Request ID: A21B8733BB9771DE; S3 Extended Request ID: 1zAtWB8gOvJKGKUBXdkWj7er8K6Ik6wUgdIUO1w41TsNo0b51B3MXrT4F4lADL+xI0Ojvf0e6z4=), S3 Extended Request ID: 1zAtWB8gOvJKGKUBXdkWj7er8K6Ik6wUgdIUO1w41TsNo0b51B3MXrT4F4lADL+xI0Ojvf0e6z4="
}
```

* **success:** “false”, pois ocorreu um erro na execução.
* **message:** mensagem de erro do componente.
* **error:** mensagem de erro recebida do servidor S3.
