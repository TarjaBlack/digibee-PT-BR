---
description: Conheça o componente e saiba como utilizá-lo.
---

# REST V2

O **REST V2** realiza chamadas a _endpoints_ de HTTP, tornando muito simples ações como GET, POST, PUT e DELETE.

A grande diferença para a V1 é a adoção de expressões em _Double Braces_ para compor URL, _headers_, _query parameters_ e corpo da mensagem, permitindo acesso direto aos dados do _pipeline_.

Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** endereço que receberá a chamada HTTP.
* **Headers:** configura todos os tipos de headers necessários para chamada (ex.: _Content-Type: application/json ou multipart/form-data_).
* **Query Params:** configura os _query parameters_ necessários para a chamada.
* **Verb:** especifica o verbo que indica o método HTTP.
* **Account:** conta a ser utilizada pelo componente.
* **Custom Account #1:** conta adicional a ser utilizada pelo componente por meio de _Double Braces_ _\{{ account.custom-1.value \}}._ Clique [aqui](broken-reference) para ler o nosso artigo sobre o tema.
* **Custom Account #2:** conta adicional a ser utilizada pelo componente por meio de _Double Braces_ _\{{ account.custom-2.value \}}._ Clique [aqui](broken-reference) para ler o nosso artigo sobre o tema.
* **Connect Timeout:** tempo de expiração da conexão (em milissegundos).
* **Read Timeout:** tempo máximo para leitura (em milissegundos).
* **Stop On Client Error:** se ativada, a opção interrompe a execução do _pipeline_ quando ocorre um erro HTTP da família 4xx na chamada ao _endpoint_.
* **Stop On Server Error:** se ativada, a opção interrompe a execução do _pipeline_ quando ocorre um erro HTTP da família 5xx na chamada ao _endpoint_.
* **Advanced Settings:** configurações avançadas.
* **Raw Mode:** se ativada, a opção recebe ou passa um _payload_ que não é JSON.
* **Raw Mode As Base64:** quando ativada, a opção mostra o retorno como base64.
* **Save As Local File:** quando ativada, a opção salva o retorno como um arquivo no diretório local do _pipeline_.
* **Response File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt). _Double Braces_ são suportados.
* **Allow Insecure Endpoints:** quando ativada, a opção permite que chamadas a _endpoints_ HTTPS não seguros sejam realizadas.
* **Enable Retries:** quanto ativada, a opção permite que sejam feitas novas tentativas. É importante destacar que a opção de _Retry_ é acionada apenas para casos de _Server Error_. Em outros casos, o componente _**Retry**_ deve ser utilizado. Saiba mais sobre este componente lendo o [artigo](https://docs.digibee.com/documentation/v/pt-br/components/logic/retry).
* **Number Of Retries:** número máximo de tentativas antes de desistir da chamada.
* **Time To Wait Between Retries:** tempo máximo entre tentativas (em milissegundos).
* **Compress Body With GZIP:** quanto ativada, a opção permite que o _body_ seja comprimido com GZIP.
* **Force HTTP 1.1:** quando ativada, a opção força a solicitação a ser executada utilizando HTTP 1.1.
* **Override Response Charset:** quando ativada, a opção irá sobrescrever o _charset_ retornado do _endpoint_ para o _charset_ especificado na propriedade “Response Charset”; do contrário, o retorno do _charset_ no _header_ “Content-Type” será respeitado. Se nenhum _charset_ no _header_ “Content-Type” for retornado, será utilizado o padrão UTF-8.
* **Response Charset:** utilizado somente quando a opção “Override Response Charset” estiver ativada, forçará o uso do _charset_ especificado na propriedade (Padrão: UTF-8).
* **Disable Connection Pooling:** quando ativada, a opção não mantém as conexões em um _pool_. O seu uso é recomendado para _endpoints_ que apresentam problemas de compatibilidade quando conexões são reutilizadas.
* **Invalidate SSL Sessions on Every Call:** quando ativada, a opção invalida sessões SSL em todas as chamadas. O seu uso é recomendado para _endpoints_ que apresentam problemas de compatibilidade quando sessões SSL são reutilizadas (ex.: retomada de sessão SSL). Leve em consideração que ativar a opção fará com que o componente tenha um _thread_ único - isso significa que todas as execuções serão sequenciais para o mesmo _**REST**_ adicionado ao _pipeline canvas_.

**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](broken-reference).

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Você pode usar a seguinte configuração no corpo da mensagem e pode fazer uso dela através de _Double Braces_:

```
{
    "id": {{ DEFAULT(message.customer.id, UUID()) }},
    "name": {{ message.customer.name }},
    "type": "1"
}
```

**IMPORTANTE:** não se aplica ao verbo GET.

### Saída <a href="#sada" id="sada"></a>

* **em caso de sucesso**

```
{
    status: 2xx,
    statusMessage: "STATUS_MESSAGE",
    body: {},
    headers: {}
}
```

* **em caso de sucesso (com a utilização da **_**flag**_** "Raw Mode As Base64")**

```
{
    status: 2xx,
    statusMessage: "STATUS_MESSAGE",
    body: "conteúdo em formato de bas64",
    headers: {}
}
```

* **em caso de sucesso (com a utilização da **_**flag “**_**Save As Local File”)**

```
{
    status: 2xx,
    statusMessage: "STATUS_MESSAGE",
    body: {file: "nome do arquivo definido na propriedade Response File Name"},
    headers: {}
}
```

* **em caso de erro**

```
{
    error: "error message",
    code: XXX,
    body: {},
    headers: {}
}
```

## REST V2 em Ação <a href="#rest-v2-em-ao" id="rest-v2-em-ao"></a>

### Enviando um arquivo binário <a href="#enviando-um-arquivo-binrio" id="enviando-um-arquivo-binrio"></a>

