---
description: Entenda mais sobre a transição para o novo modelo de acesso.
---

# Transição do novo Controle de Acesso

Junto com o novo modelo de controle de acesso, desenvolvemos esta funcionalidade para que os usuários possam sinalizar que já fizeram a transição do modelo antigo para o modelo novo. Isso permitirá ao time de Produto desligar o modelo antigo sem impacto nos realms.

Atualmente, os dois modelos de controle de acesso estão funcionando em um modelo de soma de permissões, para minimizar a perda de acesso devido a transição entre eles. Isso quer dizer que caso um usuário tenha uma permissão em qualquer um dos modelos e não tenha no outro, ele terá acesso ao recurso da Plataforma.

A data de desligamento do modelo antigo será apresentada na própria Plataforma, por meio de uma mensagem na tela de usuários. Durante esse período, serão realizadas diversas campanhas para incentivar a migração para o novo modelo de controle de acesso.

Clientes que não migrarem até o período informado, serão migrados automaticamente para o novo modelo, onde os acessos antigos serão "traduzidos" para o novo modelo.

## Antes de começar <a href="#h_a4fcde2719" id="h_a4fcde2719"></a>

Leia os seguintes artigos e conheça mais sobre o Novo Controle de Acesso:

* [Novo modelo de controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5808132-novo-modelo-de-controle-de-acesso)
* [Conceitos básicos sobre usuários.](https://intercom.help/godigibee/pt-BR/articles/5808313-conceitos-basicos-sobre-usuarios)
* [Papéis do controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5810244-papeis-do-controle-de-acesso)
* [Grupos do controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5810361-grupos-do-controle-de-acesso)

## Como executar sua transição de acessos <a href="#h_6e3d3c52ae" id="h_6e3d3c52ae"></a>

Após criar Grupos, Usuários e Papéis conforme os artigos acima, acesse a tela de Usuários onde será possível verificar se todos os usuários estão aptos à transição.

Nesta tela, aparecerá uma mensagem sobre a data limite para fazer a transição de usuário.

![](<../../.gitbook/assets/Imagem 1 (7).png>)

Os usuários que ainda não tiveram seus acessos replicados no novo modelo (ou seja, que não foram adicionados à lista de membros em grupos do controle de acesso) aparecerão com um ícone de atenção na tela de usuários.

Ao final da transição, todos os usuários devem apresentar um ícone de checkmark verde e a mensagem a seguir deve aparecer no topo da tela, substituíndo a mensagem sobre data limite da transição:

![](<../../.gitbook/assets/Imagem 2 (4).png>)

### Tutorial sobre a transição para o novo controle de acesso

Você pode assistir ao vídeo a seguir ou continuar lendo esse artigo para aprender como realizar a transição do seu realm para o novo controle de acesso:

{% embed url="https://vimeo.com/689012591" %}

### Para usuários com acessos replicados no novo modelo: <a href="#h_aae1ee6cbf" id="h_aae1ee6cbf"></a>

Neste exemplo abaixo, os três usuários já estão vinculados a um ou mais grupos. Ao clicar em "**Verificar**'', é possível visualizar os grupos aos quais o usuário pertence e a lista de permissões de cada um deles.

![](<../../.gitbook/assets/Imagem 3 (6).png>)

### Para usuários ainda sem acessos replicados no novo modelo: <a href="#h_8a410827cf" id="h_8a410827cf"></a>

Se algum usuário não pertencer a um ou mais grupos, você verá o ícone de atenção

ao lado do usuário.

![](<../../.gitbook/assets/Imagem 4.png>)

Neste cenário, você deve criar ou atualizar grupos e papéis para adicionar permissões aos usuários.

A transição de usuários pode ser realizada um a um ou de múltiplos usuários de uma só vez.

## Como migrar os usuários individualmente <a href="#h_b245713d19" id="h_b245713d19"></a>

1. Faça login na Digibee Integration Platform;
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Usuários”

![](<../../.gitbook/assets/image (21) (1).png>)

4\. Busque o usuário na barra de pesquisa;

5\. Clique em **“VERIFICAR”** ao lado do usuário\*\*;\*\*

![](<../../.gitbook/assets/Imagem 6 (5).png>)

6\. Uma tela contendo as informações do usuário aparecerá, se estiverem corretas, clique em “**REMOVER ACESSOS ANTIGOS**”.

7\. Feito isso, veremos o ícone ao lado do usuário, indicando que aquele usuário foi migrado para o novo controle de acesso.

![](<../../.gitbook/assets/Imagem 7 (2).png>)

## Como migrar múltiplos usuários <a href="#h_4a33506010" id="h_4a33506010"></a>

Para facilitar o processo de transição também é possível fazer a revogação em massa dos acessos antigos. No entanto, somente realize este processo caso tenha certeza que todos os usuários foram revisados e que estão com seus acesso configurados de maneira correta. Para realizar a transição em massa siga os seguintes passos:

1. Faça login na Digibee Integration Platform;
2. Clique no ícone de “Administração” ;
3. Entre na opção do menu “Usuários”;
4. Clique em “**VERIFICAR TODOS**” no canto superior direito.

![](<../../.gitbook/assets/Imagem 8 (2).png>)

Nesta tela podemos ver fatores importante como:

* A quantidade de usuários prontos para a transição;
* Um botão de download, que permite baixar um JSON contendo as permissões;

![](<../../.gitbook/assets/Imagem 9 (2).png>)

Para realizar a transição de todos os acessos antigos de todos os usuários de uma vez só, tenha certeza que eles já foram vinculados a novos grupos contendo suas antigas permissões. Caso contrário eles perderão acesso às funcionalidades e serviços da Digibee Integration Platform.

**IMPORTANTE**: Ao clicar no botão "**REMOVER ACESSOS ANTIGOS**”, caso todos os usuários já tenham sido replicados no novo modelo. Não existirá tela de confirmação, e todos acessos antigos serão desligados.

Quando estiver tudo pronto, clique em “**REMOVER ACESSOS ANTIGOS**”.

Caso haja alguma pendência, uma tela de confirmação aparecerá, caso queira prosseguir clique novamente em “**REMOVER ACESSOS ANTIGOS**”.

![](<../../.gitbook/assets/imagem 10.png>)

Ao finalizar estes passos, a transição dos usuários terá sido feita com sucesso e a mensagem a seguir substituirá a mensagem original sobre a data limite da transição de acesso:

**IMPORTANTE:** Ao clicar no botão de “**REMOVER ACESSOS ANTIGOS**” e confirmar a ação. Mesmo se o navegador for fechado, o processo seguirá acontecendo. Portanto, só faça o processo quando for remover os acessos antigos em definitivo.
