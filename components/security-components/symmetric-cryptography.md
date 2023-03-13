---
description: Conheça o componente e saiba como utilizá-lo.
---

# Symmetric Cryptography

O **Symmetric Cryptography** criptografa e descriptografa com base em criptografia simétrica.

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis - _ENCRYPT_ e _DECRYPT_.
* **Account:** conta que será utilizada pelo componente. É esperada uma conta _PRIVATE-KEY_. O tamanho configurado no parâmetro **Algorithm Key Size** deve corresponder ao tamanho do algoritmo _PRIVATE-KEY_. Do contrário, uma mensagem de erro será retornada.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Algorithm:** algoritmo a ser utilizado para criptografar/descriptografar dados.
* **Algorithm Key Size:** tamanho da chave do algoritmo. Como citado anteriormente, o tamanho configurado neste parâmetro deve corresponder ao tamanho do algoritmo _PRIVATE-KEY._
* **Operation Mode:** modo de operação a ser utilizado.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_).
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"._
* **Advanced Settings:** configurações avançadas.
* **Use IV:** essa opção é válida somente para a operação _ENCRYPT_. Se selecionada, a opção determina o IV (vetor de inicialização) para o modo CBC.
* **Use Your Own Key:** se selecionada, a opção utilizará a sua própria chave gerada para criptografar e descriptografar dados.
* **Encryption Key As Hex Value:** se selecionada, a opção espera/produz uma Encryption Key as Hex; do contrário, será esperada/produzida como base64.
* **Concatenate IV:** uma mensagem encriptada é esperada/produzida com o Concatenate IV (IV+MESSAGE); do contrário, um parâmetro IV será produzido durante a encriptação e IV em IV será esperado no campo _"Decryption"_.
* **IV as Hex Value:** esta opção não é disponível se **Concatenate IV** estiver habilitado. Se for selecionada, a opção espera/produz um parâmetro IV em formato Hex; do contrário, será esperada/produzida como base64.
* **Encrypted Message As Hex:** se selecionada, a opção espera/produz uma mensagem encriptada em formato Hex; do contrário, será esperada/produzida como base64.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **KEY por ACCOUNT - Operação ENCRYPT**

#### **Entrada**

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

#### **Payload**

```
{
    "data": someData,
    "data1": someData1
}

```

#### **Saída**

```
{
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```

#### **Entrada**

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

#### **Payload**

```
{
    "encryptionKey": "-- THE FOLLOWING PUBLIC KEY--",
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="    
}
```

#### **Saída**

```
{
    "ivParameterSpec": "RXZlbiBpZiBwZXJmZWN0IGNy==",
    "data": someData,
    "data1": someData1
}
```

### **KEY por REQUEST BODY - Operação ENCRYPT**

#### **Entrada**

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

#### **Payload**

```
{
    "encryptionKey": "-- THE FOLLOWING PUBLIC KEY--"
    "data": someData,
    "data1": someData1
}
```

#### **Saída**

```
{
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```

#### **Entrada**

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

#### **Payload**

```
{
    "ivParameterSpec": "RXZlbiBpZiBwZXJmZWN0IGNy==",
    "encryptionKey": "-- THE FOLLOWING PRIVATE KEY--"
    "data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
    "data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="    
}
```
