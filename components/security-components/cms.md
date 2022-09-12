---
description: Conheça o componente e saiba como utilizá-lo.
---

# CMS

O **CMS** assina e verifica mensagens com base em uma cadeia de certificados.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account**: use este parâmetro para definir a conta a ser usada pelo conector.
* **Operation:** tipos de operação do conector (Sign Fields, Sign Payload ou Verify).
* **Charset:** nome do código de caracteres para a leitura do arquivo (padrão UTF-8).
* **Hash Algorithm:** algoritmo a ser utilizado para assinar/verificar os dados (ex.: SHA256WithRSA).
* **Signed:** base do tipo base64 ou hex a ser verificada em relação ao _payload_.
* **Original:** mensagem original que foi assinada para verificação.
* **Hash in Hexadecimal:** se a opção estiver ativada, o valor a ser verificado ou assinado deve ser fornecido no formato hex; do contrário, será assinada ou verificada como base64.
* **Sign Fields:** campos a serem assinados/verificados (devem ser separados por vírgula).
* **Payload:** definido através de um valor único ou _Double Braces_ - disponível apenas para as operações SIGN PAYLOAD e VERIFY.
* **Encapsulated**: se "true" o conteúdo deve ser encapsulado na assinatura, false caso contrário.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

{% hint style="info" %}
**IMPORTANTE:** para assinar e verificar, você precisa configurar uma _account_ CERTIFICATE\_CHAIN.
{% endhint %}

## CMS em Ação <a href="#cms-em-ao" id="cms-em-ao"></a>

### Operação SIGN FIELDS <a href="#operao-sign-fields" id="operao-sign-fields"></a>

### &#x20;<a href="#h_d7cb2a0800" id="h_d7cb2a0800"></a>

**Entrada**

```
{
"parameter": "TEXT TO BE SignED"
}
```

**Saída**

```
{
"parameter": "AA01FF" // text Signed
}
```

### Operação SIGN PAYLOAD <a href="#operao-sign-payload" id="operao-sign-payload"></a>

**Entrada**

```
{
"parameter": "TEXT TO BE SignED"
}
```

**Saída**

```
{
"result": "AA01FF" // text Signed
}
```

**Resposta de requisição contendo erro**

```
{
"error": "java.io.FileNotFoundException: data1.csv (No such file or directory)",
"message": "Encountered an I/O error while executing ZipFileConnector",
"success": false
}
```
