---
description: >-
  Saiba quais são as funções de string associadas aos Double Braces e como
  utilizá-las.
---

# Funções de String

As funções foram criadas para:

* acelerar ainda mais a criação das suas integrações
* diminuir a complexidade dos seus _pipelines_
* simplificar conversões e transformações dos dados durante o fluxo dos seus _pipelines_

As funções de _string_ realizam tratamentos, operações e conversões de _string_ e estão disponíveis para componentes que suportam expressões com _Double Braces_. Para saber como passar informações para os componentes utilizando esse recurso, clique [aqui](../../funcoes-double-braces/).

### DEFAULT

Essa função em _Double Braces_ aplica um valor padrão (_default_) quando há uma referência a um valor nulo ou inexistente.

**Sintaxe**

```
DEFAULT(value:string, defaultValue:string)
```

Vamos supor que você queira atribuir um valor padrão a uma determinada propriedade com valor nulo (_null_):

```
{
  "name": null
}
```

Você pode usar a função DEFAULT da seguinte forma:

```
{
  "name": {{ DEFAULT(message.firstName, "Jacob") }}
}
```

O resultado esperado será:

```
{
  "name": "Jacob"
}
```

### TRIM

Essa função em _Double Braces_ remove espaços em branco no começo e ao final de uma _string_.

**Sintaxe**

```
TRIM(value:string)
```

Digamos que você queira remover os espaços em branco de uma _string_:

```
{
  "name": "   John Smith       "
}
```

Você pode fazer o seguinte:

```
{
  "fullName": {{ TRIM(message.name) }}
}
```

O resultado esperado será:

```
{
  "fullName": "John Smith"
}
```

### CAPITALIZE <a href="#capitalize" id="capitalize"></a>

Essa função em _Double Braces_ capitaliza uma _string_ ao alterar o primeiro caractere para letra maiúscula. Os outros caracteres não são alterados.

**Sintaxe**

```
CAPITALIZE(value:string)
```

Digamos que você precise capitalizar uma _string_. Você pode fazer o seguinte:

```
{
"name": {{ CAPITALIZE("hi, my name is jacob") }}
}
```

O resultado esperado será:

```
{
"name": "Hi, my name is jacob"
}
```

### CONCAT <a href="#concat" id="concat"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função é aplicada para concatenar parâmetros e transformá-los em uma _string_.

**Sintaxe**

```
CONCAT(, , )
```

**Regras**

* ao menos 2 parâmetros são necessários
* concatenar _null_ é o mesmo que concatenar "" (_string_ vazia)
* concatenação sempre retorna _string_
* o _campoX_ pode ser de qualquer tipo de dados, que será convertido para _string_ na concatenação

Veja um exemplo simples aplicado abaixo:

**Entrada de um componente Transformer**

```
{
"nome": "teste",
"id": " - 123",
"a": null,
"b": {
"nome": "qwert",
"id": "yuiop"
},
"c": -89912
}
```

**Utilização da função CONCAT:**

```
{
"concat": {{ CONCAT(message.nome, message.id, message.a, message.b, message.c) }}
}
```

### ESCAPE <a href="#escape" id="escape"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função é aplicada para manter os caracteres que necessitam de um _escape_ mesmo após a conversão para outro elemento. Ela deverá ser utilizada, por exemplo, quando é desejável persistir um objeto JSON que está em formato de _string_ em um banco de dados.

**Sintaxe**

```
ESCAPE(valor:string, escapeType:string<optional>)
```

Veja a seguir um exemplo simples:

```
{"jsonString": "{\"a\": 1,\"b\": 2}"}
```

A função pode ser aplicada para um _escape_:

```
{"texto": {{ ESCAPE(message.jsonString) }}}
```

Além disso, é possível especificar o tipo de _escape_ que deve ser aplicado através do parâmetro opcional _escapeType_. Nele são aceitos os valores _"CSV"_, _"HTML"_, _"JSON"_ e _"XML"_. Caso o parâmetro não seja informado, será assumido o valor _"JSON"_ por padrão.

Digamos que você possua o objeto abaixo e precise aplicar o _escape_ para um texto no formato CSV:

```
{
"text": "John,33,\"São Paulo\",Brazil,true"
}
```

Para isso, basta fazer a chamada da função conforme abaixo:

