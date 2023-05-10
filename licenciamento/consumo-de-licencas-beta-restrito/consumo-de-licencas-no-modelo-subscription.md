---
description: >-
  Saiba mais sobre a página de visualização de seus pipelines subscriptions e
  seu consumo de RTUs.
---

# Consumo de Licenças no modelo Subscription

{% hint style="info" %}
Essa _feature_ está na fase[ Beta Restrito](https://docs.digibee.com/documentation/v/pt-br/geral/programa-beta) e está disponível apenas para clientes específicos.
{% endhint %}

O recurso **Consumo de Licenças** agora permite que você rastreie seus _pipelines subscriptions_ e seus _Runtime units_ (RTUs) com facilidade. Você pode obter o número de _pipelines subscriptions_ para o seu _Realm_, bem como o valor total disponível. Além disso, você pode verificar o número de RTUs disponíveis nos ambientes de _test_ e _prod_ do seu _Realm_, para poder analisar e implantar seus _pipelines_ com mais eficiência.

## Visão geral do Consumo de Licenças

No [modelo baseado em _Subscription_](https://docs.digibee.com/documentation/v/pt-br/licenciamento/modelos-de-licenciamento/modelo-baseado-em-subscription)_,_ você pode acompanhar seu uso e gerenciar seus _pipelines subscriptions_ e seus _Runtime Units_ (RTUs)  disponíveis em seu _Realm_. Para acessar esse recurso, vá para `Configurações` no canto superior direito e clique em **Consumo de Licenças** em `Licenciamento` no canto inferior esquerdo da página.

Para acessar esta página, você deve ter a permissão de **visualizador de licença** para sua conta de usuário ou um grupo ao qual você pertence.

<figure><img src="../../.gitbook/assets/01 - gif - rtu - port.gif" alt=""><figcaption></figcaption></figure>

### Detalhes

Nesta página, você pode verificar o número de _pipeline subscriptions_ e RTUs em seu _Realm_ para um ambiente escolhido. A lista de contatos dos responsáveis está localizada no lado direito da página. Você pode procurar por um projeto específico pelo nome usando a área de **BUSCA** na parte inferior da página.&#x20;

Além disso, há um botão **EXPORTAR** próximo à barra de pesquisa que fornece um arquivo `CSV` contendo uma lista com nomes de projetos, ambientes em que se encontram, nome do _pipeline_, tamanho implantado, número de réplicas e RTUs usados.

No final da página, uma lista de todos os seus projetos é exibida, incluindo suas informações como nome do projeto, descrição, ambiente, número de _pipelines_ e RTUs usados.

Para ver uma descrição detalhada de cada projeto, clique no ícone **Ações**. A seguir, verifique cada um desses itens nas seções seguintes.

## Painel de consumo

<figure><img src="../../.gitbook/assets/02 - painel - port (1).jpg" alt=""><figcaption></figcaption></figure>

Nesta seção, você pode selecionar o ambiente para o qual deseja ver o consumo. Use o menu no canto superior esquerdo para fazer sua escolha. Depois de fazer sua escolha, será exibido o número de _pipelines_ (consumidos, disponíveis e contratados), bem como as RTUs associadas.&#x20;

Este painel fornece _insights_ e informações que permitem que você tome decisões sobre a alocação e otimização de recursos.

## Informações do projeto

### Busca

Para visualizar os detalhes de consumo de um determinado projeto, use a função de pesquisa. Selecione o projeto na caixa de pesquisa e clique no botão **BUSCA** para obter seus detalhes. Você também pode exportar a lista de consumo dos projetos para um arquivo `CSV` clicando em **EXPORTAR**.

<figure><img src="../../.gitbook/assets/03 - busca - port (1).jpg" alt=""><figcaption></figcaption></figure>

Como resultado, você obtém uma lista detalhada de cada consumo dos projetos: nome do projeto e descrição, ambiente, quantidade de _pipelines_ no projeto, quantidade de RTUs utilizadas e um ícone para clicar em **Ações**.

### Ícone Ações

Para ver informações específicas sobre um projeto selecionado, clique no ícone de Ações para abrir uma aba lateral. Depois que os **Detalhes do projeto** estiverem abertos, você poderá visualizar informações sobre cada _pipeline_ associado a esse projeto.

Essas informações incluem o nome do projeto, o ambiente, o nome do _pipeline_, o tamanho da implantação, o número de réplicas e o número de RTUs usados para a implantação.

<figure><img src="../../.gitbook/assets/04 - detalhes projeto - port.jpg" alt=""><figcaption></figcaption></figure>

### Lista de Projetos

Na parte inferior da página, você encontrará uma lista de todos os projetos no ambiente selecionado. Essa lista contém informações como o nome e a descrição do projeto, o ambiente, o número de _pipelines_, o número de RTUs usados e um ícone de Ações.

<figure><img src="../../.gitbook/assets/05 - lista - port.jpg" alt=""><figcaption></figcaption></figure>

## Lista de contatos

No canto superior direito, você encontrará uma lista de contatos contendo os responsáveis pela sua conta. Para enviar um e-mail diretamente a uma pessoa, clique no ícone do e-mail.

<figure><img src="../../.gitbook/assets/06 - contatos - port (1).jpg" alt=""><figcaption></figcaption></figure>
