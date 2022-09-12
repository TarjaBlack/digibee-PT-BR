---
description: Conheça o componente e saiba como utilizá-lo.
---

# Hash

O _**Hash**_ gera um _hash_ a partir de uma _string_ passada no campo "Payload" caso a operação selecionada seja _Hash Payload_.

No entanto, se a operação selecionada for _Hash Fields_, então o componente gera um _hash_ a partir de uma _string_ passada nos campos especificados do JSON de entrada.

Dê uma olhada nos parâmetros de configuração do componente:

* **Crypto Operation:** tipos de operação disponíveis - _Hash Fields_ e _Hash Payload._
* **Crypto Algorithm:** tipo de algoritmo utilizado para gerar o _hash_. Os possíveis valores para esse parâmetro são _MD5_, _SHA-1, SHA-256, SHA-384, SHA-512, HmacSHA1, HmacSHA256, HmacSHA384, HmacSHA512_ e _BCrypt_.
* _**Account:**_ só será exibida caso o algoritmo selecionado no campo **Crypto Algorithm** seja HmacSHA1, HmacSHA256, HmacSHA384 ou HmacSHA512. A conta deve ser do tipo _SECRET\_KEY_ e a chave para fazer o _hash_ deve ser informada.
* **Secret Key:** só será exibida se nenhuma for conta selecionada e caso o algoritmo selecionado no campo **Crypto Algorithm** seja _HmacSHA1_, _HmacSHA256_, _HmacSHA384_ ou _HmacSHA512_. Essa é uma alternativa para o componente receber a chave para a geração do _hash_ de forma dinâmica.
* **Secret Key Type:** só será exibido caso o algoritmo selecionado no campo **Crypto Algorithm** seja _HmacSHA1_, _HmacSHA256_, _HmacSHA384_ ou _HmacSHA512_. Esse campo também informa para o componente qual é o tipo da chave informada, que pode ser do tipo _String_, _Hexadecimal_ ou _base64_.
* **BCrypt Version:** versão do algoritmo BCrypt a ser considerada na geração do _hash_. Essa opção será disponibilizada apenas quando o valor do parâmetro _Crypto Algorithm_ for _BCrypt_.
* **Salt:** _string_ de 16 bytes adicionada ao valor do _hash_. Caso não seja informado, será assumido um valor aleatório. Essa opção será disponibilizada apenas quando o valor do parâmetro _Crypto Algorithm_ for _BCrypt_.
*   **Cost Factor:** determina a quantidade de rodadas para o _hash_ ser executado. O fator de custo será elevado à potência de 2 e os possíveis valores estão entre 4 e 20. Ex: se o valor do parâmetro for 10, então a quantidade de rodadas para o _hash_ será 2ˆ10 = 1024 rodadas. Essa opção será disponibilizada apenas quando o valor do parâmetro _Crypto Algorithm_ for _BCrypt._

    **IMPORTANTE**_:_ o fator de custo afeta exponencialmente tempo e recursos de processamento, pois o algoritmo será executado consecutivamente de acordo com o número de rodadas obtidas através do resultado do cálculo 2ˆ_n_, no qual _n_ é o fator de custo.
* **JSON Field Path:** JSON como caminho do campo _string_ em notação com pontos (_dotted notation_).
* **Payload:** campo para informar diretamente o _payload_ que terá o _hash_ feito. Ele será exibido apenas se a operação selecionada for _Hash Payload_.
* **Preserve Original:** se ativada, a opção preserva o campo original como propriedade "Field" no mesmo nível do original.
* **Result As Hexadecimal:** se ativada, a opção mantém o _hash_ em formato hexadecimal; do contrário, o formato será base64.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Se você selecionar a operação _Hash Fields_, o componente recebe qualquer mensagem de entrada, mas você deve configurar o caminho para o _hash_ da mensagem na propriedade **Json Field Path**. Por exemplo:

**Json Field Path:** data.test

```
{
"data": [
{"test":"xpto"},
{"test":"xpto1"},
{"test":"xpto2"},
{"test":"xpto3"}
]
}
```

Portanto, o componente faz uma busca na propriedade “test”, dentro da propriedade “data”.

Por outro lado, se você selecionar a operação _Hash Payload,_ então a mensagem de entrada deve ser informada dentro do campo _Payload_.

### Saída <a href="#sada" id="sada"></a>

**Operação Hash Fields**

