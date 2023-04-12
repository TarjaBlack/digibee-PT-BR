---
description: Conheça o componente e saiba como utilizá-lo.
---

# CMS

O **CMS** assina e verifica mensagens com base em uma cadeia de certificados.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account**: use este parâmetro para definir a conta a ser usada pelo conector.
* **Operation:** tipos de operação do conector (_Sign Fields, Sign Payload_ ou _Verify_).
* **Charset:** nome do código de caracteres para a leitura do arquivo (padrão UTF-8).
* **Hash Algorithm:** algoritmo a ser utilizado para assinar/verificar os dados (ex.: SHA256WithRSA). Este campo fica disponível apenas quando _Sign Fields_ ou _Sign Payload_ estiverem selecionados no parâmetro **Operation**.
* **Original:** mensagem original que foi assinada para verificação. Este campo fica disponível apenas quando _Verify_ estiver selecionado no parâmetro **Operation**.
* **Signed:** base do tipo base64 ou hex a ser verificada em relação ao _payload_. Este campo fica disponível apenas quando _Verify_ estiver selecionado no parâmetro **Operation**.
* **Sign Fields:** campos a serem assinados/verificados (devem ser separados por vírgula). Este campo fica disponível apenas quando _Sign Fields_ estiver selecionado no parâmetro **Operation**.
* **Payload:** definido através de um valor único ou _Double Braces._ Este campo fica disponível apenas quando _Sign Payload_ estiver selecionado no parâmetro **Operation**.
* **Hash in Hexadecimal:** se a opção estiver ativada, o valor a ser verificado ou assinado deve ser fornecido no formato hex; do contrário, será assinada ou verificada como base64.
* **Encapsulated**: se a opção estiver ativada, o conteúdo deve ser encapsulado na assinatura; caso contrário, o conteúdo não será encapsulado.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".

{% hint style="info" %}
**IMPORTANTE:** para assinar e verificar, você precisa configurar uma _account_ CERTIFICATE\_CHAIN.
{% endhint %}

## CMS em Ação <a href="#cms-em-ao" id="cms-em-ao"></a>

### Operação Sign Fields <a href="#operao-sign-fields" id="operao-sign-fields"></a>

#### **Entrada**

```
{
"parameter": "TEXT TO BE SignED"
}
```

#### **Saída**

```
{
"parameter": "AA01FF" // text Signed
}
```

### Operação Sign Payload <a href="#operao-sign-payload" id="operao-sign-payload"></a>

#### **Entrada**

```
{
"parameter": "TEXT TO BE SignED"
}
```

#### **Saída**

```
{
"result": "AA01FF" // text Signed
}
```

#### **Resposta de requisição contendo erro**

```
{
"error": "java.io.FileNotFoundException: data1.csv (No such file or directory)",
"message": "Encountered an I/O error while executing ZipFileConnector",
"success": false
}
```
