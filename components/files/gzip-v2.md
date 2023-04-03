---
description: Conheça o componente e saiba como utilizá-lo.
---

# GZIP V2

O **GZIP V2** zipa um JSON ou um texto como uma _string_ em base64 ou arquivo. O componente também realiza a compressão e descompressão de arquivos em formato gzip.&#x20;

Essa versão do componente suporta _Double Braces_. [Para entender como essa linguagem funciona, leia a documentação](../../build/double-braces/).

Dê uma olhada nos parâmetros de configuração desse componente:

* **Operation:** _Compress Fields_ comprime os campos de um JSON; _Decompress Fields_ descomprime os campos de um JSON; _Compress Payload_ comprime um _payload_ recebido; _Decompress Payload_ descomprime um _payload_ recebido; _Compress File_ comprime um arquivo recebido; _Decompress File_ descomprime um arquivo recebido.
* **JSON Fields:** caminho do JSON a ser comprimido ou descomprimido, sendo que os campos precisam ser separados por vírgula (ex.: field1,field2).
* **Preserve Original:** se ativada, a opção preserva campos originais que possuem prefixo com _underline_.
* **Binary Content:** essa opção é válida omente para as operações _Compress Fields_ e _Compress Payload_. Se ativada, a opção faz com que o dado seja tratado como binário e uma _string_ base64 será esperada.
* **Payload:** esse campo é válido somente para as operações _Compress Payload_ e _Decompress Payload_ e declara o que será comprimido/descomprimido na requisição.
* **Result As File:** esse campo é válido somente para as operações _Compress Payload_ e _Decompress Payload. S_e ativada, a opção irá salvar o resultado da compressão ou descompressão em um arquivo.
* **File Name:** nome do arquivo a ser comprimido.
* **GZIP File Name:** nome do arquivo no formato gzip.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Para as operações _Compress Fields_ e _Decompress Fields_, o componente espera receber um JSON contendo os campos configurados na propriedade **JSON Fields**.

#### **Exemplo**

Com as seguintes configurações:

```
JSON Fields = field1,field2
```

O JSON esperado deve conter pelo menos:

```
{
"field1": "SOMETHING",
"field2": "SOMETHING"
}
```

Para as operações _Compress Payload_ e _Decompress Payload_, você deve configurar o campo **Payload** para poder executar a compressão/descompressão.

#### **Exemplo**

&#x20;Com as seguintes configurações:

```
Payload = {{ message.field1 }}
```

O JSON deverá conter este valor:

```
{
"field1": "SOMETHING"
}
```

Para as operações _Compress File_ e _Decompress File_, você deve configurar o arquivo que será comprimido/descomprimido e o arquivo resultante dessa operação.

#### **Exemplo**

```
File Name = file.csv
Gzip File Name = file.gzip
```

### Saída <a href="#sada" id="sada"></a>

Para as operações _Compress Fields_ e _Decompress Fields_, a mensagem de entrada é preservada.

Para as operações _Compress Payload_ e _Decompress Payload_, caso a saída seja um arquivo:

```
{
"success": "true",
"fileName": "file.csv"
}
```

Para as operações _Compress Payload_ e _Decompress Payload_, caso a saída seja uma _string_:

```
{
"success": "true",
"result": "SOMETHING COMPRESSED/DECOMPRESSED"
}
```

Para as operações _Compress File_ e _Decompress File_:

```
{
"success": "true",
"fileName": "file.csv",
"gzipFileName": "file.csv"
}
```
