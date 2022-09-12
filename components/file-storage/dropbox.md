---
description: Conheça o componente e saiba como utilizá-lo.
---

# Dropbox



O componente _**Dropbox**_ permite que uma conexão com o serviço Dropbox seja estabelecida, além de possibilitar as seguintes operações com arquivos: _Download_, _Upload_ e _Delete_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta para que o componente possa fazer a autenticação ao serviço. É necessário utilizar uma conta do tipo OAUTH-BEARER. Para saber mais sobre as credenciais do Dropbox, clique [aqui](https://developers.dropbox.com/oauth-guide).
* **Operation:** operação a ser executada, que pode ser _Download, Upload_ ou _Delete_.
* **File Name:** nome do arquivo ou caminho completo (full file path) para o arquivo local, aplicável apenas nas operações _Download_ e _Upload_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: _tmp/file.txt_) para o arquivo remoto.
* **Remote Directory:** diretório remoto do Dropbox no qual será realizada a operação selecionada.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#h_fca0146697" id="h_fca0146697"></a>

### Entrada <a href="#h_59a360fdb5" id="h_59a360fdb5"></a>

O componente espera o preenchimento dos seguintes campos obrigatórios:

* _Account, File Name, Remote File Name_ e _Remote Directory_

Além disso, é possível fazer a passagem de parâmetros (com exceção do _Account_ e _Operation_) relacionados ao arquivo dentro do fluxo de integração. Nesse caso, o componente espera uma mensagem no seguinte formato:

```
{
    "filename": "data.csv",
    "remoteFileName": "data.csv,
    "remoteDirectory": "/"
}
```

* **Saída**

Ao executar o componente, a seguinte estrutura de JSON será gerada quando a operação for realizada com sucesso:

```
{
  "fileName": "data.csv",
  "remoteDirectory": "/",
  "remoteFileName": "data.csv",
  "success": true
}
```

Caso algum erro ocorra durante a execução da operação, a seguinte estrutura de JSON será gerada:

```
{
  "error": {
    "exception": "<DETALHES DO ERRO>",
    "message": "<MENSAGEM DE ERRO>",
    "success": false
  },
  "success": false
}
```

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

## Dropbox em Ação <a href="#h_6e5324e282" id="h_6e5324e282"></a>

### UPLOAD de um arquivo <a href="#h_1b9ed1e3e1" id="h_1b9ed1e3e1"></a>

* **Entrada**

**Arquivo local**: data.csv

**Parâmetros**

**- Account:** dropbox-test

**- Operation:** Upload

**- File Name:** data.csv

**- Remote File Name:** data.csv

**- Remote Directory**: /Public

ou

**- Account:** dropbox-test (via tela de configuração do componente)

**- Operation:** Upload (via tela de configuração do componente)

**- Payload**:

```
{
    "fileName": "data.csv",
    "remoteFileName": "data.csv",
    "remoteDirectory": "/Public"
}
```

* **Saída**

```
{
  "fileName": "data.csv",
  "remoteDirectory": "/Public",
  "remoteFileName": "data.csv",
  "success": true
}
```

### DOWNLOAD de um arquivo <a href="#h_0a995bee78" id="h_0a995bee78"></a>

* **Entrada**

**Parâmetros**

**- Account:** dropbox-test

**- Operation:** Download

**- File Name:** data.csv

**- Remote File Name:** data.csv

**- Remote Directory**: /Public

ou

**- Account:** dropbox-test (via tela de configuração do componente)

**- Operation:** Download (via tela de configuração do componente)

**- Payload:**

```
{
    "fileName": "data.csv",
    "remoteFileName": "data.csv",
    "remoteDirectory": "/Public"
}
```

* **Saída**

```
{
  "fileName": "data.csv",
  "remoteDirectory": "/Public",
  "remoteFileName": "data.csv",
  "success": true
}
```

Será realizado o _download_ do arquivo no diretório local do _pipeline._

### DELETE de um arquivo <a href="#h_f1bc720774" id="h_f1bc720774"></a>

* **Entrada**

**Parâmetros**

**- Account:** dropbox-test

**- Operation:** Delete

**- File Name:** data.csv

**- Remote File Name:** data.csv

**- Remote Directory**: /Public

ou

**Account:** dropbox-test (via tela de configuração do componente)

**Operation:** Delete (via tela de configuração do componente)

**Payload:**

```
{
    "fileName": "data.csv",
    "remoteFileName": "data.csv",
    "remoteDirectory": "/Public"
}

```

**Saída**

```
{
  "fileName": "data.csv",
  "remoteDirectory": "/Public",
  "remoteFileName": "data.csv",
  "success": true
}
```
