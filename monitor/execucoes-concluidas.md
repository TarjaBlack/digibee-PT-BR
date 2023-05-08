---
description: Acompanhe as métricas de pipelines e monitore as integrações implantadas.
---

# Execuções concluídas

Na aba de execuções concluídas, você pode acompanhar as execuções dos pipelines e de seu histórico de logs, assim como reexecutá-los.

## Seleção de ambiente&#x20;

Você pode selecionar o ambiente desejado no canto superior esquerdo. Quando você seleciona um ambiente, a página inteira é atualizada para mostrar os dados relativos aos pipelines naquele ambiente.

![](<../.gitbook/assets/seletordeambiente (2) (1).png>)

## **Campos de busca**

Você pode filtrar execuções de pipelines utilizando os seguintes parâmetros:

* **Tipo de mensagem** : o status de execução do pipeline
  * **Resposta** : execuções concluídas sem nenhuma interrupção
  * **Erro** : execuções interrompidas
  * **Todos** : qualquer execução
* **Nome do pipeline** : o nome completo do pipeline
* **Versão do pipeline** (_major_ ou _minor_)
* **Pipeline key** : um identificador único de uma execução de um pipeline
* **Payload** : o input ou output do pipeline em formato JSON. Esse campo de busca utiliza [a sintaxe simple query do Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-simple-query-string-query.html#simple-query-string-syntax)
* **Origem :** o trigger do pipeline
* **Código do Erro:** um código de erro de uma execução de pipeline, de acordo com o [padrão HTTP de códigos de erro](https://pt.wikipedia.org/wiki/Lista\_de\_c%C3%B3digos\_de\_estado\_HTTP)

As execuções concluídas são exibidas abaixo, de acordo com os parâmetros especificados:

<figure><img src="https://i.imgur.com/h5YSSAz.png" alt=""><figcaption><p>Tabela de execuções concluídas</p></figcaption></figure>

Você pode clicar no ícone de lupa para ver os [detalhes da execução](execucoes-concluidas.md#detalhes-da-execucao) ou no ícone de atualização para reexecutar o pipeline.

Para que o pipeline seja reexecutado manualmente, seu trigger deve possuir a opção “Allow Redelivery of messages” ativada. É importante notar que você deve re-executar um pipeline manualmente somente quando estiver buscando solucionar um problema, nunca como parte de seu processo de integração.

## Detalhes da execução

Se você clicar no ícone de lupa na tabela de execuções concluídas, um modal aparecerá exibindo os detalhes da execução.

<figure><img src="https://i.imgur.com/cL9NmDr.png" alt=""><figcaption><p>Modal de detalhes da execução</p></figcaption></figure>

No modal de detalhes da execução, você pode ver o(s):

* **Pipeline key** : um identificador único de uma execução de um pipeline
* **Mensagem da requisição :** os dados enviados pelo trigger do pipeline
* **Mensagem da resposta :** o _output_ do pipeline
* [**Logs da execução**](https://docs.digibee.com/help-center/v/pt-br/monitor/pipeline-logs)

Você também pode clicar no botão no canto superior direito para acessar no Canvas o _pipeline_ cuja execução você está analisando. Esse botão está na fase Beta. Você pode aprender mais sobre o programa Beta da Digibee [aqui](../geral/programa-beta.md).

<figure><img src="https://i.imgur.com/eoXbkB5.png" alt=""><figcaption></figcaption></figure>

Chamamos de “[mensagem](https://docs.digibee.com/help-center/v/pt-br/build/pipelines/processamento-de-mensagens)” o dado que é transmitido em formato JSON através do pipeline. Cada componente da pipeline recebe, manipula e exporta uma mensagem. Apenas as 50 primeiras mensagens do pipeline serão exibidas, e somente para pipelines executados em modo de teste.

Em alguns casos, a plataforma apresenta payloads truncados, de acordo com os seguintes critérios:

| Tamanho do Payload |               Exibição              |
| :----------------: | :---------------------------------: |
|   Menor que 32kb   |          Exibição completa          |
| Entre 32kb e 320kb |           Exibição parcial          |
|   Maior que 320kb  | Aviso @@DGB\_TRUNCATED@@ é mostrado |