```
{
"text": {{ ESCAPE(message.text, "CSV") }}
}
```

O resultado da execução da função será o seguinte:

```
{
"text": "\"John,33,\"\"São Paulo\"\",Brazil,true\""
}
```

Para os demais tipos, a aplicação da função é a mesma dependendo apenas do tipo de texto que deverá ser tratado. Caso seja informado algum tipo de _escape_ não esperado pela função, será lançada uma exceção.

### UNESCAPE <a href="#h_13a166924e" id="h_13a166924e"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função é aplicada para remover os _escapes_ contidos nos caracteres de um texto. Ela deverá ser utilizada, por exemplo, quando é desejável fazer a leitura de um objeto JSON que está em formato de _string_ persistido em um banco de dados.

**Sintaxe**

```
UNESCAPE(valor:string, escapeType:string<optional>)
```

Veja a seguir um exemplo simples:

```
{
"jsonString": "{\\\"a\\\": 1,\\\"b\\\": 2}"
}
```

A função pode ser aplicada para um ESCAPE:

```
{
"texto": {{ UNESCAPE(message.jsonString) }}
}

```

Além disso, é possível especificar o tipo de escape que deve ser removido através do parâmetro opcional _escapeType_. Nele são aceitos os valores _"CSV"_, _"HTML"_, _"JSON"_ e _"XML"_. Caso o parâmetro não seja informado, será assumido o valor _"JSON"_ por padrão.

Digamos que você possua o objeto abaixo e precise remover o escape de um texto no formato CSV:

```
{
"text": "\"John,33,\"\"São Paulo\"\",Brazil,true\""
}
```

Para isso, basta fazer a chamada da função conforme abaixo:

```
{
"text": {{ UNESCAPE(message.text, "CSV") }}
}
```

O resultado da execução da função será o seguinte:

```
{
"text": "John,33,\"São Paulo\",Brazil,true"
}
```

Para os demais tipos, a aplicação da função é a mesma dependendo apenas do tipo de texto que deverá ser tratado. Caso seja informado algum tipo de _escape_ não esperado pela função, será lançada uma exceção.

### INDEXOF <a href="#indexof" id="indexof"></a>

Essa função em _Double Braces_ retorna o índice dentro da primeira ocorrência de uma _string_ referente a uma _substring_ especificada.

**Sintaxe**

```
INDEXOF(str: string, strSearch: string, fromIndex:integer<optional>)
```

Digamos que você precise buscar o valor "planet" dentro da _string_ "Hello planet earth, you are a great planet." e queira saber qual é o índice de início dessa ocorrência:

```
{{ INDEXOF("Hello planet earth, you are a great planet.", "planet") }}
```

O resultado será: 6

Caso você precise buscar em uma _string_ a partir de determinado índice:

```
{{ INDEXOF("Hello planet earth, you are a great planet.", "tree", 3) }}
```

No caso acima, você está buscando a partir do índice 3. Como não será encontrado nenhum valor com as especificações passadas, então será retornado -1.

### JOIN <a href="#join" id="join"></a>

Essa função em _Double Braces_ retorna uma nova _string_ composta por cópias dos elementos unidos com uma cópia do delimitador especificado.

**Sintaxe**

```
JOIN(delimiter:string, value1:string, value2:string, ...., valueN:string)
```

* **delimiter:** delimitador a ser incorporado por cada _string_
* **values:** _string_ a ser unido

Digamos que você precise unir algumas _strings_ com um delimitador. Você pode fazer o seguinte:

```
{
"test": {{ JOIN("-", "I", "love", "this", "function") }}
}
```

O resultado esperado será:

```
{
"test": "I-love-this-function"
}
```

### LASTINDEXOF <a href="#lastindexof" id="lastindexof"></a>

Essa função em _Double Braces_ permite localizar a última ocorrência de uma sequência de caracteres em uma _string_. A função retorna o número de índice em que se inicia a sequência, realiza a busca de caracteres do final para o início da _string_ e retorna -1 se o caractere não é encontrado. A última ocorrência da _string_ vazia ("") é considerada um valor do índice.

**Sintaxe**

```
LASTINDEXOF(str: string, strSearch: string, fromIndex:integer<optional>)
```

Digamos que você queira buscar o valor "planet" dentro da _string_ "Hello planet earth, you are a great planet." e queira saber qual é o índice de início dessa ocorrência:

