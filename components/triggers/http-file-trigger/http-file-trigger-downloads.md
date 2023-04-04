---
description: Conheça o trigger e saiba como utilizá-lo.
---

# HTTP File Trigger - Downloads

O **HTTP File Trigger** baixa arquivos grandes de forma robusta e eficiente, chamando o método GET.

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Methods:** define os métodos aceitos pelo _pipeline_ (GET, PUT, POST, PATCH e DELETE).
* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double_ _Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
* **Add Cross-Origin Resource Sharing (CORS) - CORS Headers:** adicione os _CORS headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. O _Cross-Origin Resource Sharing (CORS)_ é um mecanismo que permite informar ao navegador quais origens tem a permissão para fazer requisições. Este parâmetro define o CORS especificamente ao _pipeline_ e suas restrições. Para configurar de forma global ao invés de individualmente em cada _pipeline_ consulte o artigo [CORS Global](../configuracoes-de-triggers/configuracao-global-de-cors.md).

{% hint style="info" %}
**IMPORTANTE:** utilizamos vírgula para informar múltiplos valores em um _header_, mas não adicionamos espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
{% endhint %}

* **Form Data Uploads**: habilita/desabilita o recebimento do _upload_ de _form data_ (_multi-part form data_).
* **Body Uploads**: habilita/desabilita o recebimento do _upload_ de _bodies_.
* **Body Upload Content Types**: define os _content types_ permitidos pelo _pipeline_ para o _upload_ de _bodies_.
* **Response Content Types**: define os _content types_ de resposta permitidos para o _pipeline_ - ao configurar essa resposta, você determina o formato de resposta.
* **Maximum Timeout**: define o tempo máximo de expiração (padrão = 60000).
* **Maximum Request Size:** define o tamanho máximo do arquivo na solicitação de _upload_ (em MB) (máximo = 100 MB).
* **External API:** se ativada, a opção pública a API em um _gateway_ externo.
* **Internal API:** se ativada, a opção pública a API em um _gateway_ interno.
* **mTLS enabled API:** se a opção estiver ativada, a API é publicada em um gateway dedicado a APIs com mTLS ativo por padrão. Nesse caso, o _host_ de acesso diferirá dos demais. O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT. Para utilizá-lo no seu _realm_, é necessário fazer uma solicitação via chat e assim enviaremos as informações necessárias para instalação deste serviço.
* **API Key:** se ativada, a opção vai solicitar a chave para consumo do API.
* **Token JWT:** se ativada, a opção vai solicitar o _token_ para consumo do API
* **Additional API Routes:** se ativada, a opção permite que você adicione novas rotas.
* **Remove Digibee Prefix from Route:** esta opção estará disponível somente quando os parâmetros **External API** e **Internal API** estiverem desabilitados, e os parâmetros **mTLS enabled API** e **Additional API Routes** estiverem habilitados. Defina esta opção para remover o prefixo de rota padrão Digibee "/pipeline/{realm}/v{n}" da rota do _pipeline_. Saiba mais sobre o parâmetro **Remove Digibee Prefix from Route** na [seção](http-file-trigger-downloads.md#remove-digibee-prefix-from-route) abaixo.
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

### Cenário: GET com qualquer _content type_ <a href="#cenrio-get-com-qualquer-content-type" id="cenrio-get-com-qualquer-content-type"></a>

Digamos que você tenha um arquivo com mais de 5MB. Você pode chamar um _endpoint_ de _pipeline_ configurado com HTTP Trigger via GET com qualquer _content type_ para que a requisição seja recebida e tratada_._ O arquivo é devolvido conforme o _content type_ de saída e o seu conteúdo _"as-is"_.

Para isso acontecer, basta você seguir estes passos:

1. Crie um _pipeline_ e configure seu _trigger_ como HTTP-File, incluindo o método GET e os _**Response Content Types**_ aceitos.
2. Insira um File Connector no _pipeline_ para buscar o arquivo a ser disponibilizado. Você pode, por exemplo, configurar o _**WGet**_ para obter um arquivo de uma URL passada ao _endpoint_ durante a chamada.
3. Insira o _**JSON Generator Connector**_ como o último passo do seu _pipeline_ para ser gerado um JSON no seguinte formato:

```
{ 
    "file": "file-download.pdf", 
    "Content-Type": "application/pdf"
}
```

{% hint style="info" %}
**IMPORTANTE:** esse passo é fundamental para que o _**HTTP File Trigger**_ entenda que o arquivo serve.
{% endhint %}

4\. Implante o _pipeline_.

5\. Crie um _consumer_ e o configure de modo que tenha acesso ao _pipeline_.

6\. Chame o _pipeline_ através deste _curl_:

```
curl https://godigibee.io/pipeline/realm_name/v1/pipeline_name -v -H 'Content-Type: application/pdf' -H 'apikey: generated_token' -H 'urlDownload: http://url/path'
```

* **realm\_name:** se refere ao _realm_ onde o _pipeline_ se encontra.
* **generated\_token:** se refere à chave de API gerada pelo _consumer_ recém-criado.
* **urlDownload:** parâmetro passado para o WGet Connector resolver o valor do campo URL. O atributo não é obrigatório, mas permite uma abordagem mais flexível através de _Double Braces_. Funciona perfeitamente se você definir o "path" diretamente no WGet Connector.

## Resposta do HTTP File Trigger <a href="#resposta-do-http-file-trigger" id="resposta-do-http-file-trigger"></a>

É simples definir o formato da resposta do _pipeline_. Adicione um Transformer ao final do _pipeline_ e defina a resposta:

```
{  
    "file": "file-download.pdf",  
    "code": 200,  "Content-Type": "application/pdf"
}
```

{% hint style="info" %}
**IMPORTANTE:** _**Content-Type**_** ** precisa ser um dos valores definidos em _**Response Content Types**_.
{% endhint %}

O _**HTTP File Trigger**_ responde _bodies_ que não sejam arquivos da mesma forma que o _**HTTP Trigger**_ faz. Isso permite que o _pipeline_ responda com o arquivo ou com alguma outra de acordo com o contexto da invocação. Para que o _**HTTP File Trigger**_ responda com um _body_ qualquer, basta que o último passo do _pipeline_ tenha a seguinte estrutura:

```
{ 
    "body": "informação que será escrita na saída do endpoint", 
    "Content-Type": "qual o tipo de conteúdo do body", 
    "code": <um código de retorno HTTP>
}
```

{% hint style="info" %}
**IMPORTANTE:** _**Content-Type**_** ** precisa ser um dos valores definidos em _**Response Content Types**_.
{% endhint %}
