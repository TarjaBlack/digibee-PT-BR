---
description: Conheça o componente e saiba como utilizá-lo
---

# XML Schema Validator (NEW)

O _**XML Schema Validator**_ valida um arquivo XML contra um ou múltiplos arquivos XSD.

Dê uma olhada nos parâmetros de configuração do componente:

* **XML File Name:** nome do arquivo XML que será validado
* **XSDs**: uma lista de arquivos XSDs que serão usados para validar o arquivo XML. O arquivo XSD raiz de validação deverá ser informado como primeiro arquivo, e os demais XSDs em sequência. O nome dos arquivos informados deve ser o mesmo dos especificados dentro das importações dentro dos arquivos XSD.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso artigo clicando [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

{% hint style="info" %}
**IMPORTANTE:** Este componente não permite qualquer DTD declarada no conteúdo XML. Veja no exemplo abaixo:
{% endhint %}

**Exemplo:**

{% code overflow="wrap" %}
```
"<?xml version=\"1.0\" encoding=\"UTF-8\"?><!DOCTYPE foo [ <!ENTITY xxe SYSTEM \"file:///etc/passwd\"> ]><stockCheck><productId>&xxe;</productId></stockCheck>"
```
{% endcode %}

#### **Fluxo de mensagens** <a href="#h_6393de0970" id="h_6393de0970"></a>

* #### **Entrada** <a href="#h_a16192b0f3" id="h_a16192b0f3"></a>

Não é esperado uma mensagem de entrada específica, bastando apenas preencher os campos necessários de cada operação.

* #### **Saída** <a href="#h_843055361c" id="h_843055361c"></a>

```
{
    "success": true,
    "valid": true,
    "errors": [
    {
        "lineNumber": 10,
        "columnNumber": 2,
        "message": "Invalid type",
        "publicId": null
    }]
}
```

\