```
{{ LASTINDEXOF("Hello planet earth, you are a great planet.", "planet") }}
```

O resultado será: 36

### LEFTPAD <a href="#leftpad" id="leftpad"></a>

Essa função em _Double Braces_ adiciona preenchimentos à esquerda de uma _string_ com uma _string_ especificada.

**Sintaxe**

```
LEFTPAD(value:string, size:number, [padding:string - optional])
```

* **value:** _string_ a ser preenchida
* **size:** tamanho total do preenchimento / da _string_ a ser preenchida
* **padding:** caractere do preenchimento (opcional)

Digamos que você precise adicionar um preenchimento à esquerda de uma _string_. Você pode fazer o seguinte:

```
{
"test": {{ LEFTPAD("xpto", 10, "-") }}
}
```

O resultado esperado será:

```
{
"test": "------xpto"
}
```

**IMPORTANTE:** se você não especificar o parâmetro "padding", então o preenchimento será feito com um espaço em branco.

### LOWERCASE <a href="#lowercase" id="lowercase"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função é aplicada para retornar o valor da _string_ em letras minúsculas.

**Sintaxe**

LOWERCASE(string)

```
{
“a”: "2AAA"
}
{
"lc": {{ LOWERCASE( message.a ) }}
}
```

O retorno dessa função será 2aaa.

### MATCHES <a href="#matches" id="matches"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função procura por toda a _string_, ou seja, o padrão (regex) que você está procurando deve ser exatamente igual à _string_ sendo usada para a procura.

**Sintaxe**

```
MATCHES(string, regex )
```

Vamos supor que você precisa saber se o campo está no formato de "cep" válido:

```
{
"cep": "01200-030"
}
```

No exemplo abaixo o valor "true" será atribuído, pois bate com a _regex_ passada:

```
{
"cepValido": {{ MATCHES( message.cep, "[0-9]{5}-[0-9]{3}" ) }}
}
```

O retorno dessa função será "true" ou "false".

### NORMALIZE <a href="#normalize" id="normalize"></a>

Essa função em _Double Braces_ normaliza uma sequência de valores em caracteres.

**Sintaxe**

```
NORMALIZE(value:string)
```

* **value:** _string_ a ser normalizada

Digamos que você precise normalizar uma _string_. Você pode fazer o seguinte:

```
{"test": {{ NORMALIZE("àèìòùęëæoœçáíéúūãõ") }}}
```

O resultado esperado será:

```
{"test": "aeioueeocaieuuao"}
```

### REPLACE <a href="#replace" id="replace"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função substitui cada _substring_ da _string_ que corresponde à expressão regular fornecida com a substituição que se deseja realizar.

**Sintaxe**

```
REPLACE(valor, "regExp", "valor-novo")
```

* **regExp:** expressão regular a ser informada como _string_

O resultado será uma _string_ ou _null_.

Veja a seguir um exemplo simples:

```
{
"string": "ABCDabcd",
"object": {
"this is an object": true
},
"text": "this is a test" ,
"acentos": "ÁÂÃáâãÉéíÌÍÓóÛÙúÇç"
}
```

**Exemplo de aplicação:**

```
{
"replace_simple": {{REPLACE(message.string, "[A-Z]", ".")}},
"replace_object": {{REPLACE(message.object, "\\\"", "'")}},
"replace_text": {{REPLACE(message.text, "a test", "my test")}},
"acentos": {{ REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(REPLACE(message.XML,"[\\xE0-\\xE6]", "a"),"[\\xC0-\\xC6]", "A"),"[\\xE8-\\xEB]", "e"),"[\\xC8-\\xCB]", "E"),"[\\xEC-\\xEF]", "i"),"[\\xCC-\\xCF]", "I"),"[\\xF2-\\xF6]", "o"),"[\\xD2-\\xD6]", "O"),"[\\xF9-\\xFC]", "u"),"[\\xD9-\\xDC]", "U"),"\\xE7", "c"),"\\xC7", "C") }}
}
}
```

### RIGHTPAD <a href="#rightpad" id="rightpad"></a>

Essa função em _Double Braces_ adiciona preenchimentos à direita de uma _string_ com uma _string_ especificada.

**Sintaxe**

```
RIGHTPAD(value:string, size:number, [padding:string - optional])
```

