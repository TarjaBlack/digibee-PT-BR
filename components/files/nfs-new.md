---
description: Conheça o componente e saiba como utilizá-lo.
---

# NFS

O componente **NFS** manipula arquivos. É possível listá-los, fazer o download e upload de arquivos e deletá-los.

## **Parâmetros de configuração** <a href="#h_c27c51d61a" id="h_c27c51d61a"></a>

Dê uma olhada nos parâmetros de configuração do componente:

* **Operations:** lista tipos de operação disponíveis - _Hash Fields_ e _Hash Payload._
* **Server IP:** número IP do servidor NFS. Não aceita double braces
* _**Exported Path:** caminho completo do diretório exportado do servidor NFS (esse caminho é configurado no arquivo de servidor etc/exports). Não aceita double braces_
* **Maximum Retries:** número máximo de tentativas de conexão ao servidor NFS. Não aceita double braces
* **UID:** A sigla UID significa _User Identifier_ (identificador de usuário). O Linux utiliza o número de UID para monitorar usuários e verificar suas permissões. Os arquivos e diretórios possuem inicialmente o mesmo UID do usuário que os criou. É usado para dar permissão de acesso ao arquivo. Não aceita double braces
* **GID:** O termo GID significa _Group Identifier_ (identificador de grupo). No Linux, os arquivos e diretórios são organizados em grupos. O GID de um arquivo é inicialmente herdado do usuário que cria o arquivo. É usado para dar permissão de acesso ao arquivo. Não aceita double braces
* **GIDs:** Esse parâmetro é opcional. Ele representa uma lista de, no máximo, 16 números de GID aos quais o usuário faz parte. Deve ser separado por vírgula. Ex: 0,1. Não aceita double braces.
* **File Name:** nome do arquivo local utilizado para operações de download e upload e para operação de filtro na listagem
* **Remote File Name:** nome do arquivo do servidor NFS
* **Remote Directory:** nome do diretório remoto.
* **Exact Match:** é um filtro que, se ativado, irá buscar exatamente o que for especificado no campo File Name, caso contrário ele fará uma busca aproximada.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado da propriedade _success_ será _false_ na saída do componente.

**IMPORTANTE:** Para ter acesso ao diretório do servidor NFS pelo nosso componente, o arquivo /etc/exports deverá ser configurado usando o caracter \* para mapear o IP do cliente. Isso ocorre porque os IPs dos _pods kubernetes_ são efêmeros, obrigando o usuário a realizar o mapeamento global. Ex:

`/home *(rw,sync,nohide)`

{% hint style="info" %}
**IMPORTANTE:** Para ter acesso ao diretório do servidor NFS pelo nosso componente, o arquivo /etc/exports deverá ser configurado usando o caracter \* para mapear o IP do cliente. Isso ocorre porque os IPs dos _pods kubernetes_ são efêmeros, obrigando o usuário a realizar o mapeamento global.&#x20;

Ex: `/home *(rw,sync,nohide)`
{% endhint %}

