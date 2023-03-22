---
description: Conheça o componente e saiba como utilizá-lo.
---

# WGet

O **WGet** realiza o _download_ de qualquer arquivo através de uma URL.

Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** de onde o arquivo será baixado - expressões em _Double Braces_ são suportadas.
* **Headers:** _headers_ da chamada.
* **Query Params:** _query parameters_ da chamada.
* **Account:** conta a ser utilizada pelo componente.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Allow Insecure Calls To HTTPS Endpoints:** quando ativada, a opção permite que chamadas não seguras a _endpoints_ HTTPS sejam feitas.
* **Binary File:** se ativada, a opção retorna a base64 do arquivo.
* **Local Save:** se ativada, a opção permite que o arquivo seja salvo localmente.
* **File Name:** nome do arquivo local a passar por _download_ ou _upload_.

## WGet em Ação <a href="#wget-em-ao" id="wget-em-ao"></a>

### Exemplo com Double Braces estáticos <a href="#exemplo-com-double-braces-estticos" id="exemplo-com-double-braces-estticos"></a>

URL

```url
https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
```

### Exemplo com Double Braces dinâmicos <a href="#exemplo-com-double-braces-dinmicos" id="exemplo-com-double-braces-dinmicos"></a>

URL

```
{{ message.example.url }}
```

```
https://www.download.com/file/{{ message.id }}/pdf
```

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Você não precisa especificar o formato de entrada se utilizar _Double Braces_ para preencher os parâmetros.

O **File Name** substitui o nome padrão e a **URL** substitui a URL padrão.

### Saída <a href="#sada" id="sada"></a>

Se a opção _**Local Save**_ estiver ativada:

```
{
    "fileName": "",
    "success": ""
}
```

Se as opções _**Local Save**_ e _**Binary File**_ estiverem ativadas:

```
{
    "fileBase64": ""
}
```

Se as opções _**Local Save**_ e _**Binary File**_ NÃO estiverem ativadas:

```
{
    "fileText": ""
}
```

Em caso de erro:

```
{
    "error": {
        "exception": "",
        "message": ""
    }
}
```
