---
description: Conheça o componente e saiba como utilizá-lo.
---

# AES Cryptography

O **AES Cryptography** criptografa ou descriptografa com base em criptografia simétrica.

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis - ENCRYPT FIELDS, DECRYPT FIELDS, ENCRYPT PAYLOAD e DECRYPT PAYLOAD.
* **Account:** conta a ser utilizada pelo componente - é esperada uma conta _SECRET-KEY type_ (se você quiser utilizar uma chave arbitrária, então desfaça a seleção da conta e habilite a opção "Provide Key" nas configurações avançadas).
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Algorithm Key Size:** tamanho da chave do algoritmo, disponível em 256 bits,192 bits e 128 bits. Para o tamanho de chave:

\- 256 bits, é necessário utilizar uma chave de 32 bytes;

\- 192 bits, é necessário utilizar uma chave de 24 bytes;

\- 128 bits, é necessário utilizar uma chave de 16 bytes.

* **Operation Mode:** modo de operação a ser utilizado.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_). “NoPadding” é utilizado somente quando a mensagem a ser criptografada com certeza não necessita de _padding_. O correto é sempre usar _padding_ para evitar erros na hora de criptografar/descriptografar.
* **Charset:** _charset_ da chave passada do _string type_.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Advanced Settings:** configurações avançadas.
* **Concatenate IV:** uma mensagem encriptada é esperada/produzida com o Concatenate IV (IV+MESSAGE); do contrário, um parâmetro IV será produzido durante a encriptação e IV em IV será esperado no campo "Decryption".
* **Provide IV For Encryption:** se a opção estiver ativada, será esperado um IV como parâmetro para a encriptação; do contrário, será gerado um parâmetro com zeros ou um parâmetro aleatório controlado pelo parâmetro Empty IV.
* **IV as Hex:** se a opção estiver ativada, será esperado um IV como hexadecimal; do contrário, espera-se base64.
* **IV:** vetor de inicialização a ser informado previamente para a realização de criptografia/descriptografia, que deve conter 16 bytes. Este parâmetro aceita _Double Braces_.
* **Update AAD:** additional authenticated data para a operação GCM. Se a opção estiver ativada, é possível informar o AAD para a operação GCM.
* **AAD:** additional authenticated data. Valor para a chave AAD na operação GCM.
* **Empty IV/Random IV:** se a opção estiver ativada, será gerado um IV vazio (16 bytes de zeros); do contrário, será gerado um IV aleatório.
* **Provide Key Or Generate Random:** se a opção estiver ativada, espera-se uma chave; do contrário, uma chave aleatória será gerada.
* **Secret Key:** chave em formato Hex ou base64 (controlada pelo parâmetro "Encryption Key As Hex Value") - a chave precisa ter o número de _bits_ de acordo com o parâmetro "Algorithm Key Size".
* **Encryption Key As Hex Value:** se a opção estiver ativada, a opção espera/produz uma Encryption Key as Hex; do contrário, será esperada/produzida como base64.
* **Encrypted Message As Hex:** se a opção estiver ativada, a opção espera/produz uma mensagem encriptada em formato Hex; do contrário, será esperada/produzida como base64.

**IMPORTANTE:** se você deseja utilizar a sua própria chave por conta, então será necessário configurar uma conta SECRET-KEY ou passar a respectiva propriedade através de _Double Braces_ com a chave.

## Fluxo de mensagens <a href="#h_c025db075e" id="h_c025db075e"></a>

### Entrada <a href="#h_b87248fe72" id="h_b87248fe72"></a>

Não se espera um formato específico de entrada.

### Saída <a href="#h_bde3904b70" id="h_bde3904b70"></a>

* **Crypto Operation: ENCRYPT FIELDS ou DECRYPT FIELDS**

Será mantida a mesma estrutura de entrada na saída. Caso a opção "Concatenate IV" esteja desabilitada, será gerada uma nova propriedade "IV" no JSON informado para cada campo configurado.

Exemplo:

**Entrada**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

**Concatenate IV** desabilitado:

```
{
"array": [
{"text": "ENCRYPTED TEXT", "iv": "SOME BASE64"},
{"text": "ENCRYPTED TEXT", "iv": "SOME BASE64"}
]
}
```

**Concatenate IV** habilitado:

```
{
"array": [
{"text": "ENCRYPTED TEXT"},
{"text": "ENCRYPTED TEXT"}
]
}
```

* **Crypto Operation: ENCRYPT PAYLOAD ou DECRYPT PAYLOAD**

O valor criptografado será retornado dentro da propriedade "result". Caso a opção "Concatenate IV" esteja desabilitada, será gerada uma nova propriedade "IV" no JSON informado para cada campo configurado.

**Concatenate IV** desabilitado:

```
{
"result": "ENCRYPTED TEXT",
"iv": "SOME BASE64"
}
```

**Concatenate IV** habilitado:

```
{
"result": "ENCRYPTED TEXT
}
```

## AES Cryptography em Ação <a href="#h_1e9cef2074" id="h_1e9cef2074"></a>

### **1. Criptografia ENCRYPT FIELDS** <a href="#h_4171128069" id="h_4171128069"></a>

**Crypto operation:** ENCRYPT FIELDS

**Fields To Encrypt/Decrypt:** array.text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** habilitado

**Concatenate IV:** habilitado

**Provide IV for encryption:** habilitado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** habilitado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É aconselhável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desabilitado

**Encrypted Message As Hex:** desabilitado

**Entrada**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

**Saída**

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

### 2. Criptografia ENCRYPT PAYLOAD <a href="#h_a409939f67" id="h_a409939f67"></a>

**Crypto operation:** ENCRYPT PAYLOAD

**Payload:** text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** habilitado

**Concatenate IV:** habilitado

**Provide IV for encryption:** habilitado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** habilitado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É aconselhável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desabilitado

**Encrypted Message As Hex:** desabilitado

**Entrada**

```
{}
```

**Saída**

```
{
"result": "MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU="
}
```

### 3. Descriptografar DECRYPT FIELDS <a href="#h_130432a1a0" id="h_130432a1a0"></a>

**Crypto operation:** DECRYPT FIELDS

**Fields To Encrypt/Decrypt:** array.text

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** habilitado

**Concatenate IV:** habilitado

**Provide IV for encryption:** habilitado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** habilitado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É aconselhável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desabilitado

**Encrypted Message As Hex:** desabilitado

**Entrada**

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

**Saída**

```
{
"array": [
{"text": "text"},
{"text": "text2"}
]
}
```

### 4. Descriptografar DECRYPT PAYLOAD <a href="#h_1f737c3cb4" id="h_1f737c3cb4"></a>

**Crypto operation:** DECRYPT PAYLOAD

**Payload:** MTIzNDU2Nzg5MDEyMzQ1Npp1dUf7FzjkLwD9Ezq4FSU=

**Algorithm key Size:** 256

**Operation Mode:** CBC

**Padding:** PKCS5Padding

**Advanced Settings:** habilitado

**Concatenate IV:** habilitado

**Provide IV for encryption:** habilitado

**IV:** MTIzNDU2Nzg5MDEyMzQ1NjE=

**Provide Key Or Generate Random:** habilitado

**Secret Key:** MTIzNDU2Nzg5MDEyMzQ1NjEyMzQ1Njc4OTAxMjM0NTY=

(É aconselhável armazenar essa chave em uma conta do tipo SECRET-KEY)

**Encryption Key As Hex Value:** desabilitado

**Encrypted Message As Hex:** desabilitado

**Entrada**

```
{}
```

**Saída**

```
{"result": "text"}
```
