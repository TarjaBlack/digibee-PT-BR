---
description: Conheça o componente e saiba como utilizá-lo.
---

# SFTP

O _**SFTP**_ permite estabelecer uma conexão com um serviço que suporte o protocolo SFTP (Secure File Transfer Protocol ou SSH File Transfer) e executar os comandos de _upload_, _delete_, _download_, _list_ ou _move_.

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** operação a ser executada, que pode ser _upload_, _delete_, _download_, _list_ ou _move._\

* **Account:** para o componente fazer a autenticação a um serviço SFTP é necessário usar uma _account_ do tipo BASIC ou PRIVATE KEY. O parâmetro aceita _Double Braces_.
* **Host:** nome do _host_ ou endereço IP para realizar a conexão. O parâmetro aceita _Double Braces_.
* **User Name:** deve ser usado apenas quando o _account type_ for PRIVATE KEY. O parâmetro aceita _Double Braces_.
* **Port:** número da porta - geralmente 22. O parâmetro aceita _Double Braces_.
* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo. O parâmetro aceita _Double Braces_.
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (_i.e. tmp/file.txt_) para o arquivo remoto. O parâmetro aceita _Double Braces_.
* **Remote Directory:** campo obrigatório. Diretório remoto base, pode ser relativo (_i.e. pub/tmp_) ou absoluto (_i.e. /root/pub_). O parâmetro aceita _Double Braces_.
* **Connection Timeout:** tempo de expiração da conexão com o servidor (em milissegundos).
* **Overwrite File On Upload:** se "true", em caso de arquivos com nomes conflitantes o arquivo será substituído durante o _upload._
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Proxy Enabled:** se "true", permite a configuração de um _proxy_ para estabelecer a conexão com o serviço de SFTP.
* **Host:** _host_ do _proxy._ O parâmetro aceita _Double Braces_.
* **Port:** porta do _proxy._ O parâmetro aceita Double Braces.

**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).

### **Fluxo de mensagens** <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

* **Saída**

Ao executar um componente SFTP utilizando as operações _download, upload_ ou _move_, a seguinte estrutura de JSON será gerada:

```
{
    "fileName": "picture.png",
    "remoteFileName": "imap-console-client.png",
    "remoteDirectory": "pub/example",
    "success": "true"
}
```

* **fileName:** nome do arquivo local
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **success:** "true" se a operação foi bem sucedida, "false" caso contrário

Ao executar um componente SFTP utilizando a operação _list_, a seguinte estrutura de JSON será gerada:

```
{
    "remoteDirectory": "pub/example",
    "success": true,
    "content": [{"isDirectory": false,
        "size": 1024,
        "permission": "drwx------",
        "flag": 14,
        "accessed": "Sun Nov 08 16:36:32 BRT 2020",
        "modified": "Sun Nov 08 16:36:32 BRT 2020"
    }]
}
```

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto)
* **success:** "true" se a operação foi bem sucedida, "false" caso contrário
* **content:** a lista de arquivos no _remoteDirectory_
* **file:** nome do arquivo
* **size:** tamanho do arquivo
* **isDirectory:** se o objeto retornado é um diretório, será exibido “true”; se for um arquivo, será exibido “false”
* **permissions:** uma _string_ contendo o tipo de permissão dada ao objeto
* **accessed:** data do último acesso
* **modified:** data da última modificação
* **flag:** retorna _flags_, indicando quais atributos estão presentes

**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](../../build/pipelines/processamento-de-mensagens.md) e leia o nosso artigo.
