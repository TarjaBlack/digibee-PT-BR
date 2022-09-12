---
description: Conheça o componente e saiba como utilizá-lo.
---

# RSA Cryptography

O **RSA Cryptography** criptografa e descriptografa com base no algoritmo RSA.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Crypto Operation:** tipos de operação disponíveis - ENCRYPT FIELDS, DECRYPT FIELDS, ENCRYPT PAYLOAD e DECRYPT PAYLOAD.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Operation Mode:** modo de operação a ser utilizado.
* **Padding:** utilizado em um bloco de cifra no qual os blocos são preenchidos com _bytes_ de _padding_ (ex.: AES 128 bits utiliza 16 _bytes_ de _padding_).
* **Charset:** _charset_ da chave passada do _string type_.
* **Encrypt Message As Hex:** se a opção estiver ativada, o retorno da _secret key_ será em hexadecimal; do contrário, será em base64.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Para encriptar, você precisa configurar uma PUBLIC KEY _account_ ou passar a _property key_ via _body_ com a respectiva chave.

Para decriptar, você precisa configurar uma PRIVATE KEY _account_.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

KEY por ACCOUNT

### Operação ENCRYPT FIELDS <a href="#operao-encrypt-fields" id="operao-encrypt-fields"></a>

**Entrada**

```
{
"operation": "encrypt_fields",
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

### Operação DECRYPT FIELDS <a href="#operao-decrypt-fields" id="operao-decrypt-fields"></a>

**Entrada**

```
{
"operation": "decrypt_fields",
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
