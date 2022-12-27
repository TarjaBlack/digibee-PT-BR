---
description: >-
  Saiba mais sobre o novo modelo SaaS subscription da Digibee Integration
  Platform
---

# Modelo baseado em subscription

Este artigo apresenta conceitos importantes do novo modelo baseado em _subscription_, lançado em Abril de 2022.

A Digibee oferece um modelo de SaaS baseado em _subscription_ e _committed use_, no qual o cliente tem acesso à Digibee Integration platform e aos serviços de suporte e sucesso do cliente por um determinado período. Nesse modelo, as implantações serão realizadas baseadas na quantidade de _Pipeline Subscriptions_ e RTUs (_Runtime Units_) de testes ou produção. Além disso, são aplicados limites de uso da plataforma e limitações de entrega.

Para saber mais sobre como implantar a pipeline, por favor leia o artigo de [implantação de uma pipeline](https://docs.digibee.com/help-center/v/pt-br/run/deployments).&#x20;

## Definições

### Pipeline subscription

_Pipeline subscription_ é o item de preço inicial que permite aos clientes acessar a plataforma, suporte, serviços de sucesso do cliente e Propriedade Intelectual (IP) da Digibee. Uma _pipeline subscription_ refere-se a um fluxo de integração exclusivo implantado na plataforma da Digibee. Limitado a dois (2) RTUs de produção implantados no ambiente de produção, emparelhados com um (1) RTU de teste implantado no ambiente de teste e toda a infraestrutura subjacente necessária para executá-las conforme definido no artigo [Limites de Uso](limites-de-uso.md).

### Fluxo de integração único&#x20;

Uma necessidade de negócios ou tecnologia para capturar, transformar e/ou entregar dados de uma fonte para outra. Único porque é uma única pipeline em uma versão específica.&#x20;

### Pipeline version&#x20;

É um número (ex.: 1.2) que representa o estado único de uma pipeline. A Digibee segue o esquema simplificado de Versão Semântica ([www.semver.org](https://www.semver.org)) com apenas os componentes _MAJOR_ e _MINOR_. A Digibee não suporta "rótulos adicionais para metadados de pré-lançamento e compilação", e as versões _MAJOR_ começam com 1. Para cada _pipeline subscription_, apenas uma versão principal do pipeline pode estar ativa (implantada) em um determinado ambiente e momento.

* **Versão **_**Major**_** da pipeline**: Especifica o componente de versão que controla as alterações de quebra em uma pipeline, ou seja, alterações que tornariam duas versões Major incompatíveis em termos de APIs expostas, comportamento ou saída.
* **Versão **_**Minor**_** da pipeline**: Especifica o componente de versão que controla as alterações que NÃO tornam duas versões _Minor_ diferentes com a mesma versão Major incompatíveis, em termos de APIs expostas, comportamento ou saída.&#x20;

### RTU (_Unidade Runtime_)

RTU (_Runtime Unit_) é uma medida da capacidade de computação para processar integrações na Digibee Integration Platform. Os RTUs podem ser usados para dimensionar integrações vertical e horizontalmente. Quando dimensionados verticalmente, eles podem ser usados em três tamanhos diferentes: pequeno (consome 1 RTU), médio (consome 2 RTUs) e grande (consome 4 RTUs). Quando dimensionado horizontalmente, cada nova réplica consumirá a mesma quantidade de RTU que a implantação original. Cada RTU vem com a infraestrutura subjacente para executá-los. Consulte o artigo [Limites de Uso](limites-de-uso.md) para obter mais informações.

* **RTU de teste** representa a capacidade de processamento para executar integrações em uma _subscription_ ativa em um ambiente de teste. Os RTUs devem ser pareados com uma _pipeline_ _subscription_ existente.&#x20;
* **RTU de produção** representa a capacidade de processamento para executar integrações sob uma _subscription_ ativa em um ambiente de produção. Para implantar um novo pipeline em um ambiente de produção, as _pipeline_ _subscriptions_ e os RTUs de produção devem estar disponíveis em seu domínio.&#x20;

### Limites de uso da plataforma&#x20;

Os limites de uso da plataforma são limites técnicos impostos em cada _realm_ para evitar o abuso da plataforma. Eles foram criados com base no uso médio da plataforma. Estes são alguns dos limites:&#x20;

* Tamanho de implantação e réplicas (ou seja, CPU e memória para executar um pipeline ou um conjunto de réplicas)&#x20;
* Tráfego de saída&#x20;
* Taxa de mensagens sendo produzidas/consumidas&#x20;
* Mensagens retidas na pipeline para processamento&#x20;
* Retenção de registros&#x20;
* VPN&#x20;
* Armazenamento de objetos, armazenamento Digibee e dados de relacionamento

## Principais regras&#x20;

### Regras para _pipeline subscription_ implantada&#x20;

Você pode **construir** quantas _pipelines_ quiser na Plataforma. Todos os limites são aplicados na fase de **implantação**. Cada _pipeline_ desenvolvido pode ser implantada em ambientes de teste ou produção, respeitando o número de _pipeline subscriptions_ e RTUs disponíveis.

As _pipelines_ implantadas em um ambiente consomem RTUs (teste ou produção) de acordo com o tamanho e as réplicas de implantação do _pipeline_.

Na tabela abaixo, você pode ver quantas RTUs são consumidas por cada tamanho de implantação de _pipeline_:

| **Tamanho** | **RTUs Consumidos** |
| ----------- | ------------------- |
| pequeno     | 1                   |
| médio       | 2                   |
| grande      | 4                   |

**Réplicas** consumirão tantas RTUs quanto a multiplicação do número de réplicas e o número de RTUs para o tamanho da implantação do _pipeline_.

Sempre que uma _pipeline_ é implantado em um determinado ambiente, diz-se que uma _pipeline subscription_ foi consumida nesse ambiente. Independentemente do número de RTUs disponíveis, você só poderá implantar a quantidade de pipelines correspondente à quantidade de _pipelines subscription_ disponíveis.

### Versões das pipelines&#x20;

Duas versões _Major_ diferentes da mesma _pipeline_ são consideradas duas _pipelines_ diferentes e exclusivas e, portanto, consomem duas _pipeline subscriptions_.

Para cada _pipeline subscription_, apenas uma versão de _pipeline_ pode estar ativa em um determinado ambiente e momento.&#x20;

### Validação de subscriptions e RTUs&#x20;

Antes de cada implantação da _pipeline_ em um determinado ambiente, um algoritmo é aplicado: primeiro, o algoritmo verifica se o número de _pipelines_ exclusivos implantados é menor que o número de _pipeline subscriptions_ disponíveis. Se essa verificação for aprovada, o algoritmo verificará se o número de RTUs disponíveis para esse ambiente específico pode acomodar o número de RTUs solicitadas para essa implantação de _pipeline_. Caso essa checagem passar, a _pipeline_ será implantada. Caso contrário, a implantação falhará devido à falta de _pipeline subscriptions_ disponíveis ou de RTUs disponíveis.

### Regras para RTUs implantadas

As RTUs de teste e produção se acumulam à medida que _pipeline subscriptions_ são adicionadas. Quando uma _pipeline_ é implantada em um determinado ambiente, o número de RTUs correspondentes é deduzido do número total de RTUs disponíveis nesse ambiente. Quando não houver mais RTUs disponíveis em um determinado ambiente, nenhum _pipeline_ adicional será implantado.

RTUs de teste e RTUs de produção são destinados a serem usados em seus respectivos ambientes e não podem ser trocados.

O uso de RTUs de Teste ou Produção sempre requer uma _pipeline subscription_ existente. As RTUs sobressalentes não podem ser usadas para executar pipelines que não tenham uma _pipeline subscription_ associada a ela.
