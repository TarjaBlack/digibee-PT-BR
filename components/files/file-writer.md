---
description: Conheça o componente e saiba como utilizá-lo.
---

# File Writer



O _**File Writer**_ permite que informações sejam escritas em um arquivo.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** determina o nome do arquivo que será gerado pelo componente com as informações de entrada. Esse parâmetro aceita _Double Braces_.
* **Data:** determina os dados que devem ser escritos no arquivo gerado pelo componente. O campo aceita um _array_ de _strings_ ou uma _string_ simples - caso seja um _array_, cada um dos seus itens será gravado em uma nova linha; mas se o conteúdo for um objeto (e não uma _string_), então a propriedade “Coalesce” precisa ser ativada para evitar a ocorrência de um erro. Esse parâmetro aceita _Double Braces_.
* **Policy For When File Already Exists:** parâmetro no qual é configurado o comportamento a ser seguido caso um arquivo com o mesmo nome já exista na atual execução. Existem as seguintes opções e definições:

\- Append: os dados são adicionados ao arquivo existente;

\- Override: o arquivo existente é sobreposto;

\- Fail: o fluxo é interrompido por um erro.

* **End of Line Policy:** determina a política de uso de caracteres de fim de linha. Existem as seguintes opções e definições:

\- Windows: 2 caracteres são utilizados para final de linha (CR + LF);

\- Unix: somente 1 caractere é utilizado (LF);

\- None: nenhum caractere se aplica.

* **Charset:** determina o código de caracteres que será utilizado para a criação do arquivo. O padrão é o UTF-8.
* **Binary File:** se a entrada de dados para o componente (determinado no parâmetro _**Data**_) for uma _string_ do tipo base64 e esta opção estiver ativada, então o texto será convertido e gravado no arquivo.
* **Coalesce:** se a opção estiver ativada e um valor da mensagem de entrada for correspondente à algum objeto/_array_, os dados informados serão aceitos pelo componente e o arquivo será gravado com sucesso; do contrário, ao receber um valor como objeto/_array_, será apresentado um erro como resultado e será mostrado "false" para a propriedade _**success**_.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "_**success**_".

