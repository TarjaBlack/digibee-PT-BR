---
description: Conheça o componente e saiba como utilizá-lo.
---

# FTP

O _**FTP**_ permite estabelecer uma conexão com um serviço que suporte o protocolo FTP (_File Transfer Protocol_) e executar os comandos de _upload_, _delete_, _download_, _list_ ou _move_.

**Nota:** O conector _FTP_ não funciona via VPN (_Virtual Private Network_). Um diretório FTP poderá ser acessado no _pipeline_ apenas se estiver exposto na internet, e redes VPN não se aplicam a esta regra.

Dê uma olhada nos parâmetros de configuração do componente:

* **FTP Server Operating System:** tipo de sistema operacional que o FTP roda.
* **Account:** para o componente fazer a autenticação a um serviço FTP é necessário usar uma _account_ do tipo BASIC.
* **Host:** nome do _host_ ou endereço IP para realizar a conexão. Este parâmetro aceita _Double Braces_.
* **Port:** número da porta - geralmente 21 para FTP e 990 para FTPS. Este parâmetro aceita _Double Braces_.
* **Operation:** operação a ser executada, que pode ser _upload_, _download_, listagem, _delete_ ou _move_.
* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: _tmp/file.txt_) para o arquivo remoto. Este parâmetro aceita _Double Braces_.
* **Remote Directory:** campo obrigatório. Diretório remoto base, que pode ser relativo (ex.: _pub/tmp_) ou absoluto (ex.: _/root/pub_). Este parâmetro aceita _Double Braces_.\

* **Binary File:** se "true", a transferência de arquivos será feita no modo binário (TYPE I ou Image); caso "false" o modo texto simples (TYPE A ou ASCII) será utilizado.
* **Connection Timeout:** tempo de expiração da conexão com o servidor (em milissegundos).
* **Data Timeout:** tempo de expiração para transferência de cada arquivo (em milissegundos).
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **FTP Security:** se a opção estiver ativada, o FTP é acessado de modo seguro FTPS (FTP-SSL ou FTP Secure).
* **SSL:** se a opção estiver ativada, o FTP é acessado com o protocolo criptográfico SSL (Secure Sockets Layer).
* **Implicit:** se a opção estiver ativada, a conexão SSL é estabelecida através da porta 990 antes mesmo do _login_ ou antes da transferência de arquivos.
* **Security Protocol:** tipo de protocolo de segurança que será utilizado - SSL (Secure Sockets Layer) ou TLS (Transport Layer Security).
* **Execution Type Protocol:** _private_, _clear_, _confidential_ ou _safe_.
* **Buffer Size:** tamanho de _buffer_ do canal de dados seguros.

**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Saída <a href="#sada" id="sada"></a>

Ao executar um componente FTP utilizando as operações _download, upload_ ou _move_, a seguinte estrutura de JSON será gerada:

```
{
    "status": {
        "success": true,
        "content": [
        {
            "symbolicLink": false,
            "name": "file.pdf",
            "type": 0,
            "size": 144089,
            "directory": false,
            "file": true,
            "timestamp": 1544726460000,
            "unknown": false,
            "rawListing": "-rw-rw----   1 user 10002      144089 Dec 13 16:41 file.pdf",
            "link": null,
            "hardLinkCount": 1,
            "user": "user",
            "group": "10002"
        }]
    }
}

```

* **fileName:** nome do arquivo local
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **success:** "true" se a operação sucedeu, "false" caso contrário

Ao executar um componente FTP utilizando as operação _list_, a seguinte estrutura de JSON será gerada:

```
{
     "remoteDirectory": "pub/example",
     "success": true,
     "content": [
     {
          "file": "imap-console-client.png"
     }]
}
```

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **success:** "true" se a operação sucedeu, "false" caso contrário
* **content:** a lista de arquivos no _remoteDirectory_
* **file:** nome do arquivo

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](../../build/pipelines/processamento-de-mensagens.md) e leia o nosso artigo.