* **value:** _string_ a ser preenchida
* **size:** tamanho do preenchimento
* **padding:** caractere do preenchimento (opcional)

Digamos que você precise adicionar um preenchimento à direita de uma _string_. Você pode fazer o seguinte:

```
{
"test": {{ RIGHTPAD("xpto", 10, "-") }}
}
```

O resultado esperado será:

```
{
"test": "xpto------"
}
```

Se você não especificar o parâmetro "padding", então o preenchimento será feito com um espaço em branco.

### SPLIT <a href="#h_6ef80ac1e3" id="h_6ef80ac1e3"></a>

Essa função em _Double Braces_ divide uma _string_ de acordo com a expressão regular especificada (regex).

**Sintaxe**

```
SPLIT(value:string, regex:string)
```

* **value:** _string_ a ser normalizada
* **regex:** expressão regular delimitadora

Digamos que você precise dividir uma _string_ com um _regex_. Você pode fazer o seguinte:

```
{
"test": {{ SPLIT("aaa,bbb", ",") }},
"test2": {{ SPLIT("123,abb", "\\.") }}
}
```

O resultado esperado será:

```
{
"test": ["aaa", "bbb"],
"test2": ["123", "abb"]
}
```

### SUBSTRING <a href="#substring" id="substring"></a>

Essa função em _Double Braces_ retorna uma _string_ derivada da sua própria _substring_. A _substring_ começa no "beginIndex" especificado e se estende até o caractere no índice "endIndex".

**Sintaxe**

```
SUBSTRING(value:string, beginIndex:number, [endIndex:number - optional], throwIndexOutOfBoundError:boolean - optional])
```

* **value:** _string_
* **beginIndex:** índice inicial, inclusivo
* **beginIndex:** índice final, exclusivo (opcional)
* **throwIndexOutOfBoundError:** se "true", uma exceção será lançada caso exista algum índice fora da exceção vinculada; do contrário, a _string_ passada será retornada - "true" é padrão (se "beginIndex" for negativo, ou "endIndex" for maior do que o tamanho do objeto da _string_, ou "beginIndex" for maior que "endIndex", uma exceção será lançada)

Digamos que você precise extrair uma _substring_ de uma _string_. Você pode fazer o seguinte:

```
{
"test": {{ SUBSTRING("aaS2fdeS", 3) }},
"test2": {{ SUBSTRING("aaS2fdeS", 3, 5) }},
"test3": {{ SUBSTRING("qqq", 20, 30, false) }}
}
```

O resultado esperado será:

```
{
"test": "2fdeS",
"test2": "2f",
"test3": "qqq"
}
```

Para esses casos, uma exceção será lançada:

```
{{ SUBSTRING("qqq", 20, 30) }} or {{ SUBSTRING("qqq", 20, 30, true) }}
```

ou

```
{{ SUBSTRING("qqq", 20, null, false) }}
```

### TOSTRING <a href="#tostring" id="tostring"></a>

Essa função em _Double Braces_ converte qualquer coisa para um formato _string_.

**Sintaxe**

```
TOSTRING(value:any)
```

* **value:** valor a ser convertido para _string_

Digamos que você precise passar um valor para _string_. Você pode fazer o seguinte:

```
{
"number": {{ TOSTRING(1) }},
"string": {{ TOSTRING("A") }},
"boolean": {{ TOSTRING(false) }},
"null": {{ TOSTRING(null) }}
}
```

O resultado esperado será:

```
{
"number": "1",
"number": "A",
"number": "false",
"number": ""
}
```

Também é possível passar um _array_ ou um objeto para _string_.

### UPPERCASE <a href="#h_625a0adb6b" id="h_625a0adb6b"></a>

Utilizando _Double Braces_, você pode combinar a função com o acesso ao elemento do JSON de entrada de um componente.

A função é aplicada para retornar o valor da _string_ em letras maiúsculas.

**Sintaxe**

UPPERCASE(string)

```
{
“a”: "2aaa"
}
{
"uc": {{ UPPERCASE( message.a ) }}
}
```

O retorno dessa função será 2AAA.

### CONTAINS <a href="#h_d60222ba92" id="h_d60222ba92"></a>

Essa função permite que você verifique se um determinado valor está contido em uma _string_.

**Sintaxe**:

CONTAINS(_string_, _value_)

