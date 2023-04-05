---
description: Conheça o componente e saiba como utilizá-lo.
---

# REST V1 (Descontinuado)

O **REST V1** realiza chamadas a _endpoints_ REST a partir de um _pipeline_.

\
Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** URL a ser chamada - pode conter os parâmetros seguindo o padrão {:param1}, que serão substituídos pela propriedade correspondente da mensagem de entrada.
* **Content Type:** configura o Content Type e a codificação.
* **Verb:** tipo de chamada do REST (GET, POST e PUT).
* **Account:** conta a ser utilizada pelo componente.
* **Connection Timeout:** tempo de expiração da conexão (em milissegundos).
* **Reading Timeout:** tempo máximo para leitura (em milissegundos).
* **Stop On Client Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **Stop On Server Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **Advanced Settings:** configurações avançadas
* **Inject JWT:** se ativada, a opção injeta o JWT presente na chamada do _pipeline_ (gerado ou não pelo componente **JWT)** no _header_ Authorization da chamada REST.
* **Read JWT:** se ativada, a opção coloca como resposta o JWT que fica no _header Authorization_ interno, caso exista.
* **Raw Mode:** se ativada, a opção recebe ou passa um _payload_ sem ser JSON.
* **Allow Insecure Calls To HTTPS Endpoints:** quando ativada, a opção permite que chamadas não seguras a _endpoints_ HTTPS sejam feitas.
* **Enable Retries:** quanto ativada, a opção permite que sejam feitas novas tentativas.
* **Maximum Number Of Retries Before Giving Up:** número máximo de tentativas antes de desistir da chamada.
* **Time To Wait Before Each Retry:** tempo máximo entre tentativas (em milissegundos).
* **Compress Body With GZIP:** quanto ativada, a opção permite que o _body_ seja comprimido com GZIP.

&#x20;    &#x20;

### Path Parameter <a href="#path-parameter" id="path-parameter"></a>

**Exemplo**

[http://test.com/order/$EXPAND{:id,}](http://test.com/order/%24EXPAND%7B:id,%7D)

&#x20;   &#x20;

### Query Parameter <a href="#query-parameter" id="query-parameter"></a>

**Exemplo**

[http://test.com/order$QUERY{page=:page,search=:search}\r\n\t\t\t](http://test.com/order%24QUERY%7Bpage=:page,search=:search%7D/r/n/t/t/t/t)

&#x20;     &#x20;

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

application/x-www-form-urlencoded&#x20;

```
{
	header: {
		"headerA":"valueA",
		"headerB":"valueB"
	},
		url: {
		"urlParam1": "paramValue"
	},
	formData: {
		"field1": "value1",
		"field2": "value2"
	}
}
```

&#x20;  &#x20;

multipart/form-data

```
{
	header: {
		"headerA":"valueA",
		"headerB":"valueB"
	},
	url: {
		
	},
	multiPartData: {
		"files": {
		"file_formName" "filename",
		"files_formName[]" ["filename1","filename2"]
	},	"fields": {
		"field1" : "value1",
		"field2" : "value2",
	}
	}
}
```

&#x20;   &#x20;

O componente espera uma mensagem no seguinte formato:

```
{
	header: {
	"headerA":"valueA",
	"headerB":"valueB"
	},
	url: {
	"urlParam1": "paramValue"
	},
	body: {
	// message to be sent to the endpoint
	}
}
```

&#x20;   &#x20;

### Saída <a href="#sada" id="sada"></a>

* com sucesso

```
{
    status: XXX,
    body: {},
    headers: {}
}
```

* com erro

```
{
    error: "error message",
    code: XXX,
    body: {},
    headers: {} 
}
```

&#x20;  \
**IMPORTANTE:** no caso de alguns erros, _body_ e _headers_ estarão indisponíveis.
