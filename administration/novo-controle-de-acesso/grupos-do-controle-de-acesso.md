---
description: Entenda mais sobre grupos e suas permissões.
---

# Grupos do Controle de Acesso

Os grupos são associações entre um conjunto de usuários e um ou mais papéis com seu respectivo ambiente (teste ou produção). É possível criar, editar e arquivar um grupo.

A criação do grupo possui nome, descrição e lista de usuários do grupo. Após criar um grupo, é necessário editá-lo para alterar suas permissões.

Neste passo, é possível adicionar, remover e alterar os vínculos, que são as associações entre um papel (e seus respectivos acessos) e os ambientes onde serão aplicados. Um grupo pode ter zero ou mais vínculos.

Caso o papel selecionado para um grupo possua apenas permissões para serviços que não necessitam de definição de ambiente, o campo ambiente ficará desabilitado (Ex: permissões para os serviços Global e Account não necessitam de definição do ambiente).

## Antes de começar: <a href="#h_a5010c206d" id="h_a5010c206d"></a>

Leia os seguintes artigos e conheça mais sobre o Novo Controle de Acesso:

* [Novo modelo de controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5808132-novo-modelo-de-controle-de-acesso)
* [Papéis do controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5810244-papeis-do-controle-de-acesso)
* [Conceitos básicos sobre usuários.](https://intercom.help/godigibee/pt-BR/articles/5808313-conceitos-basicos-sobre-usuarios)

## Como criar um novo grupo <a href="#h_3ac43c518a" id="h_3ac43c518a"></a>

Para criar um grupo, siga os passos a seguir:

1. Faça login na Plataforma Digibee.
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Grupos”;

![](<../../.gitbook/assets/Imagem 1 (1).png>)

4\. Clique no botão **+ CRIAR** no canto superior direito;

![](<../../.gitbook/assets/Imagem 2.png>)

5\. Preencha os campos de nome, descrição e caso deseje já incluir os usuários, selecione os usuários que pertencerão àquele grupo;

6\. Após preencher, clique em **SALVAR ;**

7\. Procure o grupo na barra de pesquisa;

![](<../../.gitbook/assets/Imagem 3 (5).png>)

8\. Clique em “Editar”;

9\. A janela de edição do grupo abrirá, clique em "Permissões";

![](<../../.gitbook/assets/Imagem 4 (1).png>)

10\. Nesta tela, clique em “**+ Vínculo"**

![](<../../.gitbook/assets/imagem 5 (1).png>)

11\. Selecione o papel e o ambiente.

12\. Clique em **SALVAR**.

**IMPORTANTE:** É possível vincular um ou mais papéis ao mesmo grupo, criando um acúmulo de permissões.

## Como editar um grupo <a href="#h_8dbe8e58b4" id="h_8dbe8e58b4"></a>

Para editar um grupo, siga os passos a seguir:

1. Faça login na Plataforma Digibee.
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Grupos”;

![](<../../.gitbook/assets/Imagem 6 (6).png>)

4\. Procure o grupo desejado na barra de pesquisa;

![](<../../.gitbook/assets/Imagem 7 (1).png>)

5\. Clique em “Editar”;

6\. A janela de edição do grupo abrirá, permitindo incluir novos membros ou alterar as permissões do grupo;

![](<../../.gitbook/assets/Imagem 8 (3).png>)

7\. Faça as alterações desejadas;

8\. Clique em **SALVAR**.

**IMPORTANTE**: Ao editar um grupo, será solicitado o motivo para registro de histórico, pois ao editar os vínculos entre papéis e grupos, os usuários atribuídos àquele grupo poderão perder acesso à Plataforma. Para consultar o histórico de alterações de um grupo, acesse a tela de auditoria da Plataforma.

## Como arquivar um grupo <a href="#h_507e74fbfb" id="h_507e74fbfb"></a>

Para arquivar um grupo, siga os passos abaixo:

1. Faça login na Plataforma Digibee.
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Grupos”;

![](<../../.gitbook/assets/Imagem 9 (1).png>)

4\. Procure o grupo desejado na barra de pesquisa;

![](<../../.gitbook/assets/imagem 10 (1).png>)

5\. Clique em “Arquivar”;

6\. Preencha o motivo do arquivamento do grupo;

![](<../../.gitbook/assets/Imagem 11 (1).png>)

![](<../../.gitbook/assets/Imagem 11.png>)

7\. Após preencher, clique em “Arquivar”

**IMPORTANTE:** Ao arquivar um grupo, será solicitado o motivo para registro de histórico. Pois, quaisquer usuários vinculados ao grupo arquivado perderão acesso às permissões atribuídas por aquele grupo. Para consultar o histórico de alterações de um grupo, acesse a tela de auditoria da Plataforma.

## Perguntas Frequentes <a href="#h_eb5d4f3092" id="h_eb5d4f3092"></a>

### Um usuário tem que estar vinculado a um grupo? <a href="#h_720b9fa566" id="h_720b9fa566"></a>

Não. Porém, se um usuário não estiver vinculado a nenhum grupo ele só terá acesso a visualizar e alterar seu perfil.

### Qual a relação entre grupos e usuários? <a href="#h_fc7dde47d4" id="h_fc7dde47d4"></a>

Um usuário pode pertencer a mais de um grupo e herdar as permissões associadas aos grupos ao qual pertence.

Caso um usuário pertença a mais de um grupo, o resultado final dos seus acessos será a **soma das permissões entre todos os grupos que ele pertence**, dentro dos ambientes de cada vínculo.

Por exemplo:

Se em um grupo "teste", o usuário pode fazer _deploys_ no ambiente de teste e em outro grupo "produção", ele pode fazer _deploys_ em produção, o resultado final será que o usuário terá acesso para fazer _deploys_ em “produção” e em “teste”.

Essa informação é bastante importante na hora de **remover** um acesso de um usuário. Pois, caso ele pertença a vários grupos com permissões repetidas, ao remover o acesso de apenas um grupo (ou do papel contido no grupo), o usuário ainda poderá ter acesso aos recursos da Plataforma.

### Como devo fazer para remover uma ou mais permissões de um usuário na Plataforma? <a href="#h_c1dc901385" id="h_c1dc901385"></a>

Ao clicar em” editar um usuário”, a Plataforma apresenta uma tela com a lista de todos os grupos aos quais ele pertence e outra com o resumo de todas as suas permissões.

É preferível que se remova os usuários dos grupos e se verifique no resumo das permissões (_User Details > Permissions),_ se a permissão foi removida de fato.

### A criação de um grupo é completamente personalizável? <a href="#h_15e5325b71" id="h_15e5325b71"></a>

Sim. Basta que o usuário tenha a permissão USER GROUP: CRIAR (GROUP:CREATE) e USER GROUP: ATUALIZAR (GROUP:UPDATE), para respectivamente criar e editar grupos e seus vínculos na Plataforma.

### O que acontece quando uma permissão é removida de um papel que está associado a um grupo? <a href="#h_b081a00dcb" id="h_b081a00dcb"></a>

No momento em que a permissão for removida do papel, todos os grupos que tinham aquele papel como vínculo, perderão o acesso.

Porém, é importante salientar que um grupo pode ter vários vínculos, ou seja, vários papéis aplicados a diferentes ambientes, e eventualmente, ao remover uma permissão de um papel, o grupo pode continuar com o acesso que foi removido devido a uma eventual acúmulo de permissões.

Para remover o acesso de um único usuário (ou seja, remover a associação a um ou mais grupos) é recomendado utilizar a funcionalidade editar usuários.
