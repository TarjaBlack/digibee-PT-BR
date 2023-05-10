---
description: Conheça o componente e saiba como utilizá-lo.
---

# ZIP File

O **ZIP File** permite a compressão de arquivos no formato zip.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** nome do arquivo a ser comprimido.
* **ZIP Operation:** define o tipo de operação (_Compress_, _Multiple Compress_ ou _Decompress_).
* **Output File Name:** nome do arquivo zip a ser gerado.
* **Custom Files Specification:** válido somente para operação _Multiple Compress_. Se a opção estiver habilitada, é possível passar dinamicamente os arquivos a serem comprimidos; do contrário, os arquivos podem ser informados individualmente via chave-valor.
* **Files:** válido somente para operação _Multiple Compress_, esse campo serve para definir os arquivos a serem comprimidos.
* **Set Charset:** válido somente para a operação _Decompress_. Se a opção estiver ativada, você pode definir um _charset_ específico para a operação.
* **Charset:** disponível apenas se **Set Charset** estiver habilitado. Selecione o _charset_ desejado nesse campo.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Entrada** <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada, podendo utilizá-la por meio de _Double Braces_.

### **Saída** <a href="#sada" id="sada"></a>

#### **Sem erro**

```
{
"fileName": "data.csv",
"success": true
}
```

**Com erro**

```
{
"success": false,
"message": "File data.csv already exists.",
"exception":
"com.digibee.pipelineengine.exception.PipelineEngineRuntimeException"
}
```

## ZIP File em Ação <a href="#zip-file-em-ao" id="zip-file-em-ao"></a>

### **Resposta de requisição** <a href="#resposta-de-requisio" id="resposta-de-requisio"></a>

```
{
"success": true,
"outputFileName": "data.zip"
}
```

* **outputFileName:** nome do arquivo escrito.
* **success:** se “true”, a operação foi executada com sucesso; se “false”, houve falha na operação.

### **Resposta de requisição contendo erro** <a href="#resposta-de-requisio-contendo-erro" id="resposta-de-requisio-contendo-erro"></a>

```
{
"exception": "java.io.FileNotFoundException: /tmp/pipeline-engine/3b3755ad-4256-429a-8898-2f7eea80f7db/data1.csv (No such file or directory)",
"message": "Encountered an I/O error while executing ZipFileConnector",
"success": false
}
```

* **success:** “false” quando a operação falha.
* **message:** mensagem sobre o erro.
* **exception:** informação sobre o tipo de erro ocorrido.

### **Manipulação de arquivos no pipeline** <a href="#manipulao-de-arquivos-no-pipeline" id="manipulao-de-arquivos-no-pipeline"></a>

O _pipeline_ possui uma área temporária e local para a manipulação de arquivos, que é separada e validada somente durante a execução do fluxo.

Dessa forma, você deve entender o acesso aos arquivos como se fosse feito em sistema de arquivos virtual. Os nomes de arquivo podem conter quaisquer caracteres válidos e extensões, os quais também podem ter um diretório sempre relativo. Por exemplo:

* data.csv
* processamento/data.csv

Qualquer tentativa de acesso a outros diretórios absolutos será bloqueada durante a execução do _pipeline_.
