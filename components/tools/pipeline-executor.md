---
description: Conheça o componente e saiba como utilizá-lo.
---

# Pipeline Executor

O _**Pipeline Executor**_ realiza chamadas síncronas ou assíncronas a outros _pipelines_ já implantados. Utilizando abordagem síncrona, é possível obter o resultado do _pipeline_ invocado.

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** SYNC para chamadas síncronas ao _pipeline_; e ASYNC para chamadas assíncronas ao _pipeline_.
* **Pipeline Name:** nome do _pipeline_ a ser invocado.
* **Version Major**: Major Version do _pipeline_ a ser invocado.
* **Payload**: _payload_ a ser enviado na invocação do _pipeline_.
* **Timeout**: tempo máximo de execução do _pipeline_ (em milissegundos).
* **Expiration**: tempo de permanência da mensagem em fila ao tentar executar o _pipeline_ (em milissegundos).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"_.

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Não se espera nenhum _payload_ específico na entrada desse componente. A entrada será configurada dinamicamente no campo “Payload” conforme a necessidade do _pipeline_ a ser invocado.

### Saída <a href="#sada" id="sada"></a>

```
{
    "operation": "SYNC",
    "pipelineName": "pipeline-example",
    "versionMajor": 1,
    "success": true,
    "payload": {},
    "pipelineResponse": {}
}
```

* **operation:** operação selecionada, SYNC ou ASYNC
* **pipelineName:** nome do _pipeline_ invocado
* **versionMajor:** versão major do _pipeline_ invocado
* **success:** se a chamada foi feita com sucesso
* **payload:** _payload_ utilizado para invocar o _pipeline_ configurado
* **pipelineResponse:** resposta do _pipeline_ executado. Essa propriedade é retornada apenas na operação SYNC.

## Pipeline Executor em Ação <a href="#pipeline-executor-em-ao" id="pipeline-executor-em-ao"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

### **Realizando uma chamada assíncrona**

**Operation:** ASYNC

**Pipeline Name:** nome do _pipeline_ a ser invocado

**Version Major:** 1

**Payload:** {}

**Timeout:** 20000

**Expiration:** 30000

**Fail On Error:** false

No cenário acima, será feita uma chamada assíncrona ao _pipeline_ configurado e o fluxo atual seguirá normalmente sem esperar a resposta do _pipeline_ invocado. Você poderá ver a execução e os _logs_ da chamada desse _pipeline_ na tela de _logs_ da Plataforma.

**Saída**

```
{
    "operation": "ASYNC",
    "pipelineName": "nome do pipeline a ser invocado",
    "versionMajor": 1,
    "success": true,
    "payload": {}
}
```

### **Realizando uma chamada síncrona**

**Operation:** SYNC

**Pipeline Name:** nome do pipeline a ser invocado

**Version Major:** 1

**Payload:** {}

**Timeout:** 20000

**Expiration:** 30000

**Fail On Error:** false

**Saída**

```
{
    "operation": "SYNC",
    "pipelineName": "nome do pipeline a ser invocado",
    "versionMajor": 1,
    "success": true,
    "payload": {},
    "pipelineResponse": {}
}
```

> **Nota:** Ao realizar implantações de _pipelines_ que utilizem o Pipeline Executor, esteja atento às configurações de execuções simultâneas tanto no _pipeline_ de origem como no de destino, especialmente quando o  o parâmetro _Operation_ estiver configurado com o valor SYNC.

{% hint style="info" %}
**IMPORTANTE:** Para evitar erros de enfileiramento de chamadas e timeout ao _pipeline_ de destino, é recomendável que a mesma configuração de execuções c seja adotada para ambos os _pipelines_ (origem e destino).
{% endhint %}

#### **Exemplos de **_**Red Flags**_**:**

pipeline1(Medium) <-> pipeline2(Small)\
pipeline1(Large) <-> pipeline2(Medium)\
pipeline1(Medium) <-> pipeline2(Small)

#### **Limite de** Execuções Simultâneas **por tipo de implantação:**

Small - max 10\
Medium - max 20\
Large - max 40\


