---
description: Conheça o componente e saiba como utilizá-lo.
---

# Parallel Execution

O _**Parallel Execution**_ permite a configuração de linhas de execução paralelas dentro do fluxo do _pipeline_.

Esse componente tem duas etapas de configuração: a dos parâmetros que definem o comportamento geral das execuções e a dos parâmetros específicos das linhas de execuções.

Dê uma olhada nos parâmetros de configuração do componente:

* **Step Name**: a propriedade pode ser utilizada para documentar, pois ela se torna o texto apresentado no componente no _pipeline canvas_.
* **Aggregation Type**: poderá ser configurado como SUMMARY ou COLLATE; veja mais abaixo.
* **Show Execution Ids:** caso seja habilitada, a propriedade fará com que o id de cada linha de execução seja informado no resultado.
* **Report Exceptions:** caso seja habilitada, a propriedade fará com que quaisquer exceções sejam informadas no resultado; veja mais abaixo.

Agora dê uma olhada nos parâmetros de configuração das linhas de execuções:

* **Description:** a propriedade pode ser utilizada para documentar as linhas de execuções, pois ela se torna o texto apresentado em cada linha no pipeline canvas.
* **Execution Id:** define o id de cada uma das execuções paralelas

## Fluxo de mensagens <a href="#h_342616e0fd" id="h_342616e0fd"></a>

### Entrada <a href="#h_109500abf4" id="h_109500abf4"></a>

Não espera nenhum _payload_ específico na entrada desse componente. No entanto, a entrada será informada a cada linha de execução paralela.

### Saída <a href="#h_059ebd5fbd" id="h_059ebd5fbd"></a>

* **Saída com Aggregation Type = SUMMARY**

Neste caso, somente um sumário sobre cada invocação paralela será exibido:

```
{
    "total": 0,
    "success": 0,
    "failed": 0
}
```

Um sumário será informado no final da execução de todas as linhas paralelas. Para que a linha de execução seja considerada como "sucesso", uma propriedade "success" com o valor “true” deverá ser informada no final da execução.

* **Saída com Aggregation Type = COLLATE e Show Execution Ids = verdadeiro**

Neste caso, o resultado de cada execução estará disponível como um item do _array_ identificado com a propriedade _executionId_, que define o caminho percorrido por aquela execução e “result” contendo o resultado dela.

```
[{"executionId": "p-a","result": {"parallel": "A"}}, 
{"executionId": "p-b","result": {"parallel": "B"}}, 
{"executionId": "p-c","result": {"parallel": "C"}}]
```

* **Saída com Aggregation Type = COLLATE e Show Execution Ids = falso**

Neste caso, o resultado de cada execução será informado como um item do _array_ sem a discriminação de qual caminho foi percorrido.

```
[{"parallel": "A"}, 
{"parallel": "B"}, 
{"parallel": "C"}]
```

* **Saída com erro e Report Exceptions = verdadeiro**

Este caso só tem relevância quando usado com Aggregation Type = COLLATE.

Caso um erro aconteça durante a execução da linha paralela _p-b_, o erro será informado na saída:

```
[{
    "executionId": "p-a",
    "result": {
        "parallel": "A"
    }
},{
    "executionId": "p-b",
    "result": {
        "timestamp": 99999, "error": "XXXX", "code": 999
    }
},{
    "executionId": "p-c",
    "result": {
        "parallel": "C"
    }
}]
```

* **Saída com erro e Report Exceptions = falso**

Este caso só tem relevância quando usado com Aggregation Type = COLLATE.

Caso um erro aconteça durante a execução da linha paralela _p-b_, null será informado como resultado:

```
[{]
    "executionId": "p-a",
    "result": {
        "parallel": "A"
    }
}, {
    "executionId": "p-b",
    "result": null
}, {
    "executionId": "p-c",
    "result": {
        "parallel": "C"
    }
}]
```

## Parallel Execution em ação <a href="#h_bc9d43a9c1" id="h_bc9d43a9c1"></a>

Veja abaixo como o componente se comporta em determinadas situações e as suas respectivas configurações.

* **Unindo o resultado das execuções paralelas**

Para unir o resultado das execuções paralelas, é importante configurar o componente Parallel Execution dentro de um Block Execution (adicionar link para ele). Ao final do Block Execution, todas as execuções paralelas serão sincronizadas e o resultado será conforme a configuração "Aggregation Type".

![](<../../.gitbook/assets/parallel execution.png>)

* **Parallel Execution é utilizado no fluxo principal do pipeline**

Caso o componente seja utilizado no fluxo principal do pipeline, então as linhas de execução paralelas serão "unidas" ao final da execução do pipeline e o mesmo será terminado com o resultado conforme a configuração "Aggregation Type".

![](<../../.gitbook/assets/parallel execution1.png>)

* **Parallel Execution é utilizado dentro de outro Parallel Execution**

Neste caso, novas linhas de execução paralelas serão iniciadas e "unidas" ao fim da linha de execução paralela que continha o Parallel Execution mais interno. O Parallel Execution mais externo somente unirá as suas respectivas linhas quando as mais internas finalizarem.

![](<../../.gitbook/assets/parallel execution2.png>)
