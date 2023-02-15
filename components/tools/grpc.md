---
description: Conheça o componente e saiba como utilizá-lo.
---

# gRPC

O componente _**gRPC**_ permite a realização de chamadas a serviços gRPC do tipo unário e _client stream_ via _payload_ ou via arquivo.

Dê uma olhada nos parâmetros de configuração do componente:

* **Method Type:** tipo de método que será utilizado na invocação do serviço. Os tipos de métodos suportados são _Unary_, _Client Stream - via Payload_ e _Client Stream - via File_. Esse parâmetro não suporta _Double Braces_.
* **URL**: endereço de chamada do serviço gRPC. Ex: localhost:50051. Esse parâmetro não suporta _Double Braces_.
* **Headers:** configura todos os tipos de _headers_ necessários para chamada (ex.: Authorization: Bearer Co4ECg1FeGFtcGxlLnByb3RvIjwKDEh).
* **Service name:** nome do serviço que está descrito dentro do arquivo de configuração .proto do servidor gRPC. Esse parâmetro não suporta _Double Braces_. No exemplo abaixo o _Service Name_ será “Greeter”:

```protobuf
service Greeter {
    rpc helloMethod(Hellorequest) returns (HelloResponse);

}
```

* **Method Name:** nome do método que está descrito dentro do arquivo de configuração .proto do servidor gRPC. Esse parâmetro não suporta _Double Braces_.

No exemplo abaixo o _Method Name_ será “helloMethod”:

```protobuf
service Greeter {
    rpc helloMethod(Hellorequest) returns (HelloResponse);

}
```

* **Proto Descriptor File:** base64 do arquivo “Descriptor” do arquivo .proto. Primeiramente, o “Descriptor” deverá ser gerado a partir de um arquivo .proto. Para fazer isso, basta rodar o seguinte comando no diretório corrente que estiver localizado o arquivo .proto:

**1. Gerar o arquivo "descriptor"**

**Arquivo .proto do diretório:** Example.proto

**Nome do arquivo descriptor a ser gerado:** proto.desc

_**protoc --include\_imports --descriptor\_set\_out=proto.desc Example.proto**_

**Download do compilador protoc:** [https://grpc.io/docs/protoc-installation/](https://grpc.io/docs/protoc-installation/)

**2. Realizar o encode deste arquivo para base64:**

```
tLmRpZ2liZWUuZ3JwY0IMRGlnaWJlZVByb3RvUAGiAgNITFdiBnByb3RvMw==
```

**3. Informar o base64 na propriedade "Proto Descriptor File"**

Esse parâmetro não suporta _Double Braces_.

* **Payload:** o _payload_ de requisição que será enviado ao servidor gRPC. Para o tipo de método _Unary_, deverá ser utlizado um objeto simples que contenha os campos definidos no arquivo .proto. Para o tipo de método _Client Stream - via Payload_ deverá ser utilizado um _array_ de objetos, onde cada item do _array_ é uma mensagem a ser enviada ao servidor gRPC. Esse parâmetro aceita Double Braces.
* **File Name:** nome do arquivo que será usado para enviar o _payload_ no modo _Client Stream - via File_. Esse arquivo deverá ser um arquivo JSON que contenha um _array_ e, dentro desse _array_, deve haver as mensagens a serem enviadas ao gRPC _server_ de forma assíncrona (_stream_).
* **JSON Path:** expressão JSON Path que irá determinar como será feita a leitura em _stream_ do arquivo JSON. Somente para o tipo de método _Client Stream - via File_.
* **Connection Timeout:** tempo de expiração da conexão com o servidor (em milissegundos).
* **Request Timeout:** tempo de expiração da chamada de requisição do componente com o servidor gRPC (em milissegundos).
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

{% hint style="info" %}
**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](broken-reference).
{% endhint %}

## Fluxo de mensagens <a href="#h_aaf20d022e" id="h_aaf20d022e"></a>

### Entrada <a href="#h_ab6f4db9e3" id="h_ab6f4db9e3"></a>

Espera-se um _payload_ de entrada que será utilizado dentro do parâmetro _payload_ do componente.

### Saída <a href="#h_c64435e814" id="h_c64435e814"></a>

Ao executar um componente SFTP utilizando as operações _download, upload_ ou _move_, a seguinte estrutura de JSON será gerada:

```
{
    "response": {},
    "success": "true"
}
```

* **response:** JSON de resposta recebido do serviço gRPC
* **success:** "true" se houve uma conexão e o _script_ foi executado mesmo se retornar erros no _stderr_

**Saída com erro**

```
{  
    "success": false,  
    "message": "Something went wrong while trying to call the gRPC server",  
    "error": "java.net.SocketTimeoutException: connect timed out"
}
```

* **success:** “false” quando a operação falha
* **message:** mensagem sobre o erro
* **exception:** informação sobre o tipo de erro ocorrido

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](../../build/pipelines/processamento-de-mensagens.md) e leia o nosso artigo.

## Componente gRPC em Ação <a href="#h_98436d3a37" id="h_98436d3a37"></a>

### **Unary**

Dado o seguinte arquivo .proto:

