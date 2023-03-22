---
description: Conheça o componente e saiba como utilizá-lo.
---

# File Reader

O **File Reader** lê um arquivo local e o converte para uma estrutura JSON que pode ser manipulada dentro do _pipeline_. O componente suporta a leitura de arquivos textos multi-linha ou arquivos binários.&#x20;

Dê uma olhada nos parâmetros de configuração do componente:

<figure><img src="../../.gitbook/assets/File Reader.gif" alt=""><figcaption></figcaption></figure>

* **File Name:** arquivo local a ser lido.
* **Charset:** nome do código de caracteres para a leitura do arquivo (padrão UTF-8).
* **Check File Size:** se a opção estiver habilitada, o **Maximum File Size** especificado será verificado.
* **Binary File:** se “verdadeiro”, o arquivo é considerado binário e a leitura consiste em uma _string_ com a representação BASE64 do conteúdo do arquivo; se "falso", o arquivo é lido como texto.
* **Maximum File Size:** especifica o tamanho máximo permitido (em _bytes_); caso o tamanho do arquivo seja superior ao valor informado, então um erro de leitura será lançado.
* **Read As A Single String:** se "verdadeiro", o arquivo texto será lido como uma única _string_; se "falso", o arquivo texto será lido como um _array_ de _strings_ em que cada item representa uma linha do arquivo.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Como é feita a leitura de arquivos textos? <a href="#como--feita-a-leitura-de-arquivos-texto" id="como--feita-a-leitura-de-arquivos-texto"></a>

Os arquivos textos são lidos linha a linha. Uma estrutura é retornada na saída do componente, com todas as linhas que foram lidas:

```
{

"data" : [

 "linha 1",

 "linha 2",

  ...

],

"fileName": "",

"lineCount": 0

}
```

* **data:** contém um vetor JSON de linhas convertidas
* **filename:** nome do arquivo utilizado como fonte para o componente
* **lineCount:** quantidade de linhas lidas do arquivo

Caso o parâmetro **Read As A Single String** passe como "verdadeiro", então a estrutura retornada vai conter todas as linhas do arquivo lidas em um único _string_:

```
{

"data" : [

 "linha 1\r\nlinha2\r\nlinha n\r\n"

],

"fileName": "",

"lineCount": 1

}
```

&#x20;    \
Note que, nesse caso, a leitura das linhas inclui o(s) caracter(es) de quebra de linha. Geralmente, se o arquivo for criado em sistemas baseados em Unix, somente a quebra de linha com \n será retornada. Por outro lado, se o arquivo for criado em sistemas baseados em Windows, será retornada a quebra de linha com  \r\n.

## Lidando com conjunto de caracteres (Charset) <a href="#lidando-com-conjunto-de-caracteres-charset" id="lidando-com-conjunto-de-caracteres-charset"></a>

Para a leitura de arquivos-texto, é importante definir o conjunto de caracteres com o mesmo valor utilizado durante a criação do arquivo. Caso um conjunto de caracteres incompatível seja utilizado, o arquivo texto poderá ser lido e interpretado de maneira incorreta. Isso leva a imprecisões em caracteres especiais, assim como letras com acentos e outros.   &#x20;

## Como é feita a leitura de arquivos binários? <a href="#como--feita-a-leitura-de-arquivos-binrios" id="como--feita-a-leitura-de-arquivos-binrios"></a>

Arquivos binários não podem ter seu conteúdo expresso de forma natural em propriedades dentro de mensagens JSON, pois muitos dos caracteres binários não são "imprimíveis". Dessa forma, o conteúdo de arquivos binários é transformado em um _string_ base64:

```
{

"data" : "VGhpcyBpcyBhIHRlc3QuCg==",

"fileName": "",

"lineCount": 0

}
```

Note que, no caso acima, a propriedade "data" não é apresentada como um _array_ de linhas, mas sim como um único _string_ em base64.      &#x20;

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ é feita de forma protegida. Todos os arquivos são acessados apenas em um diretório temporário, que é criado a cada execução do _pipeline_.
{% endhint %}
