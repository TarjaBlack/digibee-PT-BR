---
description: Conheça o componente e saiba como utilizá-lo.
---

# Mongo DB

O **Mongo DB** realiza operações em uma conexão de _database_ Mongo, retornando apenas um objeto JSON.\
&#x20;  &#x20;

{% hint style="info" %}
**IMPORTANTE:** cuidado com o consumo de memória para _datasets_ grandes.
{% endhint %}

&#x20;  &#x20;

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Use SSL/TLS to connect:** quando ativada, uma conexão com criptografia SSL/TLS será utilizada.
* **Custom SSL/TLS certificate:** define o certificado customizado que pode ser usado para a conexão com SSL/TLS. Este campo suporta expressões _Double Braces._
* **Allow invalid hostnames:** quando ativada, a opção ignora a validação de _hostnames_ em certificados SSL/TLS.
* **Operation:** operação a ser executada (FIND, AGGREGATE, DELETE ONE, DELETE MANY, INSERT ONE, INSERT MANY, UPDATE ONE, UPDATE MANY, REPLACE ONE, LIST INDEXES, CREATE INDEX e DROP INDEX).
* **Connection String:** conexão de _string_.
* **Database Name:** nome da base de dados.
* **Collection Name:** nome da coleção.
* **Expire after seconds:** tempo (em segundos) para expiração de documentos que utilizem um índice TTL. Disponível apenas se a operação CREATE INDEX for selecionada.
* **Query:** especificação Mongo a ser enfileirada. Por exemplo:\
  { \_id: ObjectId( \{{ message.$.id \}} ) }
* **Limit:** especificação do número máximo de objetos que podem ser retornados.
* **Skip:** número de objetos a serem pulados antes de retornar para a _query_.
* **Sort:** especificação do parâmetro a ser ordenado pelo campo.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Max Wait For Connection (in ms):** apresenta padrão 10000, selecione a melhor.&#x20;
* **Connection Timeout (in ms):** apresenta 30000, escolha a melhor opção.&#x20;
* **Socket Timeout (in ms):** 300000, selecione a melhor opção.&#x20;
* **Heartbeat Connection Timeout (in ms):** 10000 (ou a melhor escolha)
* **Max Connection Idle Timeout (in ms):** 1800000.&#x20;

{% hint style="info" %}
**IMPORTANTE**: Atualmente o componente suporta apenas contas _BASIC_ e deve ser informado através do campo Conta, **não diretamente** na _string_ de conexão.
{% endhint %}

Você pode:

\- utilizar um JSON fixo:

_**document = "{\\"data\\": \[{\\"object\\": 1}, {\\"object\\": 2}]}"**_\
&#x20;   _****_   &#x20;

\- conseguir algum JSON da mensagem, que vai buscar o objeto 'data' da mensagem:

_**document = "\{{ message.$.data \}}**_\
&#x20;   _****_   &#x20;

\- combinar ambos os exemplos:

_**document = "{\\"data\\": \[{\\"object\\": \{{ message.$.id1 \}}}, {\\"object\\": \{{ message.$.id2 \}}}]}"]**_

\
Se o Mongo DB precisar de alguma autenticação, você deverá criar uma conta (tipo BASIC) e utilizá-la no componente.&#x20;

Para converter _Double Braces_, nós utilizamos especificações de JSON Path. Clique [aqui](https://github.com/json-path/JsonPath) para saber mais.  \
&#x20; &#x20;

## Mongo DB em Ação <a href="#mongo-db-em-ao" id="mongo-db-em-ao"></a>

### Operação FIND <a href="#operao-find" id="operao-find"></a>

**Config**

```
{
	"operation": "FIND",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"query": "{_id: ObjectId({{ message.$.parameters.id }})}",
	"failOnError": false
}
```

&#x20;&#x20;

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	}
}
```

&#x20;  &#x20;

**Saída**

```
{"data": [...some data...],"rowCount": 10,"updateCount": 0}
```

&#x20;  &#x20;

### Operação REPLACE ONE <a href="#operao-replace-one" id="operao-replace-one"></a>

**Config**

```
{
	"data": [...some data...],
	"rowCount": 10,
	"updateCount": 0
}
```

&#x20; &#x20;

**Entrada**

```
{
	"operation": "REPLACE_ONE",
	"databaseName": "test",
	"collectionName": "model",
	"document": "{\"data\": [{\"object\": 1}, {\"object\": 2}]}",
	"url": "mongodb://localhost:27017",
	"query": "{_id: ObjectId({{ message.$.parameters.id }})}",
	"failOnError": false
}
```

&#x20;  &#x20;

**Saída**

```
{
    "data": {},
    "rowCount": 0,
    "updateCount": 1
}
```

&#x20;  &#x20;

### Operação UPDATE <a href="#operao-update" id="operao-update"></a>

**Config**

```
{
	"operation": "UPDATE",
	"databaseName": "test",
	"collectionName": "model",
	"document": "{\"$set\": {\"data\": [{\"object\": 1}, {\"object\": 2}]}}",
	"url": "mongodb://localhost:27017",
	"query": "{_id: ObjectId({{ message.$.parameters.id }})}",
	"failOnError": false
}
```

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	}
}
```