Para enviar um arquivo binário pelo _**REST V2**_, basta informar:

* o _endpoint_ de destino
* o _content type_ (MIME Type do arquivo) no _header_ (ex.: application/pdf)
* o caminho onde o arquivo se encontra (apontar no campo **File Name**)

### Como fazer requisições utilizando o content-type: MultiPart/form-data <a href="#como-fazer-requisies-utilizando-o-content-type-multipartform-data" id="como-fazer-requisies-utilizando-o-content-type-multipartform-data"></a>

A primeira coisa que você precisa fazer é especificar esse _header_ no componente (Content-Type: Multipart/form-data).

Em seguida, depois de selecionar qualquer verbo HTTP (com exceção do GET), um campo vai se abrir para que você especifique o corpo do _payload_ a ser enviado. Este deve ser o padrão para:

* **especificar campos**

```
{
"fields": {
     "nome_do_campo1": "valor_do_campo_1",
     "nome_do_campo2": "valor_do_campo_2",
     …….
    }
}
```

* **especificar arquivos**

```
{
    "files": {
        "nome_do_campo_do_arquivo1": "caminho_que_se_encontra_o_arquivo1",
        "nome_do_campo_do_arquivo2": "caminho_que_se_encontra_o_arquivo2",
        …..
    }
}
```

Caso precise de ambas as especificações, você pode combiná-las com expressões em _Double Braces_:

```
{
    "files": {
        "file": {{ message.fileName }},
        "file2": {{ message.fileName2 }}
    },
    "fields": {
        "nome": {{ message.name }},
        "'endereço": {{ message.endereco }}
    }
}
```

### Como fazer requisições utilizando o content-type: **application/x-www-form-urlencoded** <a href="#utilizao-de-accounts" id="utilizao-de-accounts"></a>

A primeira coisa que você precisa fazer é especificar esse _header_ no componente (Content-Type: application/x-www-form-urlencoded).

Em seguida, depois de selecionar qualquer verbo HTTP (com exceção do GET), um campo vai se abrir para que você especifique o corpo do _payload_ a ser enviado.

Exemplo:

```
{ "nome_do_campo1": {{ message.campo1}}, "nome_do_campo2": {{ message.campo2}} }
```

### Utilização de _accounts_ <a href="#h_a43218138b" id="h_a43218138b"></a>

Veja quais são as _accounts_ suportadas pelo _**REST V2**_:

* **APIKEY**

Com o URL-PARAM-NAME e o API-KEY definidos na conta tipo Basic, a Plataforma faz a substituição na chamada da seguinte maneira:

```
https://www.address.com?<URL-PARAM-NAME>=<API-KEY>
```

* **BASIC**

Com o USERNAME e o PASSWORD definidos na conta tipo Basic, a Plataforma faz a substituição na chamada da seguinte maneira:

[`https://www.address.com`](https://www.address.com/)

**HEADERS**

**Authorization:** `Basic BASE64(<USERNAME>:<PASSWORD>)`

* **CUSTOM\_AUTH\_HEADER**

Com o HEADER-NAME e o HEADER-VALUE definidos na conta tipo CUSTOM\_AUTH\_HEADER, a Plataforma faz a substituição na chamada da seguinte maneira:

[https://www.address.com](https://www.address.com/)

**HEADERS**

`<HEADER-NAME>: <HEADER-VALUE>`

* **OAUTH\_BEARER\_TOKEN**

Caso você já tenha um _token_ OAUTH, você pode salvá-lo nesse tipo de conta e a Plataforma faz a substituição na chamada da seguinte maneira:

`h`[`ttps://www.address.com`](https://www.address.com/)

**HEADERS**

Authorization: `Bearer <TOKEN>`

* **OAUTH\_2**

É específico de cada tipo de provedor suportado. Com essa conta, o _access token_ é passado da forma que cada _provider_ espera.

**Microsoft e Google**

[`https://www.address.com`](https://www.address.com/)

**HEADERS**

**Authorization:** `Bearer <ACCESS_TOKEN>`

**Mercado Livre**

`https://www.address.com?access_token=`\<ACCESS\_TOKEN>

Para ter uma visão geral sobre a utilização de _accounts_, clique [aqui](../../configurations/contas-accounts/) e acesse o nosso outro artigo.

* **GOOGLE\_KEY**

Você pode recorrer à essa conta caso seja necessário utilizar uma chave para autenticação no serviço Google.

Para ter uma visão geral sobre a utilização de _accounts_, clique [aqui](../../configurations/contas-accounts/) e acesse o nosso outro artigo.

* **AWS\_4**

Para você acessar algum serviço da AWS via REST, será necessário utilizar esse tipo de conta. Com ela, o componente é responsável por gerar os _headers_ de autenticação e assinar a mensagem. Para tornar isso possível, fazemos uso da assinatura AWS 4.

**IMPORTANTE:** para o DynamoDB, é necessário especificar o _header_:

* _**X-Amz-Target = DynamoDB\_20120810.GetItem**_

caso você queira buscar um item no banco de dados

* **`X-Amz-Target = DynamoDB_20120810.PutItem`**

caso você queira fazer inserção de dados

Clique [aqui](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.LowLevelAPI.html) para acessar a documentação da AWS e saber qual _header_ especificar no uso do DynamoDB.

Para os demais serviços da AWS é necessário verificar se o _header_ **X-Amz-Content-Sha256** é obrigatório. Nesse caso, você precisa informar no header do componente o valor “required”:

`X-Amz-Content-Sha256 = required`

E se for preciso utilizar mais de um tipo de _account_ na mesma chamada, tire as suas dúvidas sobre o recurso de _Double Braces custom account_ clicando [aqui](broken-reference).
