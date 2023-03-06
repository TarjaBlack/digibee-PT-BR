---
description: Conheça o componente e saiba como utilizá-lo.
---

# PBE Cryptography

O **PBE Cryptography** faz operações de criptografia e descriptografia usando o algoritmo PBE (Password Based Encryption).

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis - ENCRYPT FIELDS, DECRYPT FIELDS, ENCRYPT PAYLOAD e DECRYPT PAYLOAD.
* **Account:** conta a ser utilizada pelo componente - é esperada uma conta _SECRET-KEY type_.
* **Iteration Count:** número de iterações com o Salt.
* **Algorithm:** tipo de algoritmo a ser utilizado.
* **Fields To Encrypt/Decrypt:** campos a serem encriptados/decriptados utilizando uma notação com pontos (ex.: body.field1,body.field2,body).
* **Charset:** tipo de codificação.
* **Secret Key Type:** formato da _secret key_ (String, Hexadecimal ou Base64).
* **Fail On Error:** se a opção estiver ativada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _**sucesso**_.
* **Advanced Settings:** configurações avançadas.
* **Use Key From Payload:** se ativada, a opção utilizará a _secret key_ do _payload_.
* **Secret Key:** chave em formato Hex ou Base64.
* **Use Salt From Payload:** se ativada, a opção utilizará o Salt do _payload_; do contrário, um novo Salt será gerado.
* **Salt:** cadeia aleatória de dados utilizada para modificar um _hash_ de senha.
* **Encryption Key As Hex Value:** se a opção estiver ativada, o retorno da _secret key_ será em hexadecimal; do contrário, será em Base64 caso a opção "Use Key From Payload" também esteja ativada.
* **Salt As Hex Value:** se a opção estiver ativada, o retorno do Salt será em hexadecimal; do contrário, será em Base64.
* **Encrypted Message As Hex:** se a opção estiver ativada, o retorno da _secret key_ será em hexadecimal; do contrário, será em Base64.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Criptografar via _fields_ <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### **Entrada**

```
{
  "accountLabel": "account",
  "params": {
    "operation": "encrypt_fields",
    "iterationCount": 1000,
    "keyType": "STRING",
    "algorithm": "PBEWithMD5AndDES",
    "encryptedFields": "a.test",
    "failOnError": true
  }
}
```

#### **Payload**

```
{
  "a": {
    "test": "test"
  }
}
```

#### **Saída**

```
{
  "a": {
    "test": "ZmRmcw=="
  },
  "_salt": "ZmRmcwZmRmcw=="
}
```

### Descriptografar via _fields_

#### **Entrada**

```
{
  "accountLabel": "account",
  "params": {
    "operation": "decrypt_fields",
    "iterationCount": 1000,
    "keyType": "STRING",
    "algorithm": "PBEWithMD5AndDES",
    "encryptedFields": "a.test",
    "useSaltFromPayload": true,
    "salt": "{{ message._salt }}",
    "failOnError": true
  }
}
```

#### **Payload**

```
{
  "a": {
    "test": "ZmRmcw=="
  },
  "_salt": "ZmRmcwZmRmcw=="
}
```

#### **Saída**

```
{
  "a": {
    "test": "test"
  },
  "_salt": "ZmRmcwZmRmcw=="
}

```

### Criptografar via _payload_ <a href="#criptografarvia-payload" id="criptografarvia-payload"></a>

#### **Entrada**

```
{
"accountLabel": "pbe",
    "params": {
        "operation": "encrypt_payload",
        "iterationCount": 1000,
        "payload": "{{ message.a.test }}",
        "keyType": "STRING",
        "algorithm": "PBEWithMD5AndDES",
        "failOnError": true
    }
}
```

#### **Payload**

```
{
  "a": {
    "test": "test"
  }
}
```

#### **Saída**

```
{
  "a": {
    "test": "test"
  },
  "result": "ZmRmcw==",
  "_salt": "ZmRmcwZmRmcw=="
}
```

### Descriptografar via _payload_ <a href="#descriptografar-via-payload" id="descriptografar-via-payload"></a>

#### **Entrada** <a href="#descriptografar-via-payload" id="descriptografar-via-payload"></a>

```
{
"accountLabel": "pbe",
    "params": {
        "operation": "decrypt_payload",
        "iterationCount": 1000,
        "payload": "{{ message.a.test }}",
        "keyType": "STRING",
        "algorithm": "PBEWithMD5AndDES",
        "useSaltFromPayload": true,
"salt": "{{ message._salt }}",
        "failOnError": true
    }
}
```

#### **Payload**

```
{
  "a": {
    "test": "ZmRmcw=="
  }
}
```

#### **Saída**

```
{
  "a": {
    "test": "ZmRmcw=="
  },
  "result": "test",
  "_salt": "ZmRmcwZmRmcw=="
}
```
