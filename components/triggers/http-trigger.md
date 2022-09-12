---
description: Conheça o trigger e saiba como utilizá-lo.
---

# HTTP Trigger

Quando um _pipeline_ é configurado e publicado com o _**HTTP Trigger**_, um _endpoint_ HTTP é criado automaticamente. Você pode visualizar esse _endpoint_ após a implantação - basta clicar no cartão do _pipeline_ na tela de Runtime.

Com esse _trigger_, você tem a flexibilidade de definir diferentes tipos de conteúdo tanto para a requisição como para a resposta do _endpoint_.

Dê uma olhada nos parâmetros de configuração do _trigger_:

* **Methods:** serve para configurar os verbos HTTP a serem suportados pelo _endpoint_ após a implantação. Caso nenhum valor seja informado, será assumido o valor _default_: POST, PUT, GET, PATCH, DELETE e OPTIONS.
* **Request Content Types:** determina os tipos de conteúdo que o _endpoint_ pode receber. Se o parâmetro for deixado vazio, qualquer _Content-type_ é aceito.
* **Response Content Types:** tipos de conteúdo a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio (a resposta depende de tratamento com o _mock_ + Double Braces).
* **Response Headers:** _headers_ a serem retornados pelo _endpoint_ quando o processamento no _pipeline_ terminar. Esse parâmetro não pode ser deixado vazio e aceita _Double Braces_. Caracteres especiais não devem ser utilizados nas chaves, por conta de possiveis falhas em _proxys_ e _gateways_.
* **Add Cross-Origin Resource Sharing (CORS) - CORS Headers:** adicione os CORS headers a serem retornados pelo endpoint quando o processamento no pipeline terminar. O Cross-Origin Resource Sharing (CORS) é um mecanismo que permite informar ao navegador quais origens tem a permissão para fazer requisições. Este parâmetro define o CORS especificamente ao pipeline e suas restrições. Para configurar de forma global ao invés de individualmente em cada pipeline consulte o artigo [CORS Global .](configuracoes-de-triggers/configuracao-global-de-cors.md) Importante: Utilizei vírgula para informar multiplos valores em um header, mas não adicionei espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possiveis falhas em proxys e gateways.

{% hint style="info" %}
**Importante:** Utilizamos vírgula para informar multiplos valores em um header, mas não adicionamos espaço antes ou após a vírgula. Caracteres especiais não devem ser utilizados nas chaves, por conta de possiveis falhas em _proxys_ e _gateways_.
{% endhint %}

* **Maximum Timeout:** tempo limite para que o _pipeline_ processe informações antes de retornar uma resposta (padrão = 30000, limite = 300000). Em milissegundos. Caso o processamento demore mais do que a determinação do parâmetro, a requisição é finalizada e retorna _status-code_ 500, porém sem corpo nenhum.
* **Maximum Request Size:** tamanho máximo do _payload_ (em MB). O limite máximo do _payload_ configurável é de 5MB. Caso o _payload_ enviado pelo consumidor do _endpoint_ ultrapasse o limite, será retornada uma mensagem indicando que o tamanho máximo foi ultrapassado e um _status-code_ 413 com a seguinte mensagem:

```
{  
    "message": "Request size limit exceeded"
}
```

* **External API:** se a opção estiver ativada, a API é publicada em um _gateway_ externo.
* **Internal API:** se a opção estiver ativada, a API é publicada em um _gateway_ interno. Nesse caso, o IP interno é acessível apenas através da VPN dedicada ou do _Pipeline Executor._ O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente.
* **mTLS enabled API:** se a opção estiver ativada, a API é publicada em um gateway dedicado a APIs com mTLS ativo por padrão. Nesse caso, o host de acesso será diferente dos demais. O pipeline pode ter tanto a opção de External API quanto a Internal API habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT. Para utilizá-lo no seu realm, é necessário fazer uma solicitação via chat e assim enviremos as informações necessárias para instalação deste serviço.
* **API Key:** se a opção estiver ativada, o _endpoint_ pode ser consumido apenas se for enviada uma chave de API previamente configurada na Plataforma.
* **Token JWT:** se a opção estiver ativada, o _endpoint_ pode ser consumido apenas se for enviado um _token_ JWT previamente gerado por outro _endpoint_ com essa capacidade. Leia o artigo da [implementação JWT](../security-components/digibee-jwt/implementacao-do-digibee-jwt.md) para obter mais detalhes.
* **Additional API Routes:** se a opção estiver ativada, o _trigger_ permite que você configure novas rotas. Veja mais sobre esse parâmetro abaixo.
* **Routes:** exibido somente quando o parâmetro _Additional API Routes_ estiver habilitado. É aqui que você consegue definir as rotas adicionais do _endpoint_.
* **Allow Redelivery Of Messages:** se a opção estiver ativada, permite o reenvio da mensagem em caso de falha do _Pipeline Engine_. Leia o artigo sobre o [Pipeline Engine](../../plataforma/pipeline-engine.md) para obter mais detalhes.
* **mTLS enabled API (BETA Restricted):** se a opção estiver ativada, a API é publicada em um _gateway_ dedicado a APIs com mTLS ativo por padrão. Nesse caso, o _host_ de acesso será diferente dos demais_._ O _pipeline_ pode ter tanto a opção de **External API** quanto a **Internal API** habilitadas simultaneamente, mas é recomendado deixá-las inativas. Este parâmetro não suporta API Key e JWT e está em fase Beta Restricted. Para utilizá-lo no seu realm, é necessário fazer uma solicitação via chat e a Digibee irá avaliar a sua inclusão no programa Beta Restricted.

