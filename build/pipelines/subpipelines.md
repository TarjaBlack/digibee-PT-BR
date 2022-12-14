---
description: Entenda o que são e como funcionam.
---

# Subpipelines

_Subpipelines_ são subfluxos do _pipeline_ necessariamente vinculados e disparados por um componente do fluxo principal, por exemplo, o [For Each](../../components/logic/for-each/).

Vamos imaginar um processo chamado “Validação de Dados de Cliente”. Esse processo obtém os dados dos clientes através do _endpoint_ REST e então verifica se cada registro de cliente possui os dados necessários.

Para iterar pela coleção de registros, usaremos o componente **For Each (Processa clientes)**.

<figure><img src="../../.gitbook/assets/image3 (2) (2).png" alt=""><figcaption></figcaption></figure>

Toda vez que um componente com capacidade de iterar por coleções é adicionado a um _pipeline_, dois _subpipelines_ são criados: _**onProcess**_ e _**onException**_.

<figure><img src="../../.gitbook/assets/image7 (2).png" alt=""><figcaption></figcaption></figure>

### _**onProcess**_ <a href="#onprocess" id="onprocess"></a>

Este _subpipeline_ implementa o subfluxo que processa cada item da coleção. Ele tem seu próprio Canvas, que pode ser acessado pelo menu do componente:

<figure><img src="../../.gitbook/assets/image5 (6).png" alt=""><figcaption></figcaption></figure>

No caso do processo “Validação de Dados de Cliente”, o _subpipeline **onProcess**_ trata todos os registros da coleção de clientes individualmente e verifica se o atributo “Data de Nascimento” está preenchido em cada um deles:

<figure><img src="../../.gitbook/assets/image6 (1).png" alt=""><figcaption></figcaption></figure>

Ao término de cada execução do _subpipeline **onProcess**_, um atributo _success_ é retornado, indicando se houve sucesso ou falha na execução. Por padrão, esse atributo é retornado com valor “_false”_. Assim, você precisa informar explicitamente quando a execução ocorrer conforme esperado.

No processo “Validação de Dados de Cliente”, a seguinte resposta de sucesso será retornada pelo componente **JSON Generator (Sucesso)** quando o atributo “Data de Nascimento” estiver preenchido:

```
{"success": true}
```

Caso o atributo “Data de Nascimento” esteja vazio, o componente **JSON Generator (Falha)** retorna o atributo com valor “_false”_:

```
{"success": false}
```

Nesse caso, é gerada uma exceção através do componente **Assert (Erro Interno)**:

<figure><img src="../../.gitbook/assets/image4 (2).png" alt=""><figcaption></figcaption></figure>

O atributo _**Fail On Error**_ indica que a execução do fluxo do _pipeline_ será interrompida e será lançada uma exceção caso a condição do componente Assert não for validada.

{% hint style="info" %}
**Nota:** Quando a exceção é gerada por um componente de um _subpipeline_, a execução do _subpipeline **onException** _ é iniciada. Por outro lado, se a exceção decorrer de um componente do fluxo principal, a execução do _pipeline_ será interrompida por erro.
{% endhint %}

### _**onException**_ <a href="#onexception" id="onexception"></a>

Este _subpipeline_ implementa o fluxo que trata uma exceção na execução do _subpipeline **onProcess**_. Ele tem seu próprio Canvas, que pode ser acessado pelo menu do componente:

<figure><img src="../../.gitbook/assets/image1 (4).png" alt=""><figcaption></figcaption></figure>

Quando o _**onException**_ é executado no processo “Validação de Dados de Cliente”, uma chamada é feita a um _endpoint_ REST, registrando o incidente e gerando uma mensagem de erro na página [Pipeline Logs](../../monitor/pipeline-logs.md).

<figure><img src="../../.gitbook/assets/image2 (3).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Nota:** A utilização do _**onException**_ é opcional, no entanto, é uma prática fortemente recomendada. Diversos componentes da Digibee Integration Platform suportam o atributo _**Fail On Error**_ e permitem que estratégias de tratamento de erro e recuperação sejam implementadas através do _**onException**_, tornando o _pipeline_ muito mais robusto e resiliente.
{% endhint %}

Para saber mais, leia o [artigo ](https://docs.digibee.com/documentation/v/pt-br/build/pipelines)[_Pipeline_](https://docs.digibee.com/documentation/v/pt-br/build/pipelines).
