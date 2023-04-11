---
description: Tenha uma visão geral das ferramentas disponíveis na página Build.
---

# Visão geral de Build

Na página de Build, você pode criar e gerenciar pipelines e projetos. Nesta página, você pode encontrar o botão CRIAR no canto superior direito, a lista de Projetos no canto esquerdo e a lista de pipelines na parte inferior.

## Build layout

Ao selecionar Build, o layout da página aparece como mostrado na figura abaixo. No canto superior esquerdo estão o **Pipeline** e as **Cápsulas**. Quando você seleciona Pipeline, os projetos e pipelines criados são exibidos.

No meio da tela, abaixo das informações do Novo Canvas, você encontrará todos os pipelines criados. Ao clicar em Cápsulas, as Cápsulas criadas também serão exibidas. No canto direito você encontrará o botão **CRIAR**.

Nas próximas seções, você aprenderá mais sobre cada ferramenta.

<figure><img src="../.gitbook/assets/01 - Build Layout - port.jpg" alt=""><figcaption></figcaption></figure>

## Botão CRIAR

Você pode clicar no botão **CRIAR** no canto superior direito da tela para criar um novo pipeline ou projeto. Você também pode encontrar o botão CRIAR na tela Run.

<figure><img src="../.gitbook/assets/02 - CRIAR.jpg" alt=""><figcaption></figcaption></figure>

### Criar um pipeline

Para criar um pipeline, selecione **Pipeline** ou **Pipeline (Beta)**. Se você selecionar Pipeline (Beta), um novo pipeline será criado usando o novo Canvas. [Para saber mais sobre o Canvas, leia este artigo.](https://docs.digibee.com/documentation/v/pt-br/build/canvas)

<figure><img src="../.gitbook/assets/03 - icone.jpg" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
IMPORTANTE: A diferença entre Pipeline e Pipeline Beta é que na versão Beta você terá o Novo Canvas, onde são disponibilizadas diversas funcionalidades e você terá um melhor desempenho na criação e manutenção de seus pipelines. [Para saber mais sobre o Novo Canvas, leia este artigo.](https://docs.digibee.com/documentation/v/pt-br/build/novo-canvas-beta-restrito)
{% endhint %}

### Criar um projeto

Para criar um novo projeto, selecione **Projeto**. Projetos são pastas onde você pode armazenar seus pipelines. Uma folha lateral aparecerá onde você pode inserir o nome e a descrição do projeto e atribuir o projeto a usuários específicos.

<figure><img src="../.gitbook/assets/04 - criar projeto.jpg" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
IMPORTANTE: Se você marcar **Selecionar todos os usuários**, todos os usuários em seu domínio poderão acessar o novo projeto e, portanto, os pipelines nele.
{% endhint %}

<figure><img src="../.gitbook/assets/05 - associacao.jpg" alt=""><figcaption></figcaption></figure>

Se você deseja que apenas determinados grupos tenham acesso ao seu projeto, clique em **Grupo associados** e selecione os grupos aos quais deseja conceder acesso ao seu projeto.

Após selecionar e preencher os campos, clique em **Salvar** e seu projeto estará criado.

## Projetos

No canto esquerdo da tela Build, você verá uma lista de projetos aos quais você tem acesso e dentro de cada projeto você encontrará os pipelines que foram criados. [Para saber mais sobre projetos e como eles funcionam, leia este artigo sobre Projetos.](https://docs.digibee.com/documentation/v/pt-br/build/projetos)

<figure><img src="../.gitbook/assets/06 - Projetos.jpg" alt=""><figcaption></figcaption></figure>

### Lista de pipelines

Quando você clica em um projeto, os pipelines desse projeto são exibidos em ordem alfabética. Você verá o nome e a versão de cada pipeline, bem como botões para criar uma nova versão do pipeline e visualizar seu histórico de construção.&#x20;

[Você pode aprender mais sobre o histórico de versões de pipelines neste artigo.](https://docs.digibee.com/documentation/v/pt-br/build/pipelines/historico-de-versoes-de-pipelines)

<figure><img src="../.gitbook/assets/07 - lista pipelines.jpg" alt=""><figcaption></figcaption></figure>

## Cápsulas

Perto de Pipeline no lado esquerdo, temos Cápsulas. É funcionam como se os componentes disponíveis na plataforma fossem átomos e as cápsulas fossem moléculas que agrupam os átomos em tarefas mais complexas para resolver um determinado problema.&#x20;

<figure><img src="../.gitbook/assets/08 - Capsulas.jpg" alt=""><figcaption></figcaption></figure>

[Para saber mais sobre isso, leia nosso artigo sobre Cápsulas aqui.](https://docs.digibee.com/documentation/v/pt-br/build/capsulas)
