---
description: Saiba quais são as funções associadas aos Double Braces e como utilizá-las.
---

# Funções Double Braces

As funções foram criadas para:

* acelerar ainda mais a criação das suas integrações;
* diminuir a complexidade dos seus _pipelines;_
* simplificar conversões e transformações dos dados durante o fluxo dos seus _pipelines._

As funções estão disponíveis para componentes que suportam expressões com _Double Braces_. Para saber como passar informações para os componentes utilizando esse recurso, leia o artigo [Double Braces e Entrada de Dados](double-braces-e-entrada-de-dados.md).

Veja a seguir como as funções se agrupam de acordo com o que executam.

### DE COMPARAÇÃO <a href="#de-comparao" id="de-comparao"></a>

As funções deste grupo realizam comparações de entradas booleanas. Para saber mais, leia o artigo [Funções de Comparação](funcoes-de-comparacao.md):

* AND
* NOT
* OR
* XOR

### NUMÉRICAS <a href="#numricas" id="numricas"></a>

As funções deste grupo realizam tratamentos de números. Para saber mais, leia o artigo [Funções Numéricas](funcoes-numericas.md):

* FORMATNUMBER
* TODOUBLE
* TOINT
* TOLONG

### CONDICIONAIS <a href="#condicionais" id="condicionais"></a>

As funções deste grupo retornam um valor de acordo com o critério que você estabeleceu. Para testes lógicos e condições, serão utilizados operadores nessas funções. Para saber mais, leia o artigo [Funções Condicionais](funcoes-condicionais.md):

* EQUALTO
* GREATERTHAN
* GREATERTHANEQUAL
* IF
* LESSTHAN
* LESSTHANEQUAL
* ISOBJECT
* ISARRAY
* ISBOOLEAN
* ISSTRING
* ISNUMBER
* ISNULL
* SWITCHCASE

### DE DATA <a href="#de-data" id="de-data"></a>

As funções deste grupo realizam tratamento, geração e conversão de datas. Para saber mais, leia o artigo [Funções de Data](funcoes-de-data.md):

* FORMATDATE
* NOW
* SUMDATE
* TOISODATE
* DIFFDATE

### DE ARQUIVO <a href="#de-arquivo" id="de-arquivo"></a>

As funções deste grupo realizam consultas a metadados e fazem validações em arquivos. Para saber mais, leia o artigo [Funções de Arquivo](funcoes-de-arquivo.md):&#x20;

* FILEEXISTS
* FILESIZE

### DE JSON <a href="#de-json" id="de-json"></a>

As funções deste grupo realizam operações em objetos do tipo JSON. Para saber mais, leia o artigo [Funções de JSON](funcoes-de-json.md):

* JSONPATH
* TOJSON
* UNESCAPEJSON
* GETELEMENTAT
* LASTELEMENT
* REMOVEAT
* ARRAYTOOBJECT
* OBJECTTOARRAY
* NEWEMPTYOBJECT
* NEWEMPTYARRAY

### MATEMÁTICAS <a href="#matemticas" id="matemticas"></a>

As funções deste grupo realizam operações matemáticas. Para saber mais, leia o artigo [Funções Matemáticas](funcoes-matematicas.md):

* ABS
* CEIL
* DIVIDE
* LOG
* MAX
* MIN
* MOD
* MULTIPLY
* POW
* ROUND
* SQRT
* SUBTRACT
* SUM

### DE STRING <a href="#de-string" id="de-string"></a>

As funções deste grupo realizam tratamentos, operações e conversões de _string_. Para saber mais, leia o artigo [Funções de String](funcoes-de-string.md):

* CAPITALIZE
* CONCAT
* ESCAPE
* INDEXOF
* JOIN
* LASTINDEXOF
* LEFTPAD
* LOWERCASE
* MATCHES
* NORMALIZE
* REPLACE
* RIGHTPAD
* SPLIT
* SUBSTRING
* TOSTRING
* UPPERCASE
* CONTAINS

### DE UTILIDADES <a href="#de-utilidades" id="de-utilidades"></a>

As funções deste grupo realizam operações diversas, que não se enquadram em nenhuma das categorias anteriores. Para saber mais, leia o artigo [Funções de Utilidade](double-braces-funcoes-de-utilidades.md):&#x20;

* BASEDECODE
* BASEENCODE
* UUID
* TOBOOLEAN
* SIZE

## Combinação de funções <a href="#combinao-de-funes" id="combinao-de-funes"></a>

Vamos supor que você precise remover os espaços e garantir que o valor padrão seja enviado caso esteja ausente:

```
{
"nome": "João",
"tipo": " PF "
}
```

Você pode aplicar uma função para atribuir um valor padrão quando o elemento não for passado na entrada e para remover os espaços caso o valor exista:

```
{
"nome": {{ message.nome }},
"tipo": {{ DEFAULT( TRIM(message.tipo), "PJ" ) }}
}
```

**Nota:** Lembre-se que uma expressão Double Braces irá resolver todas as funções contidas nessa expressão ao mesmo tempo, diferente de outras linguagens de programação onde a expressão é resolvida somente após confirmar a condição IF como verdadeira ou falsa. Uma expressão Double Braces irá funcionar da seguinte forma:

Entrada\*\*:\*\*

```
{
    "data": "2022-10-26T03:00:00Z"
}
```

DOUBLE BRACES - Expressão\*\*:\*\*

```
{
    "format": {{ IF(EQUALTO(SIZE(message.data),20),FORMATDATE( message.data, "yyyy-MM-dd'T'HH:mm:ss'Z'", "dd/MM/yyyy"),FORMATDATE( message.data, "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", "dd/MM/yyyy")) }}
}
```

Resultado\*\*:\*\*

```
{

"success": false, "message": "Encountered a configuration error while generating JSON", "error": "com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: com.digibee.doublebraces.service.DoubleBracesConfigurationException: Syntax error parsing double braces expression {{ IF(EQUALTO(SIZE(message.data),20),FORMATDATE( message.data, \"yyyy-MM-dd'T'HH:mm:ss'Z'\", \"dd/MM/yyyy\"),FORMATDATE( message.data, \"yyyy-MM-dd'T'HH:mm:ss.SSS'Z'\", \"dd/MM/yyyy\")) }}: Could not parse date/time evaluating function FORMATDATE. Error: Text '2022-10-26T03:00:00Z' could not be parsed at index 19"

}
```

