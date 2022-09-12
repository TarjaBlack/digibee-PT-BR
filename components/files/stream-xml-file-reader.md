---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream XML File Reader

O _**Stream XML File Reader**_ realiza a leitura de um arquivo XML local e, com base na configuração de um nó desejado e campos de contexto, faz a entrega de uma estrutura XML e de propriedades de contexto para cada nó encontrado e dispara _subpipelines_ para processar cada mensagem. O componente deve ser utilizado para arquivos grandes quando há a necessidade de ler partes do todo de forma eficiente.

Dê uma olhada nos parâmetros de configuração do componente:

* **File name:** nome do arquivo XML local.
* **Charset:** nome do código de caracteres para a leitura do arquivo (padrão UTF-8).
* **Node Path:** caminho do nó desejado do arquivo XML a ser transmitido. Ex.: //root/level1/level2/desirednode
* **Context Paths**: defina aqui caminhos de _tag_ pai que representam campos que adicionam contexto ao nó desejado. Caso haja mais de um, separe-os por vírgula. Ex.: //root/node1/code,//root/node2/description.
* **Ignore Paths**: defina aqui os caminhos que serão ignorados e não retornarão ao nó desejado. Ex.: //root/node1/email,//root/node2/city
* **Ignore Nested Child Nodes**: se a opção estiver habilitada, os nós filhos aninhados (nós que não são filhos diretos do nó desejado) serão ignorados. Nesse caso, o nó de mesmo nível do nó desejado será retornado, mas os nós abaixo do mesmo serão ignorados.
* **Element Identifier:** atributo que será enviado em caso de erros.
* **Paralell Execution Of Each Iteration:** ocorre em paralelo com a execução do _loop_.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do _pipeline_ apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro "Fail On Error" não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines (onProcess_ e _onException_).

## Fluxo de mensagens <a href="#h_9935e06ea4" id="h_9935e06ea4"></a>

### Entrada <a href="#h_ddefd24400" id="h_ddefd24400"></a>

Não se espera nenhuma mensagem de entrada específica e sim apenas a existência de um arquivo XML no diretório local do _pipeline_ e o preenchimento dos campos obrigatórios “File Name” e “Node Path” para o processamento do arquivo.

### Saída <a href="#h_3c41e7bad5" id="h_3c41e7bad5"></a>

```
{
"total": 0,
"success": 0,
"failed": 0
}
```

* **total:** número total de linhas processadas
* **success:** número total de linhas processadas com sucesso
* **failed:** número total de linhas cujo processamento falhou

**IMPORTANTE:** para saber se uma linha foi processada corretamente, deve haver o retorno { "success": true } para cada linha processada.

O componente joga uma exceção se o “File Name” não existir ou não puder ser lido.

A manipulação de arquivos dentro de um pipeline ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

O _**Stream XML File Reader**_ realiza processamento em lote. Para entender melhor o conceito, clique [aqui](../../tutoriais-e-melhores-praticas/processamento-em-lote.md).

## Stream XML File Reader em Ação <a href="#h_6eb38d0ab7" id="h_6eb38d0ab7"></a>

Os cenários a seguir estão utilizando como base o seguinte arquivo XML:

**Nome do arquivo:** file.xml

**Conteúdo:**

```
<?xml version="1.0" encoding="UTF-8"?>
<root>
<list-info qty="4">products</list-info>
<products>
<product>
<price>20.75</price>
<product>Chair</product>
<tags>
<element>NEW</element>
<element>FURNITURE</element>
</tags>
</product>
<product>
<price>399.99</price>
<product>TV</product>
<tags>
<element>NEW</element>
<element>FURNITURE</element>
</tags>
</product>
<product>
<price>100</price>
<product>Couch</product>
<tags>
<element>NEW</element>
<element>FURNITURE</element>
</tags>
</product>
<product>
<price>78.99</price>
<product>Table</product>
<tags>
<element>NEW</element>
<element>FURNITURE</element>
</tags>
</product>
</products>
</root>
```

### Realizando o stream do arquivo informando o nó desejado <a href="#h_dcd89dcaa5" id="h_dcd89dcaa5"></a>

