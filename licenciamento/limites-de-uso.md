---
description: Saiba mais sobre os limites de uso da Digibee Integration Platform
---

# Limites de uso

Este artigo apresenta os limites de uso aplicados na execução de _pipelines_ na Digibee Integration Platform.

Os limites de uso da plataforma são limites técnicos, criados com base no uso médio da plataforma e aplicados em cada _realm_, ou seja, no espaço privado de cada cliente dentro da plataforma, em que as integrações são construídas, armazenadas e executadas.

A aplicação dos limites é feita de acordo com a assinatura ativa, e considerando o tamanho da sua implantação. Se você não conhece os tamanhos de implantação, leia o artigo sobre a [implantação de uma _pipeline_](https://docs.digibee.com/documentation/v/pt-br/run/deployments).

Esta política de uso surgiu para melhorar o gerenciamento dos recursos oferecidos pela plataforma e trazer mais transparência ao processo.

## Consumindo recursos

Recursos computacionais são todos os itens consumidos para execução das integrações entre sistemas. Estes recursos pertencem ao [_Runtime Unit_](https://docs.digibee.com/documentation/v/pt-br/run/runtime) (RTU). A seguir, explicamos um pouco sobre cada recurso.

* **Capacidade de processamento**: é a forma de medir o tamanho de uma RTU.
* **Tráfego de saída**: é a forma de medir a quantidade de dados trafegados para fora da rede da Digibee Integration Platform.
* **Mensagem**: é a carga processada sempre que uma pipeline recebe uma solicitação, realiza o processamento e produz uma resposta.
* **MPS** (Mensagens Por Segundo): é a métrica que calcula quantas mensagens são processadas por um determinado _pipeline_ em uma única janela de 1 segundo. O número máximo de MPS é calculado para todo o _Realm_. Esse número é compartilhado em todos os pipelines implantados. O MPS está diretamente correlacionado com o tempo médio de processamento e não necessariamente com o número máximo de execuções simultâneas.
* **Fila**: a plataforma permite que as filas de pipeline sejam preenchidas com mensagens pendentes a serem processadas. O limite imposto ao enfileiramento é calculado por todas as RTUs implantadas em uma única _pipeline_.
* **Logs de execuções concluídas**: para estes _logs_, que são mostrados na página de Monitor da plataforma, sob Execuções concluídas, o limite é dado pelo tempo de retenção ou quantidade de mensagens, o que vier primeiro. A quantidade de mensagens é contabilizada pelo número de RTUs implementadas em uma determinada _pipeline_.&#x20;
* **Pipeline logs:** para estes _logs_, que são mostrados na página de Monitor da plataforma, sob Pipeline logs, o limite é dado pelo tempo de retenção ou quantidade de byes armazenados, o que vier primeiro. A quantidade de bytes armazenados é contabilizada pelo número de RTUs implementadas em uma determinada _pipeline_.&#x20;
* **Digibee Storage**: é o sistema de armazenamento em nuvem para que as _pipelines_ leiam e gravem arquivos. A forma como esses arquivos são acessados ​​é através do uso do [Digibee Storage Connector](https://docs.digibee.com/documentation/v/pt-br/components/file-storage/digibee-storage). A plataforma aplica limites no número de _bytes_ armazenados neste sistema _Cloud Storage_.&#x20;
* **Object Store**: a Digibee fornece acesso a um [sistema de armazenamento temporário de objetos](https://docs.digibee.com/documentation/v/pt-br/components/structured-data/object-store) que pode armazenar qualquer tipo de objeto JSON. Esses objetos podem ser consultados com base em regras específicas.&#x20;
  * Até 60 RTUs: 2 vCPU e 4GB RAM
  * Até 120 RTUs: 2 vCPU e 8GB RAM
  * Até 180 RTUs: 4 vCPU e 12GB RAM

Os armazenamentos de **Objetos de Produção** são fornecidos em camadas que crescem à medida que o número de RTUs aumenta, e em um padrão semelhante para cada novo bloco de 60 RTUs.&#x20;

Embora a equipe do **Digibee Capacity** sempre revise essas camadas para que as _pipelines_ possam fazer o melhor uso dos _Object Stores_, os clientes devem projetar suas pipelines de acordo com as práticas recomendadas dos _Object Stores_. O uso excessivo do _Object Store_ pode incorrer em penalidades de desempenho para as _pipelines_.

_**Test Object Stores**_ são compartilhados entre _Realms_ e crescem de acordo com as definições do **Digibee Capacity Team**. Os Armazenamentos de Objetos de Teste não devem ser muito usados. Eles devem ser usados ​​para validar os aspectos funcionais das _pipelines_.

* **Gestão de Relacionamento**: a Digibee fornece acesso a um sistema de gerenciamento de relacionamento ID, que pode armazenar mapeamentos entre dados em diferentes sistemas. O limite implícito no sistema de gerenciamento de relacionamento está relacionado à quantidade de mapeamentos exclusivos armazenados.
* **Virtual Private Network** (VPN): é possível acessar os sistemas locais de nossos clientes por meio de conexões VPN. Os _gateways_ VPN são dimensionados em intervalos de acordo com o número de RTUs na assinatura existente. As VPNs de teste são fornecidas como uma única instância de _gateway_, enquanto as VPNs de produção são fornecidas em pares para redundância.&#x20;

## Limites de cada recurso

### Limites de uso da capacidade de RTU de teste

| Limite                       | Categoria    | Valor de Limite Teste                                  | Crescimento por                         | Escopo                                     |
| ---------------------------- | ------------ | ------------------------------------------------------ | --------------------------------------- | ------------------------------------------ |
| Capacidade de processamento  | Proporcional | 64 MB / 20% de CPU / 10 execuções simultâneas          | Cada RTU                                | Um único RTU                               |
| Tráfego de saída             | Proporcional | 10GB por RTU (mensal)                                  | Cada RTU                                | Todos os RTUs no _Realm_                   |
| Mensagens Por Segundo (MPS)  | Proporcional | 1 MPS por RTU                                          | Cada RTU                                | Todos os RTUs no _Realm_                   |
| Fila                         | Proporcional | Máximo de 100.000 de mensagens na fila                 | Cada RTU                                | RTUs implantados para uma única _pipeline_ |
| Logs de execuções concluídas | Proporcional | 7 dias ou 604,800 mensagens                            | Cada RTU                                | RTUs implantados para uma única _pipeline_ |
| Pipeline logs                | Proporcional | 3 dias ou 250 MB                                       | Cada RTU                                | RTUs implantados para uma única _pipeline_ |
| Digibee Storage              | Proporcional | 10MB                                                   | Cada RTU                                | Todos os RTUs no _Realm_                   |
| _Object Store_               | Intervalo    | Veja a definição de _Object Store_ para mais detalhes. | N/A Converse com seu _Account Manager._ | Todos os RTUs no _Realm_                   |
| Gestão de Relacionamento     | Proporcional | 100.000 objetos (base) e 10.000 objetos (por RTU)      | Cada RTU                                | Todos os RTUs no _Realm_                   |
| VPNs                         | Intervalo    | 1 gateway de VPN (a capacidade do gateway VPN cresce)  | Grupo de 10 RTUs                        | Todos os RTUs no _Realm_                   |

### Limites de uso da capacidade de RTU de produção

| Limite                       | Categoria    | Valor Limite Produção                                                | Crescimento por  | Escopo                                     |
| ---------------------------- | ------------ | -------------------------------------------------------------------- | ---------------- | ------------------------------------------ |
| Capacidade de processamento  | Proporcional | 64MB / 20% CPU / 10 execuções simultâneas                            | Cada RTU         | Um único RTU                               |
| Tráfego de saída             | Proporcional | 1 TB por RTU (mensal)                                                | Cada RTU         | Todos os RTUs no _Realm_                   |
| Mensagens Por Segundo (MPS)  | Proporcional | 1 MPS por RTU                                                        | Cada RTU         | Todos os RTUs no _Realm_                   |
| Fila                         | Proporcional | Máximo de 1.000.000 de mensagens na fila                             | Cada RTU         | RTUs implantados para uma única _pipeline_ |
| Logs de execuções concluídas | Proporcional | 30 dias ou 2.592.000 mensagens                                       | Cada RTU         | RTUs implantados para uma única _pipeline_ |
| Pipeline logs                | Proporcional | 10 dias ou 1 GB                                                      | Cada RTU         | RTUs implantados para uma única _pipeline_ |
| Digibee Storage              | Proporcional | 100MB                                                                | Cada RTU         | Todos os RTUs no _Realm_                   |
| _Object Store_               | Intervalo    | Veja a definição de _Object Store_ para mais detalhes.               | Grupo de 60 RTUs | Todos os RTUs no _Realm_                   |
| Gestão de Relacionamento     | Proporcional | 10.000.000 objetos (base) 1.000.000 objetos (por RTU)                | Cada RTU         | Todos os RTUs no _Realm_                   |
| VPNs                         | Intervalo    | 2 _gateways_ VPN (redundantes, a capacidade do _gateway_ VPN cresce) | Grupo de 10 RTUs | Todos os RTUs no _Realm_                   |