{% hint style="info" %}
**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. [Para entender como essa linguagem funciona, leia o nosso artigo clicando aqui.](https://docs.digibee.com/documentation/v/pt-br/build/double-braces/funcoes-double-braces)
{% endhint %}

## Manipulação de arquivos no pipeline <a href="#h_449aaa0da6" id="h_449aaa0da6"></a>

O _pipeline_ possui uma área temporária e local para a manipulação de arquivos, que é separada e validada somente durante a execução do fluxo.

Dessa forma, você deve entender o acesso aos arquivos como se fosse feito em um sistema de arquivos virtual. Os nomes de arquivo podem conter qualquer caractere válido e extensões de arquivo, os quais também podem ter um diretório sempre relativo.

Por exemplo: data.csv ou processamento/data.csv.

Qualquer tentativa de acesso a outros diretórios absolutos será bloqueada durante a execução do _pipeline_.

## Fluxo de mensagens <a href="#h_7aad867a94" id="h_7aad867a94"></a>

### **Entrada**

O componente aceita qualquer mensagem de entrada, podendo utilizá-la por meio de _Double Braces_.

### **Saída**

O componente retorna um JSON contendo o nome do arquivo criado e a propriedade _success_ contendo o valor _**true**_.

* **Sem erro**

```
{
"fileName": "data.csv",
"success": true
}
```

* **Com erro**

```
{
"success": false,
"message": "File data.csv already exists.",
"exception":
"com.digibee.pipelineengine.exception.PipelineEngineRuntimeException"
}
```

## File Writer em Ação <a href="#h_77239802e5" id="h_77239802e5"></a>

Abaixo será demonstrado como o componente se comporta em determinada situação e a sua respectiva configuração.

### **Criar arquivo txt contendo uma **_**string**_** enviada por **_**Double Braces**_

Para esse exemplo, será utilizada uma entrada de dados estática e no final o arquivo será lido com o componente [**File Reader**](file-reader.md)**.**

O componente File Writer será configurado da seguinte forma:

<figure><img src="../../.gitbook/assets/File Writer 1.gif" alt=""><figcaption></figcaption></figure>

#### **Entrada**

```
{
"data": "To Kill a Mockingbird\n1984\nHarry Potter and the Philosopher’s Stone\nThe Lord of the Rings\nThe Great Gatsby\nPride and Prejudice\nThe Diary Of A Young Girl\nThe Book Thief\nThe Hobbit\nLittle Women\nFahrenheit 451\nJane Eyre\nAnimal Farm\nGone with the Wind\nThe Catcher in the Rye\nCharlotte’s Web\nThe Lion, the Witch\nThe Grapes of Wrath\nLord of the Flies\nThe Kite Runner\nOf Mice and Men\nA Tale of Two Cities\nRomeo and Juliet\nThe Hitchhikers Guide to the Galaxy\nWuthering Heights\nThe Color Purple\nAlice in Wonderland\nFrankenstein\nThe Adventures of Huckleberry Finn\nSlaughterhouse-Five"
}
```

#### **Saída**

```
{
"fileName": "booklist.txt",
"success": true
}
```

* **fileName:** nome do arquivo que foi escrito
* **success:** se “true”, a operação foi executada com sucesso; se “false”, a propriedade “Fail On Error” foi ativada

#### **Leitura do arquivo criado**

```
{
"data": [
"To Kill a Mockingbird",
"1984",
"Harry Potter and the Philosopher’s Stone",
"The Lord of the Rings",
"The Great Gatsby",
"Pride and Prejudice",
"The Diary Of A Young Girl",
"The Book Thief",
"The Hobbit",
"Little Women",
"Fahrenheit 451",
"Jane Eyre",
"Animal Farm",
"Gone with the Wind",
"The Catcher in the Rye",
"Charlotte’s Web",
"The Lion, the Witch",
"The Grapes of Wrath",
"Lord of the Flies",
"The Kite Runner",
"Of Mice and Men",
"A Tale of Two Cities",
"Romeo and Juliet",
"The Hitchhikers Guide to the Galaxy",
"Wuthering Heights",
"The Color Purple",
"Alice in Wonderland",
"Frankenstein",
"The Adventures of Huckleberry Finn",
"Slaughterhouse-Five"
],
"fileName": "booklist.txt",
"lineCount": 30
}
```

### **Criar arquivo txt contendo um dado em base64 que será convertido ao gravar arquivo**

Para esse exemplo, será utilizada uma entrada de dados estática e, no final, o arquivo será lido com o componente [**File Reader**](file-reader.md)**.**

O componente File Writer será configurado da seguinte forma:

<figure><img src="../../.gitbook/assets/File Writer 2.png" alt=""><figcaption></figcaption></figure>

#### **Entrada**

```
{
"data": "VG8gS2lsbCBhIE1vY2tpbmdiaXJkCjE5ODQKSGFycnkgUG90dGVyIGFuZCB0aGUgUGhpbG9zb3BoZXLigJlzIFN0b25lClRoZSBMb3JkIG9mIHRoZSBSaW5ncwpUaGUgR3JlYXQgR2F0c2J5ClByaWRlIGFuZCBQcmVqdWRpY2UKVGhlIERpYXJ5IE9mIEEgWW91bmcgR2lybApUaGUgQm9vayBUaGllZgpUaGUgSG9iYml0CkxpdHRsZSBXb21lbgpGYWhyZW5oZWl0IDQ1MQpKYW5lIEV5cmUKQW5pbWFsIEZhcm0KR29uZSB3aXRoIHRoZSBXaW5kClRoZSBDYXRjaGVyIGluIHRoZSBSeWUKQ2hhcmxvdHRl4oCZcyBXZWIKVGhlIExpb24sIHRoZSBXaXRjaApUaGUgR3JhcGVzIG9mIFdyYXRoCkxvcmQgb2YgdGhlIEZsaWVzClRoZSBLaXRlIFJ1bm5lcgpPZiBNaWNlIGFuZCBNZW4KQSBUYWxlIG9mIFR3byBDaXRpZXMKUm9tZW8gYW5kIEp1bGlldApUaGUgSGl0Y2hoaWtlcnMgR3VpZGUgdG8gdGhlIEdhbGF4eQpXdXRoZXJpbmcgSGVpZ2h0cwpUaGUgQ29sb3IgUHVycGxlCkFsaWNlIGluIFdvbmRlcmxhbmQKRnJhbmtlbnN0ZWluClRoZSBBZHZlbnR1cmVzIG9mIEh1Y2tsZWJlcnJ5IEZpbm4KU2xhdWdodGVyaG91c2UtRml2ZQ=="
}
```

#### **Saída**

```
{
"fileName": "booklist.txt",
"success": true
}
```

#### **Leitura do arquivo criado**

```
{
"data": [
"To Kill a Mockingbird",
"1984",
"Harry Potter and the Philosopher’s Stone",
"The Lord of the Rings",
"The Great Gatsby",
"Pride and Prejudice",
"The Diary Of A Young Girl",
"The Book Thief",
"The Hobbit",
"Little Women",
"Fahrenheit 451",
"Jane Eyre",
"Animal Farm",
"Gone with the Wind",
"The Catcher in the Rye",
"Charlotte’s Web",
"The Lion, the Witch",
"The Grapes of Wrath",
"Lord of the Flies",
"The Kite Runner",
"Of Mice and Men",
"A Tale of Two Cities",
"Romeo and Juliet",
"The Hitchhikers Guide to the Galaxy",
"Wuthering Heights",
"The Color Purple",
"Alice in Wonderland",
"Frankenstein",
"The Adventures of Huckleberry Finn",
"Slaughterhouse-Five"
],
"fileName": "booklist.txt",
"lineCoun
```

### **Criar arquivo txt contendo uma entrada de dado feita através de um JSON multinível**

Para esse exemplo, será utilizada uma entrada de dados estática e, no final, o arquivo será lido com o componente [**File Reader**](file-reader.md)**.**

O componente File Writer será configurado da seguinte forma:

<figure><img src="../../.gitbook/assets/File Writer 3.jpg" alt=""><figcaption></figcaption></figure>

#### **Entrada**

```
{
"data": {
"products": [
{
"name": "Samsung 4k Q60T 55",
"price": 3278.99
},
{
"name": "Samsung galaxy S20 128GB",
"price": 3698.99
}
]
}
}
```

#### **Saída**

```
{
"fileName": "product.txt",
"success": true
}
```

#### **Leitura do arquivo criado**

```
{
"data": [
"{\"products\":[{\"name\":\"Samsung 4k Q60T 55\",\"price\":3278.99},{\"name\":\"Samsung galaxy S20 128GB\",\"price\":3698.99}]}"
],
"fileName": "product.txt",
"lineCount": 1
}
```

Dessa forma, o JSON com diversos níveis informado ao componente será inserido como uma única linha no arquivo TXT.

### **Arquivo já existe na execução com a política de falha**

Para esse exemplo, dois componentes File Writer serão configurados, um seguido do outro com as opções.

O componente File Writer será configurado da seguinte forma:

<figure><img src="../../.gitbook/assets/File Writer 4.jpg" alt=""><figcaption></figcaption></figure>

Ao final, o _canvas_ terá o seguinte formato:

![](<../../.gitbook/assets/file writer 5.png>)

#### **Entrada**

```
{
"data": "To Kill a Mockingbird\n1984\nHarry Potter and the Philosopher’s Stone\nThe Lord of the Rings\nThe Great Gatsby\nPride and Prejudice\nThe Diary Of A Young Girl\nThe Book Thief\nThe Hobbit\nLittle Women\nFahrenheit 451\nJane Eyre\nAnimal Farm\nGone with the Wind\nThe Catcher in the Rye\nCharlotte’s Web\nThe Lion, the Witch\nThe Grapes of Wrath\nLord of the Flies\nThe Kite Runner\nOf Mice and Men\nA Tale of Two Cities\nRomeo and Juliet\nThe Hitchhikers Guide to the Galaxy\nWuthering Heights\nThe Color Purple\nAlice in Wonderland\nFrankenstein\nThe Adventures of Huckleberry Finn\nSlaughterhouse-Five"
}
```

#### **Saída**

```
{
"success": false,
"message": "File booklist.txt already exists.",
"exception": "com.digibee.pipelineengine.exception.PipelineEngineRuntimeException"
}
```

* **success:** “false” quando a operação falha
* **message:** mensagem sobre o erro
* **exception:** informação sobre o tipo de erro ocorrido
