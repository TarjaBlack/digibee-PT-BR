---
description: Conheça o componente e saiba como utilizá-lo.
---

# PGP

O **PGP (Pretty Good Privacy)** é um componente de criptografia que fornece autenticação e privacidade criptográfica para a comunicação de dados.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** define a conta que será usada pelo conector. A conta deve ser PUBLIC ou PRIVATE-KEY.
* **Operation:** define o tipo de operação(_Encrypt Fields, Decrypt Fields, Encrypt Payload, Decrypt Payload, Encrypt File_ ou _Decrypt File_).
* **Fields:** nome dos campos a serem criptografados dentro do JSON de entrada (devem estar separados por vírgula (ex.: param1,param2). Este parâmetro fica disponível somente quando _Encrypt Fields_ ou _Decrypt Fields_ estiverem selecionados no parâmetro **Operation**.
* **Payload:** pode ser definido como um valor único ou por _Double Braces_ para obter e definir um _payload_. Este parâmetro fica disponível somente quando _Encrypt Payload_ ou _Decrypt Payload_ estiverem selecionados no parâmetro **Operation**.
* **Charset:** _charset_ do texto.
* **File Name:** nome do arquivo a ser criptografado/descriptografado. Este parâmetro suporta expressões Double Braces e fica disponível somente quando _Encrypt File_ ou _Decrypt File_ estiverem selecionados no parâmetro **Operation.**
* **Output File Name:** nome do arquivo criptografado a ser gerado. Este parâmetro suporta expressões Double Braces e fica disponível somente quando _Encrypt File_ ou _Decrypt File_ estiverem selecionados no parâmetro **Operation.**
* **Hexadecimal:** se a opção estiver ativada, o valor a ser verificado ou assinado deve ser fornecido no formato hex; do contrário, será assinada ou verificada como base64.
* **Armor:** se a opção estiver ativada, irá encriptar as mensagens em ASCII para que elas sejam enviadas em formato padrão, assim como e-mail.
* **Zip:** se a opção estiver ativada, irá zipar a mensagem antes de ser encriptada.
* **Integrity Check:** se a opção estiver ativada, irá verificar a integridade da mensagem.
* **Fail On Error:** se a opção estiver ativada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Operação Encrypt Fields <a href="#operao-encrypt-fields" id="operao-encrypt-fields"></a>

#### **Entrada**

```
{
"parameter": "TEXT TO BE ENCRYPTED"
}
```

#### **Saída**

```
{
"parameter": "AA01FF" // text encrypted
}
```

### Operação Decrypt Fields <a href="#operao-decrypt-fields" id="operao-decrypt-fields"></a>

#### **Entrada**

```
{
"parameter": "AA01FF" // text encrypted
}
```

#### **Saída**

```
{
"parameter": "TEXT DECRYPTED"
}
```

### **Operação Encrypt Payload** <a href="#operao-encrypt-payload" id="operao-encrypt-payload"></a>

#### **Entrada**

```
{
"parameter": "TEXT TO BE ENCRYPTED"
}
```

#### **Saída**

```
{
"result": "AA01FF" // text encrypted
}
```

### Operação Decrypt Payload <a href="#operao-decrypt-payload" id="operao-decrypt-payload"></a>

#### **Entrada**

```
{
"parameter": "AA01FF" // text encrypted
}
```

#### **Saída**

```
{
"result": "TEXT DECRYPTED"
}
```

### **Operação Encrypt File** <a href="#operao-encrypt-file" id="operao-encrypt-file"></a>

#### **Entrada**

```
{
"fileName": "file.txt"
}
```

#### **Saída**

```
{
"outputFileName": "file.txt.pgp" // file encrypted
}
```

### Operação Decrypt File <a href="#operao-decrypt-file" id="operao-decrypt-file"></a>

#### **Entrada**

```
{
"fileName": "file.txt.pgp" // file encrypted
}
```

#### **Saída**

```
{
"outputFileName": "file.txt.dec" // file decrypted
}
```

### **Saída contendo erro** <a href="#sada-contendo-erro" id="sada-contendo-erro"></a>

```
{
"error": "java.io.FileNotFoundException: data1.csv (No such file or directory)",
"success": false
}
```

* **success:** “false” quando a operação falha.
* **error:** informação sobre o tipo de erro ocorrido.
