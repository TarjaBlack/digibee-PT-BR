---
description: Conheça o componente e saiba como utilizá-lo.
---

# SOAP V3 (BETA)

O SOAP V3 invoca endpoints SOAP de um pipeline. O componente utiliza _templates_ Apache FreeMaker para gerar a mensagem de chamada que converte o retorno de SOAP para JSON, tentando ao máximo não corromper a conversão. Expressões em _Double Braces_ são suportadas.

Dê uma olhada nos parâmetros de configuração do componente:

* **URL:** URL a ser chamada - pode conter os parâmetros seguindo o padrão `{:param1}`, que serão substituídos pela propriedade correspondente da mensagem de entrada.
* **Account:** conta a ser utilizada pelo componente. Leia a documentação sobre [Contas (Accounts)](https://docs.digibee.com/documentation/v/pt-br/configurations/contas-accounts) para saber mais sobre os tipos de contas disponíveis.
* **Custom Account #1:** conta adicional a ser utilizada pelo componente por meio de _Double Braces_ `{{ account.custom-1.value }}`. Leia o artigo [Funções Double Braces](../../build/double-braces/funcoes-double-braces/#de-data) para saber mas sobre o tema.&#x20;
* **Custom Account #2:** conta adicional a ser utilizada pelo componente por meio de _Double Braces_ `{{ account.custom-2.value }}`. Leia o artigo [Funções Double Braces](../../build/double-braces/funcoes-double-braces/#de-data) para saber mas sobre o tema.
* **Send the Request Body from a File:** se habilitada, a opção considera o conteúdo a ser enviado na chamada através de um arquivo; do contrário, será considerado o que for especificado em **Template (XML).**
* **Request Body File Name:** informa o nome do arquivo a ser enviado na chamada SOAP, se a opção **Send the Request Body from a File** estiver ativada.
* **Template (XML):** _template_ Apache FreeMarker para que a mensagem SOAP seja enviada na solicitação. Este campo não estará disponível se a opção **Send the Request Body from a File** estiver habilitada.
* **Headers:** _headers_ da chamada.
* **Query Params:** _query parameters_ da chamada.
* ​​**Attachments (MTOM):** adiciona ou remove opções para configurar arquivos ou conteúdos binários a serem enviados na requisição utilizando a tecnologia _MTOM_. Este parâmetro não estará disponível se a opção **Send the Request Body from a File** estiver habilitada.
* **Is Binary:** se ativada, o conector deverá receber o conteúdo binário e o ID do arquivo a ser enviado na requisição, do contrário, deve ser informado o nome do arquivo. Disponível apenas quando o parâmetro **Attachments (MTOM)** estiver adicionado.
* **File Name:** quando a opção **Is Binary** estiver desativada, este campo informa o nome do arquivo a ser enviado junto do XML configurado em **Template (XML)**. Disponível apenas quando o parâmetro **Attachments (MTOM)** estiver adicionado.
* **File ID:** quando a opção **Is Binary** estiver ativada, este campo informa o ID do arquivo a ser enviado junto do XML configurado em **Template (XML)**. Disponível apenas quando o parâmetro **Attachments (MTOM)** estiver adicionado.
* **Base64 Content:** quando a opção **Is Binary** estiver ativada, este campo informa o conteúdo em Base64 a ser enviado junto do XML configurado em **Template (XML)**. Disponível apenas quando o parâmetro **Attachments (MTOM)** estiver adicionado.
* **WS-Security:** configura a camada de segurança da requisição utilizando a tecnologia WS-Security. Este parâmetro não estará disponível caso a opção **Send the Request Body from a File** esteja ativada.
* **Type**: tipo de propriedade a ser inserida na camada de segurança no XML da requisição. Atualmente o conector suporta apenas os tipos _Timestamp_ e _UsernameToken_. Disponível apenas quando o parâmetro **WS-Security** estiver adicionado.
* **Time to live:** tempo em segundos a ser utilizado para gerar a data de criação e expiração. Disponível apenas se _Timestamp_ estiver selecionado em **Type**.&#x20;
* **Millisecond precision:** define se a data de criação e expiração devem incluir precisão em milissegundos. Disponível apenas se _Timestamp_ estiver selecionado em **Type**.
* **Username:** nome de usuário da conta a ser utilizada. Disponível apenas se _UsernameToken_ estiver selecionado em **Type**.&#x20;
* **Password:** senha da conta a ser utilizada. Disponível apenas se _UsernameToken_ estiver selecionado em **Type**.
* **Password Type:** tipo de senha a ser utilizada. Disponível apenas se _UsernameToken_ estiver selecionado em **Type**.
* **Add Nonce:** se ativa, inclui um Nonce. Disponível apenas se _UsernameToken_ estiver selecionado em **Type**.
* **Add Created:** se ativa, inclui a data de criação. Disponível apenas se _UsernameToken_ estiver selecionado em **Type**.

{% hint style="info" %}
**IMPORTANTE**: os parâmetros **Username** e **Password** devem ser configurados usando os campos **Custom Account #1** ou **Custom Account #2** (conta tipo _BASIC_).
{% endhint %}

* **Connection Timeout:** tempo de expiração da conexão (em milissegundos).
* **Reading Timeout:** tempo máximo para leitura (em milissegundos).
* **Stop On Client Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **Stop On Server Error:** se ativada, a opção vai gerar um erro para suspender a execução do _pipeline_.
* **All Values As String:** se ativada, a opção vai retornar todos os valores dentro das propriedades XML em _string_.
* **Is Multipart Response:** se ativada, será esperada uma resposta _Multipart_ da chamada, e será exibida uma lista contendo cada _Part_ retornada.
* **With Namespace:** se ativada, a opção mantém os _namespaces_ no retorno do XML.
* **Override Response Charset:** quando ativada, a opção irá sobrescrever o _charset_ retornado do _endpoint_ para o _charset_ especificado em **Response Charset**. Quando desabilitada, ela respeitará o retorno do _charset_ no campo _Content-Type_ (dentro do parâmetro **Headers**). Caso não retorne nenhum _charset_ no _Content-Type_, o padrão utilizado será UTF-8.
* **Response Charset:** determina o uso do _charset_ especificado neste campo. Disponível somente quando a opção **Override Response Charset** estiver ativa. Padrão: UTF-8.
* **Advanced Settings:** se ativada, os seguintes parâmetros estarão disponíveis:
* **Allow Insecure:** quando ativada, a opção permite que chamadas não seguras a _endpoints_ HTTPS sejam feitas.
* **Raw Mode:** se ativada, a opção recebe ou passa um _payload_ sem ser JSON.
* **Save As Local File:** quando ativada, a opção salva o retorno como um arquivo no diretório local do _pipeline_. O arquivo será salvo apenas quando houver sucesso na chamada SOAP, ou seja, quando o _http status code_ da resposta estiver entre 200 e 399.
* **Response File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt) onde será salva a resposta da chamada SOAP. _Double Braces_ são suportados. Este campo é mostrado apenas se **Save As Local File** estiver ativado.
* **Enable Retries:** quanto ativada, a opção permite que sejam feitas novas tentativas.
* **Maximum Number Of Retries Before Giving Up:** número máximo de tentativas antes de desistir da chamada. Este campo é mostrado apenas se **Enable Retries** estiver ativado.
* **Time To Wait Before Each Retry:** tempo máximo entre tentativas (em milissegundos). Este campo é mostrado apenas se **Enable Retries** estiver ativado.

