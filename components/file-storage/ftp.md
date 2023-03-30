---
description: Conheça o componente e saiba como utilizá-lo.
---

# FTP

O _**FTP**_ permite estabelecer uma conexão com um serviço que suporte o protocolo FTP (_File Transfer Protocol_) e executar os comandos de _Upload_, _Delete_, _Download_, _List_ ou _Move_.

{% hint style="info" %}
**Nota:** O conector _FTP_ não funciona via VPN (_Virtual Private Network_). Um diretório FTP poderá ser acessado no _pipeline_ apenas se estiver exposto na internet, e redes VPN não se aplicam a esta regra.
{% endhint %}

Dê uma olhada nos parâmetros de configuração do componente:

* **FTP Server Operating System:** tipo de sistema operacional que o FTP roda.
* **Account:** para o componente fazer a autenticação a um serviço FTP é necessário usar uma _account_ do tipo BASIC.
* **Host:** nome do _host_ ou endereço IP para realizar a conexão. Este parâmetro aceita _Double Braces_.
* **Port:** número da porta - geralmente 21 para FTP e 990 para FTPS. Este parâmetro aceita _Double Braces_.
* **Operation:** operação a ser executada, que pode ser _Upload_, _Delete_, _Download_, _List_ ou _Move_.
* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo. Este parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (ex.: tmp/file.txt) para o arquivo remoto. Este parâmetro aceita _Double Braces_.
* **Remote Directory:** campo obrigatório. Diretório remoto base, que pode ser relativo (ex.: _pub/tmp_) ou absoluto (ex.: __ /root/pub). Este parâmetro aceita _Double Braces_.
* **Binary File:** se _"true"_, a transferência de arquivos será feita no modo binário (TYPE I ou Image); caso _"false"_ o modo texto simples (TYPE A ou ASCII) será utilizado.
* **Connection Timeout:** tempo de expiração da conexão com o servidor (em milissegundos).
* **Data Timeout:** tempo de expiração para transferência de cada arquivo (em milissegundos).
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.
* **FTP Security:** se a opção estiver ativada, o FTP é acessado de modo seguro FTPS (FTP-SSL ou FTP Secure).
* **SSL:** se a opção estiver ativada, o FTP é acessado com o protocolo criptográfico SSL (_Secure Sockets Layer_).
* **Implicit:** se a opção estiver ativada, a conexão SSL é estabelecida através da porta 990 antes mesmo do _login_ ou antes da transferência de arquivos.
* **Remote Verification:** se a opção estiver ativada, permite a verificação do _host_ remoto para confirmar se o _host_ conectado é o mesmo _host_ que está conectado à conexão de controle.
* **Security Protocol:** tipo de protocolo de segurança que será utilizado - SSL (_Secure Sockets Layer_) ou TLS (_Transport Layer Security_).
* **Execution Type Protocol:** _private_, _clear_, _confidential_ ou _safe_.
* **Buffer Size:** tamanho de _buffer_ do canal de dados seguros.

Alguns dos parâmetros acima suportam _Double Braces_. [Para entender como essa linguagem funciona, leia a documentação](../../build/double-braces/).

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Saída <a href="#sada" id="sada"></a>

Ao executar um componente FTP utilizando as operações _Download, Upload_ ou _Move_, a seguinte estrutura de JSON será gerada:

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

* **fileName:** nome do arquivo local.
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto.
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **success:** "true" se a operação sucedeu, "false" caso contrário.

Ao executar um componente FTP utilizando a operação _List_, a seguinte estrutura de JSON será gerada:

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

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **success:** "true" se a operação sucedeu, "false" caso contrário.
* **content:** a lista de arquivos no "_remoteDirectory"._
* **file:** nome do arquivo.

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.
{% endhint %}

Para entender melhor o fluxo das mensagens na Digibee Integration Platform, [leia a documentação sobre Processamento de mensagens](../../build/pipelines/processamento-de-mensagens.md).
