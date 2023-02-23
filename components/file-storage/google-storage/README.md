---
description: Conheça o componente e saiba como utilizá-lo.
---

# Google Storage



O _**Google Storage**_ permite que uma conexão com o serviço Google Storage seja estabelecida e possibilita as seguintes operações com arquivos: _List_, _Download_, _Upload_ e _Delete_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** para o componente fazer a autenticação ao serviço, é necessário usar uma _account_ do tipo PRIVATE KEY. Para saber mais sobre credenciais, clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br).\

* **Operation:** operação a ser executada, que pode ser _Upload_, _Download_, _List_ ou _Delete_.
* **Project ID:** ID do projeto onde a operação com o arquivo será realizada.
* **Bucket Name:** esse recurso representa um _bucket_ no Google Cloud Storage - há um único _namespace_ compartilhado por todos os _buckets_.
* **Page Size:** tamanho da página, ou seja, a quantidade de itens a serem retornados quando utilizada a operação _List_. Se o valor não for especificado, todos os itens são retornados. Caso haja mais itens do que a quantidade determinada neste parâmetro, é possível pedir uma segunda página (veja _Page Token_), a qual retorna os itens restantes.
* **Page Token:** _token_ utilizado para solicitar a próxima página quando utilizada a operação _List._ Nessa próxima página será retornada a quantidade de itens definidos no parâmetro _Page Size._
* **File Name:** nome do arquivo ou caminho completo (full file path) para o arquivo local, disponível apenas nas operações _Download_ e _Upload_. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: _tmp/file.txt_) para o arquivo remoto. Este parâmetro aceita _Double Braces_ e é apresentado nas operações _Download_, _Upload e Delete_.
* **Remote Directory:** diretório remoto base, que pode ser relativo (ex.: _pub/tmp_) ou absoluto (ex.: _/root/pub_), no qual será realizada a operação selecionada. Este parâmetro aceita _Double Braces_ e é apresentado nas operações _List_, _Download_, _Upload_ e _Delete_.
* **Generate Download Link:** se a opção estiver ativada, um _link_ público para _download_ do arquivo é gerado. Este parâmetro é aplicável apenas na operação _Upload_.
* **Link Expiration:** tempo para expiração do _link_ em milissegundos. Este parâmetro é válido apenas se a opção _Generate Download Link_ estiver ativada.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](../../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Não se espera nenhuma mensagem de entrada específica e sim apenas o preenchimento dos parâmetros obrigatórios que variam conforme a operação selecionada. Veja abaixo a obrigatoriedade de parâmetros para cada operação:

* _List: Account, Project ID, Bucket Name_
* _Download_: _Account, Project ID, Bucket Name, File Name e Remote File Name_
* _Upload_: _Account, Project ID, Bucket Name, File Name e Remote File Name_
* _Delete_: _Account, Project ID, Bucket Name e Remote File Name_

No caso da operação _Update_ é necessária a existência de um arquivo no diretório local do _pipeline_.

### Saída <a href="#sada" id="sada"></a>

Ao executar o componente utilizando a operação _list_, a seguinte estrutura de JSON será gerada:

```
{
  "content": [
    {
      "name": "temp//tmp/processed/file-3.txt",
      "contentType": "application/octet-stream",
      "contentEncoding": null,
      "createTime": 1581689153448,
      "bucket": "test-bucket",
      "size": 10
    },
    { ... }
  ],
  "pageToken": "XXXXXXXXXXXXL3RtcC9wcm9jZXNzZWQvZmlsZS0zLnR4dA==",
  "fileName": null,
  "remoteFileName": null,
  "remoteDirectory": "",
  "success": true
}
```

*   **content:** um vetor (_array_) de objetos para cada arquivo encontrado

    **- name:** nome do arquivo remoto

    **- contentType:** _MIME type_ do arquivo

    **- contentEncoding:** _encoding_ do arquivo, caso exista

    **- createTime:** _timestamp_ da data de criação do arquivo

    **- bucket:** _bucket_ onde o arquivo se encontra

    **- size:** tamanho do arquivo em _bytes_
* **pageToken:** _token_ para recuperar próxima página
* **fileName:** nome do arquivo local
* **remoteFileName:** nome do arquivo remoto
* **remoteDirectory:** nome da pasta base remota
* **success:** "true" se a última operação ocorreu com sucesso
* **error:** surge se um erro ocorreu e o _**Fail on Error**_ é "false"

Ao executar o componente utilizando as operações _download, upload_ e _delete_, a seguinte estrutura de JSON será gerada:

```
{
  "fileName": "file.txt",
  "remoteFileName": "tmp/iso-8859-1-test.txt",
  "remoteDirectory": "",
  "success": true
}
```

* **fileName:** nome do arquivo local
* **remoteFileName:** nome do arquivo remoto
* **remoteDirectory:** nome da pasta base remota
* **success:** "true" se a última operação ocorreu com sucesso

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

## Google Storage em Ação <a href="#h_08d59df345" id="h_08d59df345"></a>

### LIST de arquivos <a href="#h_1c1aa08075" id="h_1c1aa08075"></a>

* **Entrada**

**Parâmetros**

**Account:** google-storage-test

**Operation:** List

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**Remote Directory**: DGB-413

**Page Size**: 2

* **Saída**

```
{
  "content": [
    {
      "name": "DGB-413/",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552394033410,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 11
    },
    {
      "name": "DGB-413/iso8859-2.txt",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552395963553,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 55
    }
  ],
  "pageToken": "ChVER0ItNDEzL2lzbzg4NTktMi50eHQ=",
  "fileName": null,
  "remoteFileName": null,
  "remoteDirectory": "DGB-413",
  "success": true
}
```

Como é possível ver, o resultado acima retorna a propriedade _pageToken_ com um valor de referência para a próxima página. Essa propriedade será retornada quando o parâmetro _Page Size_ é configurado (no exemplo está definido com o valor 2) e também quando há mais arquivos para serem listados.

### LIST de vários arquivos usando paginação <a href="#h_8ef178b35a" id="h_8ef178b35a"></a>

* **Entrada**

**Parâmetros**

**Account:** google-storage-test

**Operation:** List

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**Remote Directory**: DGB-413

**Page Size**: 2

**Page Token:** ChVER0ItNDEzL2lzbzg4NTktMi50eHQ=

**Saída**

```
{
  "content": [
    {
      "name": "DGB-413/utf-16-test.txt",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552394973030,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 70
    },
    {
      "name": "DGB-413/utf-test.txt",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552394644597,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 55
    }
  ],
  "fileName": null,
  "remoteFileName": null,
  "remoteDirectory": "DGB-413",
  "success": true
}
```

No resultado acima a propriedade _pageToken_ não foi retornada. Isso sinaliza que não há mais arquivos a serem listados.

### DOWNLOAD de um arquivo <a href="#h_474291aeb1" id="h_474291aeb1"></a>

* **Entrada**

**Parâmetros**

**Account:** google-storage-test

**Operation:** Download

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**File Name:** iso8859-2.txt

**Remote File Name:** iso8859-2.txt

**Remote Directory**: DGB-413

**Saída**

```
{
  "fileName": "iso8859-2.txt",
  "remoteFileName": "iso8859-2.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}
```

Será realizado o _download_ do arquivo no diretório local do _pipeline._

### UPLOAD de um arquivo <a href="#h_75c35bbddc" id="h_75c35bbddc"></a>

* **Entrada**

**Arquivo local**: file.txt

**Parâmetros**

**Account:** google-storage-test

**Operation:** Upload

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**File Name:** file.txt

**Remote File Name:** file.txt

**Remote Directory**: DGB-413

**Saída**

```
{
  "fileName": "file.txt",
  "remoteFileName": "file.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}
```

### UPLOAD de um arquivo gerando link para download <a href="#h_a5f5aa1c88" id="h_a5f5aa1c88"></a>

* **Entrada**

**Arquivo local**: file.txt

**Parâmetros**

**Account:** google-storage-test

**Operation:** Upload

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**File Name:** file.txt

**Remote File Name:** file.txt

**Remote Directory**: DGB-413

**Generate A Download Link:** true

**Link Expiration (in ms):** 600000

**Saída**

```
{
  "fileName": "file.txt",
  "remoteFileName": "file.txt",
  "remoteDirectory": "DGB-413",
  "success": true,
  "urlGenerated": "<URL TO DOWNLOAD THE FILE>"
}
```

Com a configuração dos parâmetros de entrada acima, o arquivo ficará disponível para _download_ por 10 minutos (600000ms) através do link gerado na propriedade de saída _urlGenerated_.

### DELETE de um arquivo <a href="#h_d87f706dd2" id="h_d87f706dd2"></a>

* **Entrada**

**Parâmetros**

**Account:** google-storage-test

**Operation:** Delete

**Project ID**: digibee-test

**Bucket Name**: **** digibee-test-digibee-test-bucket

**Remote File Name:** file.txt

**Remote Directory**: DGB-413

**Saída**

```
{
  "fileName": null,
  "remoteFileName": "file.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}
```
