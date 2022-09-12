---
description: Conheça o componente e saiba como utilizá-lo.
---

# Symmetric Cryptography

O **Symmetric Cryptography** criptografa e descriptografa com base em criptografia simétrica.

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis - ENCRYPT e DECRYPT.
* **Account:** conta a ser utilizada pelo componente.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Algorithm:** algoritmo a ser utilizado para criptografar/descriptografar dados.
* **Algorithm Key Size:** tamanho da chave do algoritmo.
* **Operation Mode:** modo de operação a ser utilizado.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Advanced Settings:** configurações avançadas.
* **Use IV:** se selecionada, a opção determina o IV (vetor de inicialização) para o modo CBC.
* **Use Your Own Key:** se selecionada, a opção utilizará a sua própria chave gerada para criptografar e descriptografar dados.
* **Encryption Key As Hex Value:** se selecionada, a opção espera/produz uma Encryption Key as Hex; do contrário, será esperada/produzida como base64.
* **Concatenate IV:** uma mensagem encriptada é esperada/produzida com o Concatenate IV (IV+MESSAGE); do contrário, um parâmetro IV será produzido durante a encriptação e IV em IV será esperado no campo "Decryption".
* **Encrypted Message As Hex:** se selecionada, a opção espera/produz uma mensagem encriptada em formato Hex; do contrário, será esperada/produzida como base64.

**IMPORTANTE:** se você deseja utilizar a sua própria chave por conta, então será necessário configurar uma conta SECRET-KEY ou passar a respectiva propriedade. Você pode especificá-la por uma solicitação, conforme o modelo abaixo:

```
{    "encryptionKey": "-- THE FOLLOWING KEY--"}
```

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

* **KEY por ACCOUNT**

### Operação ENCRYPT <a href="#operao-encrypt" id="operao-encrypt"></a>

**Entrada**

```
{
    "operation": "encrypt",
    "useOwnKey": true,
    "useIV": true,
    "algorithm": "AES",
    "operationMode": "CBC",
    "padding": "PKCS5Padding",
    "failOnError": true,
    "encryptedMessageAsHex": false,
    "iVAsHex": false,
    "encryptedFields": "data,data1"
}
```

**Payload**

```
{
    "data": someData,
    "data1": someData1
}

```

**Saída**

```
{
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```

**Entrada**

```
{
    "operation": "encrypt",
    "useOwnKey": true,
    "useIV": true,
    "algorithm": "AES",
    "operationMode": "CBC",
    "padding": "PKCS5Padding",
    "failOnError": true,
    "encryptedMessageAsHex": false,
    "iVAsHex": false,
    "encryptedFields": "data,data1"    
}
```

**Payload**

```
{
    "encryptionKey": "-- THE FOLLOWING PUBLIC KEY--",
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="    
}
```

**Saída**

```
{
    "ivParameterSpec": "RXZlbiBpZiBwZXJmZWN0IGNy==",
    "data": someData,
    "data1": someData1
}
```

* **KEY por REQUEST BODY**

### Operação ENCRYPT <a href="#operao-encrypt" id="operao-encrypt"></a>

**Entrada**

```
{
    "operation": "encrypt",
    "useOwnKey": true,
    "useIV": true,
    "algorithm": "AES",
    "operationMode": "CBC",
    "padding": "PKCS5Padding",
    "failOnError": true,
    "encryptedMessageAsHex": false,
    "iVAsHex": false,
    "encryptedFields": "data,data1"    
}
```

**Payload**

```
{
    "encryptionKey": "-- THE FOLLOWING PUBLIC KEY--"
    "data": someData,
    "data1": someData1
}
```

**Saída**

```
{
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```

**Entrada**

```
{
    "operation": "decrypt",
    "useOwnKey": true,
    "useIV": true,
    "algorithm": "AES",
    "operationMode": "CBC",
    "padding": "PKCS5Padding",
    "failOnError": true,
    "encryptedMessageAsHex": false,
    "iVAsHex": false,
    "encryptedFields": "data,data1"    
}
```

**Payload**

```
{
    "ivParameterSpec": "RXZlbiBpZiBwZXJmZWN0IGNy==",
    "encryptionKey": "-- THE FOLLOWING PRIVATE KEY--"
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="    
}
```
