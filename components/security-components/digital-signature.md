---
description: Conheça o componente e saiba como utilizá-lo.
---

# Digital Signature

O **Digital Signature** assina e verifica mensagens com base em chaves públicas e privadas.\


Dê uma olhada nos parâmetros de configuração do componente:

* **Account**: use este parâmetro para definir a conta a ser usada pelo conector.
* **Operation:** tipos de operação do componente (Sign Fields, Sign Payload ou Verify).
* **Charset:** nome da codificação que faz a leitura do valor.
* **Hash Algorithm:** algoritmo a ser utilizado para assinar/verificar os dados (ex.: SHA256WithRSA).
* **Public Key Algorithm:** tipo do algoritmo de chave pública (ex.: RSA). Este campo fica disponível apenas quando _Verify_ estiver selecionado no parâmetro **Operation**.
* **Hash:** base do tipo base64 ou hex a ser verificada em relação ao _payload_. Este campo fica disponível apenas quando _Verify_ estiver selecionado no parâmetro **Operation**.
* **Sign Fields:** campos a serem assinados/verificados (devem ser separados por vírgula). Este campo fica disponível apenas quando _Sign Fields_ estiver selecionado no parâmetro **Operation**.
* **Hash in Hexadecimal:** se a opção estiver ativada, o valor a ser verificado ou assinado deve ser fornecido no formato hex; do contrário, será assinada ou verificada como base64.
* **Payload**: definido através de um valor único ou _Double Braces_. Este campo fica disponível apenas quando _Sign Payload_ ou _Verify_ estiverem selecionados no parâmetro **Operation**.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".

{% hint style="info" %}
**IMPORTANTE:** para assinar, você precisa configurar uma _account_ PRIVATE\_KEY ou enviar a propriedade da chave via _body_. Para verificar, você precisa configurar uma _account_ PUBLIC\_KEY ou enviar a propriedade da chave via _body_.
{% endhint %}

## Digital Signature em Ação <a href="#digital-signature-em-ao" id="digital-signature-em-ao"></a>

### Operação Sign Fields <a href="#operao-sign-fields" id="operao-sign-fields"></a>

1\. Na sua paleta de componentes, selecione o **Digital Signature**.

2\. Abra as configurações do componente.

3\. No campo **Operation**, selecione _Sign Fields_.

4\. Insira as seguintes especificações nos campos indicados:

* **Sign Fields:** parameter
* **Hash Algorithm:** SHA256WithRSA

5\. Mantenha as opções **Hash in Hexadecimal** e **Fail On Error** ativadas.

6\. Clique em Confirmar.

7\. Faça o _deploy_ do _pipeline_.

8\. O _pipeline_ vai receber um _payload_ como este:

```
{"parameter": "Test for encryption"}
```

9\. O resultado do teste executado vai aparecer conforme demonstrado abaixo:

```
{
"parameter": "....032281762E01B6C50C1DE825A2FD5A177CCFD5C1DB54E88ADD188A0B80311E672EDE5F8B......"
}
```

### Operação Sign Payload <a href="#operao-sign-payload" id="operao-sign-payload"></a>

1\. Na sua paleta de componentes, selecione o **Digital Signature**.

2\. Abra as configurações do componente.

3\. No campo **Operation**, selecione _Sign Payload_.

4\. Insira as seguintes especificações nos campos indicados:

* **Payload:** \[{ \\"result\\": \\"\{{ message.$.parameter \}}\\"}]
* **Hash Algorithm:** SHA256WithRSA

5\. Mantenha as opções **Hash in Hexadecimal** e **Fail On Error** ativadas.

6\. Clique em Confirmar.

7\. Faça o _deploy_ do _pipeline_.

8\. O resultado do teste executado vai aparecer conforme demonstrado abaixo:

```
{
"result": "....032281762E01B6C50C1DE825A2FD5A177CCFD5C1DB54E88ADD188A0B80311E672EDE5F8B......"
}
```

### Operação Verify <a href="#operao-verify" id="operao-verify"></a>

1\. Na sua paleta de componentes, selecione o **Digital Signature**.

2\. Abra as configurações do componente.

3\. No campo **Operation**, selecione _Verify_.

4\. Insira as seguintes especificações nos campos indicados:

* **Sign Fields:** \{{ message.$.signed \}}
* **Parameter:** \{{ message.$.rawData \}}
* **Hash Algorithm:** SHA256WithRSA
* **Public Key Algorithm:** RSA

5\. Mantenha as opções **Hash in Hexadecimal** e **Fail On Error** ativadas.

6\. Clique em Confirmar.

7\. Faça o _deploy_ do _pipeline_.

8\. O _pipeline_ vai receber um _payload_ como este:

```
{
"rawData": "Test for encryption",
"signed": "...032281762E01B6C50C1DE825A2FD5A177CCFD5C1DB54E...."
}
```

\
9\. O resultado do teste executado vai aparecer conforme demonstrado abaixo:

```
{
"success": true
}
```
