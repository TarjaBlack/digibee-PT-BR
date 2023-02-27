---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON to CSV V2

O _**JSON to CSV V2**_ permite a criação de arquivos e estruturas CSV a partir de um JSON de entrada.

Dê uma olhada nos parâmetros de configuração do componente:

* **Output as File:** se a propriedade estiver ativada, o CSV gerado será salvo como arquivo; do contrário, o resultado será um _array_ de _strings_ e cada um dos seus índices corresponde a uma linha do CSV.
* **File Name:** nome do arquivo CSV a ser gerado. Essa opção será exibida somente quando a opção **Output as File estiver** ativada.
* **Append File:** se a propriedade estiver ativada, os dados serão acrescentados a um arquivo existente (arquivos inexistentes serão criados); do contrário, será criado sempre um novo arquivo a cada execução. Essa opção será exibida somente quando a opção **Output as File** estiver ativada.
* **Headers:** _headers_ do CSV, separados por vírgula. Ex: header1,header2,...,headerN. Os _headers_ devem possuir o mesmo nome das chaves do objeto JSON.
* **Delimiter:** delimitador que será usado para gerar o CSV.
* **Body:** JSON de entrada a partir do qual será gerado o CSV. O JSON deve ser um _array_ de objetos.
* **Show Headers:** se a propriedade estiver ativada, os _headers_ serão informados no CSV; do contrário, o CSV não apresentará os _headers_.
* **Coalesce:** se a propriedade estiver ativada, será gerado qualquer tipo de objeto JSON como _string_ com valor do CSV; do contrário, será lançada uma exceção se o valor for um objeto ou um _array_.
* **Generate Columns With Quotes:** se a propriedade estiver ativada, todos os valores das colunas de todas as linhas serão gerados com aspas; do contrário, as colunas não serão geradas com aspas, exceto se for necessário escapar algum caractere especial (aspas e o delimitador dentro do valor da coluna).
* **End Of Line Policy:** política de quebra de linha dentro do arquivo (LINUX = \n e WIDOWS = \r\n). Essa opção será exibida somente quando a opção **Output as File** estiver ativada.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

É necessário informar um _array_ de objetos no campo **Body** e informar no campo **Headers** os _headers_ correspondentes às chaves desses objetos. Exemplo:

**Headers:** header1,header2,header3

**Body:**

```
[
    {"header1": "some_value","header2": "some_value","header3": "some_value"}
]
```

### Saída <a href="#sada" id="sada"></a>

Caso a opção **Output as File** esteja habilitada:

```
{
    "success": true,
    "fileName": FILE_NAME
}
```

* **success:** propriedade que indica se a execução foi bem sucedida ou não
* **fileName:** nome do arquivo gerado

Caso a opção **Output as File** esteja desabilitada:

```
{
    "success": true,
    "data": [
        "header1,header2,header3",
        "some_value,some_value,some_value"
    ]
}

```

* **success:** propriedade que indica se a execução foi bem sucedida ou não
* **data:** CSV gerado como um _array_ de strings

Para entender melhor o fluxo das mensagens na Digibee Integration Platform, leia o artigo sobre [Processamento de mensagens](../../build/pipelines/processamento-de-mensagens.md).

\
