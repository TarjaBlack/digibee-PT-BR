---
description: Conheça o componente e saiba como utilizá-lo.
---

# Digibee Storage

O _**Digibee Storage**_ se conecta ao _storage_ da Digibee Integration Plaform, possibilitando que sejam realizadas as seguintes operações com arquivos: _List_, _Download_, _Upload_ e _Delete_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** operação a ser executada (_Upload_, _Download_, _List_ ou _Delete_).
* **File Name:** nome do arquivo ou caminho completo (full file path) para o arquivo local, disponível apenas nas operações _Download_ e _Upload_. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: _tmp/file.txt_) para o arquivo remoto. Este parâmetro aceita _Double Braces_ e é apresentado nas operações _Download_, _Upload e Delete_.
* **Page Size:** tamanho da página, ou seja, a quantidade de itens a serem retornados quando a operação _List_ é utilizada. Se o valor não for especificado, todos os itens são retornados. Caso haja mais itens do que a quantidade determinada neste parâmetro, é possível solicitar uma segunda página (veja _Page Token_), a qual retorna os itens restantes.
* **Page Token:** _token_ utilizado para solicitar a próxima página quando a operação _List_ é executada_._ Nessa próxima página será retornada a quantidade de itens definidos no parâmetro _Page Size_.
* **Remote Directory:** diretório remoto base no qual será realizada a operação selecionada. Este parâmetro aceita _Double Braces_ e é apresentado nas operações _List_, _Download_, _Upload_ e _Delete_.
* **Generate Download Link:** se a opção estiver ativada, um _link_ público para _download_ do arquivo é gerado. Este parâmetro é aplicável apenas na operação _Upload_.
* **Link Expiration:** tempo para expiração do _link_ em milissegundos. Este parâmetro é válido apenas se a opção _Generate Download Link_ estiver ativada.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de mensagens <a href="#h_191bb9fbb4" id="h_191bb9fbb4"></a>

### Entrada <a href="#h_4b8ce53e87" id="h_4b8ce53e87"></a>

Não se espera nenhuma mensagem de entrada específica, mas apenas o preenchimento dos parâmetros obrigatórios que variam conforme a operação selecionada. Veja abaixo a obrigatoriedade de parâmetros para cada operação:

* _**List:**_ todos os parâmetros são opcionais
* _**Download**_**:** _File Name_ e _Remote File Name_
* _**Upload**_**:** _File Name_ e _Remote File Name_
* _**Delete**_**:** _Remote File Name_

No caso da operação _Update_, o arquivo informado no parâmetro _File Name_ precisa estar no diretório local do _pipeline_.

### **Saída** <a href="#h_9cc44295bd" id="h_9cc44295bd"></a>

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

* **content:** um vetor (_array_) de objetos para cada arquivo encontrado
  * **name:** nome do arquivo remoto
  * **contentType:** _MIME type_ do arquivo
  * **contentEncoding:** _encoding_ do arquivo, caso exista
  * **createTime:** _timestamp_ da data de criação do arquivo
  * **bucket:** _bucket_ onde o arquivo se encontra
  * **size:** tamanho do arquivo em _bytes_
* **pageToken:** _token_ para recuperar próxima página quando o parâmetro _Page Size_ é informado
* **fileName:** nome do arquivo local
* **remoteFileName:** nome do arquivo remoto
* **remoteDirectory:** nome da pasta base remota
* **success:** "true" se a última operação ocorreu com sucesso
* **error:** surge se um erro ocorreu e o _**Fail on Error**_ é "false"

Ao executar o componente utilizando as operações _Download, Upload_ e _Delete_, a seguinte estrutura de JSON será gerada:

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

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.
{% endhint %}

## Digibee Storage em Ação <a href="#h_73e9b4b21e" id="h_73e9b4b21e"></a>

* **LIST de arquivos**

**Entrada**

**Parâmetros**

**- Operation:** List

**- Remote Directory**: DGB-413

**- Page Size**: 2

**Saída**

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

Como é possível ver, o resultado acima retorna a propriedade _pageToken_ com um valor de referência para a próxima página. Essa propriedade será retornada quando o parâmetro _Page Size_ é configurado (no exemplo está definido com o valor 2) e também quando há mais arquivos a serem listados.

* ### LIST de vários arquivos usando paginação <a href="#h_739c9f3068" id="h_739c9f3068"></a>

**Entrada**

**Parâmetros**

**- Operation:** List

**- Remote Directory**: DGB-413

**- Page Size**: 2

**- Page Token:** ChVER0ItNDEzL2lzbzg4NTktMi50eHQ=

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

* **DOWNLOAD de um arquivo**

**Entrada**

**Parâmetros**

**- Operation:** Download

**- File Name:** iso8859-2.txt

**- Remote File Name:** iso8859-2.txt

**- Remote Directory**: DGB-413

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

* **UPLOAD de um arquivo**

**Entrada**

**Arquivo local**: file.txt

**Parâmetros**

**- Operation:** Upload

**- File Name:** file.txt

**- Remote File Name:** file.txt

**- Remote Directory**: DGB-413

**Saída**

```
{
  "fileName": "file.txt",
  "remoteFileName": "file.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}

```

* **UPLOAD de um arquivo gerando link para download**

**Entrada**

**Arquivo local**: file.txt

**Parâmetros**

**- Operation:** Upload

**- File Name:** file.txt

**- Remote File Name:** file.txt

**- Remote Directory**: DGB-413

**- Generate A Download Link:** true

**- Link Expiration (in ms):** 600000

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

Com a configuração dos parâmetros de entrada acima, o arquivo ficará disponível para download por 10 minutos (600000ms) através do link gerado na propriedade de saída _urlGenerated_.

* **DELETE de um arquivo**

**Entrada**

**Parâmetros**

**- Operation:** Delete

**- Remote File Name:** file.txt

**- Remote Directory**: DGB-413

**Saída**

```
{
  "fileName": null,
  "remoteFileName": "file.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}

```