Se você selecionar a operação _Hash Fields_, a saída contém a mesma estrutura de entrada, porém exibindo o _hash_ da mensagem. Caso a propriedade **Preserve Original** estiver habilitada, então a saída preserva o campo original no mesmo nível, adicionando o prefixo '\_' na frente do campo:

```
{
"data": [
{
"test": "3851b1ae73ca0ca6e3c24a0256a80ace",
"_test": "xpto"
},
{
"test": "ca9e9bf198149d78f4aad334c838a263",
"_test": "xpto1"
},
{
"test": "83709b4f9067a83bbdfb0c358dc23a5e",
"_test": "xpto2"
},
{
"test": "e427f7e6f1bd29d91ea0cc53e40fba12",
"_test": "xpto3"
}
]
}
```

**Operação Hash Payload**

Se você selecionar a operação _Hash Payload_, a saída exibe a propriedade "result" com o _hash_ da mensagem passada:

```
{
"result": "3851b1ae73ca0ca6e3c24a0256a80ace"
}
```

**Erro**

```
{
"success": false,
"message": "Something went wrong while trying to use the HashConnector. Error: java.lang.StringIndexOutOfBoundsException: String index out of range: 1",
"error": "java.lang.StringIndexOutOfBoundsException: String index out of range: 1"
}
```

* **success:** “false”, pois ocorreu um erro na execução
* **message:** mensagem de erro do componente
* **error:** mensagem de erro recebida do algoritmo de _hash_

## Hash em Ação <a href="#hash-connector-em-ao" id="hash-connector-em-ao"></a>

### Operação Hash Fields <a href="#operao-hash-fields" id="operao-hash-fields"></a>

**Exemplo 1**

* **Crypto Operation:** Hash Fields
* **Crypto Algorithm:** SHA-256
* **JSON Field Path:** data.test
* **Preserve Original:** habilitado
* **Result As Hexadecimal:** habilitado

**Entrada**

```
{
"data": [
{"test":"xpto"},
{"test":"xpto1"},
{"test":"xpto2"},
{"test":"xpto3"}
]
}
```

**Saída**

```
{
"data": [
{
"test": "2e954593b0b51547656f7f06ec3818a2b42fed46307b81bd493133aa1ce45173",
"_test": "xpto"
},
{
"test": "8b948d95169f851545f8161fb4dc8e1d37a4c79014ac1d02186fa8946a91aab9",
"_test": "xpto1"
},
{
"test": "4c9e0d7ca22d9ab7cc675de59226f9477fd847ede13894b835d0ae204139f63a",
"_test": "xpto2"
},
{
"test": "b5bd5abe3eb5958153af6615df06ccbdfe5857a13da2601f49e4de9fbb102f9a",
"_test": "xpto3"
}
]
}
```

**Exemplo 2**

* **Crypto Operation:** Hash Fields
* **Crypto Algorithm:** HmacSHA256
* **Account:** vazio
* **Secret Key:** 001def0209
* **Secret Key Type:** Hexadecimal (a chave passada na propriedade _Secret Key_ deve estar em hexadecimal)
* **JSON Field Path:** data.test
* **Preserve Original:** habilitado
* **Result As Hexadecimal:** habilitado

**Entrada**

```
{
"data": [
{"test":"xpto"},
{"test":"xpto1"},
{"test":"xpto2"},
{"test":"xpto3"}
]
}
```

**Saída**

```
{
"data": [
{
"test": "257966929b29a6e0618d47a152e2856a888072400a5cb458fa1d40ff3cedc734",
"_test": "xpto"
},
{
"test": "ce0e754ab2f57f1fca1a00fce3e834a6940bea8013ae59b6641a4911e349b480",
"_test": "xpto1"
},
{
"test": "ff0cd9c0df219f99567aeb25d7d5ab9acff3c29728b0f4f71f50e750750a26d5",
"_test": "xpto2"
},
{
"test": "04a11cbc118ea455c0072e6c70607f68324e5444c8a4795443d25933d9dfa9c6",
"_test": "xpto3"
}
]
}
```

**Exemplo 3**

* **Crypto Operation:** Hash Fields
* **Crypto Algorithm:** BCrypt
* **Bcrypt Version:** 2y
* **Salt:** N9qo8uLOickgx2ZM
* **Cost:** 6
* **JSON Field Path:** data.test
* **Preserve Original:** habilitado

**Entrada**

```
{
"data": [
{"test":"xpto"},
{"test":"xpto1"},
{"test":"xpto2"},
{"test":"xpto3"}
]
}
```

