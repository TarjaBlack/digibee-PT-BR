---
description: Conheça o trigger e saiba como utilizá-lo.
---

# REST Trigger

Quando um _pipeline_ é configurado e publicado com o _**REST Trigger**_, um _endpoint_ REST é criado automaticamente. Você pode visualizar esse _endpoint_ após a implantação - basta clicar no cartão do _pipeline_ na tela de Run.

Com esse _trigger_, você pode criar APIs que atendem o padrão REST e definir rapidamente quais os métodos que seu _endpoint_ responderá.

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Methods:** serve para configurar os verbos HTTP a serem suportados pelo _endpoint_ após a implantação. Caso nenhum valor seja informado, será assumido o valor _default_: POST, PUT, GET, PATCH, DELETE e OPTIONS.
* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possíveis falhas em _proxys_ e _gateways_.
* **Maximum Timeout:** tempo limite para que o _pipeline_ processe informações antes de retornar uma resposta (padrão = 30000, limite = 300000). Em milissegundos. Caso o processamento demore mais do que a determinação do parâmetro, a requisição é finalizada e retorna _status-code_ 500, porém sem corpo nenhum.
* **Maximum Request Size:** tamanho máximo do _payload_ (em MB). O limite máximo do _payload_ configurável é de 5MB. Caso o _payload_ enviado pelo consumidor do _endpoint_ ultrapasse o limite, será retornada uma mensagem indicando que o tamanho máximo foi ultrapassado e um _status-code_ 413 com a seguinte mensagem:

```
{  
    "message": "Request size limit exceeded"
}
```

* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possiveis falhas em _proxys_ e _gateways_.
* **Add Cross-Origin Resource Sharing (CORS) - CORS Headers:** adicione os _CORS_ _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. O _Cross-Origin Resource Sharing (CORS)_ é um mecanismo que permite informar ao navegador quais origens tem a permissão para fazer requisições. Este parâmetro define o CORS especificamente ao _pipeline_ e suas restrições. Para configurar de forma global ao invés de individualmente em cada _pipeline,_ consulte o artigo [CORS Global](configuracoes-de-triggers/configuracao-global-de-cors.md).&#x20;

{% hint style="info" %}
**IMPORTANTE:** utilizamos vírgula para informar multiplos valores em um _header_, mas não adicionamos espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possiveis falhas em _proxys_ e _gateways_.
{% endhint %}

