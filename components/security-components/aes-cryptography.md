---
description: Conheça o componente e saiba como utilizá-lo.
---

# AES Cryptography

O **AES Cryptography** criptografa ou descriptografa com base em criptografia simétrica.

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis (_Encrypt Fields, Decrypt Fields, Encrypt Payload_ e _Decrypt Payload_).
* **Account:** conta a ser utilizada pelo componente. É esperada uma conta _SECRET-KEY type._ Se você quiser utilizar uma chave arbitrária, então desfaça a seleção da conta e ative a opção **Provide Key Or Generate Random**, em **Advanced Settings**.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Algorithm Key Size:** tamanho da chave do algoritmo, disponível em 256 bits,192 bits e 128 bits.&#x20;

{% hint style="info" %}
Você deve usar as seguintes chaves dependendo de cada tamanho:

* 256 bits, é necessário utilizar uma chave de 32 bytes;
* 192 bits, é necessário utilizar uma chave de 24 bytes;
* 128 bits, é necessário utilizar uma chave de 16 bytes.
{% endhint %}

* **Operation Mode:** modo de operação a ser utilizado (CBC, OFB, CTR, CFB, GCM ou ECB).
* **GCM Tag Length:** define a _tag lenght_ (128 bits, 120 bits, 112 bits, 104 bits ou 96 bits). Este campo está disponível apenas quando GCM estiver selecionado no parâmetro **Operation Mode**.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_). A opção _NoPadding_ é utilizada somente quando a mensagem a ser criptografada com certeza não necessita de _padding_. O correto é sempre usar _padding_ para evitar erros na hora de criptografar/descriptografar.
* **Charset:** _charset_ da chave passada do _string type_.
* **Fail On Error:** se a opção estiver ativada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".
* **Advanced Settings:** se a opção estiver ativada, você pode acessar as seguintes configurações:
* **Concatenate IV:** uma mensagem encriptada é esperada/produzida com o Concatenate IV (IV+MESSAGE); do contrário, um parâmetro IV será produzido durante a encriptação e IV em IV será esperado no campo "_Decryption_".
* **Provide IV For Encryption:** se a opção estiver ativada, será esperado um IV como parâmetro para a encriptação; do contrário, será gerado um parâmetro com zeros ou um parâmetro aleatório controlado pelo parâmetro **Empty IV or Random IV?**.
* **Empty IV or Random IV?:** se a opção estiver ativada, será gerado um IV vazio (16 bytes de zeros); do contrário, será gerado um IV aleatório.
* **IV as Hex Value:** se a opção estiver ativada, será esperado um IV como hexadecimal; do contrário, espera-se base64. Este parâmetro não fica disponível quando **Concatenate IV** estiver ativado.
* **Update AAD:** _additional authenticated data_ para a operação GCM. Se a opção estiver ativada, é possível informar o AAD para a operação GCM. Esta opção está disponível apenas quando GCM estiver selecionado no parâmetro **Operation Mode**.
* **AAD:** _additional authenticated data_. Valor para a chave AAD na operação GCM. Esta opção está disponível apenas quando **Update AAD** estiver ativado e GCM estiver selecionado no parâmetro **Operation Mode**.
* **IV:** vetor de inicialização a ser informado previamente para a realização de criptografia/descriptografia, que deve conter 16 bytes. Este parâmetro fica disponível somente quando **Provide IV For Encryption** estiver ativado e aceita _Double Braces_.
* **Provide Key Or Generate Random:** se a opção estiver ativada, espera-se uma chave; do contrário, uma chave aleatória será gerada.
* **Secret Key:** chave em formato Hex ou base64 (controlada pelo parâmetro **Encryption Key As Hex Value**). A chave precisa ter o número de _bits_ de acordo com o parâmetro **Algorithm Key Size**.
* **Encryption Key As Hex Value:** se a opção estiver ativada, a opção espera/produz uma _Encryption Key_ em formato Hex; do contrário, será esperada/produzida como base64.
* **Encrypted Message As Hex:** se a opção estiver ativada, a opção espera/produz uma mensagem encriptada em formato Hex; do contrário, será esperada/produzida como base64.