**Saída**

```
{
"data": [
{
"test": "$2y$06$RhjvZxfzRC7nW0rlcBHYROhJmATBMG6eXfkYkffexdfdFHzzp27Iu",
"_test": "xpto"
},
{
"test": "$2y$06$RhjvZxfzRC7nW0rlcBHYROm9TaJZ6QQUstIomnJG/Qgc7fPU5x8S.",
"_test": "xpto1"
},
{
"test": "$2y$06$RhjvZxfzRC7nW0rlcBHYROHAP1dIbNu3SenuQ6B.W9OkJ0/NzYF6e",
"_test": "xpto2"
},
{
"test": "$2y$06$RhjvZxfzRC7nW0rlcBHYROPsXkmxUVt8Suo8d3GuOl9q0pryw6iJy",
"_test": "xpto3"
}
]
}
```

### Operação Hash Payload <a href="#operao-hash-payload" id="operao-hash-payload"></a>

**Exemplo 1**

* **Crypto Operation:** Hash Payload
* **Crypto Algorithm:** SHA-256
* **Payload:** xpto
* **Result As Hexadecimal:** habilitado

**Saída**

```
{
"result": "2e954593b0b51547656f7f06ec3818a2b42fed46307b81bd493133aa1ce45173"
}
```

**Exemplo 2**

* **Crypto Operation:** Hash Payload
* **Crypto Algorithm:** HmacSHA512
* **Account:** vazio
* **Secret Key:** 001def0209
* **Secret Key Type:** Hexadecimal (a chave passada na propriedade _Secret Key_ deve estar em hexadecimal)
* **Payload:** xpto
* **Result As Hexadecimal:** habilitado

**Saída**

```
{
"result": "517da9449385a43478309459adf9304bd3c8f63cd1d388abd5cbc02b81d8ccb39d303f877019aebfed073166e6c410197e10077f6df3f7a3b3f50adb8cd09580"
}
```

**Exemplo 3**

* **Crypto Operation:** Hash Payload
* **Crypto Algorithm:** BCrypt
* **Bcrypt Version:** 2b
* **Salt:** N9qo8uLOickgx2ZM
* **Cost:** 10
* **Payload:** \{{ message.data \}}

**Entrada**

```
{
"data": [
{"test":"xpto"},
{"test":"xpto1"},
{"test":"xpto2"},
{"test":"xpto3"}
]
}
```

**Saída**

```
{
"result": "$2b$10$RhjvZxfzRC7nW0rlcBHYROa3UXROXVeKZ3oK4DSc1mV6iJ/pBqBm6"
}
```

**IMPORTANTE**_:_ o fator de custo no algoritmo _BCrypt_ afeta exponencialmente o tempo e os recursos de processamento, pois o algoritmo será executado consecutivamente de acordo com o número de rodadas obtidas através do resultado do cálculo 2^n, no qual "n" é o fator de custo.

Veja alguns exemplos de execução para servir de parâmetro de duração do cálculo do _hash_. Como premissa para aplicar o _hash_ do algoritmo _Bcrypt_ estão sendo utilizados um _payload_ de 1MB e um fator de custo com o mínimo e o máximo permitido. Os resultados obtidos são:

*   **Cost Factor 4**

    **- Pipeline Small:** média de 0.98s

    **- Pipeline Medium:** média de 0.64s

    **- Pipeline Large:** média de 0.07s
*   **Cost Factor 20**

    **- Pipeline Small:** média de 8m 7s

    **- Pipeline Medium:** média de 3m 56s

    **- Pipeline Large:** média de 1m 53s

Os resultados acima podem variar de acordo com o fluxo de integração construído, com o tamanho da mensagem a ter o _hash_ aplicado e com o fator de custo.

Outro ponto importante a ser destacado diz respeito aos limites do fator de custo. O fator de custo do algoritmo _Bcrypt_ permite uma faixa entre 4 e 31. No entanto, fatores acima de 20 acabam consumindo carga de processamento e tempo muito alto, inviabilizando os parâmetros de _timeout_ de execução de um _pipeline_. Com isso, o componente Hash foi limitado a aceitar no máximo 20 como valor de fator de custo. Partindo dessa premissa, quando for realizado o _hash_ de um valor por meio do componente Hash e com a utilização do algoritmo _BCrypt_, atente-se ao limite de 20 como fator de custo. Dessa forma são evitados problemas de validação ou checagem no seu fluxo de integração.