#### Additional API Routes <a href="#h_b4715f137e" id="h_b4715f137e"></a>

Conforme explicado anteriormente, essa opção serve para configurar rotas novas no _endpoint_.

Ao implantar um _pipeline_, uma URL é criada automaticamente. No entanto, você pode customizar a rota de acordo com o que for mais conveniente. Isso inclui também o recebimento de parâmetros através da rota.

Depois que os _pipelines_ são implantados, as URLs adquirem a seguinte estrutura:

TEST: https://test.godigibee.io/pipeline/{realm}/v{n}/{pipeline-name}

&#x20;ou PROD: https://api.godigibee.io/pipeline/{realm}/v{n}/{pipeline-name}

* **{realm}:** corresponde ao Realm
* **v{n}:** versão principal (major) do _pipeline_
* **{pipeline-name}:** nome dado ao _pipeline_

#### **Rota estática customizada** <a href="#h_9bd4c185b3" id="h_9bd4c185b3"></a>

Vamos supor que você criou o _pipeline_ product-list. Levando em consideração o comentário acima, a sua URL teria a seguinte aparência:

```
https://test.godigibee.io/pipeline/realm/v1/product-list
```

Agora, veja como configurar uma rota estática para esse caso.

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/300361598/98b19e28dc784c6d0650bedf/1zGq3cxkhxxKdY22MavRoKRzJBhhgWXscC46HnwZo7QPAtLf6AxsJeGh0ZHJsXhy6CU3TVXsT-xI-YtJt56BCotCtBONwRPtLpMeH5AQgL4178dYl1aJvPa5yO9xPBUw28DBrSYi)

Com essas configurações aplicadas e o _pipeline_ implantado, você obtém uma nova URL:

```
https://test.godigibee.io/pipeline/realm/v1/products
```

#### Rota customizada com parâmetro no caminho <a href="#h_00b02edd10" id="h_00b02edd10"></a>

Usando como exemplo o mesmo _pipeline_ configurado anteriormente, veja como configurar a rota:

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/300361603/d5b2eb8b57481ff2ede2d16a/\_hzEZw6S\_mhvso--W9dpfjfVCcpAcZv\_i3MSMdLQVDQzLFeplSWvj1YuUOWMYX8B6mIyhzX-BwngN633ey68Ga-0KcffADTP97kDL-EDcn5NvkXPtu4mtHpLs3zBwbMSB7ktjGn\_)

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

## **Adding Response Headers** <a href="#h_965b5606ac" id="h_965b5606ac"></a>

Conforme explicado anteriormente, essa opção serve para configurar _headers_ na resposta do _endpoint_.

**IMPORTANTE**: Não utilizar caracteres especiais.

![](https://lh5.googleusercontent.com/nDuAL25oSOFX0SKlukgUcbkUGGJsUbZuBqsfEuEZyW0dtFfh5AKKy\_aB1Q-u9KWMIKq1K6DyEAM7D3KqLnZsRGQzRRNzfVKWBTs4ksN2nqhBT9NJ6gWAobdMsMQM3qM7xjxGadt7)

Para utilizar esse valor enviado pela rota dentro do _pipeline_, recorra à sintaxe _Double Braces_:

`{{ message.parameter }}`

### **HTTP Trigger em Ação** <a href="#h_8dce545afc" id="h_8dce545afc"></a>

Veja a seguir como o _trigger_ se comporta em determinada situação e a sua respectiva configuração.

#### API de consulta de informações com retorno em XML <a href="#h_24fbb8c420" id="h_24fbb8c420"></a>

Observe como configurar um _pipeline_ com o _**HTTP Trigger**_ para retornar uma informação de dentro do _pipeline_ em formato XML e como o retorno deve ser tratado especificamente para esse _trigger_.

Primeiramente, crie um novo _pipeline_ e configure o _trigger_. A configuração pode ser feita da seguinte forma:

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/300361607/203b92abf3624304ce8dc49b/eIvFiQjW7nK4EEXXQfBmr\_XxnHb9K3b32HVRm2cHzKRa6awLxsf2fK8tPGdSo3CTRzno80dXjdcPB1pseaSKl1B8FilxP7fyvR\_P5aQbr6V85ktOsGHr2tWwVRi7xAaLf9BKppxY)