## Usando a tecnologia _MTOM_

para utilizar a tecnologia _MTOM_, é necessário que o arquivo ou conteúdo em Base64 seja referenciado diretamente no XML da requisição, sendo substituído pelo valor configurado em **File Name** ou **File ID**, dentro da tag padrão `<inc:Include>` junto do _namespace_ obrigatório `xmlns:inc="http://www.w3.org/2004/08/xop/include"` , referentes ao _MTOM_.&#x20;

Lembre-se que **File Name** e **File ID** ficam disponíveis apenas quando **Is Binary** estiver ativado em **Attachments (MTOM).**&#x20;

Exemplo ao configurar o campo **File Name/File ID** com o valor "`myImage.png"`:

**XML original:**

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

**XML ativando MTOM:**

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

## Sobre o _template_ variável&#x20;

O nome da variável também pode conter sinal de menos `(-)`, ponto `(.)` e dois pontos `(:)` em qualquer posição, desde que eles sejam acompanhados de uma barra invertida `(\)` logo antes. Do contrário, os sinais podem ser interpretados como operadores.

## Sobre substituição de números&#x20;

```
<#assign x=42>

  ${x}

  ${x?string}  <#-- the same as ${x} -->

  ${x?string.number}

  ${x?string.currency}

  ${x?string.percent}

  ${x?string.computer}

```

### Resultado&#x20;

```
 42

  42

  42

  $42.00

  4,200%

  42

```



### Formato de número&#x20;

```
<#setting number_format="0.####">
```

Para verificar se o campo não é nulo:&#x20;

```
<#if varTest??>${varTest}</#if>
```