**Entrada**

* **file.xml**

**File Name:** file.xml

**Node Path:** //root/products/product

**Saída**

```
{
"total": 4,
"success": 4,
"failed": 0
}
```

Cada elemento identificado pelo caminho do nó desejado será processado de forma independente:

* **Primeiro subfluxo**

```
{
"node":"<product><price>20.75</price><product>Chair</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Segundo subfluxo**

```
{
"node":"<product><price>399.99</price><product>TV</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Terceiro subfluxo**

```
{
"node":"<product><price>100</price><product>Couch</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Quarto subfluxo**

```
{
"node":"<product><price>78.99</price><product>Table</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

### Realizando o stream do arquivo informando o nó desejado e campos de contexto <a href="#h_100ca898cb" id="h_100ca898cb"></a>

**Entrada**

* **file.xml**

**File Name:** file.xml

**Node Path:** //root/products/product

**Context Paths:** //root/list-info

**Saída**

```
{
"total": 4,
"success": 4,
"failed": 0
}
```

Cada elemento identificado pelo caminho do nó desejado será processado de forma independente:

* **Primeiro subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>20.75</price><product>Chair</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Segundo subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>399.99</price><product>TV</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Terceiro subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>100</price><product>Couch</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

* **Quarto subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>78.99</price><product>Table</product><tags><element>NEW</element><element>FURNITURE</element></tags></product>"
}
```

### Realizando o stream do arquivo informando o nó desejado, campos de contexto e nós à serem ignorados: <a href="#h_a6b1dbfa6e" id="h_a6b1dbfa6e"></a>

**Entrada**

* **file.xml**

**File Name:** file.xml

**Node Path:** //root/products/product

**Context Paths:** //root/list-info

**Ignore Paths:** //root/products/product/tags

**Saída**

```
{
"total": 4,
"success": 4,
"failed": 0
}
```

Cada elemento identificado pelo caminho do nó desejado será processado de forma independente:

* **Primeiro subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>20.75</price><product>Chair</product></product>"
}
```

* **Segundo subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>399.99</price><product>TV</product></product>"
}
```

* **Terceiro subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>100</price><product>Couch</product></product>"
}
```

* **Quarto subfluxo**

```
{
"context": {
"root": {
"list-info": {
"attributes": {
"qty": "4"
},
"value": "products"
}
}
},
"node": "<product><price>78.99</price><product>Table</product></product>"
}
```

### Realizando o stream do arquivo informando o nó desejado e ignorando nós filhos aninhados <a href="#h_086a4fe07b" id="h_086a4fe07b"></a>

**Entrada**

* **file.xml**

**File Name:** file.xml

**Node Path:** //root/products/product

**Ignore Nested Child Nodes:** verdadeiro

**Saída**

```
{
"total": 4,
"success": 4,
"failed": 0
}
```

Cada elemento identificado pelo caminho do nó desejado será processado de forma independente:

* **Primeiro subfluxo**

```
{
"data": {
"node": "<product><price>20.75</price><product>Chair</product><tags></tags></product>"
},
"success": true
}
```

* **Segundo subfluxo**

```
{
"node": "<product><price>399.99</price><product>TV</product><tags></tags></product>"
}
```

* **Terceiro subfluxo**

```
{
"node": "<product><price>100</price><product>Couch</product><tags></tags></product>"
}
```

* **Quarto subfluxo**

```
{
"node": "<product><price>78.99</price><product>Table</product><tags></tags></product>"
}
```

## Informações adicionais <a href="#h_39608ec0fd" id="h_39608ec0fd"></a>

O _**Stream XML File Reader**_ utiliza um mecanismo de leitura por eventos, por meio do qual cada tipo de dado presente no arquivo é um evento a ser processado. Com isso, existem alguns tipos de evento que não estão contemplados durante o _stream_ do arquivo. São eles:

* PROCESSING INSTRUCTION
* START DOCUMENT
* END DOCUMENT
* SPACE
* ENTITY REFERENCE
* ENTITY DECLARATION
* DTD
* NOTATION DECLARATION