```protobuf
Example.proto

syntax = "proto3";
package digibee;

service Greeter {
  rpc unary (HelloRequest) returns (HelloReply) {}
  rpc clientStream (stream HelloRequest) returns (HelloReply) {}
  rpc serverStream (HelloRequest) returns (stream HelloReply) {}
  rpc Bidi(stream HelloRequest) returns (stream HelloReply);
}

message HelloRequest {
  string name = 1;
  string address = 2;
}

message HelloReply {
  string message = 1;
  int32 status = 2;
}
```

Primeiramente, é preciso gerar o arquivo _“descriptor”_:

1\. Dentro do diretório do arquivo, executar o comando:

_**protoc --include\_imports --descriptor\_set\_out=proto.desc Example.proto**_

2\. Com o “descriptor” em mão, gerar o base64 do arquivo proto.desc e adicioná-lo no campo _Proto Descriptor File_.

Configurações do componente:

**Method Type**: Unary

**URL**: localhost:50051

**Service Name**: Greeter

**Method Name**: unary

**Proto Descriptor File**: \<BASE64 DO ARQUIVO DESCRIPTOR GERADO ACIMA>

**Payload**:

```
{
    "name": "Charles",
    "address": "390 Fifth Avenue"
}
```

**Connect Timeout**: 30000

**Request Timeout**: 30000

**Fail On Error**: desabilitado

**Resposta**

```
{
    "message": "Hi Charles",
    "status": 200
}
```

### **Client Stream - via Payload**

Dado o arquivo .proto:

```protobuf
Example.proto

syntax = "proto3";
package digibee;

service Greeter {
  rpc unary (HelloRequest) returns (HelloReply) {}
  rpc clientStream (stream HelloRequest) returns (HelloReply) {}
  rpc serverStream (HelloRequest) returns (stream HelloReply) {}
  rpc Bidi(stream HelloRequest) returns (stream HelloReply);
}

message HelloRequest {
  string name = 1;
  string address = 2;
}

message HelloReply {
  string message = 1;
  int32 status = 2;
}
```

Primeiramente, é preciso gerar o arquivo _“descriptor_”:

1\. Dentro do diretório do arquivo, executar o comando:

_**protoc --include\_imports --descriptor\_set\_out=proto.desc Example.proto**_

2\. Com o “descriptor” em mão, gerar o base64 do arquivo proto.desc e adicioná-lo no campo _Proto Descriptor File_.

Configurações do componente:

**Method Type**: Client Stream - via Payload

**URL**: localhost:50051

**Service Name**: Greeter

**Method Name**: clientStream

**Proto Descriptor File**: \<BASE64 DO ARQUIVO DESCRIPTOR GERADO ACIMA>

**Payload**:

```
[
    {
        "name": "Charles",
        "address": "390 Fifth Avenue"
    },
    {
        "name": "Paul",
        "address": "32 Seventh Avenue"
    },
    {
        "name": "Yan",
        "address": "12 Fourth Avenue"
    }
]
```

**Connect Timeout**: 30000

**Request Timeout**: 30000

**Fail On Error**: desabilitado

**Resposta**

```
{
    "message": "Hi Charles, Paul and Yan",
    "status": 200
}
```

### **Client Stream - via File**

Dado o seguinte arquivo .proto:

```protobuf
Example.proto

syntax = "proto3";
package digibee;

service Greeter {
  rpc unary (HelloRequest) returns (HelloReply) {}
  rpc clientStream (stream HelloRequest) returns (HelloReply) {}
  rpc serverStream (HelloRequest) returns (stream HelloReply) {}
  rpc Bidi(stream HelloRequest) returns (stream HelloReply);
}

message HelloRequest {
  string name = 1;
  string address = 2;
}

message HelloReply {
  string message = 1;
  int32 status = 2;
}
```

Primeiramente, é preciso gerar o arquivo _“descriptor”:_

1\. Dentro do diretório do arquivo, executar o comando:

_**protoc --include\_imports --descriptor\_set\_out=proto.desc Example.proto**_

2\. Com o “descriptor” em mão, gerar o base64 do arquivo proto.desc e adicioná-lo no campo _Proto Descriptor File_.

Configurações do componente:

**Method Type**: Client Stream - via Payload

**URL**: localhost:50051

**Service Name**: Greeter

**Method Name**: clientStream

**Proto Descriptor File**: \<BASE64 DO ARQUIVO DESCRIPTOR GERADO ACIMA>

**File Name**: file.json

{% code title="file.json" %}
```
{ 
    "infos": [
        {
            "name": "Charles",
            "address": "390 Fifth Avenue"
        },
        {
            "name": "Paul",
            "address": "32 Seventh Avenue"
        },
        {
            "name": "Yan",
            "address": "12 Fourth Avenue"
        }
    ]
}

```
{% endcode %}

**JSON Path**: $.infos\[\*]

**Connect Timeout**: 30000

**Request Timeout**: 30000

**Fail On Error**: desabilitado

**Resposta**

```
{
    "message": "Hi Charles, Paul and Yan",
    "status": 200
}
```

\