* **External API:** se a opção estiver ativada, a API é publicada em um _gateway_ externo.
* **Internal API:** se a opção estiver ativada, a API é publicada em um _gateway_ interno. Nesse caso, o IP interno é acessível apenas através da VPN dedicada ou do _Pipeline Executor._ O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente.
* **mTLS enabled API:** se a opção estiver ativada, a API é publicada em um _gateway_ dedicado a APIs com mTLS ativo por padrão. Nesse caso, o _host_ de acesso será diferente dos demais. O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT. Para utilizá-lo no seu _realm_, é necessário fazer uma solicitação via chat e assim enviremos as informações necessárias para instalação deste serviço.
* **API Key:** se a opção estiver ativada, o _endpoint_ pode ser consumido apenas se for enviada uma chave de API previamente configurada na Digibee Integration Platform. Existe um parâmetro de configuração global que obriga todos os _pipelines_ a serem publicados apenas com a opção **API Key** habilitada. A única forma de desativar esse parâmetro é por solicitação via chat. A desativação pode ser realizada de 2 formas: para um único _pipeline_, sendo que você precisa enviar o nome dele, ou globalmente, que o desativará para todos os _pipelines_ do seu _realm_.
* **Token JWT:** se a opção estiver ativada, o _endpoint_ pode ser consumido apenas se for enviado um _token_ JWT previamente gerado por outro _endpoint_ com essa capacidade. Leia o artigo da [implementação JWT](../security-components/digibee-jwt/implementacao-do-digibee-jwt.md) para obter mais detalhes.
* **Additional API Routes:** se a opção estiver ativada, o _trigger_ permite que você configure novas rotas. Veja mais sobre esse parâmetro na [seção](rest-trigger.md#h\_843b46ed62) abaixo.
* **Remove Digibee Prefix from Route:** esta opção estará disponível somente quando os parâmetros **External API** e **Internal API** estiverem desabilitados, e os parâmetros **mTLS enabled API** e **Additional API Routes** estiverem habilitados. Defina esta opção para remover o prefixo de rota padrão Digibee "/pipeline/{realm}/v{n}" da rota do _pipeline_. Saiba mais sobre o parâmetro **Remove Digibee Prefix from Route** na [seção](rest-trigger.md#remove-digibee-prefix-from-route) abaixo.
* **Routes:** exibido somente quando o parâmetro **Additional API Routes** __ estiver habilitado. É aqui que você consegue definir as rotas adicionais do _endpoint_.
* **Allow Redelivery Of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_. Leia o artigo sobre o [Pipeline Engine](../../plataforma/pipeline-engine.md) para obter mais detalhes.

## Additional API Routes <a href="#h_843b46ed62" id="h_843b46ed62"></a>

Conforme explicado anteriormente, essa opção serve para configurar rotas novas no _endpoint_.

Ao implantar um _pipeline_, uma URL é criada automaticamente. No entanto, você pode customizar a rota de acordo com o que for mais conveniente. Isso inclui também o recebimento de parâmetros através da rota.

Depois que os pipelines são implantados, as URLs adquirem a seguinte estrutura:&#x20;

TEST:&#x20;

```
https://test.godigibee.io/pipeline/{realm}/v{n}/{pipeline-name} 
```

ou PROD:&#x20;

```
https://api.godigibee.io/pipeline/{realm}/v{n}/{pipeline-name}
```

* **{realm}:** corresponde ao _realm_.&#x20;
* **v{n}:** versão principal (_major_) do _pipeline_.&#x20;
* **{pipeline-name}:** nome dado ao pipeline.

## Rota estática customizada <a href="#h_caf7632844" id="h_caf7632844"></a>

Vamos supor que você criou o _pipeline_ _product-list_. Levando em consideração o comentário acima, a sua URL teria a seguinte aparência:

```
https://test.godigibee.io/pipeline/realm/v1/product-list
```

Agora, veja como configurar uma rota estática para esse caso.

![](../../.gitbook/assets/Screenshot\_14.png)

Com essas configurações aplicadas e o _pipeline_ implantado, você obtém uma nova URL:

```
https://test.godigibee.io/pipeline/realm/v1/products
```

## Rota customizada com parâmetro no caminho <a href="#h_7e05ebe9ba" id="h_7e05ebe9ba"></a>

Usando como exemplo o mesmo _pipeline_ configurado anteriormente, veja como configurar a rota:

![](../../.gitbook/assets/Screenshot\_15.png)

Com essas configurações aplicadas e o _pipeline_ implantado, você obtém uma nova URL:

```
https://test.godigibee.io/pipeline/realm/v1/products/:id
```

Nesse caso, o consumidor do _endpoint_ pode enviar uma requisição contendo o _id_ de um produto e retornar apenas as informações dele. Exemplo da URL na requisição:

```
https://test.godigibee.io/pipeline/realm/v1/products/10156
```

Para utilizar esse valor enviado pela rota dentro do _pipeline_, recorra à sintaxe _Double Braces_:

```
{{ message.queryAndPath.id }}
```

## **Remove Digibee Prefix from Route**

Como explicado anteriormente, esta opção é recomendada para remover o prefixo de rota padrão Digibee da rota do _pipeline_.

Digamos que você tenha criado um _pipeline_ e definido o _trigger_ da seguinte forma:

<figure><img src="../../.gitbook/assets/Doc update triggers Remove Digibee Prefix mar 2023 (2).png" alt=""><figcaption></figcaption></figure>

Com as configurações aplicadas e o pipeline implantado, você terá uma nova URL:

```
https://test.godigibee.io/products
```

{% hint style="info" %}
**IMPORTANTE:** ao remover o prefixo padrão e definir a rota do _pipeline_ pelo parâmetro **Additional API Routes**, tenha cuidado para não definir uma rota de _pipeline_ existente que esteja em uso por outros _pipelines_. Caso você tenha mais do que uma versão principal do _pipeline_, também é importante ter em mente que o versionamento da rota do _pipeline_ deve ser feito pelo usuário devido à ausência de um parâmetro para versionamento da rota. Por exemplo: /pipeline/realm/v1/.
{% endhint %}

## REST Trigger em Ação <a href="#h_957f91b1a8" id="h_957f91b1a8"></a>

Veja a seguir como o _trigger_ se comporta em determinada situação e a sua respectiva configuração.

### **API de consulta de informações com retorno em JSON**

Observe como configurar um _pipeline_ com o _**REST Trigger**_ para retornar uma informação de dentro do _pipeline_ em formato JSON e como o retorno deve ser tratado especificamente para esse _trigger_.

Primeiramente, crie um novo _pipeline_ e configure o _trigger_. A configuração pode ser feita da seguinte forma:

![](../../.gitbook/assets/Screenshot\_16.png)

Com as configurações acima, você determina que:

* o _endpoint_ funciona apenas com o verbo GET.

Além disso, você determina que a API é do tipo externa e não precisa de _token_ para a comunicação.

{% hint style="info" %}
**IMPORTANTE:** esse exemplo serve apenas para fins educacionais. Em alguns casos você não deve deixar o _endpoint_ aberto por questões de segurança.
{% endhint %}

Agora observe como configurar um [MOCK](https://intercom.help/godigibee/pt-BR/articles/3186321-json-generator) no _pipeline_ para que ele seja o provedor de dados que o _endpoint_ retorna ao final. Coloque o componente indicado, conecte-o ao _trigge_r e configure-o com o seguinte JSON:

```
{    "data": {        "products": [            {                "name": "Samsung 4k Q60T 55",                "price": 3278.99            },            {                "name": "Samsung galaxy S20 128GB",                "price": 3698.99            }        ]    }}
```

Feito isso, o _endpoint_ já retornará automaticamente o JSON que definimos acima como resposta do endpoint.

Após a implantação, pegue a URL gerada e envie uma requisição do tipo GET. O _endpoint_ deve retornar o _status-code_ 200, e o corpo da resposta deve ter a mesma aparência do JSON que previamente definimos dentro do conector MOCK.

### **API de envio de informações com retorno em JSON**

Observe como configurar um _pipeline_ com o _**REST Trigger**_ para retornar uma informação de dentro do _pipeline_ em formato JSON e como o retorno deve ser tratado especificamente para esse _trigger_.

Primeiramente, crie um novo _pipeline_ e configure o _trigger_. A configuração pode ser feita da seguinte forma:

![](../../.gitbook/assets/Screenshot\_18.png)

Com as configurações acima, você determina que:

* o _endpoint_ funciona apenas com o verbo POST.

Além disso, você determina que a API é do tipo externa e não precisa de _token_ para a comunicação.

{% hint style="info" %}
**IMPORTANTE:** esse exemplo serve apenas para fins educacionais. Em alguns casos você não deve deixar o _endpoint_ aberto por questões de segurança.
{% endhint %}

Agora observe como configurar um [MOCK](../tools/json-generator.md) no _pipeline_ para que ele modifique os dados recebidos e que o _endpoint_ retornará ao final. Coloque o componente indicado, conecte-o ao _trigge_r e configure-o com o seguinte JSON:

```
{
    "data": {
        "products": [
            {
                "name": "Samsung 4k Q60T 55",
                "price": 3278.99
            },
            {
                "name": "Samsung galaxy S20 128GB",
                "price": 3698.99
            },
            {{ message.body.product }}
        ]
    }
```

Com isso configurado, um _payload_ com um novo produto será recebido e esse será adicionado ao _array_. Após isso, o _pipeline_ retornará para o consumidor o array com o novo produto adicionado.

Após a implantação, pegue a _url_ gerada e envie uma requisição do tipo POST com o seguinte _body_:

```
{
    "product": {
        "name": "Samsung galaxy note 10 256GB",
        "price": 2879.99
    }
}
```

O _endpoint_ deve retornar o _status-code_ 200, e o corpo da resposta deve ter a seguinte aparência:

```
{
  "data": {
    "products": [
      {
        "name": "Samsung 4k Q60T 55",
        "price": 3278.99
      },
      {
        "name": "Samsung galaxy S20 128GB",
        "price": 3698.99
      },
      {
        "name": "Samsung galaxy note 10 256GB",
        "price": 2879.99
      }
    ]
  }
}

```

Sempre que você realizar uma requisição ao _endpoint_ criado, a estrutura da mensagem que o _trigger_ entrega ao _pipeline_ é sempre a mesma e segue este padrão:

```
{
  "body": "{}",
  "form": {},
  "headers": {
    "Host": "pipeline-trigger-http:8100",
    "Connection": "keep-alive",
    "X-Forwarded-For": "***",
    "X-Forwarded-Proto": "http",
    "X-Forwarded-Host": "***",
    "my-custom-header": "a"
  },
  "queryAndPath": {
    "id": "1"
  },
  "method": "POST",
  "contentType": "application/json",
  "path": "/pipeline/digibee/v1/trigger-rest/1"

}
```

* **body:** conteúdo a ser enviado no _payload_ do _request_ para ser transformado em _string_ neste campo.
* **form:** se o _form-data_ for utilizado no _request_, os dados enviados são entregues neste campo.
* **headers:** os _headers_ enviados no _request_ são entregues neste campo, mas alguns são preenchidos automaticamente de acordo com a ferramenta utilizada para realizar o _request._
* **queryAndPath:** os parâmetros de _query_ e _path_ passados na URL são entregues neste campo.
* **method:** método HTTP utilizado no _request_ a ser entregue neste campo.
* **contentType:** quando informado no _request_, o valor do _Content-type_ é repassado para o _pipeline_ dentro desse campo.
* **path**: o _path_ utilizado na URL no _request_ é repassado nesse campo.
* **absoluteURI:** a URI absoluta do _request_ é passada nesse campo.
