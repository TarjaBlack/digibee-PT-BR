---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream File Reader Pattern

O _**Stream File Reader Pattern**_ lê um arquivo de texto local em blocos de linha conforme o _pattern_ configurado e dispara _subpipelines_ para processar cada mensagem. Esse recurso deve ser utilizado para arquivos grandes.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** nome do arquivo local.
* **Tokenizer**: XML, PAIR e REGEX. Utilizando a opção XML, é possível informar o nome da _tag_ XML para que o componente envie o bloco que a contenha. Utilizando a opção PAIR, é possível configurar um _token_ de início e um _token_ de término para que o componente retorne ao subfluxo todas as linhas entre ambos os _tokens_. Utilizando a opção REGEX, é necessário informar uma expressão regular para que o componente retorne o bloco entre as expressões regulares.
* **Token**: _token_ que será utilizado para buscar o padrão no arquivo informado.
* **End Token**: _token_ de término. Utilizado somente para o _Tokenizer_ PAIR.
* **Include Tokens**: para a inclusão de _tokens_ de início e término. Utilizado somente para o _Tokenizer_ PAIR.
* **Group**: valor inteiro que determina o valor de agrupamento retornado pelo componente ao encontrar um _match_ com o padrão definido.
* **Element Identifier:** atributo que será enviado em caso de erros.
* **Parallel Execution Of Each Iteration:** ocorre em paralelo com a execução do _loop_.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do _pipeline_ apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro "Fail On Error" não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines_ (onProcess e onException).

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

```
{
"filename": "fileName"
}
```

O “Local File Name” substitui o arquivo local padrão.

### Saída <a href="#sada" id="sada"></a>

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

A manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

O _**Stream File Reader Pattern**_ realiza processamento em lote. Para entender melhor o conceito, clique [aqui](https://intercom.help/godigibee/pt-BR/articles/4541136-processamento-em-lote).

## Stream File Reader Pattern em Ação <a href="#stream-file-reader-pattern-em-ao" id="stream-file-reader-pattern-em-ao"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

* **Utilizando o **_**Tokenizer**_** XML e buscando informações de **_**tags**_** que podem estar em várias linhas**

Dado que se deseja ler o seguinte arquivo XML:

**file.xml**

```
<m:documents>
<m:hashes>
<m:hashe>4rt4</m:hashe>
<m:hashe>6565g</m:hashe>
</m:hashes>
<m:orders xmlns:m="urn:shop" xmlns:cat="urn:shop:catalog">
<m:order>
<id>1</id><date>2014-02-25</date>
</m:order>
<m:order>
<id>2</id><date>2014-02-25</date>
</m:order>
</m:documents>
```

Configurando o componente para apenas retornar o bloco XML da _tag_ "order":

**File Name:** file.xml

**Tokenizer:** XML

**Token:** order

O resultado será 2 subfluxos contendo os valores que estão dentro da _tag_ “order”:

**Primeiro:**

```
<m:order>
<id>1</id><date>2014-02-25</date>
</m:order>
```

**Segundo:**

```
<m:order>
<id>2</id><date>2014-02-25</date>
</m:order>
```

* **Utilizando o **_**Tokenizer**_** PAIR para ler um arquivo onde tenha um **_**token**_** de início e término para cada bloco**

**file.txt**

```
###
Log1: Log info
Log2: Log info
--###
###
Log1: Log info
--###
###
Log1: Log info
Log2: Log info
Log3: Log info
--###
```

**File Name:** file.txt

**Tokenizer:** PAIR

**Token:** ###

**End Token:** --###

**Include Tokens:** desabilitado

O resultado será 3 subfluxos contendo os valores que estão dentro dos _tokens_ de início (###) e término (--###):

**Primeiro:**

```
Log1: Log info
Log2: Log info
```

**Segundo:**

```
Log1: Log info
```

**Terceiro:**

```
Log1: Log info
Log2: Log info
Log3: Log info
```

* **Usando o **_**Tokenizer**_** REGEX para buscar todos as linhas entre padrões**

**file.txt**

```
ID-3591d344-d74f-446e-867a-210d17345b50
Some text
xpto
ID-033e8b36-6b1e-42e8-aeb1-dc8498ffa6cb
Other text
xxx
```

Então deseja-se buscar o padrão:

**ID-\b\[0-9a-f]{8}\b-\[0-9a-f]{4}-\[0-9a-f]{4}-\[0-9a-f]{4}-\b\[0-9a-f]{12}\b**

**File Name:** file.txt

**Tokenizer:** REGEX

**Token:** ID-\b\[0-9a-f]{8}\b-\[0-9a-f]{4}-\[0-9a-f]{4}-\[0-9a-f]{4}-\b\[0-9a-f]{12}\b

O resultado será 2 subfluxos contendo os valores que casam com o padrão REGEX informado.

**Primeiro:**

```
Some text
xpto
```

**Segundo:**

```
Other text
xxx
```

* **Usando o **_**Tokenizer**_** REGEX para buscar todas as linhas entre padrões e agrupando os resultados de 2 em 2**

**file.txt**

```
ID-3591d344-d74f-446e-867a-210d17345b50
Some text
xpto
ID-033e8b36-6b1e-42e8-aeb1-dc8498ffa6cb
Other text
xxx
```

Então deseja-se buscar o padrão:

**ID-\b\[0-9a-f]{8}\b-\[0-9a-f]{4}-\[0-9a-f]{4}-\[0-9a-f]{4}-\b\[0-9a-f]{12}\b**

**File Name:** file.txt

**Tokenizer:** REGEX

**Token:** ID-\b\[0-9a-f]{8}\b-\[0-9a-f]{4}-\[0-9a-f]{4}-\[0-9a-f]{4}-\b\[0-9a-f]{12}\b

**Group:** 2

O resultado será 1 subfluxo contendo os valores que casam com o padrão REGEX informado.

```
Some text
xpto
ID-\b[0-9a-f]{8}\b-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-\b[0-9a-f]{12}\b
{12}\\b
Other text
xxx
```

Quando o _Tokenizer_ REGEX é utilizado no agrupamento, o padrão encontrado como saída é exibido.

**IMPORTANTE:** caso o padrão informado no arquivo não seja encontrado, então o retorno será uma execução com todo o arquivo. Atente-se ao especificar o REGEX.
