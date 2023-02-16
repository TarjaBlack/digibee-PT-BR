---
description: Conheça o componente e saiba como utilizá-lo.
---

# WebDav V2



O **WebDAV -V2** permite o uso de _Bouble Braces_ nos parâmetros _File Name, Remote File Name e Remote Directory. Leia a Documentação WebDav aqui._

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Host:** nome do _host_ para conexão.
* **File Name:** nome do arquivo local sem caminho. Permite o uso de _Double Braces._
* **Remote File Name:** nome do arquivo remoto sem caminho. Permite o uso de _Double Braces_.
* **Remote Directory:** diretório remoto. Permite o uso de _Double Braces_.&#x20;
* **FTP Operation:** comando utilizado para _download_, _upload_, list ou _delete_.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem no seguinte formato:

```
{            "fileName": "file",    "remoteFileName": "remoteFileName",    "remoteDirectory": "remoteDirectory"}
```

O **Local File Name** substitui o arquivo local padrão e o **Remote File Name** substitui o arquivo remoto padrão.

### Saída <a href="#sada" id="sada"></a>

```
{            "status" : {        "fileName": "",        "remoteFileName": "",        "remoteDirectory": "",        "success": ""    }}
```

**Local File Name** é o arquivo local gerado a partir de um _download_. **Remote File Name** é o arquivo remoto gerado a partir de um _upload_ de sucesso.

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

## WebDAV em Ação <a href="#webdav-em-ao" id="webdav-em-ao"></a>

### Delete <a href="#delete" id="delete"></a>

* **Configuração**

```
{    "type": "connector",    "name": "webdav-connector",    "stepName": "test-ftp",    "accountLabel": "webdav",    "params": {        "operation": "DELE",        "fileName": "data.csv",        "remoteFileName": "data11.csv",        "host": "https://ftp13.interfile.com.br/",        "remoteDirectory": "/remote.php/webdav"    }}
```

* **Saída**

```
{    "fileName": "data.csv",    "remoteFileName": "data11.csv",    "remoteDirectory": "/remote.php/webdav",    "success": true}
```

### Download <a href="#download" id="download"></a>

* **Configuração**

```
{    "type": "connector",    "name": "webdav-connector",    "stepName": "test-ftp",    "accountLabel": "webdav",    "params": {        "operation": "RETR",        "host": "https://ftp13.interfile.com.br/"    }}
```

* **Entrada**

```
{    "fileName": "data.csv",    "remoteFileName": "data11.csv",    "remoteDirectory": "/remote.php/webdav"}
```

* **Saída**

```
{    "fileName": "data.csv",    "remoteFileName": "data11.csv",    "remoteDirectory": "/remote.php/webdav",    "success": true}
```

### Upload <a href="#upload" id="upload"></a>

* **Configuração**

```
{    "type": "connector",    "name": "webdav-connector",    "stepName": "test-ftp",    "accountLabel": "webdav",    "params": {        "operation": "STOR",        "host": "https://ftp13.interfile.com.br/"    }}
```

* **Entrada**

```
{    "fileName": "data.csv",    "remoteFileName": "data11.csv",    "remoteDirectory": "/remote.php/webdav"}
```

## &#x20;<a href="#h_27544ad302" id="h_27544ad302"></a>

* **Saída**

```
{    "fileName": "data.csv",    "remoteFileName": "data11.csv",    "remoteDirectory": "/remote.php/webdav",    "success": true}
```
