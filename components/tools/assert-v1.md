---
description: Conheça o componente e saiba como utilizá-lo.
---

# Assert V1

O _**Assert V1**_ permite criar a interrupção da execução de seu _pipeline_ quando uma condição definida por você não for atendida. Essa condição será avaliada de acordo com itens da mensagem do _pipeline_ que o componente _Assert_ receber, através de uma Linguagem de Expressão.

Dê uma olhada nos parâmetros de configuração do componente:

* **Condition:** condição passada através da Linguagem de Expressão SIMPLE, que quando não for verdadeira, fará com que a execução do _pipeline_ seja interrompida.
* **Error Message:** define a mensagem de erro que é retornada pelo _pipeline_ quando a condição passada não for verdadeira.
* **HTTP Status Code:** status HTTP de retorno do componente.

### Fluxo de Mensagens <a href="#h_3754861f51" id="h_3754861f51"></a>

#### Entrada <a href="#h_2c44e91511" id="h_2c44e91511"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela através da Linguagem de Expressão SIMPLE.

#### Saída <a href="#h_cb1c6911f5" id="h_cb1c6911f5"></a>

O componente não altera nenhuma informação da mensagem de entrada quando a condição é verdadeira. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se este componente for o último passo do _pipeline_.

Quando a condição não for verdadeira, a saída desse componente seguirá a estrutura padrão:

```
{  
    "timestamp": <momento da interrupção no formato timestamp>,  
    "error": "<mensagem configurada no parâmetro Error Message>",  
    "code": <status code configurado no parâmetro HTTP Status Code>
}
```

### Tecnologia SIMPLE <a href="#h_3f95554491" id="h_3f95554491"></a>

É uma Linguagem de Expressão destinada a ser simples e prática para avaliar Expressões e Predicados sem exigir novas dependências ou conhecimento da tecnologia JSON Path.

Imagine que você precise validar determinada informação de cidade trafegada pelo _pipeline_:

```
{
    "cidade" : "São Paulo"
}
```

Apenas mensagens que contenham o campo "cidade" com o valor "São Paulo" devem ser aceitas. Do contrário, a execução do _pipeline_ deve ser interrompida.

O parâmetro _Condition_ do componente _Assert V1_ deverá ser configurado da seguinte maneira:

```
#{cidade} == 'São Paulo'
```

Conheça as demais opções para a declaração de expressões SIMPLE:

* **==**\
  Igual a
* **=\~**\
  Igual a, ignorando maiúsculas e minúsculas (quando comparando _strings_)
* **>**\
  Maior que
* **>=**\
  Maior ou igual a
* **<**\
  Menor que
* **!=**\
  Diferente
* **!=\~**\
  Diferente de, ignorando maiúsculas e minúsculas (quando comparando _strings_)
* **regex**\
  Valida uma RegEx contra a _string_ informada

Ex.: #{cidade} regex 'S.\*'

* **&&**\
  Operador lógico E.

Ex.: #{cidade} == 'Sao Paulo' && #{estado} == 'SP'

* **||**\
  Operador lógico OU.

Ex.: #{cidade} == 'Sao Paulo' || #{estado} == 'SP'

* **contains**\
  Valida se determinado valor está contido em uma _string_

Ex.: #{cidade} contains 'Paulo'

\
