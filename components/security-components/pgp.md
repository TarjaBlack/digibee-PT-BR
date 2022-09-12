---
description: Conheça o componente e saiba como utilizá-lo.
---

# PGP



O **PGP (Pretty Good Privacy)** é um componente de criptografia que fornece autenticação e privacidade criptográfica para a comunicação de dados.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** nome do arquivo a ser comprimido.
* **Zip Operation:** define o tipo de operação, que pode ser "Encrypt Fields", "Decrypt Fields" , "Encrypt Payload" , "Decrypt Payload", "Encrypt File" ou "Decrypt File".
* **Fields:** nome dos campos a serem criptografados dentro do JSON de entrada (devem estar separados por vírgula - ex.: param1,param2).
* **Charset:** _charset_ do texto.
* **File Name:** nome do arquivo a ser criptografado/descriptografado.
* **Output File Name:** nome do arquivo criptografado a ser gerado.
* **Hexadecimal:** se “true”, o valor a ser verificado ou assinado deve ser fornecido no formato hex; do contrário, será assinada ou verificada como base64.
* **Armor:** se ativada, a opção vai encriptar as mensagens em ASCII para que elas sejam enviadas em formato padrão, assim como e-mail.
* **Zip:** se ativada, a opção zipa a mensagem antes de ser encriptada.
* **Fail On Error:** se a opção estiver ativada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _**success**_.

### &#x20;<a href="#h_8c2b2a1da9" id="h_8c2b2a1da9"></a>

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Operação ENCRYPT FIELDS <a href="#operao-encrypt-fields" id="operao-encrypt-fields"></a>

**Entrada**

```
{
"parameter": "TEXT TO BE ENCRYPTED"
}
```

**Saída**

```
{
"parameter": "AA01FF" // text encrypted
}
```

### Operação DECRYPT FIELDS <a href="#operao-decrypt-fields" id="operao-decrypt-fields"></a>

**Entrada**

```
{
"parameter": "AA01FF" // text encrypted
}
```

**Saída**

```
{
"parameter": "TEXT DECRYPTED"
}
```

### &#x20;<a href="#h_c2e659bb7d" id="h_c2e659bb7d"></a>

### **Operação ENCRYPT PAYLOAD** <a href="#operao-encrypt-payload" id="operao-encrypt-payload"></a>

**Entrada**

```
{
"parameter": "TEXT TO BE ENCRYPTED"
}
```

### &#x20;<a href="#h_e7714acdfa" id="h_e7714acdfa"></a>

**Saída**

```
{
"result": "AA01FF" // text encrypted
}
```

### Operação DECRYPT PAYLOAD <a href="#operao-decrypt-payload" id="operao-decrypt-payload"></a>

**Entrada**

```
{
"parameter": "AA01FF" // text encrypted
}
```

**Saída**

```
{
"result": "TEXT DECRYPTED"
}
```

### **Operação ENCRYPT FILE** <a href="#operao-encrypt-file" id="operao-encrypt-file"></a>

**Entrada**

```
{
"fileName": "file.txt"
}
```

### &#x20;<a href="#h_db5604fc04" id="h_db5604fc04"></a>

**Saída**

```
{
"outputFileName": "file.txt.pgp" // file encrypted
}
```

### &#x20;<a href="#h_0eadde11ce" id="h_0eadde11ce"></a>

### Operação DECRYPT FILE <a href="#operao-decrypt-file" id="operao-decrypt-file"></a>

**Entrada**

```
{
"fileName": "file.txt.pgp" // file encrypted
}
```

**Saída**

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

* **success:** “false” quando a operação falha
* **error:** informação sobre o tipo de erro ocorrido