&#x20; &#x20;

**Saída**

```
{
	"data": {},
	"rowCount": 0,
	"updateCount": 1
}
```

&#x20; &#x20;

### Operação UPDATE\_MANY <a href="#operao-updatemany" id="operao-updatemany"></a>

**Config**

```
{
	"operation": "UPDATE_MANY",
	"databaseName": "test",
	"collectionName": "model",
	"document": "{\"$set\": {\"data\": [{\"object\": 1}, {\"object\": 2}]}}",
	"url": "mongodb://localhost:27017",
	"query": "{name: ObjectId({{ message.$.parameters.name }})}",
	"failOnError": false
}
```

**Entrada**

```
{
	"parameters": {
		"name": "NAME"
	}
}
```

&#x20; &#x20;

**Saída**

```
{{
	"data": {},
	"rowCount": 0,
	"updateCount": 1
}
```

&#x20; &#x20;

### Operação DELETE <a href="#operao-delete" id="operao-delete"></a>

**Config**

```
{
	"operation": "DELETE",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"query": "{_id: ObjectId({{ message.$.parameters.id }})}",
	"failOnError": false
}
```

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	}
}
```

&#x20;&#x20;

**Saída**

```
{
	"data": {},
	"rowCount": 10,
	"updateCount": 0
}
```

### Operação DELETE MANY <a href="#operao-delete-many" id="operao-delete-many"></a>

**Config**

```
{
	"operation": "DELETE_MANY",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"query": "{name: {{ message.$.data.name }}}",
	"failOnError": false
}
```

&#x20; &#x20;

**Entrada**

```
{
	"data": {
		"name": "NAME"
	}
}
```

&#x20; &#x20;

**Saída**

```
{
	"data": {},
	"rowCount": 10,
	"updateCount": 0
}
```

&#x20; &#x20;

### Operação INSERT <a href="#operao-insert" id="operao-insert"></a>

**Config**

```
{
	"operation": "INSERT",
	"databaseName": "test",
	"collectionName": "model",
	"document": "{\"data\": {{ message.$.body }}}",
	"url": "mongodb://localhost:27017",
	"failOnError": false
}
```

&#x20; &#x20;

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	},
	"body": [
		{"a": 1},
		{"a": 2}
	]
}
```

**Saída**

```
{
	"data": {},
	"rowCount": 0,
	"updateCount": 1
}
```

### Operação INSERT MANY <a href="#operao-insert-many" id="operao-insert-many"></a>

**Config**

```
{
	"operation": "INSERT_MANY",
	"databaseName": "test",
	"collectionName": "model",
	"document": "{{ message.$.body }}",
	"url": "mongodb://localhost:27017",
	"failOnError": false
}

```

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	},
	"body": [
		{"a": 1},
		{"a": 2}
	]
}
```

\
**Saída**

```
{
	"data": {},
	"rowCount": 0,
	"updateCount": 1
}
```

&#x20; &#x20;

### Operação AGGREGATE <a href="#operao-aggregate" id="operao-aggregate"></a>

**Config**

```
{
	"operation": "AGGREGATE",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"query": "[{\"$match\":{\"zip\":\"90210\"}},{\"$group\":{\"_id\":null,\"count\":{\"$sum\":1}}}]",
	"failOnError": false
}
```

**Entrada**

```
{
	"parameters": {
		"id": "5c87c7af06c3af7dbedc7bb3"
	}
}
```

**Saída**

```
{
	"data": [...some data...],
	"rowCount": 10,
	"updateCount": 0
}
```

### Operação LIST INDEXES

**Config**

```
{
	"operation": "LIST_INDEXES",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"failOnError": false
}
```

**Entrada**

```
{ }
```

**Saída**

```
{
	"data": [...some data...],
	"rowCount": 10
}
```

### Operação CREATE INDEX

**Config**

```
{
	"operation": "CREATE_INDEX",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"expireAfterSeconds": "3600",
	"query": "{ \"createdAt\": 1 }",
	"failOnError": false
}
```

**Entrada**

```
{ }
```

**Saída**

```
{
	"data": "createdAt_1",
	"updateCount": 1
}
```

### Operação DROP INDEX

**Config**

```
{
	"operation": "DROP_INDEX",
	"databaseName": "test",
	"collectionName": "model",
	"url": "mongodb://localhost:27017",
	"query": "{ \"createdAt\": 1 }",
	"failOnError": false
}
```

**Entrada**

```
{ }
```

**Saída**

```
{
	"data": { },
	"updateCount": 1
}
```

\
O **Mongo DB** suporta _Double Braces_ estáticos nos seguintes parâmetros previamente especificados:

* operation&#x20;
* url

Para ler o nosso artigo sobre _Double Braces_, clique [aqui](broken-reference).
