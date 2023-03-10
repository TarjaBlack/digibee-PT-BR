---
description: Aprenda a usar as funções Double Braces de string
---

# Funções de string

As funções de _string_ são usadas para manipular dados de _string_. Estas são as funções de _string_ que você pode usar com a linguagem Double Braces da Digibee:

## CAPITALIZE <a href="#_u5refs2xpjlr" id="_u5refs2xpjlr"></a>

Coloca o primeiro caractere de uma _string_ em caixa alta. Outros caracteres não são afetados.

### Sintaxe <a href="#_6s6rcbdgcmc6" id="_6s6rcbdgcmc6"></a>

```
CAPITALIZE(value : string) -> string
```

* `value`: a _string_ cuja primeira letra deve ser maiúscula.

Retorna: uma string que é uma versão de value com o primeiro caractere em caixa alta.

### Exemplo de uso <a href="#_x0vw7o6t67vq" id="_x0vw7o6t67vq"></a>

```
{{ CAPITALIZE("hello, world!") }}
```

O resultado esperado é:

```
"Hello, world!"
```

## CONCAT <a href="#_8prry81brr15" id="_8prry81brr15"></a>

Concatena qualquer número de _strings_ em uma única _string_.

### Sintaxe <a href="#_uby7flrwwf94" id="_uby7flrwwf94"></a>

```
CONCAT(*values: string) -> string
```

* `values`: qualquer número de _strings_ a serem concatenadas.

Retorna: a _string_ concatenada.

### Exemplo de uso <a href="#_kh4zq3bj4kzz" id="_kh4zq3bj4kzz"></a>

```
{{ CONCAT("Hello", ", ", "world!") }}
```

O resultado esperado é:

```
"Hello, world!"
```

## CONTAINS <a href="#_qct9pufrayjq" id="_qct9pufrayjq"></a>

Verifica se uma _substring_ está contida em uma determinada _string_.

### Sintaxe <a href="#_458txb5idk20" id="_458txb5idk20"></a>

```
CONTAINS(main_string: string, sub_string: string) -> boolean
```

* `main_string`: a _string_ principal a ser pesquisada.
* `sub_string`: a _substring_ a ser procurada.

Retorna: um valor booleano indicando se a substring foi encontrada ou não. Retorna `true` se a _substring_ for encontrada na string principal e `false`, caso contrário.

### Exemplo de uso <a href="#_5ruj3vqxkwiv" id="_5ruj3vqxkwiv"></a>

```
{{ CONTAINS("Hello, world!", "world") }}
```

O resultado esperado é:

```
true
```

## DEFAULT <a href="#_u0ejuwlrilku" id="_u0ejuwlrilku"></a>

Retorna um valor padrão quando uma referência é feita a um valor nulo ou inexistente.

### Sintaxe <a href="#_dop8rov3lypp" id="_dop8rov3lypp"></a>

```
DEFAULT(value: string, defaultValue: string) -> string
```

* `value`: o valor a ser verificado quanto à nulidade ou inexistência.
* `defaultValue`: o valor padrão a ser retornado se value for nulo ou inexistente.

Retorna: `value`, se value não for nulo ou inexistente, ou `defaultValue`, se for.

### Exemplo de uso <a href="#_gho3jiacv49a" id="_gho3jiacv49a"></a>

Suponha que você esteja usando esta função no parâmetro JSON de um componente JSON Generator que recebe o seguinte _payload_:

```json
{
"nome": "João Silva",
"idade": null
}
```

Você pode usar a função DEFAULT para substituir o valor nulo por uma string "não disponível".

```
{
"nome": "João Silva",
"idade" : {{ DEFAULT(message.idade, "não disponível") }}
}
```

O resultado esperado é:

```json
{
"nome": "João Silva",
"idade": "não disponível"
}
```

Leia este artigo para saber mais sobre como referenciar dados com Double Braces.

## ESCAPE <a href="#_jcnbxsk1rf4u" id="_jcnbxsk1rf4u"></a>

Codifique uma _string_ usando sequências de escape.

### Sintaxe <a href="#_iacdzn8uylg5" id="_iacdzn8uylg5"></a>

```
ESCAPE(value: string, escapeType: string<opcional>) -> string
```

* `value`: a _string_ a ser codificada.
* `escapeType`: o tipo de sequência de escape a ser utilizada. As opções válidas são "JSON", "XML", "CSV" e "HTML". Caso não especificado, assume valor padrão "JSON".

Retorna: uma nova string na qual certos caracteres foram substituídos por sequências de escape.