Com as configurações acima, você determina que:

* o _endpoint_ funciona apenas com o verbo GET;
* a requisição aceita somente _content-type_ relacionados ao XML;
* o _response_ retorna somente _content-type_ relacionados ao XML.

Além disso, você determina que a API é do tipo externa e não precisa de _token_ para a comunicação.

**IMPORTANTE:** esse exemplo serve apenas para fins educacionais. Em alguns casos você não deve deixar o _endpoint_ aberto por questões de segurança.

Agora observe como configurar um [MOCK](../tools/json-generator.md) no _pipeline_ para que ele seja o provedor de dados que o _endpoint_ retorna ao final. Coloque o componente indicado, conecte-o ao _trigge_r e configure-o com o seguinte JSON:

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
            }
        ]
    }
}
```

O próximo passo é adicionar um componente que transforme o JSON previamente criado em um padrão XML. Para isso, utilize o [JSON To XML Transformer](../tools/json-to-xml-transformer.md), adicione-o no _canvas_ e conecte-o logo após o JSON Generator colocado previamente. Mantenha a configuração da seguinte forma:

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/300361610/32f515a62dd0445765885d10/L1l4cLO6j3cr5q\_uPe972uQsUTLj6e7wmUgQWGFDofsATk2ghhW7ltj2zZ3ico4B7acvq2oKJJl6ZaPIRL7ZgMPFl9dN1uLB932359UkhzCYPK-0ywr0gJZqB9dFmJHdb9ObaNPn)

Feito isso, o último passo é formatar e determinar como será realizado o retorno dessas informações para o consumidor. Coloque um MOCK novamente, sendo que dessa vez a sua função é apenas formatar a resposta. Conecte-o à saída do JSON To XML Transformer.

Para a configurar esse MOCK, utilize o seguinte JSON:

```
{    
    "code": 200,    
    "body": {{ message.data }},    
    "Content-Type": "text/xml"
}
```

* **code:** HTTP _Status Code_ a ser retornado pelo _endpoint_ após a finalização da requisição
* **body:** corpo da mensagem de resposta (_Double Braces_ estão sendo utilizados para repassar a informação convertida no passo anterior). Esse item precisa ser necessariamente uma _string_. Se o dado que você deseja enviar é um JSON, utilize a função [TOSTRING](../../build/funcoes-double-braces/funcoes-de-string.md).
* **Content-type:** tipo de conteúdo do corpo da resposta. Todos os tipos são suportados, porém precisam ser declarados no campo **Response Content Types**.

Ao finalizar todas essas configurações, você deve ter um _pipeline_ parecido com o que a imagem abaixo demonstra:

![](https://digibee-d5ff4ba226ed.intercom-attachments-7.com/i/o/300361620/f3a5130508b5232d5a6930f9/n-2HIOx9VOY4lKRD04AkPO4y3BD3LwAn5clkl8yqW38PahaJUmlQUFKbI3DPTNnFUAFqB6mDUzKG1vcadaG8ARyjBUR-behvriLyQgjy-miDozZPAMXtgnnY2iNjlY1xsBZHnFsn)

Após a implantação, pegue a _url_ gerada e envie uma requisição do tipo GET. O _endpoint_ deve retornar o _status-code_ 200, conforme definido anteriormente, e o corpo da resposta deve ter a seguinte aparência:

```
<?xml version='1.0' encoding='UTF-8' standalone='no' ?>
<doc>
  <products>
    <name>Samsung 4k Q60T 55</name>
    <price>3278.99</price>
  </products>
  <products>
    <name>Samsung galaxy S20 128GB</name>
    <price>3698.99</price>
  </products>
</doc>
```

Sempre que você realizar uma requisição ao _endpoint_ criado, a estrutura da mensagem que o _trigger_ entrega ao _pipeline_ é sempre a mesma e segue este padrão:

```
{
  "body": "<xml>\n\t<id>1</id>\n</xml>\t",
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
  "contentType": "application/xml",
  "path": "/pipeline/digibee/v1/trigger-http/1"
}
```

* **body:** conteúdo a ser enviado no _payload_ do _request_ para ser transformado em _string_ neste campo
* **form:** se o _form-data_ for utilizado no _request_, os dados enviados são entregues neste campo
* **headers:** os _headers_ enviados no _request_ são entregues neste campo, mas alguns são preenchidos automaticamente de acordo com a ferramenta utilizada para realizar o _request_
* **queryAndPath:** os parâmetros de _query_ e _path_ passados na URL são entregues neste campo
* **method:** método HTTP utilizado no _request_ a ser entregue neste campo
* **contentType:** quando informado no _request_, o valor do _Content-type_ é repassado para o _pipeline_ dentro deste campo
* **path**: o _path_ utilizado na URL no _request_ é repassado nesse campo

\
