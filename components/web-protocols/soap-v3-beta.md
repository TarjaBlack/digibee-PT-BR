---
description: Conheça o componente e saiba como utilizá-lo.
---

# SOAP V3 (BETA)

O SOAP V3 invoca endpoints SOAP de um pipeline. Expressões em Double Braces são suportadas.

Além disso, o componente utiliza templates Apache FreeMaker para gerar a mensagem de chamada que converte o retorno de SOAP para JSON, tentando ao máximo não corromper a conversão.

## Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** URL a ser chamada - pode conter os parâmetros seguindo o padrão {:param1}, que serão substituídos pela propriedade correspondente da mensagem de entrada.
* **Account:** conta a ser utilizada pelo componente.
* **Custom Account #1:** conta adicional a ser utilizada pelo componente por meio de Double Braces \{{ account.custom-1.value \}}. Clique aqui para ler o nosso artigo sobre o tema.&#x20;
* **Custom Account #2:** conta adicional a ser utilizada pelo componente por meio de Double Braces \{{ account.custom-2.value \}}. Clique aqui para ler o nosso artigo sobre o tema.
* **Send the Request Body from a File:** se habilitada, a opção considera o conteúdo a ser enviado na chamada através de um arquivo; do contrário, será considerado o que for especificado em "Template".
* **File Name:** informa o nome do arquivo a ser enviado na chamada SOAP, se a opção “Send the Request Body from a File” estiver ativada.
* **Template:** template Apache FreeMarker para que a mensagem SOAP seja enviada na solicitação.
* **HEADERS:** headers da chamada.
* **QUERY PARAMS:** query parameters da chamada.
* ​​Attachments (MTOM): configura arquivos ou conteúdos binários a serem enviados na requisição utilizando a tecnologia MTOM&#x20;
  * Is Binary: se ativada, o conector deverá receber o conteúdo binário e o ID do arquivo a ser enviado na requisição, do contrário, deve ser informado o nome do arquivo.&#x20;
  * File Name: informa o nome do arquivo a ser enviado junto do XML configurado em Template (Is Binary desativada).&#x20;
  * File ID: informa o ID do arquivo a ser enviado junto do XML configurado em Template. (Is Binary ativada)&#x20;
  * Base64 Content: informa o conteúdo em Base64 a ser enviado junto do XML configurado em Template. (Is Binary ativada).

{% hint style="info" %}
**IMPORTANTE**: para utilizar a tecnologia MTOM, é necessário que o arquivo ou conteúdo em Base64 seja referenciado diretamente no XML da requisição, sendo substituído pelo valor configurado em File Name ou File ID, dentro da tag [inc:Include](inc:Include) padrão junto do namespace (xmlns:inc="http://www.w3.org/2004/08/xop/include") obrigatório, referentes ao MTOM. Exemplo ao configurar o campo File Name/File ID com o valor "myImage.png":
{% endhint %}

XML original:

```
<soapenv:Envelope>
   <soapenv:Header/>
   <soapenv:Body>
        ...
        <file>iVBORw0KGgoAAAAN... (Base64 content)</file>
        ...
   </soapenv:Body>
</soapenv:Envelope>

```

XML ativando MTOM:

```
<soapenv:Envelope>
   <soapenv:Header/>
   <soapenv:Body>
        ...
        <file><inc:Include href="cid:myImage.png" xmlns:inc="http://www.w3.org/2004/08/xop/include"/></file>
        ...
   </soapenv:Body>
</soapenv:Envelope>

```

### A opção WS-Security é desativada caso a opção _Send the Request Body_ from a _File_ for ativada.

* **WS-Security:** configura a camada de segurança da requisição utilizando a tecnologia WS-Security.&#x20;
* **Type**: tipo de propriedade a ser inserida na camada de segurança no XML da requisição. Atualmente o conector suporta apenas os tipos Timestamp e UsernameToken.&#x20;
* **Time to live:** tempo em segundos a ser utilizado para gerar a data de criação e expiração (Type Timestamp).&#x20;
* **Millisecond precision:** define se a data de criação e expiração devem incluir precisão em milissegundos (Type Timestamp).
* **Username:** nome de usuário da conta a ser utilizada (Type UsernameToken).&#x20;
* **Password:** senha da conta a ser utilizada (Type UsernameToken).&#x20;
* **Password Type:** tipo de senha a ser utilizada (Type UsernameToken).&#x20;
* **Add Nonce:** se ativa, inclui um Nonce (Type UsernameToken).&#x20;
* **Add Created:** se ativa, inclui a data de criação (Type UsernameToken).
* **Connection Timeout:** tempo de expiração da conexão (em milissegundos).
* **Reading Timeout:** tempo máximo para leitura (em milissegundos).
* **Stop On Client Error:** se ativada, a opção vai gerar um erro para suspender a execução do pipeline.
* **Stop On Server Error:** se ativada, a opção vai gerar um erro para suspender a execução do pipeline.
* **All Values As String:** se ativada, a opção vai retornar todos os valores dentro das propriedades XML em string.
* **Is Multipart Response:** se ativada, será esperada uma resposta _Multipart_ da chamada, e será exibida uma lista contendo cada _Part_ retornada.
* **With Spacename:** se ativada, a opção mantém os spacenames no retorno do XML.
* **Advanced Settings:** configurações avançadas.
* **Allow Insecure Calls To HTTPS Endpoints:** quando ativada, a opção permite que chamadas não seguras a endpoints HTTPS sejam feitas.
* **Raw Mode:** se ativada, a opção recebe ou passa um payload sem ser JSON.
* **Save As Local File:** quando ativada, a opção salva o retorno como um arquivo no diretório local do pipeline. O arquivo será salvo apenas quando houver sucesso na chamada SOAP, ou seja, quando o http status code da resposta estiver entre 200 e 399.
* **Response File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt) onde será salva a resposta da chamada SOAP. Double Braces são suportados.
* **Enable Retries:** quanto ativada, a opção permite que sejam feitas novas tentativas.
* **Maximum Number Of Retries Before Giving Up:** número máximo de tentativas antes de desistir da chamada.
* **Time To Wait Before Each Retry:** tempo máximo entre tentativas (em milissegundos).
* **Override Response Charset:** quando ativada, a opção irá sobrescrever o charset retornado do endpoint para o charset especificado na propriedade Response Charset. Quando desabilitada ela respeitará o retorno do charset no header Content-Type. Caso não retorne nenhum charset no content type o padrão utilizado será UTF-8.
* **Response Charset:** utilizado somente quando a opção Override Response Charset estiver ativa e forçará o uso do charset especificado nesta propriedade. Padrão: UTF-8.

### Sobre o template variável&#x20;

O nome da variável também pode conter sinal de menos (-), ponto (.) e dois pontos (:) em qualquer posição, desde que eles sejam acompanhados de uma barra invertida () logo antes. Do contrário, os sinais podem ser interpretados como operadores.

#### Sobre substituição de números&#x20;

```
<#assign x=42>

  ${x}

  ${x?string}  <#-- the same as ${x} -->

  ${x?string.number}

  ${x?string.currency}

  ${x?string.percent}

  ${x?string.computer}

```



#### Resultado&#x20;

```
 42

  42

  42

  $42.00

  4,200%

  42

```



#### Formato de número&#x20;

```
<#setting number_format="0.####">
```

#### Para verificar se o campo não é nulo:&#x20;

```
<#if varTest??>${varTest}</#if>
```
