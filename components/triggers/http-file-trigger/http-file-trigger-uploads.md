---
description: Conheça o trigger e saiba como utilizá-lo.
---

# HTTP File Trigger - Uploads

O **HTTP File Trigger** envia arquivos grandes (com tamanho superior a 5MB) para _pipelines_ de forma robusta e eficiente, utilizando HTTP.

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Methods:** define os métodos aceitos pelo _pipeline_ (GET, PUT, POST, PATCH e DELETE).
* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
* **Add Cross-Origin Resource Sharing (CORS) - CORS Headers:** adicione os CORS headers a serem retornados pelo _endpoint_ quando o processamento no pipeline terminar. O _Cross-Origin Resource Sharing (CORS)_ é um mecanismo que permite informar ao navegador quais origens tem a permissão para fazer requisições. Este parâmetro define o CORS especificamente ao _pipeline_ e suas restrições. Para configurar de forma global ao invés de individualmente em cada _pipeline,_ consulte o [artigo CORS Global](https://docs.digibee.com/documentation/v/pt-br/components/triggers/configuracoes-de-triggers/configuracao-global-de-cors).&#x20;

{% hint style="info" %}
**IMPORTANTE:** Utilizamos vírgula para informar múltiplos valores em um header, mas não adicionamos espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
{% endhint %}

* **Form Data Uploads**: habilita/desabilita o recebimento do _upload_ de _form data_ (_multi-part form data_).
* **Body Uploads**: habilita/desabilita o recebimento do _upload_ de _bodies_.
* **Body Upload Content Types**: define os _content types_ permitidos pelo _pipeline_ para o _upload_ de _bodies_.
* **Response Content Types**: define os _content types_ de resposta permitidos para o _pipeline_ - ao configurar essa resposta, você determina o formato de resposta.
* **Maximum Timeout**: define o tempo máximo de expiração (padrão = 60000).
* **Maximum Request Size:** define o tamanho máximo do arquivo na solicitação de upload (em MB) (máximo = 100 MB).
* **External API:** se ativada, a opção publica a API em um _gateway_ externo.
* **Internal API:** se ativada, a opção publica a API em um _gateway_ interno.
* **mTLS enabled API:** se a opção estiver ativada, a API é publicada em um gateway dedicado a APIs com mTLS ativo por padrão. Nesse caso, o host de acesso será diferente dos demais. O pipeline pode ter tanto a opção de _External_ API quanto a Internal API habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT. Para utilizá-lo no seu _realm_, é necessário fazer uma solicitação via chat e assim enviaremos as informações necessárias para instalação deste serviço.
* **API Key:** se ativada, a opção vai solicitar a chave para consumo do API.
* **Token JWT:** se ativada, a opção vai solicitar o _token_ para consumo do API.
* **Additional API Routes:** se ativada, a opção permite que você adicione novas rotas.
* **API Routes:** rotas customizáveis.
* **Security (Legacy):** se ativada, a opção determina a necessidade de uso de um _token_ JWT para acessar a API exposta.
* **Allow Redelivery Of Messages:** se ativada, a opção permite que as mensagens sejam entregues novamente caso o Pipeline Engine falhe.

### HTTP File Trigger em Ação <a href="#http-file-trigger-em-ao" id="http-file-trigger-em-ao"></a>

#### Cenário 1: POST de um arquivo com _content type_ "multipart/form-data" <a href="#cenrio-1-post-de-um-arquivo-com-content-type-multipartform-data" id="cenrio-1-post-de-um-arquivo-com-content-type-multipartform-data"></a>

Digamos que você queira enviar um arquivo com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com HTTP Trigger via POST com o _content type_ "multipart/form-data" __ para que esse arquivo fique disponível para ser trabalhado pelo _pipeline_.

Veja como fazer isso:

1. Crie um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Form Data Uploads**_.
2. Implante o _pipeline_.
3. Crie um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chame o _pipeline_ através deste _curl_:

```
curl -d “@file_name” https://godigibee.io/pipeline/realm_name/v1/http-file-upload  -v -H 'Content-Type: application/pdf' -H 'apikey: generated_token'
```

* **file\_name:** se refere a um arquivo local
* **realm\_name:** se refere ao _Realm_ onde o _pipeline_ se encontra
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado

\
O _pipeline_ receberá um _array_ _**files\[]**_ contendo:

* fileName
* param
* contentType

Dessa maneira, o arquivo pode ser referenciado e acessado a partir do _pipeline_:

```
{
  "body": null,
  "form": {},
  "headers": {
  ...
  },
  "queryAndPath": {},
  "method": "POST",
  "contentType": "application/pdf",
  "path": "/pipeline/realm_name/v1/http-file-upload",
  "files": [
    {      
      "fileName": "55acdc09-c0fc-4f6a-b3ee-f4199076b0c4",
      "param": "body",
      "contentType": "application/pdf"    
    }  
  ]
}
```

#### Cenário 2: POST de múltiplos arquivos com _content type_ "multipart/form-data" <a href="#cenrio-2-post-de-mltiplos-arquivos-com-content-type-multipartform-data" id="cenrio-2-post-de-mltiplos-arquivos-com-content-type-multipartform-data"></a>

Digamos que você tenha vários arquivos com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com HTTP Trigger via POST com o _content type_ "multipart/form-data" __ para que esses arquivos fiquem disponíveis para serem trabalhados pelo _pipeline_.

Para viabilizar isso, basta seguir estes passos:

1. Crie um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Form Data Uploads**_.
2. Implante o _pipeline_.
3. Crie um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chame o _pipeline_ através deste _curl_:

```
curl -F dgbfile1=@file_name1 -F dgbfile2=@file_name2 https://godigibee.io/pipeline/realm_name/v1/http-file-upload -v -H 'apikey: generated_token'
```

* **file\_name1:** se refere a um arquivo local
* **file\_name2:** se refere a um arquivo local
* **realm\_name:** se refere ao _Realm_ onde o _pipeline_ se encontra
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado

O _pipeline_ receberá um _array_ _**files\[]**_ contendo:

* fileName
* originalFileName
* param
* charset
* contentLength
* contentType

Dessa maneira, os arquivos podem ser referenciados e acessados a partir do _pipeline_:

```
{
  "body": "",
  "form": {},
  "headers": {
    ...
  },
  "queryAndPath": {},
  "method": "POST",
  "contentType": "multipart/form-data; boundary=------------------------b3c985803b952f2c",
  "path": "/pipeline/realm_name/v1/http-file-upload",
  "files": [
    {
      "fileName": "96f3ecb2-1c72-4980-9f01-6f44cafc719f",
      "originalFileName": "file1",
      "param": "dgbfile1",
      "contentType": "application/octet-stream",
      "charset": "UTF-8",
      "contentLength": 5242880
    },
    {
      "fileName": "58fb844f-a1d1-4788-b9b4-30df4b69165e",
      "originalFileName": "file2",
      "param": "dgbfile2",
      "contentType": "application/octet-stream",
      "charset": "UTF-8",
      "contentLength": 5242880
    }
  ]
}

```

#### Cenário 3: POST com qualquer _content type_ e _body_ com mais de 5 MB

Digamos que você tenha vários arquivos com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com HTTP Trigger via POST com qualquer _content type_ para que esses arquivos fiquem disponíveis para serem trabalhados pelo _pipeline_.

Tudo o que você tem que fazer é:

1. Criar um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Body Uploads**_.
2. Implantar o _pipeline_.
3. Criar um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chamar o _pipeline_ através deste _curl_:

```
curl -d '@file_name1' https://godigibee.io/pipeline/realm_name/v1/http-file-upload -v -H 'apikey: generated_token'
```

* **file\_name:** se refere a um arquivo local
* **realm\_name:** se refere ao _Realm_ onde o _pipeline_ se encontra
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado

O _pipeline_ receberá um _array_ _**files\[]**_ contendo:

* fileName
* param
* charset
* contentType

Dessa maneira, os arquivos podem ser referenciados e acessados a partir do _pipeline_:

```
{
  "body": null,
  "form": {},
  "headers": {
    ...
  },
  "queryAndPath": {},
  "method": "POST",
  "contentType": "application/pdf",
  "path": "/pipeline/realm_name/v1/http-file-upload",
  "files": [
    {
      "fileName": "55acdc09-c0fc-4f6a-b3ee-f4199076b0c4",
      "param": "body",
      "contentType": "application/pdf"
    }
  ]
}
```

\


### Resposta do HTTP File Trigger <a href="#resposta-do-http-file-trigger" id="resposta-do-http-file-trigger"></a>

É simples definir o formato da resposta do _pipeline_. Adicione um _Transformer_ ao final do _pipeline_ e defina a resposta:

```
{  
    "body": "<xml>Output 1</xml>",  
    "code": 200,  
    "Content-Type": "application/xml"
}
```

{% hint style="info" %}
**IMPORTANTE:** _**Content-Type**_** ** precisa ser um dos valores definidos em _**Response Content Types**_.
{% endhint %}

Clique [aqui](http-file-trigger-downloads.md) para ler o artigo que explica como garantir que a saída do _pipeline_ seja um arquivo.

\
