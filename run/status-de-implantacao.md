---
description: Entenda o novo recurso em Run e como usá-lo.
---

# Status de implantação

Ao executar um _pipeline_ na fase de Run, algumas informações são exibidas no _card_ do _pipeline_, como o dia e a hora em que foi implantado. Com o novo recurso, agora é possível obter informações sobre o _pipeline_ em tempo real e saber como ele funciona.

## Informações em tempo real&#x20;

Agora, quando o _pipeline_ é implantado, é possível ver o status da implantação em tempo real. Com as seguintes informações: **Falha**, **Em progresso** e **Disponível**:

<figure><img src="../.gitbook/assets/Status informação.png" alt=""><figcaption></figcaption></figure>

## **Status: Falha**

Se as informações no _pipeline_ aparecerem como **Falha**, isso significa que algo de errado aconteceu e a implantação foi interrompida. Essas informações podem ser usadas para determinar o que causou a falha do _pipeline_.&#x20;

Por exemplo, pode ser um erro na etapa de _**Build**_ ou uma seleção de **Tamanho** que não tem suporte porque o _pipeline_ é muito grande.

<figure><img src="../.gitbook/assets/Status Falha.jpg" alt=""><figcaption></figcaption></figure>

## **Status: Em progresso**

O status **Em progresso** informa como está indo a implantação do _pipeline_. Essas informações possibilitam o gerenciamento do tempo de implantação dos _pipelines_ e o planejamento da próxima implantação.

<figure><img src="../.gitbook/assets/Status Em progresso.jpg" alt=""><figcaption></figcaption></figure>

## **Status: Disponível**

Se o status do _pipeline_ for **Disponível**, significa que a implantação do _pipeline_ foi concluída com sucesso. Com essas informações, você já pode começar a implantar outro _pipeline_. Dessa forma, você pode gerenciar os _pipelines_ que deseja implantar.

<figure><img src="../.gitbook/assets/Status Disponível.jpg" alt=""><figcaption></figcaption></figure>
