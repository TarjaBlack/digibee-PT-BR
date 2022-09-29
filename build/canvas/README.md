---
description: >-
  Saiba mais sobre o ambiente de construção de pipelines da Digibee Integration
  Plaform
---

# Canvas

O _Canvas_ é o ambiente de construção de _pipelines_ da Digibee Integration Plaform. Através dele, você consegue desenvolver integrações simples ou complexas arrastando e soltando componentes pré-configurados com rapidez e precisão.

## Informações iniciais <a href="#h_c2c95ff14a" id="h_c2c95ff14a"></a>

Para criar seu pipeline, acesse a aba Build e clique em **+CRIAR**, selecionando a opção _**Pipeline**_.

## Configurações do _pipeline_ <a href="#h_8e2011d038" id="h_8e2011d038"></a>

Antes de partir para a construção do fluxo, é preciso configurar o _pipeline_. Para isso, clique na engrenagem (![](https://lh3.googleusercontent.com/PDFbPxPG25G7iTGz\_erHpVfi3DftPBrZ-2LZtRx2weEXKTIaol65mA6UrA19ZkOLuga6I60mf0imvLK8BomnmaHcGQmNw\_7aJRPAMDOtgwMjbHK976caIlTPuxoBIPVDS2xdOLhAHe1URou8TQ)) no canto superior direito do Canvas.

![](<../../.gitbook/assets/01 (1).png>)

Na página de configurações do _pipeline_, se necessário, configure os seguintes campos:

![](<../../.gitbook/assets/02 (6).png>)

* **Descrição**: descreva o _pipeline_.
* **“É multi-instância?”**: acione esta opção caso o _pipeline_ a ser criado seja multi-instância. Para saber mais sobre essa funcionalidade, leia o artigo [Multi-instância](../../configurations/multi-instancia.md).
* **Campo sensível:** defina quais dados precisam ser mascarados durante a execução do fluxo.
* **InSpec:** especifique a entrada do fluxo do _pipeline_.
* **OutSpec:** especifique a saída do fluxo do _pipeline_.

Após configurar o _pipeline_, você poderá partir para a construção do fluxo.&#x20;

## Crie um fluxo <a href="#h_c35f0fc316" id="h_c35f0fc316"></a>

Todo _pipeline_ é composto por um _trigger_ e por pelo menos um componente, que devem ser conectados entre si para que possam estabelecer um fluxo de integração. No _Canvas_ você consegue organizar e configurar o _trigger_ e os componentes do seu _pipeline_ de acordo com a sua necessidade de negócio.

### Trigger <a href="#h_080f25dba4" id="h_080f25dba4"></a>

O primeiro passo para criar um fluxo é escolher um _trigger_. O _trigger_ é o elemento que define como a execução do _pipeline_ será iniciada - através de uma chamada externa, em resposta a um evento ou via agendamento, por exemplo. Atualmente, estão disponíveis diferentes tipos de _trigger_, são eles:

* rest
* event
* scheduler (custom, midnight, 30min, 5min)
* http
* http-file
* email
* email-v2
* kafka
* rabbitmq
* jms

Para defini-lo, basta clicar na engrenagem sobre o trigger (![](https://lh3.googleusercontent.com/LXIoYs3fSutzp-9Zmw3u-Xx5wLMCRBnBdkFCXsoHbH3lWww\_FQoMi9Z6-xnXTQBPPP4ad9yWIlZaXm2Fyy7F7nrU092dti3-OUUSw7TohMZ5d\_cA66IKSJ9Un7eaZlwFTvcKRYMo6UQU8QPUMQ)) e escolher entre as opções listadas, conforme o exemplo abaixo:

![](../../.gitbook/assets/03.gif)

### Componentes <a href="#h_282c4b0fe6" id="h_282c4b0fe6"></a>

Os componentes representam etapas do fluxo e são escolhidos de acordo com as suas necessidades de negócio. Combine todas as etapas do processo de integração que deseja realizar utilizando a lista de componentes à direita do _Canvas_.

![](<../../.gitbook/assets/04 (2).gif>)

Para excluir uma conexão ou um componente específico do fluxo, clique na lixeira (![](https://lh4.googleusercontent.com/UorzdVWqIhXA06h8\_-fZraoDF1k\_0-8Hx\_T5r1wRIwTA2gU9omhLlBNyjIRHiAvlwEmshX5SUitkaCKpWTE9hel6oadijB6h69-zqu3ZwjWBdla08FaHxVdInVJ-D4u2NQxOQeagENEhs5mttA)) e no **X**.

![](../../.gitbook/assets/05.gif)

Para configurar o componente a ser utilizado, clique na engrenagem sobre ele (![](https://lh3.googleusercontent.com/LXIoYs3fSutzp-9Zmw3u-Xx5wLMCRBnBdkFCXsoHbH3lWww\_FQoMi9Z6-xnXTQBPPP4ad9yWIlZaXm2Fyy7F7nrU092dti3-OUUSw7TohMZ5d\_cA66IKSJ9Un7eaZlwFTvcKRYMo6UQU8QPUMQ)) para acessar o formulário de configuração. No exemplo abaixo, é possível visualizar o formulário do [componente Google Drive](../../components/file-storage/google-drive.md).

![](<../../.gitbook/assets/06 (1).gif>)

Para saber mais a respeito de cada componente disponível em nossa lista, acesse a nossa [Documentação de componentes](broken-reference/).

### Botões de controle do _Canvas_ <a href="#h_18ac7e89a6" id="h_18ac7e89a6"></a>

![](<../../.gitbook/assets/07 (7).png>)

Você pode facilmente navegar pelo pipeline através dos botões **Reorganizar** (![](https://lh3.googleusercontent.com/J27T\_GWpXoBVLl4TWDx1fp6efXkbGFo9wgmIDTc6Efa1J9mF1c7GU-Shbrpm039UvBZoDqGsQZ58Yja7v3Jvy\_rrBMW\_d3fOtdFMtc7o2B6EpxCz8RlLTd7bZl-GgMXdaAQ-2wuKwHRXxN7txw)), **Ampliar zoom** (![](https://lh6.googleusercontent.com/2qvd6tDFPXxQQEw7JOdrf6z18Aa\_TBZDVXwI5hOyISuAb7dnn\_-CR4oQ7CG0\_Q4UDmza3dRguNiat4etM6U5FOa2Ed0xhJquz4cxE7Drgmlu8rFPJkA39ffwODdbf2baOFfypbQRsFp5fA7Aiw)) e **Reduzir zoom** (![](https://lh5.googleusercontent.com/g\_yrggzADfZNnyO-S1rL53A6whsgcX2XB9oSwGcc5Xd8rIx-qS8yWSpVKHcYnCk3w77cgHkXhVdLKAESPfgL8JkjBSL3n8Sxjj0pJVfCEJs0HSgUl9UimJtyt5plrt4Bf9DWupCVOYOay7Ljag)). O primeiro é utilizado para reorganizar os componentes utilizados de forma que facilite a visualização de cada etapa do fluxo; os outros dois são utilizados para controlar o zoom do _Canvas_.

### Test mode <a href="#h_ae41fc1aa6" id="h_ae41fc1aa6"></a>

O Test mode é uma funcionalidade da Digibee Integration Plaform que permite que você execute e teste seu _pipeline_ diretamente da área de desenvolvimento. Utilize o Test mode sempre que quiser avaliar o fluxo de integração, depurar e solucionar problemas. Para saber mais sobre essa funcionalidade, leia o artigo [Test mode](test-mode/).

## Salve o _pipeline_ <a href="#h_aa813df937" id="h_aa813df937"></a>

Por fim, após construir seu fluxo de integração, clique em **Salvar** no canto superior direito da tela, e defina um nome, uma descrição (opcional) e o projeto no qual o _pipeline_ estará alocado.

![](<../../.gitbook/assets/08 (3).png>)

![](<../../.gitbook/assets/09 (4).png>)

Caso deseje saber ainda mais sobre _pipelines_, leia o artigo [Pipeline](../pipelines/).
