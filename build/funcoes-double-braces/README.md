---
description: Saiba quais são as funções Double Braces e como utilizá-las
---

# Funções Double Braces

Você pode usar funções Double Braces para manipular dados em um _pipeline_.

## Sintaxe

As funções Double Braces são usadas entre dois conjuntos de chaves e um espaço em branco, com o nome da função seguido por uma lista de parâmetros entre parênteses, como abaixo:

```
{{ NOMEDAFUNÇÃO(param1, param2) }}
```

Funções Double Braces são _case-insensitive_, isto é, não diferenciam entre letras maiúsculas e minúsculas. Entretanto, nós recomendamos como uma melhor prática escrevê-las com letras maiúsculas.

## Funções aninhadas

Você pode fazer chamadas a funções Double Braces dentro de outras funções, como abaixo:

```
{{ FUNÇÃOEXTERNA(FUNÇÃOINTERNA(param1, param2), param3) }}
```

Quando usa essa sintaxe, as funções são executadas de dentro para fora. Isto é, no exemplo acima, `FUNÇÃOINTERNA` é executada primeiro e seu _output_ é usado como um parâmetro de `FUNÇÃOEXTERNA`, que é executada por último.

## Lista de funções

Abaixo, listamos as funções Double Braces por grupos baseados em seu uso.

### DE COMPARAÇÃO <a href="#de-comparao" id="de-comparao"></a>

Usadas para comparar _inputs_ booleanos. Para saber mais, leia o artigo [Funções de Comparação](../double-braces/funcoes-double-braces/funcoes-de-comparacao.md):

* AND
* NOT
* OR
* XOR

### NUMÉRICAS <a href="#numricas" id="numricas"></a>

Usadas para manipular valores numéricos. Para saber mais, leia o artigo [Funções Numéricas](../double-braces/funcoes-double-braces/funcoes-numericas.md):

* FORMATNUMBER
* TODOUBLE
* TOINT
* TOLONG

### CONDICIONAIS <a href="#condicionais" id="condicionais"></a>

As funções desse grupo retornam um valor de acordo com um critério específico. Para saber mais, leia o artigo [Funções Condicionais](../double-braces/funcoes-double-braces/funcoes-condicionais.md):

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

Usadas para manipular datas. Para saber mais, leia o artigo [Funções de Data](../double-braces/funcoes-double-braces/funcoes-de-data.md):

* FORMATDATE
* NOW
* SUMDATE
* TOISODATE
* DIFFDATE

### DE ARQUIVO <a href="#de-arquivo" id="de-arquivo"></a>

Usadas para consultar metadados e validar arquivos. Para saber mais, leia o artigo [Funções de Arquivo](../double-braces/funcoes-double-braces/funcoes-de-arquivo.md):&#x20;

* FILEEXISTS
* FILESIZE

### DE JSON <a href="#de-json" id="de-json"></a>

Usadas para manipular objetos JSON. Para saber mais, leia o artigo [Funções de JSON](../double-braces/funcoes-double-braces/funcoes-de-json.md):

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

Usadas para fazer operações matemáticas. Para saber mais, leia o artigo [Funções Matemáticas](../double-braces/funcoes-double-braces/funcoes-matematicas.md):

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

Usadas para manipular _strings_. Para saber mais, leia o artigo [Funções de String](../double-braces/funcoes-double-braces/funcoes-de-string.md):

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

### DE UTILIDADE <a href="#de-utilidades" id="de-utilidades"></a>

Usadas para fazer operações que não se encaixam nas outras categorias. Para saber mais, leia o artigo [Funções de Utilidade](../double-braces/funcoes-double-braces/double-braces-funcoes-de-utilidades.md):&#x20;

* BASEDECODE
* BASEENCODE
* UUID
* TOBOOLEAN
* SIZE