### Exemplo de uso <a href="#_q7iuh97f1pq" id="_q7iuh97f1pq"></a>

```
{{ ESCAPE("<h1>Hello, world!</h1>", "HTML") }}
```

O resultado esperado é:

```
"&lt;h1&gt;Hello, world!&lt;/h1&gt;"
```

## INDEXOF <a href="#_kswb7z2j6nn1" id="_kswb7z2j6nn1"></a>

Retorna o índice da primeira ocorrência de uma _substring_ dentro de uma _string_ determinada. Essa pesquisa diferencia maiúsculas de minúsculas e o índice começa em 0.

### Sintaxe <a href="#_9c39nu7bpwdg" id="_9c39nu7bpwdg"></a>

```
INDEXOF(main_string: string, sub_string: string, fromIndex: integer<opcional>) -> int
```

* `main_string`: a _string_ principal a ser pesquisada.
* `sub_string`: a _substring_ a ser procurada.
* `fromIndex`: o índice a partir do qual a pesquisa deve começar. Caso não especificado, assume valor padrão 0.

Retorna: um _integer_ indicando o índice da primeira ocorrência da _substring_ na _string_ principal. Se a _substring_ não for encontrada, a função retorna -1.

### Exemplos de uso <a href="#_q7imvveo5mhr" id="_q7imvveo5mhr"></a>

```
{{ INDEXOF("Hello, world!", "world") }}
```

O resultado esperado é:

```
7
```

```
{{ INDEXOF("Hello, world!", "welcome") }}
```

O resultado esperado é:

```
-1
```

## JOIN <a href="#_xefrecgsy97h" id="_xefrecgsy97h"></a>

Concatena uma lista de _strings_ em uma única _string_ com um caractere separador especificado entre cada _string_.

### Sintaxe <a href="#_tjipxi8tdjus" id="_tjipxi8tdjus"></a>

```
JOIN(separator: string, *values: string) -> string
```

* `separator`: uma _string_ representando o caractere separador a ser usado entre cada _string_.
* `values`: qualquer número de _strings_ a serem concatenados.

Retorna: a _string_ concatenada com o caractere separador especificado entre cada _string_ no _input_.

### Exemplos de uso <a href="#_a0rnwz6l4ijv" id="_a0rnwz6l4ijv"></a>

```
{{ JOIN(" ", "Estas","palavras", "são", "separadas","por","espaços") }}
```

O resultado esperado é:

```
"Estas palavras são separadas por espaços"
```

```
{{ JOIN("-", "Estas","palavras", "são","separadas","por","hífens") }}
```

O resultado esperado é:

```
"Estas-palavras-são-separadas-por-hífens"
```

## LASTINDEXOF <a href="#_owe5flwpcov" id="_owe5flwpcov"></a>

Retorna o índice da última ocorrência de uma _substring_ dentro de uma determinada _string_. Essa pesquisa diferencia maiúsculas de minúsculas e o índice começa em 0.

### Sintaxe <a href="#_sthrzot2h1zp" id="_sthrzot2h1zp"></a>

```
LASTINDEXOF(main_string: string, sub_string: string) -> int
```

* `main_string`: a _string_ principal a ser pesquisada.
* `sub_string`: a _substring_ a ser procurada.
* `fromIndex`: o índice a partir do qual a pesquisa deve começar. O padrão é 0.

Retorna: um _integer_ indicando o índice da última ocorrência da _substring_ na _string_ principal. Se a _substring_ não for encontrada, a função retornará -1.

### Exemplos de uso <a href="#_k7sx9ikrxytw" id="_k7sx9ikrxytw"></a>

```
{{ LASTINDEXOF("Hello, world!", "o") }}
```

O resultado esperado é:

```
8
```

```
{{ LASTINDEXOF("Hello, world!", "a") }}
```

Como a substring "a" não está contida na string "Hello, world!", o resultado esperado é:

```
-1
```

## LEFTPAD <a href="#_i5y3iur4q91u" id="_i5y3iur4q91u"></a>

Preenche o lado esquerdo de uma determinada _string_ com um caractere especificado até um tamanho específico.

### Sintaxe <a href="#_19khl617u9dv" id="_19khl617u9dv"></a>

```
LEFTPAD(value: string, length: integer, character:string<opcional>) -> string
```

* `value`: a _string_ de entrada a ser preenchida.
* `length`: o comprimento da string desejada.
* `character`: o caractere que será usado para preencher o lado esquerdo da string de entrada. Por padrão, um espaço em branco.

