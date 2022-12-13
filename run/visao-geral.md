---
description: Entenda os conceitos relacionados a Run e suas funcionalidades.
---

# Visão Geral

Run é uma das três fases da _Digibee Integration Platform_, a segunda após a construção do _pipeline_ na fase anterior de _Build_. Seu objetivo é fazer a implantação do _pipeline_, que já possui _triggers_ configurados, executá-lo e colocar a integração em produção.

## Layout de Run

Ao selecionar a fase Run, o layout da página aparecerá como na imagem abaixo. No canto superior esquerdo, estão localizados os ambientes de teste (_test_) e produção (_prod_) dos _pipelines_ a serem executados.

<figure><img src="../.gitbook/assets/layout run.jpg" alt=""><figcaption></figcaption></figure>

## **Ambientes**

Há dois ambientes nos quais é possível fazer a execução dos _pipelines_: ** **_**test**_ ou _**prod**_.

<figure><img src="../.gitbook/assets/seletordeambiente (2).png" alt=""><figcaption></figcaption></figure>

O ambiente ** **_**test**_** ** é usado para avaliar a construção do _pipeline_, ou seja, para testar e modificar suas aplicações. Desta forma, você tem um ambiente onde pode validar os _pipelines_ antes de irem para produção.

Já no ambiente _**prod**_** ** é onde o processo final de implantação do _pipeline_ ocorre após ter sido testado e validado.

## **Selecione o projeto**

Após escolher o ambiente de execução, no canto esquerdo da tela selecione o projeto que deseja implantar. Você pode [saber mais sobre os projetos aqui](https://docs.digibee.com/documentation/v/pt-br/build/projetos). Todas as versões desenvolvidas dos _pipelines_ aparecerão na tela para seleção.

<figure><img src="../.gitbook/assets/Projetos.jpg" alt=""><figcaption></figcaption></figure>

Cada _pipeline_ contém as informações de tamanho, execuções simultâneas, réplicas e licenças. Para mais detalhes sobre cada item, [leia o artigo sobre os conceitos de Run](https://docs.digibee.com/documentation/v/pt-br/run/runtime).

<figure><img src="../.gitbook/assets/cards port.jpg" alt=""><figcaption></figcaption></figure>

## **Opções no **_**pipeline**_

Algumas opções estão disponíveis no _pipeline_. Se clicar nos três pontos, duas aparecerão: **Remover implantação,** **Exibir pipeline** e **Reimplantar.**

<figure><img src="../.gitbook/assets/tres pontos.jpg" alt=""><figcaption></figcaption></figure>

A primeira opção é **Remover implantação** e, clicando nela, você pode excluir a implantação feita. Essa ação removerá somente a implantação com sua versão selecionada, não afetando outras versões.

A segunda opção é **Exibir **_**pipeline**_. Ao clicar nela, toda a arquitetura do _pipeline_ desenvolvido é exibida, assim como as informações selecionadas no _trigger_.

A terceira opção é **Reimplantar**. A principal função do Reimplantar é fazer a implantação do mesmo _pipeline_, mas alterando suas configurações. [Para saber mais sobre como reimplantar um pipeline, leia este artigo.](https://docs.digibee.com/documentation/v/pt-br/run/reimplantando-um-pipeline)



## **Selecione o **_**pipeline**_

Após fazer a implantação de um _pipeline_ novo ou selecionar um já existente, algumas informações aparecerão, como o nome do _pipeline_, versão, data e quem fez a implantação.

Além disso, o tamanho, execuções simultâneas, réplicas e licenças escolhidas anteriormente também serão exibidos. Veja mais no [artigo sobre como implantar um _pipeline_](https://docs.digibee.com/documentation/v/pt-br/run/deployments).

<figure><img src="../.gitbook/assets/selecionar pipeline.jpg" alt=""><figcaption></figcaption></figure>

Ao clicar em [_**Rest Trigger (API)**_](https://docs.digibee.com/documentation/v/pt-br/components/triggers/rest-trigger), você tem acesso a mais detalhes sobre: _endpoint, maximum timeout, additional API routes, API key, token JWT, the maximum allowed request sinc., external API, allow redelivery of messages, methods_ e _internal API_. Temos uma [lista de artigos sobre os _triggers_ disponíveis](https://docs.digibee.com/documentation/v/pt-br/components/triggers).

<figure><img src="../.gitbook/assets/trigger run.jpg" alt=""><figcaption></figcaption></figure>

## **Próxima fase**

Você pode acompanhar como o _pipeline_ está funcionando na próxima fase da _Digibee Integration Platform_, chamada _Monitor._

Lá você terá informações como o número de _pipeline_ criados e implantados, a quantidade de contas criadas, um gráfico da monitoração e também um relatório individual. Para saber mais sobre esta fase, [leia o artigo que preparamos](https://docs.digibee.com/documentation/v/pt-br/monitor/dashboards).

_****_

****
