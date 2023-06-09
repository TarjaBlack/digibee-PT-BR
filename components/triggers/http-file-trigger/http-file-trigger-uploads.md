---
description: Conheça o trigger e saiba como utilizá-lo.
---

# HTTP File Trigger - Uploads

O **HTTP File Trigger** envia arquivos grandes (com tamanho superior a 5MB) para _pipelines_ de forma robusta e eficiente, utilizando HTTP.

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Methods:** define os métodos aceitos pelo _pipeline_ (GET, PUT, POST, PATCH e DELETE).
* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
* **Add Cross-Origin Resource Sharing (CORS) - CORS Headers:** adicione os _CORS headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. O _Cross-Origin Resource Sharing (CORS)_ é um mecanismo que permite informar ao navegador quais origens tem a permissão para fazer requisições. Este parâmetro define o CORS especificamente ao _pipeline_ e suas restrições. Para configurar de forma global ao invés de individualmente em cada _pipeline,_ consulte o [artigo CORS Global](https://docs.digibee.com/documentation/v/pt-br/components/triggers/configuracoes-de-triggers/configuracao-global-de-cors).&#x20;

{% hint style="info" %}
**IMPORTANTE:** utilizamos vírgula para informar múltiplos valores em um header, mas não adicionamos espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
{% endhint %}

* **Form Data Uploads**: habilita/desabilita o recebimento do _upload_ de _form data_ (_multi-part form data_).
* **Body Uploads**: habilita/desabilita o recebimento do _upload_ de _bodies_.
* **Body Upload Content Types**: define os _content types_ permitidos pelo _pipeline_ para o _upload_ de _bodies_.
* **Response Content Types**: define os _content types_ de resposta permitidos para o _pipeline_ - ao configurar essa resposta, você determina o formato de resposta.
* **Maximum Timeout**: define o tempo máximo de expiração (padrão = 60000).
* **Maximum Request Size:** define o tamanho máximo do arquivo na solicitação de upload (em MB) (máximo = 100 MB).
* **External API:** se ativada, a opção publica a API em um _gateway_ externo.
* **Internal API:** se ativada, a opção publica a API em um _gateway_ interno.
* **mTLS enabled API:** se a opção estiver ativada, a API é publicada em um _gateway_ dedicado a APIs com mTLS ativo por padrão. Nesse caso, o _host_ de acesso será diferente dos demais. O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT. Para utilizá-lo no seu _realm_, é necessário fazer uma solicitação via chat e assim enviaremos as informações necessárias para instalação deste serviço.
* **API Key:** se ativada, a opção vai solicitar a chave para consumo do API.
* **Token JWT:** se ativada, a opção vai solicitar o _token_ para consumo do API.
* **Additional API Routes:** se ativada, a opção permite que você adicione novas rotas.
* **Remove Digibee Prefix from Route:** esta opção estará disponível somente quando os parâmetros **External API** e **Internal API** estiverem desabilitados, e os parâmetros **mTLS enabled API** e **Additional API Routes** estiverem habilitados. Defina esta opção para remover o prefixo de rota padrão Digibee "/pipeline/{realm}/v{n}" da rota do _pipeline_. Saiba mais sobre o parâmetro Remove Digibee Prefix from Route na [seção](http-file-trigger-uploads.md#remove-digibee-prefix-from-route) abaixo.
* **API Routes:** rotas customizáveis.
* **Rate Limit:** se a opção estiver ativada, uma configuração de _rate limiting_ será aplicada no _API Gateway_. Esta opção estará disponível somente quando o parâmetro **API Key** estiver ativado. Veja mais sobre esse parâmetro na seção abaixo.
* **Limit by:** define a entidade na qual os limites serão aplicados. Opções: _API_.
* **Aggregate by:** define a entidade agregadora dos limites. Opções. _Consumer_ e _API Keys_.
* **Options:** define o limite de requisições que podem ser feitas dentro de um período de tempo.
* **Interval:** define o intervalo de tempo para o limite de requisições. Opções: _second, minute, hour, day_ e _month_.
* **Limit:** define o número máximo de requisições que os usuários podem fazer no intervalo de tempo especificado.
* **Allow Redelivery Of Messages:** se ativada, a opção permite que as mensagens sejam entregues novamente caso o _Pipeline Engine_ falhe.

## Remove Digibee Prefix from Route

Como explicado anteriormente, esta opção é recomendada para remover o prefixo de rota padrão Digibee da rota do _pipeline_.

Digamos que você tenha criado um _pipeline_ e definido o _trigger_ da seguinte forma:

<figure><img src="../../../.gitbook/assets/Doc update triggers Remove Digibee Prefix mar 2023 (2).png" alt=""><figcaption></figcaption></figure>

Com as configurações aplicadas e o _pipeline_ implantado, você terá uma nova URL:

```
https://test.godigibee.io/products
```

{% hint style="info" %}
**IMPORTANTE:** ao remover o prefixo padrão e definir a rota do _pipeline_ pelo parâmetro **Additional API Routes**, tenha cuidado para não definir uma rota de _pipeline_ existente que esteja em uso por outros _pipelines_. Caso você tenha mais do que uma versão principal do _pipeline_, também é importante ter em mente que o versionamento da rota do _pipeline_ deve ser feito pelo usuário devido à ausência de um parâmetro para versionamento da rota. Por exemplo: /pipeline/realm/v1/.
{% endhint %}

## Rate Limit <a href="#http-file-trigger-em-ao" id="http-file-trigger-em-ao"></a>

Ao criarmos APIs, geralmente queremos limitar o número de requisições da API que usuários podem fazer em um dado intervalo de tempo.

Esta ação pode ser executada ativando a opção **Rate Limit** e aplicando as seguintes configurações:

<figure><img src="../../../.gitbook/assets/Rate Limit OK example april 2023.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**IMPORTANTE:** se a API possui rotas adicionais, o limite é compartilhado entre todas as rotas. Para aplicar as configurações de _rate limit_, a API precisa ser configurada com uma _API Key_ para que o parâmetro **Aggregate by** possa ser usado por grupos de _API Keys_ (opção _Consumer_) ou _API Keys_ individuais (opção _API Key_).

Se vários parâmetros **Interval** estiverem configurados com valores repetidos, apenas um desses valores é considerado. Também é necessário que um valor maior que zero seja informado para o parâmetro **Limit**.

Se as opções de _rate limiting_ não forem definidas corretamente, elas serão ignoradas e um _warning log_ será emitido. Você pode visualizar esse _log_ na página de Pipeline Logs.
{% endhint %}

## HTTP File Trigger em Ação <a href="#http-file-trigger-em-ao" id="http-file-trigger-em-ao"></a>

### Cenário 1: POST de um arquivo com _content type_ "multipart/form-data" <a href="#cenrio-1-post-de-um-arquivo-com-content-type-multipartform-data" id="cenrio-1-post-de-um-arquivo-com-content-type-multipartform-data"></a>

Digamos que você queira enviar um arquivo com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com **HTTP Trigger** via POST com o _content type_ _"multipart/form-data"_ para que esse arquivo fique disponível para ser trabalhado pelo _pipeline_.

Veja como fazer isso:

1. Crie um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Form Data Uploads**_.
2. Implante o _pipeline_.
3. Crie um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chame o _pipeline_ através deste _curl_:

```
curl -d “@file_name” https://godigibee.io/pipeline/realm_name/v1/http-file-upload  -v -H 'Content-Type: application/pdf' -H 'apikey: generated_token'
```

* **file\_name:** se refere a um arquivo local.
* **realm\_name:** se refere ao _realm_ onde o _pipeline_ se encontra.
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado.

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

### Cenário 2: POST de múltiplos arquivos com _content type_ "multipart/form-data" <a href="#cenrio-2-post-de-mltiplos-arquivos-com-content-type-multipartform-data" id="cenrio-2-post-de-mltiplos-arquivos-com-content-type-multipartform-data"></a>

Digamos que você tenha vários arquivos com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com **HTTP Trigger** via POST com o _content type_ _"multipart/form-data"_ para que esses arquivos fiquem disponíveis para serem trabalhados pelo _pipeline_.

Para viabilizar isso, basta seguir estes passos:

1. Crie um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Form Data Uploads**_.
2. Implante o _pipeline_.
3. Crie um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chame o _pipeline_ através deste _curl_:

```
curl -F dgbfile1=@file_name1 -F dgbfile2=@file_name2 https://godigibee.io/pipeline/realm_name/v1/http-file-upload -v -H 'apikey: generated_token'
```

* **file\_name1:** se refere a um arquivo local.
* **file\_name2:** se refere a um arquivo local.
* **realm\_name:** se refere ao _realm_ onde o _pipeline_ se encontra.
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado.

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

### Cenário 3: POST com qualquer _content type_ e _body_ com mais de 5 MB

Digamos que você tenha vários arquivos com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com **HTTP Trigger** via POST com qualquer _content type_ para que esses arquivos fiquem disponíveis para serem trabalhados pelo _pipeline_.

Tudo o que você tem que fazer é:

1. Criar um _pipeline_ e configure seu _trigger_ como HTTP-File, habilitando a opção _**Body Uploads**_.
2. Implantar o _pipeline_.
3. Criar um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.
4. Chamar o _pipeline_ através deste _curl_:

```
curl -d '@file_name1' https://godigibee.io/pipeline/realm_name/v1/http-file-upload -v -H 'apikey: generated_token'
```

* **file\_name:** se refere a um arquivo local.
* **realm\_name:** se refere ao _realm_ onde o _pipeline_ se encontra.
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado.

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

## Resposta do HTTP File Trigger <a href="#resposta-do-http-file-trigger" id="resposta-do-http-file-trigger"></a>

É simples definir o formato da resposta do _pipeline_. Adicione um _Transformer_ ao final do _pipeline_ e defina a resposta:

```
{  
    "body": "<xml>Output 1</xml>",  
    "code": 200,  
    "Content-Type": "application/xml"
}
```

Outra solução é indicada em situações onde há uma limitação de tamanho de resposta para _payloads_ maiores que 5 MB. Nesse caso, é recomendável que a resposta do _pipeline_ seja um arquivo e não um _payload_. Isso pode ser feito usando o componente [_**File Writer**_](../../files/file-writer.md) para gerar o arquivo e referenciá-lo na resposta do _pipeline_ através da propriedade _"file"_ ao invés da propriedade _"body"_:

```
{
"file": {{ message.fileName }},
"code": 200,
"Content-Type": "application/json"
}
```

{% hint style="info" %}
**IMPORTANTE:** _**Content-Type**_ precisa ser um dos valores definidos em _**Response Content Types**_.
{% endhint %}

Leia o artigo [HTTP File Trigger - Downloads](https://docs.digibee.com/documentation/v/pt-br/components/triggers/http-file-trigger/http-file-trigger-downloads) para saber como se certificar de que a saída do pipeline seja um arquivo.