Retorna: uma string preenchida do comprimento desejado com o caractere especificado preenchendo o lado esquerdo da string de entrada. Se o comprimento da _string_ de entrada já for maior ou igual ao especificado, a _string_ original será retornada.

### Exemplos de uso <a href="#_901u12i46to1" id="_901u12i46to1"></a>

```
{{ LEFTPAD("example", 10, "-")
```

O resultado esperado é:

```
"---example"
```

```
{{ LEFTPAD("hello", 5, "*")
```

Como "hello" já possui 5 caracteres, o resultado esperado é:

```
"hello"
```

## LOWERCASE <a href="#_1qtjpnqc926u" id="_1qtjpnqc926u"></a>

Converte todos os caracteres em minúsculos.

### Sintaxe <a href="#_e2dahugdq9eb" id="_e2dahugdq9eb"></a>

```
LOWERCASE(value: string) -> string
```

* `value`: a _string_ de entrada a ser convertida em letras minúsculas.

Retorna: a _string_ que é o equivalente em minúsculas da _string_ de entrada.

### Exemplo de uso <a href="#_jwtcq8vpgtk4" id="_jwtcq8vpgtk4"></a>

```
{{ LOWERCASE("HELLO, WorLD!") }}
```

O resultado esperado é:

```
"Hello, world!"
```

## MATCHES <a href="#_5twdmzt1o15n" id="_5twdmzt1o15n"></a>

Verifica se uma _string_ corresponde a uma expressão regular.

### Sintaxe <a href="#_sz6pggv20xpg" id="_sz6pggv20xpg"></a>

```
MATCHES(value: string, pattern: string) -> boolean
```

* `value`: uma _string_ que deve ser comparada com a expressão regular fornecida.
* `pattern`: um padrão de expressão regular que deve ser usado para corresponder à _string_ de entrada.

Retorna: true, se a _string_ de entrada corresponder à expressão regular, false, caso contrário.

### Exemplo de uso <a href="#_v2fv78elowng" id="_v2fv78elowng"></a>

```
{{ MATCHES("123-456-7890", "\\d{3}-\\d{3}-\\d{4}") }}
```

O resultado esperado é:

```
true
```

## NORMALIZE <a href="#_qgr0hemlgztw" id="_qgr0hemlgztw"></a>

Transforma quaisquer caracteres especiais em caracteres não especiais.

### Sintaxe <a href="#_kyisoauwfqhp" id="_kyisoauwfqhp"></a>

```
NORMALIZE(value: string) -> string
```

* `value`: a string a ser normalizada.

Retorna: a string normalizada com caracteres especiais substituídos por suas contrapartes não especiais.

### Exemplo de uso <a href="#_m40boknqon1o" id="_m40boknqon1o"></a>

```
{{ NORMALIZE("São Paulo") }}
```

O resultado esperado é:

```
"Sao Paulo"
```

## RANDOMSTRINGS <a href="#_59ckydivpz17" id="_59ckydivpz17"></a>

Gera _strings_ aleatórias dados um conjunto de caracteres e o comprimento da _string_.

### Sintaxe <a href="#_1c5lm1kzig1m" id="_1c5lm1kzig1m"></a>

```
RANDOMSTRINGS(charset: string, length: int) -> string
```

* `charset`: o conjunto de caracteres a ser usado. As opções são: `"ALPHANUMERIC"`, `"ALPHABETIC"` , `"ASCII"`, e `"NUMERIC"`.
* `length`: o comprimento da _string_ de saída.

### Exemplo de uso <a href="#_u9pc3a26p6tc" id="_u9pc3a26p6tc"></a>

```
{{ RANDOMSTRINGS("ALPHANUMERIC",10) }}
```

O _output_ varia porque é aleatório. Um _output_ possível é:

```
"lUbCIs7T3G"
```

## REPLACE <a href="#_ab5usfq04ub0" id="_ab5usfq04ub0"></a>

Substitui todas as ocorrências de uma _substring_ em uma _string_ com base em uma determinada expressão regular.

### Sintaxe <a href="#_kjovog5400n4" id="_kjovog5400n4"></a>

```
REPLACE(value: string, pattern: string, replacement: string) -> string
```

* `value`: a _string_ a ser pesquisada e alterada.
* `pattern`: um padrão de expressão regular que especifica a _substring_ a ser pesquisada.
* `replacement`: uma _string_ que substituirá todas as ocorrências do padrão correspondente na _string_ de entrada.

### Exemplo de uso <a href="#_s6p5s6ciiy91" id="_s6p5s6ciiy91"></a>

