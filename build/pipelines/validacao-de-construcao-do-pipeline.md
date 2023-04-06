---
description: Saiba mais sobre a funcionalidade de validação de construção de pipelines.
---

# Linter - Validação de construção do pipeline (Beta)

{% hint style="danger" %}
**IMPORTANTE:** esta funcionalidade está em Beta. [Para saber mais, leia o artigo Programa beta.](https://docs.digibee.com/documentation/v/pt-br/geral/programa-beta)
{% endhint %}

O Novo _Canvas_ exibe alertas durante a construção de _pipelines_ que ajudam os desenvolvedores a identificarem e corrigirem problemas comuns mais rapidamente.

<figure><img src="../../.gitbook/assets/beta (2).gif" alt=""><figcaption></figcaption></figure>

## Localizar problemas <a href="#h_37abb7de8a" id="h_37abb7de8a"></a>

Para cada componente que apresentar um problema durante a criação do _pipeline_, o _Canvas_ exibe um alerta com detalhes e informações. Muitas das validações têm o propósito de aviso e não demandarão correções nem serão intrusivas enquanto você cria seu _pipeline_.

## Alertas <a href="#h_303cf6c6b1" id="h_303cf6c6b1"></a>

Os problemas validados durante a construção do _pipeline_ são divididos em **Erros** e **Avisos**. Essa divisão de alertas ajuda o desenvolvedor a entender o nível de gravidade do problema apontado pelo _Canvas_.

### Erros <a href="#h_9f1e8a34bd" id="h_9f1e8a34bd"></a>

Os alertas de **Erro** apontam falhas graves na construção do _pipeline_. Eles devem ser corrigidos, senão não será possível salvá-lo.

Hoje, o _Canvas_ apresenta erros da seguinte categoria:

* Estrutura: erros estruturais que impedem o processamento do fluxo de integração.

### Avisos <a href="#h_4a0b2bf4a9" id="h_4a0b2bf4a9"></a>

Os alertas de **Aviso** exibem pontos de melhoria na construção do _pipeline_. Hoje, o _Canvas_ exibe avisos da seguinte categoria:

* Boas práticas: hábitos de construção que tornam seu _pipeline_ mais saudável, e podem facilitar futuras manutenções e melhorias.

## Lista de alertas

Para cada problema encontrado durante a construção de pipelines, um alerta é mostrado em seu componente de origem e em uma lista. Os alertas são divididos seguindo as categorias acima e é possível visualizar quantos alertas de cada tipo há separadamente.\


À partir da lista é possível:

1\. Visualizar a imagem e nome do componente com problema junto a uma descrição e link para documentação com orientações sobre como resolvê-lo.

2\. Esconder os alertas temporariamente.

3\. Navegar entre os sub-níveis do pipeline até o componente com erro.

4\. Abrir o formulário de configuração do componente para editá-lo.

<figure><img src="https://lh5.googleusercontent.com/61aaGRoKfmLr2Jt5ItNDcwgstJCq90MZSbig3cy_FW2WRLpOlMzDSNbB6ahkGCxG15sMds0UNVDi1yv6y7nYYTueZ6OwvtFyEnp9d5Z2Ayx2S60WMI9aGX5BWoaAzlPG8OYAwk3z7-Q2IaFofgLtLKs" alt=""><figcaption></figcaption></figure>

Para visualizar a lista, basta clicar no ícone![](https://lh5.googleusercontent.com/wZYM7meIdyA5nNTJ6eFF6oGeGdiYmibzKWph4gkpok0NgMs866kLRHFQokvmBW5T7gfJsGpQjarh1WnsbKn8ugElhwisrANN\_jawM-8orE0plP5deNJRkqhPoYGEdGvs1eLTzoPwoRaXRP24zJsmMc4) localizado na barra de tarefas.

## Corrigir problemas <a href="#h_b0ce49bd21" id="h_b0ce49bd21"></a>

Todas as validações do Novo _Canvas_ apresentam informações que te ajudam a corrigir o problema. Passe o mouse sobre o ícone ⚠ para que as informações sejam exibidas. Desse modo, você poderá lê-las e verificar a aplicabilidade de cada sugestão no seu _pipeline_.

Esta página lista todos os possíveis alertas desenvolvidos até agora, contendo detalhes e informações de como você pode corrigir e aprimorar seu _pipeline_.

### Choice <a href="#h_7d5f476e64" id="h_7d5f476e64"></a>

#### 1. O componente Choice precisa ter um "when" configurado (estrutura) <a href="#h_60dd2adfb4" id="h_60dd2adfb4"></a>

O Choice permite o desvio de fluxo dentro de um _pipeline_. Para utilizar esse componente corretamente, é necessário configurar suas condicionais ‘**when**’. Cada **when** define uma condição que realiza um desvio no fluxo para uma linha de execução específica. É necessário ter pelo menos 1 condição **when** configurada.

Desse modo, defina pelo menos uma condição **when** para evitar a interrupção do fluxo do _pipeline_.

#### 2. O componente Choice precisa ter um "otherwise" configurado (estrutura) <a href="#h_c28a2f1936" id="h_c28a2f1936"></a>

O Choice permite o desvio de fluxo dentro de um _pipeline_. Para utilizar esse componente corretamente, é necessário configurar seu comando ‘**otherwise**’. O **otherwise** é o comando a ser executado quando nenhuma das condições **when** é atendida. É necessário ter 1 condição **otherwise** configurada.

Portanto, defina o comando **otherwise** a ser executado caso nenhuma das condições **when** for considerada verdadeira.

### Componentes de subfluxo <a href="#h_dbbaf3893a" id="h_dbbaf3893a"></a>

Os seguintes problemas se referem aos componentes que permitem a estruturação de [_subpipelines_](subpipelines.md), ou seja, subfluxos do _pipeline_. _Subpipelines_ são estruturados a partir dos seguintes componentes:

* [Block Execution](../../components/logic/block-execution.md)
* [Do While](../../components/logic/do-while.md)
* [For Each](../../components/logic/for-each/)
* [Retry](../../components/logic/retry.md)
* [Stream Excel](../../components/files/stream-excel.md)
* [Stream File Reader](../../components/files/stream-file-reader.md)
* [Stream File Reader Pattern](../../components/files/stream-file-reader-pattern.md)
* [Stream JSON File Reader](../../components/files/stream-json-file-reader.md)
* [Stream XML File Reader](../../components/files/stream-xml-file-reader.md)
* [Stream DB V1](../../components/structured-data/stream-db-v1.md)
* [Stream DB V3](../../components/structured-data/stream-db-v3.md)

#### 1. O onProcess precisa ter ao menos um componente conectado (estrutura) <a href="#h_da096f50b4" id="h_da096f50b4"></a>

O onProcess define um dos subfluxos do _pipeline_. Estruture e conecte _o subpipeline_ onProcess para que o fluxo do _pipeline_ não seja interrompido.

#### 2. O onException precisa ter ao menos um componente conectado (boas práticas) <a href="#h_9d3d716b24" id="h_9d3d716b24"></a>

O onException é o _subpipeline_ onde é implementado o fluxo que trata uma exceção na execução do onProcess_._ Estruture e conecte o subfluxo onException para que o fluxo do _pipeline_ não seja interrompido.

#### 3. Existe ao menos um problema dentro de onProcess (estrutura) <a href="#h_d239301ae7" id="h_d239301ae7"></a>

O onProcess define um dos subfluxos do _pipeline_. Verifique os problemas do _subpipeline_ onProcess para prosseguir com a criação do seu _pipeline_.

#### 4. Existe ao menos um problema dentro de onException (estrutura) <a href="#h_6e976cba62" id="h_6e976cba62"></a>

O onException é o _subpipeline_ onde é implementado o fluxo que trata uma exceção na execução do onProcess_._ Verifique os problemas do subfluxo onException para prosseguir com a criação do seu _pipeline_.

### Parallel <a href="#h_9d4020c448" id="h_9d4020c448"></a>

#### 1. O componente Parallel precisa ter ao menos uma execução configurada (estrutura) <a href="#h_b67a910580" id="h_b67a910580"></a>

O Parallel permite a configuração de linhas de execução paralelas dentro do fluxo do _pipeline_. Conecte o Parallel a outro componente para evitar a interrupção do fluxo.

{% hint style="info" %}
**Nota:** O Parallel deve ser sempre seguido por outro componente para que o fluxo possa ser executado.
{% endhint %}

#### 2. O componente Parallel deve ter ao menos duas execuções configuradas (boas práticas) <a href="#h_18325c9190" id="h_18325c9190"></a>

O Parallel permite a configuração de uma ou mais linhas de execução paralelas dentro do fluxo do _pipeline_. Como boa prática, recomendamos que utilize o Parallel apenas quando seu fluxo precisar de duas execuções ou mais ocorrendo simultaneamente.

### Triggers <a href="#h_67d63ac161" id="h_67d63ac161"></a>

#### 1. Trigger não configurado. Para implantar o pipeline, configure o trigger (estrutura) <a href="#h_2689472af5" id="h_2689472af5"></a>

O _trigger_ define como a execução do _pipeline_ será iniciada. Para configurar o _trigger_, selecione uma das opções disponibilizadas pela Digibee Integration Platform. A seguir, conecte-o ao início do fluxo para implantar o _pipeline_ posteriormente. [Para mais informações, acesse a documentação dos triggers.](https://docs.digibee.com/documentation/v/pt-br/components/triggers)

{% hint style="info" %}
**Nota:** Você pode salvar o _pipeline_ mesmo sem configurar o _trigger_. No entanto, não será possível implantá-lo.
{% endhint %}

### Componentes descontinuados <a href="#h_67d63ac161" id="h_67d63ac161"></a>

#### 1. Versão do componente descontinuada. Existe uma versão nova deste componente (boas práticas) <a href="#h_831a10b00b" id="h_831a10b00b"></a>

A versão do componente que você está tentando utilizar foi descontinuada. Isso significa que há uma nova versão incrementada e melhorada disponível para uso.

**Exemplo:** O componente SOAP possui três versões, [SOAP V1](https://docs.digibee.com/help-center/v/pt-br/components/web-protocols/soap-v2/soap-v1), [SOAP V2](https://docs.digibee.com/help-center/v/pt-br/components/web-protocols/soap-v2) e [SOAP V3](https://docs.digibee.com/help-center/v/pt-br/components/web-protocols/soap-v3). Recomendamos a versão mais atual do componente, a SOAP V3, para aprimorar seu _pipeline_.

{% hint style="info" %}
**Nota:** A versão descontinuada do componente ainda pode ser utilizada. No entanto, é importante informar que incrementos e melhorias são feitos na última versão do componente.
{% endhint %}

### Cápsulas

#### 1. Esta Cápsula não pode ser usada aqui porque ela não existe neste realm (estrutura)

A Cápsula que você está tentando utilizar não existe no _realm_ no qual você está operando. Você precisa apagá-la ou substituí-la por outro conector, fluxo ou uma Cápsula existente neste _realm_.

### Session Management

#### 1. O campo não foi declarado anteriormente (boas práticas)

Não foi possível utilizar o campo (operação GET) porque o mesmo não foi declarado (operação PUT) anteriormente.

#### 2. O campo foi declarado, mas não está sendo usado (boas práticas)

O campo foi declarado anteriormente (operação PUT), mas não está sendo utilizado.&#x20;

Configure um novo componente Session Management para utilizar (operação GET) ou deletar (operação DELETE) o campo declarado anteriormente.
