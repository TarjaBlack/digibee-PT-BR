---
description: Conheça o componente e saiba como utilizá-lo.
---

# Asymmetric Cryptography

O **Asymmetric Cryptography** criptografa e descriptografa com base em _keys_ públicas e privadas.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Crypto Operation:** tipos de operação disponíveis - ENCRYPT e DECRYPT.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Algorithm:** algoritmo a ser utilizado para criptografar/descriptografar dados.
* **Operation Mode:** modo de operação a ser utilizado.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Para encriptar, você precisa configurar uma PUBLIC KEY _account_ ou passar a _property key_ via _body_ com a respectiva chave.

Para descriptar, você precisa configurar uma PRIVATE KEY _account_ ou passar a _property key_ via _body_ com a respectiva chave.

Se a _key_ não foi configurada na _account_, você precisa especificar na solicitação conforme o modelo abaixo:

```
{"encryptionKey": "-- THE FOLLOWING PUBLIC KEY--"}
```

## Asymmetric Cryptography em Ação <a href="#asymmetric-cryptography-em-ao" id="asymmetric-cryptography-em-ao"></a>

### KEY por ACCOUNT <a href="#key-por-account" id="key-por-account"></a>

**Config**

```
{
"operation": "encrypt",
"algorithm": "RSA",
"operationMode": "ECB",
"padding": "OAEPWithSHA1AndMGF1Padding",
"encryptedFields": "data,data1",
"failOnError": true
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

**Config**

```
{
"operation": "decrypt",
"algorithm": "RSA",
"operationMode": "ECB",
"padding": "OAEPWithSHA1AndMGF1Padding",
"encryptedFields": "data,data1",
"failOnError": true
}
```

**Payload**

```
{
"data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
"data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```

**Saída**

```
{
"data": someData,
"data1": someData1
}
```

### KEY por REQUEST BODY <a href="#key-por-request-body" id="key-por-request-body"></a>

**Config**

```
{
"operation": "encrypt",
"algorithm": "RSA",
"operationMode": "ECB",
"padding": "OAEPWithSHA1AndMGF1Padding",
"encryptedFields": "data,data1",
"failOnError": true
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

**Config**

```
{
"operation": "decrypt",
"algorithm": "RSA",
"operationMode": "ECB",
"padding": "OAEPWithSHA1AndMGF1Padding",
"encryptedFields": "data,data1",
"failOnError": true
}
```

**Payload**

```
{
"encryptionKey": "-- THE FOLLOWING PRIVATE KEY--"
"data": "RXZlbiBpZiBwZXJmZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH=",
"data1": "RXZlbiBpZifd441mZWN0IGNyeXB0b2dyYXBoaWMgcm91dGluZXMgYXJlIH="
}
```
