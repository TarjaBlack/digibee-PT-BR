---
description: Saiba como implantar um pipeline em teste ou em produção
---

# Implantação de um pipeline

Uma vez que o fluxo do _pipeline_ tenha sido criado, o próximo passo é disponibilizá-lo para uso, isto é, implantá-lo. Na aba _Run_, você consegue implantar seu _pipeline_ em segundos com base no tamanho da implantação. Essa implantação pode acontecer tanto no ambiente de teste (_test_) quanto no ambiente de produção (_prod_).

Se quiser saber mais sobre a etapa de Run, onde é feita a gestão das implantações, consulte o [artigo Conceitos de Run](runtime.md).

## **Como implantar um **_**pipeline**_**?** <a href="#h_a34f6b010d" id="h_a34f6b010d"></a>

O processo para implantar o _pipeline_ em teste ou em produção é simples. Veja:

### Tela de Run

Acesse a tela de _Run_ e clique no botão **+ CRIAR**.

![](<../.gitbook/assets/1 - Run - Tela Principal (1).jpg>)

### Configurando o _pipeline_ a ser implantado

#### Selecionando o _pipeline_, a versão e o tamanho

Selecione um pipeline e sua versão, e em seguida, escolha o tamanho da implantação. Caso seja um _pipeline_ _multi-instance_, selecione uma instância também.&#x20;

As opções de configuração serão mostradas como no exemplo abaixo:

![](<../.gitbook/assets/2 - Implantar Pipeline.jpg>)

Caso o _pipeline_ já esteja implantado, uma seção será exibida informando as configurações atuais, e essas serão automaticamente aplicadas à nova implantação.&#x20;

Ainda nesta seção, é possível visitar o _pipeline_ atualmente implantado através do _link_ **Abrir o **_**pipeline**_** em uma nova aba**.

![](<../.gitbook/assets/3 - Implatacao Atual Pipeline.jpg>)

#### Selecionando as execuções simultâneas&#x20;

Selecione a quantidade de execuções simultâneas, como no exemplo abaixo:

<figure><img src="../.gitbook/assets/Exec. simu..jpg" alt=""><figcaption></figcaption></figure>

#### Selecionando a quantidade de réplicas  <a href="#h_dcf51c688c" id="h_dcf51c688c"></a>

Defina a quantidade de réplicas a serem utilizadas na implantação:

<figure><img src="../.gitbook/assets/Replica.jpg" alt=""><figcaption></figcaption></figure>

Caso o _pipeline_ já tenha sido implantado anteriormente, uma mensagem irá aparecer logo abaixo da seleção de réplicas.

### Implantar o _pipeline_ <a href="#h_9069fee6cc" id="h_9069fee6cc"></a>

Clique no botão **IMPLANTAR**. Ao clicar no botão **IMPLANTAR**, um resumo de todas as escolhas feitas será exibido.

Para usuários com Modelo Baseado em _Pipeline_ será exibida uma tela com o cálculo das licenças consumidas.

![](<../.gitbook/assets/7 - Botao Implantar.jpg>)

Para usuários com Modelo Baseado em _Subscription_ será exibida uma tela com o cálculo de RTUs e subscrições.

<figure><img src="../.gitbook/assets/pt deploying.png" alt=""><figcaption></figcaption></figure>

> Note que a partir de 01/04/2022 adotamos um novo modelo de controle e precificação de implantação, por isso, existe uma tela de confirmação com novas informações. Saiba mais sobre o [Modelo Baseado em _Subscription_](https://docs.digibee.com/help-center/v/pt-br/geral/novo-modelo-saas-subscription).

### **Feedback** <a href="#h_b71ada9afe" id="h_b71ada9afe"></a>

Gostaríamos de saber quais são os seus comentários e sugestões sobre essa funcionalidade. Veja como é fácil enviar o seu feedback:

![](../.gitbook/assets/Gif.gif)
