---
description: Conheça o componente e saiba como utilizá-lo.
---

# Choice

O **Choice** permite o desvio de fluxo dentro de um _pipeline_. Ele faz parte de um conjunto de componentes que auxilia na organização das integrações.   &#x20;

Dê uma olhada nos parâmetros de configuração desse componente:

* **Label:** define o nome do caminho. Esse nome deve ser único, não podendo se repetir no _pipeline_.
* **Type:** define a estrutura de desvio que o fluxo deve seguir (**When** ou **Otherwise**). Leia a seção [Type](choice.md#type) para saber mais.
* **Type Rule:** define o tipo de linguagem (**Simple** ou **JSON Path**) que será utilizada para a declaração da condição (quando **When** for escolhido no parâmetro **Type**). Leia a seção [Type Rule](choice.md#type-rules) para saber mais.
* **Condition:** declara a condição utilizada para definir se o caminho deve ser executado. Quando as condições previamente definidas gerarem conflito ou causarem uma sobreposição, apenas uma delas será executada (quando **When** for escolhido no parâmetro **Type**).

{% hint style="info" %}
**IMPORTANTE:** os parâmetros de configuração não estarão disponíveis se o componente não estiver conectado a outros componentes no _pipeline_. Uma vez que você. Após conectá-lo corretamente, clique no ponto de conexão para acessar os parâmetros (ícone de engrenagem) como mostrado no detalhe da imagem abaixo:
{% endhint %}

<figure><img src="../../.gitbook/assets/Choice_image detail update_fev2023.png" alt=""><figcaption></figcaption></figure>

## Type

Para trabalhar com esse componente, você precisa conhecer os dois tipos de estrutura do _**Choice**_. Eles são utilizados para criar os caminhos:&#x20;

* **When:** define uma condição que realiza um desvio no seu fluxo para uma linha de execução específica. É necessário ter pelo menos uma condição declarada.&#x20;
* **Otherwise:** a estrutura é executada quando nenhuma das condições **When** é atendida. É necessário ter pelo menos uma condição declarada.&#x20;

## Type Rule <a href="#type-rules" id="type-rules"></a>

### **JSON Path**

Define expressões que passam por um componente JSON para alcançar um subconjunto. Quando você estiver utilizando o _**Choice**_, será feito um _match_ para executar o caminho.\
&#x20;

Imagine que, no passo anterior ao _**Choice**_, o seu fluxo de dados possui a seguinte saída:

```
{
    "cidade" : "Sao Paulo"
}
```

A seguinte condição declarada como **When** validaria a execução do desvio:

```
$.[?(@.cidade == 'Sao Paulo')]
```

&#x20;            &#x20;

Conheça as demais opções para a declaração **JSON Path**:

* **$:** a raiz do objeto ou _array_.
* **.**_**propriedade:**_** ** seleciona uma propriedade específica no objeto relacionado.
* **\['**_**propriedade**_**']:** seleciona uma propriedade específica no objeto relacionado. Coloque apenas aspas simples ao redor do nome da propriedade. Dica: considere essa instrução caso o nome da propriedade contenha caracteres especiais, assim como espaços, ou caso comece com caracteres diferentes de A..Za..z\_.
* **\[**_**n**_**]:** seleciona o elemento _n_ de um _array_. Os índices começam com 0.
* **\[**_**indice1**_**,**_**indice2**_**,**_**…**_**]:** seleciona elementos do _array_ com índices específicos e retorna uma lista.
* **..**_**propriedade:**_** ** recursiva descendente: busca um nome de propriedade decrescentemente e retorna um _array_ de todos os valores com esse nome de propriedade. Sempre retorna uma lista, mesmo que apenas 1 propriedade seja encontrada.
* **\*:** o curinga seleciona todos os elementos em um objeto ou _array_, qualquer que seja os seus nomes ou índices. Por exemplo, endereço.\* significa todas as propriedades do objeto endereço e livro\[\*] significa todos os itens de um _array_ de livro.
* **\[**_**entrada**_**:saida] / \[**_**entrada**_**:]:** seleciona elementos de um _array_ de entrada e até, porém não necessariamente, um _array_ de saída. Se a saída é omitida, selecione todos os _arrays_ até o final do _array_. Uma lista é retornada.
* **\[:**_**n**_**]:** seleciona os primeiros _n_ elementos do _array_. Uma lista é retornada.
* **\[**_**-n**_**:]:** seleciona os últimos _n_ elementos do _array_. Uma lista é retornada.
* **\[?(**_**expressao**_**)]:** expressão de filtro. Seleciona todos os elementos em um objeto ou _array_ que coincidem com o filtro especificado. Uma lista é retornada.
* **\[(**_**expressao**_**)]:** expressões de _script_ podem ser utilizadas no lugar de nomes explícitos de propriedades ou índices. Por exemplo, \[(@.tamanho-1)], que seleciona o último item de um _array_. Aqui, tamanho se refere ao tamanho do _array_ em questão mais do que um arquivo JSON nomeado "tamanho".
* **@:** utilizado em expressões de filtro para fazer referência ao nó atual que está sendo processado.
* **==:** igual a .1 e '1' são considerados o mesmo resultado. Valores de _string_ devem ser anexados em aspas simples (e não em aspas): \[?(@.cor=='vermelho')].
* **!=:** diferente de. Valores de _string_ devem ser anexados em aspas simples.
* **>:** maior que.
* **>=:** maior ou igual a.
* **<:** menor que.
* **<=:** menor ou igual a.
* **=\~:** compatível com uma RedEx Java Script regular. Por exemplo, \[?(@.descricao =\~ /gato.\*/i)] faz _match_ em itens cuja descrição começa com "gato" (ignora maiúsculas e minúsculas).&#x20;
* **!:** utilizado para negar um filtro. Por exemplo, \[?(!@.isbn)] casa itens que não possuem a propriedade "isbn".&#x20;
* **&&:** operador lógico E. Exemplo:

```
[?(@.categoria=='ficcao' && @.preco < 10)]
```

* ||: operador lógico OU. Exemplo:

```
[?(@.categoria=='ficcao' || @.preco < 10)]
```

Leia esse [artigo sobre JSON Path](https://goessner.net/articles/JsonPath/) para saber mais sobre o tema.

### Simple <a href="#simple" id="simple"></a>

É basicamente uma linguagem pequena e simples para avaliar expressões e predicados sem exigir novas dependências ou conhecimento do JSON Path.\
&#x20;             &#x20;

Imagine que, no passo anterior ao _**Choice**_, o seu fluxo de dados possui a seguinte saída:

```
{
    "cidade" : "São Paulo"
}
```

&#x20;A condição declarada como **When** validaria a execução do desvio:

```
#{cidade} == 'São Paulo'
```

&#x20;       &#x20;

Conheça as demais opções para a declaração **Simple**:

* **==:** igual a.
* **=\~:** igual a, ignorando maiúsculas e minúsculas (quando comparando _strings_).
* **>:** maior que.
* **>=:** maior ou igual a.
* **<:** menor que.
* **!=:** diferente.
* **!=\~:** diferente de, ignorando maiúsculas e minúsculas (quando comparando _strings_).
* **regex:** valida uma RegEx contra a _string_ informada. Exemplo: #{cidade} regex 'S.\*'
* **&&:** operador lógico E. Exemplo:

```
 #{cidade} == 'Sao Paulo' && #{estado} == 'SP'
```

* **||:** operador logico OU. Exemplo:

```
#{cidade} == 'Sao Paulo' || #{estado} == 'RJ'
```

&#x20;                    &#x20;

&#x20;**Exemplo:**

<figure><img src="../../.gitbook/assets/Choice_example update_fev2023.png" alt=""><figcaption></figcaption></figure>