Digamos que você precise verificar se a _string_ abaixo contém o valor "function":

```
{
"field": "Testing the new function CONTAINS()"
}
```

Verificando:

```
{
"contains": {{ CONTAINS(message.field, "function") }}
}
```

O resultado será:

```
{
"contains": true
}
```

### **RANDOMSTRINGS** <a href="#h_c8ce1fb4d6" id="h_c8ce1fb4d6"></a>

Essa função permite que você gere _strings_ randômicas com base em um _charset_ e um tamanho.

**Sintaxe**:

RANDOMSTRINGS(_charset_, _size_)

Digamos que você precise gerar _strings_ randômicas com base em diferentes _charsets_ e com tamanhos de 20 caracteres.

Gerando as _strings_:

```
{
"alphanumeric": {{ RANDOMSTRINGS("ALPHANUMERIC", 20) }},
"ascii": {{ RANDOMSTRINGS("ASCII", 20) }},
"numeric": {{ RANDOMSTRINGS("NUMERIC", 20) }},
"alphabetic": {{ RANDOMSTRINGS("ALPHABETIC", 20) }}
}
```

O resultado será:

```
{
"alphanumeric": "Oj3DApYQL7uTCodbXlXq",
"ascii": "GV>o8G/pNFofal.A.14X",
"numeric": "02747673464573026135",
"alphabetic": "bOHtZafvGOpdltVrrcEu"
}
```

Os _charsets_ aceitos são _ALPHANUMERIC_, _ASCII_, _NUMERIC_ e _ALPHABETIC_, __ e o tamanho limite da _string_ é de 1000 caracteres.

Conheça também as funções:

* [de comparação](funcoes-de-comparacao.md)
* [numéricas](funcoes-numericas.md)
* [condicionais](funcoes-condicionais.md)
* [de data](funcoes-de-data.md)
* [de arquivo](funcoes-de-arquivo.md)
* [de JSON](funcoes-de-json.md)
* [matemáticas](funcoes-matematicas.md)
* [de utilidades](double-braces-funcoes-de-utilidades.md)

**STRINGMATCHES**

Essa função permite realizar buscas de valores dentro de uma _String_ com base em uma _Regex_, retornando os resultados encontrados dentro de um _array_.

**Sintaxe:**&#x20;

```
STRINGMATCHES(value: string, regex: string, patternFlag: string)
```

* **value:** _string_ a ser preenchida
* **regex:** será utilizado na busca
* **patternFlag:** flag que pode definir um padrão para o match da regex (opcional)

**Obs:** Segue abaixo a tabela das _patternFlags_ válidas:

\
**CANON\_EQ**

Habilita a equivalência canônica.

**CASE\_INSENSITIVE**

Ativa a correspondência que não diferencia maiúsculas de minúsculas.

**COMMENTS**

Permite espaços em branco e comentários no padrão.

**DOTALL**

Ativa o modo de pontos.

**LITERAL**

Habilita a análise literal do padrão.

**MULTILINE**

Ativa o modo multilinha.

**UNICODE\_CASE**

Ativa a dobra de maiúsculas e minúsculas com reconhecimento _unicode_.

**UNICODE\_CHARACTER\_CLASS**

Habilita a versão _‘unicode’_ de classes de caracteres predefinidas e classes de caracteres _posix_.

**UNIX\_LINES**

Habilita o modo de linhas Unix.

### Digamos que você queira fazer as buscas abaixo. <a href="#h_0dd73d08fc" id="h_0dd73d08fc"></a>



Gerando as _‘strings’_:

```
{"normal": {{ STRINGMATCHES("7801111111blahblah  780222222 mumbojumbo7803333333 thisnthat 7804444444", "780{1}\\d{7}") }},"case_sensitive": {{ STRINGMATCHES("Para maiores informações, veja o Capítulo 3.4.5.1", "(capítulo \d+(\.\d)*)") }},"case_insensitive": {{ STRINGMATCHES("Para maiores informações, veja o Capítulo 3.4.5.1", "(capítulo \d+(\.\d)*)", "CASE_INSENSITIVE") }}}
```

O resultado será:

```
{"normal": [ "7801111111",  "7803333333",  "7804444444" ],"case_sensitive": [],"case_insensitive": ["Capítulo 3.4.5.1"] }
```

\
