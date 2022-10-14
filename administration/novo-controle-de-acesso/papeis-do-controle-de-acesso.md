---
description: Entenda mais sobre papéis.
---

# Papéis do Controle de Acesso

Os papéis agrupam as permissões de acesso aos serviços da Digibee Integration Platform. E devem ser usados para mapear os acessos dos usuários que fazem um trabalho similar dentro da Plataforma. Para isso, basta criar um papel e agrupar todas as permissões daquela função.

É possível, **criar, editar, duplicar e arquivar** um papel e também duplicar papéis de sistema para facilitar a criação de novos papéis. Para saber mais sobre papéis de sistemas, leia o artigo sobre [Papéis de sistema e grupos padrão.](https://intercom.help/godigibee/pt-BR/articles/5811758-papeis-de-sistema-e-grupos-padrao)

Ao editar ou arquivar um papel, será solicitado um motivo para a ação de registro de histórico. Para consultar o histórico de alterações de um papel, acesse a tela de auditoria da Plataforma.

## Antes de começar: <a href="#h_4acf5b5178" id="h_4acf5b5178"></a>

Leia os seguintes artigo e conheça mais sobre o Novo Controle de Acesso:

* [Novo modelo de controle de acesso.](https://intercom.help/godigibee/pt-BR/articles/5808132-novo-modelo-de-controle-de-acesso)
* [Conceitos básicos sobre usuários](https://intercom.help/godigibee/pt-BR/articles/5808313-conceitos-basicos-sobre-usuarios)

## Como criar seu primeiro papel <a href="#h_3cbcaa1595" id="h_3cbcaa1595"></a>

Para criar um papel siga os seguintes passos:

1. Faça login na Digibee Integration Platform.
2. Clique no ícone de “Administração”
3. Entre na opção do menu “Papéis”.

![](<../../.gitbook/assets/Imagem 1 (9) (1).png>)

4\. Clique no botão **+ CRIAR** no canto superior direito.

5\. Em seguida, aparecerá uma tela onde devem ser preenchidos os campos de nome e descrição.

6\. Abaixo existem as permissões de acesso: **CRIAR**, **LER**, **ATUALIZAR**, **REMOVER** e **ESPECÍFICO** que devem ser marcadas individualmente de acordo com cada serviço e funcionalidade.

![](<../../.gitbook/assets/image (23).png>)

7\. Após feito esse processo, clique em **SALVAR** no canto inferior direito.

**Observação:** Após criar um papel, você pode vinculá-lo a um grupo. Para saber mais leia a nossa [documentação sobre como vincular um papel a um grupo](https://docs.digibee.com/documentation/v/pt-br/administration/novo-controle-de-acesso/grupos-do-controle-de-acesso#como-vincular-um-papel-a-um-grupo).

Existe também a possibilidade de criar os papéis a partir dos papéis já predefinidos na Plataforma usando a opção de duplicar papéis:

1. Entre no menu “Papéis”.
2. Selecione o papel pré-definido que deseje duplicar;

![](<../../.gitbook/assets/Imagem 3 (2).png>)

3\. Clique no ícone de visualizar papel;

4\. Será aberta uma página de visualização, clique em **DUPLICAR PAPEL;**

5\. Após isso, será aberta uma página contendo a cópia daquele papel, após realizar as alterações desejadas, clique em salvar que o papel terá sido criado com sucesso;

O mesmo pode ser feito com papéis criados na Plataforma, facilitando a criação de novos papéis.

## Como editar um papel <a href="#h_79989fc37c" id="h_79989fc37c"></a>

Para editar um papel siga os seguintes passos:

1. Faça login na Digibee Integration Platform;
2. Clique no ícone de “Administração”
3. Entre na opção do menu “Papéis”;

![](<../../.gitbook/assets/Imagem 4 (4) (1).png>)

5\. Busque na barra de pesquisa ou na tela de navegação o papel a ser editado;

6\. Clique em “Atualizar”;

7\. Em seguida, uma janela contendo as informações do papel selecionado aparecerá, nela você poderá editar as informações do papel;

![](<../../.gitbook/assets/Imagem 5 (4).png>)

8\. Após realizar as alterações, clique em **SALVAR.**

***

## Como arquivar um papel <a href="#h_5511fe06e1" id="h_5511fe06e1"></a>

Para arquivar um papel siga os seguintes passos:

1. Faça login na Digibee Integration Platform;
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Papéis”;
4. Busque na barra de pesquisa ou na tela de navegação o papel a ser arquivado;

![](<../../.gitbook/assets/Imagem 6 (7).png>)

5\. Clique em “Arquivar”;

6\. Uma tela solicitando uma justificativa da arquivação aparecerá. Após digitar, clique em **CONFIRMAR**;

![](<../../.gitbook/assets/image (11).png>)

## Perguntas frequentes <a href="#h_f4c0b05002" id="h_f4c0b05002"></a>

1.  #### Quem pode criar novos papéis? <a href="#h_17bc6286e4" id="h_17bc6286e4"></a>

    Com o novo Controle de Acesso, teremos novos recursos que não existiam na plataforma, entre eles: Grupos e Papéis. Para liberar acesso a estes novos recursos, durante a implantação, todos os usuários que tiverem a permissão USER:CREATE e USER:UPDATE no antigo modelo, receberão automaticamente as novas permissões para criar grupos e papéis no modelo antigo.

    Recomenda-se associar os usuários aos grupos padrões ou criar novos grupos e papéis onde os usuários terão um acesso adequado no novo modelo. Após a validação do novo modelo, o administrador do realm deve desligar o modelo antigo.
2. #### Como eu devo utilizar os papéis pré-definidos da Plataforma? <a href="#h_776475740c" id="h_776475740c"></a>

O sistema já traz alguns papéis pré-definidos para facilitar a criação de grupos, com esses papéis pré-definidos ou a criação de novos papéis a partir da sua cópia. Para maiores detalhes, consulte o documento sobre [Papéis de sistemas e grupos padrão.](https://intercom.help/godigibee/pt-BR/articles/5811758-papeis-de-sistema-e-grupos-padrao)
