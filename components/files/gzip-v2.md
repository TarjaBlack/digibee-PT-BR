---
description: Conheça o componente e saiba como utilizá-lo.
---

# Gzip V2

O **Gzip V2** zipa um JSON ou um texto como uma _string_ em base64 ou arquivo. Com ele também é possível fazer a compressão e descompressão de arquivos em formato gzip. Essa versão do componente suporta _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](broken-reference).

Dê uma olhada nos parâmetros de configuração desse componente:

* **Operation:** "compress\_fields" comprime os campos de um JSON; "decompress\_fields" descomprime os campos de um JSON; "compress\_payload" comprime um payload recebido; "decompress\_payload" descomprime um payload recebido; compress\_file" comprime um arquivo recebido; decompress\_file" descomprime um arquivo recebido.
* **JSON Field:** caminho do JSON a ser comprimido ou descomprimido, sendo que os campos precisam ser separados por vírgula (ex.: field1,field2).
* **Preserve Original:** se ativada, a opção preserva campos originais que possuem prefixo com _underline_.
* **Binary Content:** se ativada, a opção faz com que o dado seja tratado como binário e uma _string_ base64 será esperada.
* **Payload:** esse campo é válido somente para as operações “compress\_payload” e “decompress\_payload” e declara o que será comprimido/descomprimido na requisição.
* **Result As File:** se ativada, a opção irá salvar o resultado da compressão ou descompressão em um arquivo (válido somente para as operações “compress\_payload” e “decompress\_payload”).
* **File Name:** nome do arquivo a ser comprimido.
* **Gzip File Name:** nome do arquivo no formato gzip.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Para as operações “compress\_fields” e “decompress\_fields”, o componente espera receber um JSON contendo os campos configurados na propriedade JSON Field.

**Exemplo**

* Configurando:

```
JSON Field = field1,field2
```

O JSON esperado deve conter pelo menos:

```
{
"field1": "SOMETHING",
"field2": "SOMETHING"
}
```

Para as operações “compress\_payload” e “decompress\_payload”, você deve configurar o campo “Payload” para poder executar a compressão/descompressão.

**Exemplo**

Payload = \{{ message.field1 \}}

O JSON deverá conter este valor:

```
{
"field1": "SOMETHING"
}
```

Para as operações “compress\_file” e “decompress\_file”, você deve configurar o arquivo que será comprimido/descomprimido e o arquivo resultante dessa operação.

**Exemplo**

File Name = file.csv

Gzip File Name = file.gzip

### Saída <a href="#sada" id="sada"></a>

Para as operações “compress\_fields” e “decompress\_fields”, a mensagem de entrada é preservada.

Para as operações “compress\_payload” e “decompress\_payload”, caso a saída seja um arquivo:

```
{
"success": "true",
"fileName": "file.csv"
}
```

Para as operações “compress\_payload” e “decompress\_payload”, caso a saída seja uma _string_:

```
{
"success": "true",
"result": "SOMETHING COMPRESSED/DECOMPRESSED"
}
```

Para as operações “compress\_file” e “decompress\_file”:

```
{
"success": "true",
"fileName": "file.csv",
"gzipFileName": "file.csv"
}
```