Alguns dos parâmetros acima suportam chaves duplas. [Para entender melhor como essa linguagem funciona, leia nosso artigo clicando aqui](https://docs.digibee.com/documentation/v/pt-br/build/double-braces).

## **Plataformas Digibee suportadas** <a href="#h_d2062816e7" id="h_d2062816e7"></a>

Apenas plataformas de Saas Dedicado.

Não é suportado em SaaS Digibee devido às características do protocolo NFS que funcionam somente em redes privadas e locais.

## **Versões suportadas** <a href="#h_1d93083b29" id="h_1d93083b29"></a>

Suportamos somente o NFS versão 3.

## **Fluxo de mensagens** <a href="#h_7c97f4e4b6" id="h_7c97f4e4b6"></a>

* ### **Entrada** <a href="#h_e76a65fbc5" id="h_e76a65fbc5"></a>

Não é necessário nenhuma mensagem específica na entrada, bastando apenas configurar os campos necessários para cada operação.

* **Saída**

**LIST**

```
{
"files": [
{
"name": "file.txt",
"isDirectory": false,
"lastModified": 1630959695395,
"size": 0,
"fileId": 137410,
"type": 1
}
],
"success": true
}
```

**UPLOAD e DOWNLOAD**

```
{
"remoteDirectory": "/",
"fileName": "file.txt",
"remoteFileName": "file-remote.txt",
"success": true
}
```

**DELETE**\


```
{
"remoteDirectory": "/",
"remoteFileName": "file-remote.txt",
"success": true
}
```

**Erro**

```
{
"success": false,
"message": "com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: Error loading connector nfs-connector. Error: com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: com.emc.ecs.nfsclient.mount.MountException: mount failure, server: 192.168.56.101, export: /var/nfs/digibee, nfs version: 3, returned state: 13",
"error": "com.emc.ecs.nfsclient.mount.MountException: mount failure, server: 192.168.56.101, export: /var/nfs/digibee, nfs version: 3, returned state: 13"
}
```

* **success:** “false”, pois ocorreu um erro na execução
* **message:** é a mensagem de erro do componente
* **error:** é a mensagem de erro recebida do conector NFS

## **NFS em ação** <a href="#h_d469f3a11f" id="h_d469f3a11f"></a>

**1. Listando com filtro - Exact Match desabilitado**

Server IP : 192.168.56.101

Exported Path: /var/nfs/general

Operation : LIST\_FILTER,

Remote Directory: /

File Name: test,

Exact Match: desabilidato

UID: 0,

GID: 0,

Maximum Retries: 3,

Fail On Error: desabilitado

Resposta:

```
{
"files": [
{
"name": "test.txt",
"isDirectory": false,
"lastModified": 1630959695395,
"size": 0,
"fileId": 137410,
"type": 1
},
{
"name": "file-test.txt",
"isDirectory": false,
"lastModified": 1630959695395,
"size": 0,
"fileId": 137410,
"type": 1
}

],
"success": true
}
```

**2- Listando com filtro - Exact Match habilitado**

Server IP : 192.168.56.101

Exported Path: /var/nfs/general

Operation : LIST\_FILTER,

Remote Directory: /

File Name: test.txt,

Exact Match: habilidato

UID: 0,

GID: 0,

Maximum Retries: 3,

Fail On Error: desabilitado

Resposta:

```
{
"files": [
{
"name": "test.txt",
"isDirectory": false,
"lastModified": 1630959695395,
"size": 0,
"fileId": 137410,
"type": 1
}
],
"success": true
}
```

3- Download

Server IP : 192.168.56.101

Exported Path: /var/nfs/general

Operation : DOWNLOAD,

Remote Directory: /

File Name : file.txt

Remote File Name : file-remote.txt,

UID: 0,

GID: 0,

Maximum Retries: 3,

Fail On Error: desabilitado

Resposta:

```

{
"remoteDirectory": "/",
"fileName": "file.txt",
"remoteFileName": "file-remote.txt",
"success": true
}
```

**4- Upload**

Server IP : 192.168.56.101

Exported Path: /var/nfs/general

Operation : UPLOAD,

Remote Directory: /

File Name : file.txt

Remote File Name : file-remote.txt,

UID: 0,

GID: 0,

Maximum Retries: 3,

Fail On Error: desabilitado

Resposta:

```
{
"remoteDirectory": "/",
"fileName": "file.txt",
"remoteFileName": "file-remote.txt",
"success": true
}
```

**5- Delete**

Server IP : 192.168.56.101

Exported Path: /var/nfs/general

Operation : DOWNLOAD,

Remote Directory: /

Remote File Name : file-remote.txt,

UID: 0,

GID: 0,

Maximum Retries: 3,

Fail On Error: desabilitado

Resposta:

```
{
"remoteDirectory": "/",
"remoteFileName": "file-remote.txt",
"success": true
}
```