```
{{ REPLACE("Hello, world!", "Hello", "Bonjour") }}
```

O resultado esperado é:

```
"Bonjour, world!"
```

## RIGHTPAD <a href="#_abaqq7vaco4v" id="_abaqq7vaco4v"></a>

Preenche o lado direito de uma determinada _string_ com um caractere especificado até um comprimento específico.

### Sintaxe <a href="#_nrl46ji1uy" id="_nrl46ji1uy"></a>

```
RIGHTPAD(value: string, length: integer, character:string<opcional>) -> string
```

* `value`: a _string_ de entrada a ser preenchida.
* `length`: o comprimento da _string_ desejada.
* `character`: o caractere que será usado para preencher o lado direito da _string_ de entrada. Por padrão, um espaço em branco.

Retorna: uma _string_ preenchida do comprimento desejado com o caractere especificado preenchendo o lado direito da _string_ de entrada. Se o comprimento da _string_ de entrada já for igual ou maior que o especificado, a _string_ original será retornada.

### Exemplos de uso <a href="#_96a3m2a6t8ot" id="_96a3m2a6t8ot"></a>

```
{{ RIGHTPAD("example", 10, "-") }}
```

O resultado esperado é:

```
"example---"
```

```
{{ RIGHTPAD("hello", 5, "*") }}
```

Como "hello" já possui 5 caracteres, o resultado esperado é:

```
"hello"
```

## SPLIT <a href="#_nqvcbybjckxv" id="_nqvcbybjckxv"></a>

Divide uma string em um _array_ de strings com base em um padrão de expressão regular especificado.

### Sintaxe <a href="#_88tmjxmdgfdm" id="_88tmjxmdgfdm"></a>

```
SPLIT(value: string, pattern: string) -> Array[string]
```

* `value`: a _string_ a ser dividida.
* `pattern`: um padrão de expressão regular que especifica o ponto de divisão. A _string_ será dividida em todas as ocorrências do padrão.

Retorna: um _array_ de strings resultante da operação de divisão.

### Exemplo de uso <a href="#_dgmmk5jpdi99" id="_dgmmk5jpdi99"></a>

```
{{ SPLIT("Hello, world!", " ") }}
```

O resultado esperado é:

```
["Hello,", "world!"]
```

## STRINGMATCHES <a href="#_ofjxv13z3aye" id="_ofjxv13z3aye"></a>

Retorna um _array_ de todas as expressões correspondentes em uma _string_ que atendem a um determinado padrão de expressão regular.

### Sintaxe <a href="#_a1t1wj98psbs" id="_a1t1wj98psbs"></a>

```
STRINGMATCHES(value: string, pattern: string, patternFlag: string<opcional>) -> Array[string]
```

* `value`: uma _string_ para procurar correspondências.
* `pattern`: um padrão de expressão regular para corresponder à _string_.
* `patternFlag`: o comportamento do mecanismo de expressão regular. Isso pode ser usado para modificar o comportamento de correspondência da expressão regular. Se não for especificado, o mecanismo de expressão regular usará seu comportamento padrão. As opções são:
  * `CANON_EQ`: ativa a correspondência de equivalência canônica de caracteres Unicode. Quando esse _pattern flag_ é ativado, os caracteres que parecem idênticos são correspondidos, mesmo que tenham codepoints diferentes no Unicode.
  * `CASE_INSENSITIVE`: desativa a diferenciação de maiúsculas e minúsculas.
  * `COMMENTS`: permite comentários no padrão de expressão regular. Você pode adicionar comentários após uma hashtag #.
  * `DOTALL`: ativa o modo "dotall", que permite que um ponto. corresponda ao caractere de nova linha\n.
  * `LITERAL`: quando este sinalizador é especificado, a string de entrada que especifica o padrão é tratada como uma sequência de caracteres literais. Metacaracteres ou sequências de escape na sequência de entrada não terão nenhuma interpretação especial.
  * `MULTILINE`: ativa a correspondência em várias linhas.
  * `UNICODE_CASE`: permite correspondência sem distinção entre maiúsculas e minúsculas de caracteres Unicode, levando em consideração as _case folding rules_ do Unicode.
  * `UNICODE_CHARACTER_CLASS`: permite classes de caracteres Unicode no padrão de expressão regular.
  * `UNIX_LINES`: altera o comportamento dos metacaracteres ^ e $ para coincidir com o início e o fim de uma linha, respectivamente, em vez do início e do fim da _string_ de entrada.

