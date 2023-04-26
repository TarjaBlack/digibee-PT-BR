---
description: Saiba mais sobre o primeiro modelo de licenciamento oferecido pela Digibee.
---

# Modelo baseado em Pipeline

O modelo baseado em _Pipeline_ foi o primeiro licenciamento oferecido pela Digibee a seus clientes. Esse licenciamento ainda é usado por alguns clientes, mas não está mais disponível comercialmente. Tenha uma visão geral do que este licenciamento oferece e como funciona na Digibee Integration Platform.

## Licenças

No modelo baseado em _Pipeline_, pelo menos dez (10) licenças são oferecidas por cliente. Cada licença inclui um (1) _Pipeline_ e um (1) RTU (_Runtime Unit_). Cada implantação, seja no ambiente de _test_ ou _prod_, consome uma (1) licença.

Observe que você pode criar quantos _pipelines_ desejar. A licença é consumida somente quando implanta um _pipeline_.

## Ambientes

Com este modelo de licenciamento, você pode usar apenas os ambientes padrão da Digibee Integration Platform: _**test**_ e _**prod**_. Se você quiser criar mais ambientes, o modelo _**Capacity**_ dá a opção de ter mais ambientes.&#x20;

[Se você quiser saber mais sobre o modelo Capacity, leia este artigo.](https://docs.digibee.com/documentation/v/pt-br/licenciamento/modelos-de-licenciamento/modelo-baseado-em-capacity)

## Hospedagem da plataforma

A Digibee Integration Platform é hospedada pelo _Google Cloud Platform_ (GCP), o que significa que a plataforma é desenvolvida de acordo com o modelo _Software as a Service_ (_SaaS_). Isso significa que a infraestrutura de Nuvem (_Cloud)_ que faz parte desse modelo é de responsabilidade da Digibee e não do cliente.

Existe ainda outro modelo de licenciamento, o modelo _Capacity_ , em que o cliente pode utilizar o sua própria Nuvem (_Cloud_), além de na Digibee Integration Platform poder ser utilizados diferentes tipos de nuvens.&#x20;

## Plataforma compartilhada

A Digibee Integration Platform é uma plataforma compartilhada onde todas as contas compartilham da mesma plataforma e de todos os recursos disponíveis. Entretanto, cada conta de usuário pertence a um único _Realm_.&#x20;

Os dados não podem ser compartilhados entre _Realms_ e essas informações não são compartilhadas entre eles. Tudo é controlado pelo sistema de segurança da Digibee.

## Necessidades de infraestrutura e negócios

Um ponto importante neste modelo são as necessidades de infraestrutura e negócios da empresa, ou seja, um (1) _pipeline_ dá direito a uma (1) licença, o que corresponde a um _Small Runtime_ (RTU) _slot_. Os tamanhos de implantação oferecidos pela Digibee Integration Platform são: _Small_ (1 RTU ou 1 licença), _Medium_ (2 RTUs ou 2 licenças), e _Large_ (4 RTUs  ou 4 licenças).

| Tamanho  | Consumo de Licença |
| -------- | ------------------ |
| _Small_  | 1                  |
| _Medium_ | 2                  |
| _Large_  | 4                  |

Por exemplo, neste modelo, se de dez (10) _Pipelines_, um tiver que ser utilizado no tamanho _Large_ (4 RTUs), apenas sete (7) fluxos serão cobertos em dez (10) RTUs, assumindo sempre o mesmo ambiente, como podemos ver abaixo:

<figure><img src="../../.gitbook/assets/Runtime - port.jpg" alt=""><figcaption></figcaption></figure>

Nesse caso, você precisaria comprar mais licenças para continuar usando os fluxos restantes. O modelo baseado em _**Subscription**_ funciona de maneira diferente: cada _pipeline_ tem 2 RTUs em _**prod**_ e 1 RTU em _**test**_, o que facilita a implantação do pipeline.

[Saiba mais sobre o modelo baseado em _Subscription_ neste artigo.](https://docs.digibee.com/documentation/v/pt-br/licenciamento/modelos-de-licenciamento/modelo-baseado-em-subscription)

## Consumo de licenças

No modelo baseado em _Pipeline_ e nos outros modelos, você pode acompanhar seu uso e gerenciar os _pipelines_ e as licenças disponíveis em seu _Realm_. Basta acessar as configurações no canto superior direito e clicar em **Consumo de licenças** no canto inferior esquerdo da página.

<figure><img src="../../.gitbook/assets/Consumo licença.jpg" alt=""><figcaption></figcaption></figure>

Nesta página você pode ter uma visão geral do consumo em seu _Realm_. Para acessar esta página, você deve pertencer a um grupo vinculado à função que possa **visualizar licenças**.
