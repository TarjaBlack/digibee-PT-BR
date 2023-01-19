---
description: Conheça o componente e saiba como utilizá-lo.
---

# Digibee JWT

O **Digibee JWT** gera e decodifica _tokens_ JWT para uso interno na Digibee Integration Platform. Em outras palavras, o _token_ gerado por esse componente serve para as comunicações que ocorrem entre _pipelines_ configurados com o _REST Trigger_ ou HTTP Trigger e seus derivados - desde que as autenticações do tipo JWT sejam configuradas.

Dê uma olhada nos parâmetros de configuração do componente:

![](<../../../.gitbook/assets/ezgif.com-gif-maker (23).gif>)

* **Operation:** GENERATE (que gera um _token_ JWT) e DECODE (que decodifica um _token_ JWT).
* **Scopes:** escopos para o _token_ JWT separados por vírgula (ex.: SCOPE1,SCOPE2,...,...).
* **Expiration:** tempo de expiração (em milissegundos). Aqui, sugerimos um número entre 0 e 31536000 (equivalente a 31536000000 milissegundos) (365 dias) que restringe a vida útil do JWT ao número máximo de segundos de expiração. Qualquer JWT com uma vida útil mais longa será recusado. Se esse valor for fornecido, a expiração da propriedade `claims- to-verify` também deverá ser especificada. Um período indefinido é representado pelo valor padrão de 0. Esta opção deve ser configurada tendo em mente uma possível distorção do relógio.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Operação GENERATE <a href="#operao-generate" id="operao-generate"></a>

O componente pode receber qualquer objeto na entrada e irá repassar o _body_ completo para geração do _token_. Se você quiser passar os **Scopes** e/ou **Expiration** dinamicamente, informe-os conforme ilustrado abaixo, junto com qualquer parâmetro adicional dentro da mensagem de entrada:

```
{
"scopes": "SCOPE1,SCOPE2,...,...",
"expiration": 1602790847,
"randomProperty": "someValue",
...
}
```

**Saída**

```
{
"status": "logged"
}
```

A propriedade _**Authorization**_ será colocada com o _token_ no _header_ de resposta \_\_ gerado pelas especificações acima.

**Exemplo**

_**Authorization**_: Bearer eyW4T.....

### Operação DECODE <a href="#operao-decode" id="operao-decode"></a>

Para essa operação, o componente não espera nenhuma estrutura mensagem de entrada, mas apenas um _token_ JWT no _header_ de solicitação durante a execução.

**Header**

Authorization: Bearer eyW4T.....

**Entrada**

```
{
"scopes": "SCOPE1,SCOPE2,...,...",
"expiration": 1602790847,
"randomProperty": "someValue",
...
}
```

**Saída**

```
{
"body": {
"dataToken": {
"consumer_name": "digibee",
"realm": "digibee",
"parameter1": "parameter_value",
"parameter2": "parameter_value",
...
}
}
}
```

**Erro**

```
{
error: "error message",]
code: XXX,
body: {
},
headers: {
}
}
```

**IMPORTANTE:** para alguns erros, _body_ e _headers_ estão indisponíveis.

## Digibee JWT em ação <a href="#digibee-jwt-em-ao" id="digibee-jwt-em-ao"></a>

Criamos um artigo sobre esse componente. Caso queira entender melhor o seu uso e aplicação, clique [aqui](implementacao-do-digibee-jwt.md).

## Tecnologia <a href="#tecnologia" id="tecnologia"></a>

Para entender melhor como o _token_ JWT \_\_ é gerado a partir desse componente, veja o exemplo a seguir.

Para todo JWT é necessário informar os _headers_, pois eles contêm toda a informação do algoritmo a ser utilizado na criptografia do _token_. Portanto, os _headers_ padrão do _token_ gerado são:

```
{
"alg": "HS256",
"typ": "JWT"
}
```

O _token_ JWT também é composto de um _payload_, que inclui toda a informação que trafega no _token_. Isso é informado na entrada do componente:

```
{
"scopes": [],
"consumer_name":"digibee",
"realm": "REALM",
"someRandomProperty": "someRandomValue",
….
}
```

O UUID é gerado aleatoriamente junto com a criação do _token_, o qual precisa ser assinado. Veja como identificar o UUID:

```
HMACSHA256(
base64UrlEncode(header) + "." +
base64UrlEncode(payload),
RANDOM_UUID
)
```

Ao final da execução, o _token_ será gerado dentro do _header **Authorization:**_

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.jY3Sv72B0BlRCrxLauMXHJi5zLY3v2BmknciOEh3q2c
```

### Posicionamento e entrada de dados do JWT

A ordem onde o **Digibee JWT** é inserido no _pipeline_ também influencia a operação e determina quais dados serão inseridos no _token_ JWT. Isso ocorre pois o componente adiciona ao _token_ qualquer conteúdo que esteja em um _step_ anterior (incluindo os dados recebidos na entrada do _pipeline_).

É importante considerar esse comportamento. Portanto, o **Digibee JWT** não deve ser colocado como primeiro componente em um _pipeline_. Componentes como **** [**JSON Transformer**](https://docs.digibee.com/documentation/v/pt-br/components/tools/json-transformer)**,** [**Transformer (JOLT)**](https://docs.digibee.com/documentation/v/pt-br/components/tools/transformer-jolt) **** e [**JSON Generator**](https://docs.digibee.com/documentation/v/pt-br/components/tools/json-generator) devem ser utilizados antes do JWT para determinar uma entrada de dados apropriada.

O exemplo abaixo indica uma entrada de dados recomendável no JWT:

```

{
"id": "d0c6392b-6f3d-49ac-a135-4649aaa74f22",
"number": 1,
"e-mail": "email@email.com"
}

```



Se você quiser saber mais sobre _tokens_ JWT, clique [aqui](https://jwt.io/).