{% hint style="info" %}
**IMPORTANTE:** se você deseja utilizar a sua própria chave por conta, então será necessário configurar uma conta SECRET-KEY ou passar a respectiva propriedade através de _Double Braces_ com a chave.
{% endhint %}

## Fluxo de mensagens <a href="#h_c025db075e" id="h_c025db075e"></a>

### Entrada <a href="#h_b87248fe72" id="h_b87248fe72"></a>

Não se espera um formato específico de entrada.

### Saída <a href="#h_bde3904b70" id="h_bde3904b70"></a>

### **Crypto Operation: Encrypt Fields ou Decrypt Fields**

Será mantida a mesma estrutura de entrada na saída. Caso a opção **Concatenate IV** esteja desativada, será gerada uma nova propriedade "IV" no JSON informado para cada campo configurado.

**Exemplo**

#### **Entrada**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

**Concatenate IV** desativado:

```
{
"array": [
{"text": "ENCRYPTED TEXT", "iv": "SOME BASE64"},
{"text": "ENCRYPTED TEXT", "iv": "SOME BASE64"}
]
}
```

**Concatenate IV** ativado:

```
{
"array": [
{"text": "ENCRYPTED TEXT"},
{"text": "ENCRYPTED TEXT"}
]
}
```

### **Crypto Operation: Encrypt Payload ou Decrypt Payload**

O valor criptografado será retornado dentro da propriedade "result". Caso a opção **Concatenate IV** esteja desativada, será gerada uma nova propriedade "IV" no JSON informado para cada campo configurado.

**Concatenate IV** desativado:

```
{
"result": "ENCRYPTED TEXT",
"iv": "SOME BASE64"
}
```

**Concatenate IV** ativado:

```
{
"result": "ENCRYPTED TEXT
}
```

## AES Cryptography em Ação <a href="#h_1e9cef2074" id="h_1e9cef2074"></a>

### **Criptografia Encrypt Fields** <a href="#h_4171128069" id="h_4171128069"></a>

**Crypto operation:** Encrypt Fields

**Fields To Encrypt/Decrypt:** array.text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** ativado

**Concatenate IV:** ativado

**Provide IV for encryption:** ativado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** ativado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É recomendável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desativado

**Encrypted Message As Hex:** desativado

#### **Entrada**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

#### **Saída**

```
{
"array": [
{
"text": "MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU="
},
{
"text": "MTIzNDU2Nzg5MDEyMzQ1NijQdN4bFfeBL9Z6vCfzMTw="
}
]
}
```

### Criptografia Encrypt Payload <a href="#h_a409939f67" id="h_a409939f67"></a>

**Crypto operation:** Encrypt Payload

**Payload:** text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** ativado

**Concatenate IV:** ativado

**Provide IV for encryption:** ativado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** ativado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É recomendável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desativado

**Encrypted Message As Hex:** desativado

#### **Entrada**

```
{}
```

#### **Saída**

```
{
"result": "MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU="
}
```

### Descriptografar Decrypt Fields <a href="#h_130432a1a0" id="h_130432a1a0"></a>

**Crypto operation:** Decrypt Fields

**Fields To Encrypt/Decrypt:** array.text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** ativado

**Concatenate IV:** ativado

**Provide IV for encryption:** ativado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** ativado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É recomendável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desativado

**Encrypted Message As Hex:** desativado

#### **Entrada**

```
{
"array": [
{
"text": "MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU="
},
{
"text": "MTIzNDU2Nzg5MDEyMzQ1NijQdN4bFfeBL9Z6vCfzMTw="
}
]
}
```

#### **Saída**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

### Descriptografar Decrypt Payload <a href="#h_1f737c3cb4" id="h_1f737c3cb4"></a>

**Crypto operation:** Decrypt Payload

**Payload:** MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU=

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** ativado

**Concatenate IV:** ativado

**Provide IV for encryption:** ativado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** ativado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É recomendável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desativado

**Encrypted Message As Hex:** desativado

#### **Entrada**

```
{}
```

#### **Saída**

```
{"result": "text"}
```
