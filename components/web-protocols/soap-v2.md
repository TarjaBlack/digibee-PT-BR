---
description: Conheça o componente e saiba como utilizá-lo.
---

# SOAP V2

O _**SOAP V2**_ invoca _endpoints_ SOAP de um _pipeline_. Expressões em _Double Braces_ são suportadas.

Além disso, o componente utiliza _templates_ Apache FreeMaker para gerar a mensagem de chamada que converte o retorno de SOAP para JSON, tentando ao máximo não corromper a conversão.

Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** URL a ser chamada - pode conter os parâmetros seguindo o padrão {:param1}, que serão substituídos pela propriedade correspondente da mensagem de entrada.
* **Account:** conta a ser utilizada pelo componente.
* **Send the Request Body from a File:** se habilitada, a opção considera o conteúdo a ser enviado na chamada através de um arquivo; do contrário, será considerado o que for especificado em "Template".
* **File Name:** informa o nome do arquivo a ser enviado na chamada SOAP, se a opção “Send the Request Body from a File” estiver ativada.
* **Template:** _template_ Apache FreeMarker para que a mensagem SOAP seja enviada na solicitação.
* **HEADERS:** _headers_ da chamada.
* **QUERY PARAMS:** _query_ parameters da chamada.
* **Connection Timeout:** tempo de expiração da conexão (em milissegundos).
* **Reading Timeout:** tempo máximo para leitura (em milissegundos).
* **Stop On Client Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **Stop On Server Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **All Values As String:** se ativada, a opção vai retornar todos os valores dentro das propriedades XML em _string_.
* **With Spacename:** se ativada, a opção mantém os _spacenames_ no retorno do XML.
* **Advanced Settings:** configurações avançadas.
* **Allow Insecure Calls To HTTPS Endpoints:** quando ativada, a opção permite que chamadas não seguras a _endpoints_ HTTPS sejam feitas.
* **Raw Mode:** se ativada, a opção recebe ou passa um _payload_ sem ser JSON.
* **Save As Local File:** quando ativada, a opção salva o retorno como um arquivo no diretório local do _pipeline_. O arquivo será salvo apenas quando houver sucesso na chamada SOAP, ou seja, quando o _http status code_ da resposta estiver entre 200 e 399.
* **Response File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt) onde será salva a resposta da chamada _SOAP_. _Double Braces_ são suportados.
* **Enable Retries:** quanto ativada, a opção permite que sejam feitas novas tentativas.
* **Maximum Number Of Retries Before Giving Up:** número máximo de tentativas antes de desistir da chamada.
* **Time To Wait Before Each Retry:** tempo máximo entre tentativas (em milissegundos).
* **Override Response Charset:** quando ativada, a opção irá sobrescrever o charset retornado do endpoint para o charset especificado na propriedade Response Charset. Quando desabilitada ela respeitará o retorno do charset no header Content-Type. Caso não retorne nenhum charset no content type o padrão utilizado será UTF-8.
* **Response Charset:** utilizado somente quando a opção Override Response Charset estiver ativa e forçará o uso do charset especificado nesta propriedade. Padrão: UTF-8.

## Fluxo de mensagens

### Entrada

```
body: “<a><b>{{ message.b }}</b><#list><references as reference><c>${reference.name}</c></references></#list></a>”
```

### Saída

```
{
    headers: {{ message.headers }},
    queryParams: {{ message.queryParams }},
    references: [
        {name:1},
        {name:2}
    ],
    b: “test”
}
```

## SOAP V2 em ação

### **Sobre o template variável**

O nome da variável também pode conter sinal de menos (-), ponto (.) e dois pontos (:) em qualquer posição, desde que eles sejam acompanhados de uma barra invertida (\\) logo antes. Do contrário, os sinais podem ser interpretados como operadores.

### **Sobre substituição de números**

### Entrada

```html
<#assign x=42>
  ${x}
  ${x?string}  <#-- the same as ${x} -->
  ${x?string.number}
  ${x?string.currency}
  ${x?string.percent}
  ${x?string.computer}
```

### **Saída**

```
42
42
42
$42.00
4,200%
42
```

### **Formato de número**

```
<#setting number_format="0.####">
```

### Para verificar se o campo não é nulo

```
<#if varTest??>${varTest}</#if>
```