Retorna: um _array_ de todas as expressões correspondentes na _string_ que satisfazem o padrão inserido.

### Exemplo de uso <a href="#_o90k2cjhdf73" id="_o90k2cjhdf73"></a>

```
{{ STRINGMATCHES("Hello, world!", "hello", "CASE_INSENSITIVE") }}
```

O resultado esperado é:

```
["Hello"]
```

## SUBSTRING <a href="#_4lv8cj2bw3yp" id="_4lv8cj2bw3yp"></a>

Extrai uma _substring_ de uma determinada _string_.

### Sintaxe <a href="#_zbja9kv9tu53" id="_zbja9kv9tu53"></a>

```
SUBSTRING(value: string, start: int, end: int<opcional>, throwIndexOutOfBoundError: boolean<opcional>) -> string
```

* `value`: a _string_ original da qual a _substring_ deve ser extraída.
* `start`: o índice inicial da _substring_. O índice começa em 0.
* `end`: o índice final da _substring_. Se não for fornecido, a extração terminará no último caractere da _string_ original.
* `throwIndexOutOfBoundError`: se `true`, um erro será gerado se os índices fornecidos estiverem fora do intervalo. Caso contrário, a string original será retornada. Assume valor `true` por padrão.

Retorna: a _substring_ extraída da _string_ original.

### Exemplo de uso <a href="#_yx33otwo5z89" id="_yx33otwo5z89"></a>

```
{{ SUBSTRING("Hello, world!", 0, 5) }}
```

O resultado esperado é:

```
"Hello"
```

### TOSTRING <a href="#_wkohwbnpqdjx" id="_wkohwbnpqdjx"></a>

Converte um objeto em sua representação de _string_.

### Sintaxe <a href="#_qhjkeg4256p" id="_qhjkeg4256p"></a>

```
TOSTRING(object: any) -> string
```

* `object`: o objeto a ser convertido em uma _string_. Pode ser de qualquer tipo.

### Exemplo de uso <a href="#_z38h9j3mb06s" id="_z38h9j3mb06s"></a>

```
{{ TOSTRING(123) }}
```

O resultado esperado é:

```
"123"
```

## TRIM <a href="#_r5osknm614n5" id="_r5osknm614n5"></a>

Remove espaços em branco no início e no final de uma string.

### Sintaxe <a href="#_yg6q0zbm7yuu" id="_yg6q0zbm7yuu"></a>

```
TRIM(value: string) -> string
```

* `value`: a _string_ a ser aparada.

Retorna: uma string que é uma versão aparada de `value`.

### Exemplo de uso <a href="#_3rybn846ywry" id="_3rybn846ywry"></a>

```
{{ TRIM(" Hello, world! ") }}
```

O resultado esperado é:

```
"Hello, world!"
```

## UNESCAPE <a href="#_vwrtkku5t0ab" id="_vwrtkku5t0ab"></a>

Decodifica uma _string_ que possui sequências de escape.

### Sintaxe <a href="#_kxdb7tczlzfb" id="_kxdb7tczlzfb"></a>

```
UNESCAPE(value: string, escapeType: string<opcional>) -> string
```

* `value`: a _string_ a ser decodificada.
* `escapeType`: o tipo de sequência de escape a ser utilizada. As opções válidas são `"JSON"`, `"XML"`, `"CSV"` e `"HTML"`. O padrão é `"JSON"`.

Retorna: uma nova _string_ na qual certos caracteres foram substituídos por sequências de escape.

### Exemplo de uso <a href="#_kwxq4uz99533" id="_kwxq4uz99533"></a>

```
{{ UNESCAPE("&lt;h1&gt;Hello, world!&lt;/h1&gt;", "HTML") }}
```

O resultado esperado é:

```
"<h1>Hello, world!</h1>"
```

## UPPERCASE <a href="#_8fagsvhi79b4" id="_8fagsvhi79b4"></a>

Converte todos os caracteres em maiúsculas.

### Sintaxe <a href="#_tn6cmucn4z5a" id="_tn6cmucn4z5a"></a>

```
UPPERCASE(value: string) -> string
```

* `value`: a _string_ de entrada cujos caracteres devem ser convertidos em letras maiúsculas.

Retorna: o equivalente maiúsculo da _string_ de entrada.

### Exemplo de uso <a href="#_ifo9sfjnp4ap" id="_ifo9sfjnp4ap"></a>

```
{{ UPPERCASE("Hello, world!") }}
```

O resultado esperado é:

```
"HELLO, WORLD!"
```
