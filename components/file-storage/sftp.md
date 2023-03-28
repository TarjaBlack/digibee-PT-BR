---
description: Conheça o componente e saiba como utilizá-lo.
---

# SFTP

O _**SFTP**_ se conecta a um serviço que suporte o protocolo SFTP (_Secure File Transfer Protocol_ ou _SSH File Transfer_) para fazer upload, deleção, download, listagem ou mover arquivos.

Os parâmetros desse componente são:

* **Operation:** operação a ser executada: _upload_, _delete_, _download_, _list_ ou _move._
* **Account:** conta do tipo BASIC ou PRIVATE KEY. Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Host:** _host_ ou endereço IP a ser usado na conexão. Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Username:** usado apenas quando o _account type_ for PRIVATE KEY.  Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Port:** número da porta. Geralmente, assume valor 22.  Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **File Name:** nome do arquivo ou caminho completo (_full file path_) para o arquivo.  Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Remote File Name:** nome do arquivo remoto ou caminho relativo (_i.e. tmp/file.txt_) para o arquivo remoto.  Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Remote Directory:** Diretório remoto base, pode ser relativo (_i.e. pub/tmp_) ou absoluto (_i.e. /root/pub_).  Esse parâmetro é obrigatório. Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Connection Timeout:** tempo limite de expiração da conexão com o servidor (em milissegundos).
* **Overwrite File On Upload:** se `true`, arquivos com nomes confiltantes serão substituídos ao fazer um _upload._
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Proxy Enabled:** se `true`, você poderá configurar um _proxy_ para estabelecer a conexão com o serviço de SFTP.
* **Host:** _host_ do _proxy._ Disponível apenas se Proxy Enabled estiver ativado. Esse campo aceita [expressões Double Braces](../../build/double-braces/).
* **Port:** porta do _proxy._ Disponível apenas se Proxy Enabled estiver ativado. Esse campo aceita [expressões Double Braces](../../build/double-braces/).

## **Fluxo de mensagens** <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Saída**

Ao executar um componente SFTP utilizando as operações _download, upload_ ou _move_, a seguinte estrutura de JSON será gerada:

```
{
    "fileName": "picture.png",
    "remoteFileName": "imap-console-client.png",
    "remoteDirectory": "pub/example",
    "success": "true"
}
```

* **fileName:** nome do arquivo local.
* **remoteFileName:** caminho do arquivo remoto ou caminho relativo do arquivo remoto.
* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **success:** "true" se a operação foi bem sucedida, "false" caso contrário.

Ao executar um componente SFTP utilizando a operação _list_, a seguinte estrutura de JSON será gerada:

```
{
   "remoteDirectory":"pub/example",
   "success":true,
   "content":[
      {
         "file":"file.txt",
         "isDirectory":false,
         "size":1024,
         "permission":"-rwxrwxrwx",
         "flag":14,
         "accessed":"Sat Jan 14 09:21:05 UTC 2023",
         "modified":"Sat Jan 14 09:21:05 UTC 2023"
      }
   ]
}
```

* **remoteDirectory:** caminho do diretório remoto base (relativo ou absoluto).
* **success:** "true" se a operação foi bem sucedida, "false" caso contrário.
* **content:** a lista de arquivos no _remoteDirectory._
* **file:** nome do arquivo.
* **size:** tamanho do arquivo.
* **isDirectory:** se o objeto retornado é um diretório, será exibido “true”; se for um arquivo, será exibido “false”.
* **permissions:** uma _string_ contendo o tipo de permissão dada ao objeto.
* **accessed:** data do último acesso.
* **modified:** data da última modificação.
* **flag:** retorna _flags_, indicando quais atributos estão presentes.

{% hint style="info" %}
**IMPORTANTE:** A manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.
{% endhint %}

Para entender melhor o fluxo das mensagens na Plataforma, [leia esse artigo](../../build/pipelines/processamento-de-mensagens.md).
