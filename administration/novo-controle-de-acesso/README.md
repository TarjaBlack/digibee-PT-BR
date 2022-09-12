---
description: A nova funcionalidade de gestão de permissões da Digibee HIP.
---

# Novo Controle de Acesso

## Visão Geral <a href="#h_2920fcba8e" id="h_2920fcba8e"></a>

O Controle de Acesso _****_ é o novo recurso de gestão de acesso para usuários na Digibee Integration Plaform. A partir dele são definidas as permissões de acesso dentro de um _realm_.

As atualizações passaram a permitir o agrupamento e reuso de perfis de acessos similares para melhorar a experiência da gestão de acesso do _realm._ O novo modelo de Controle de Acesso permite uma gestão mais ágil, prática e eficaz dos usuários e seus acessos.

## Conceitos relacionados ao Controle de Acesso <a href="#h_91b5e85b5a" id="h_91b5e85b5a"></a>

Agora o **Controle de Acesso** possui 3 etapas de criação de acesso: **usuários, papéis e grupos**. Desta forma, para o usuário ter acesso às funcionalidades da Plataforma o mesmo deve pertencer a um grupo que por sua vez possui um ou mais papéis associados

![](<../../.gitbook/assets/Imagem 1.png>)

**Usuários:** Representam as pessoas que têm acesso à Plataforma e possui os dados pessoais dos usuário, como nome, sobrenome, e-mail e fuso horário .

**Papéis:** Representam um conjunto de permissões, normalmente correspondentes às atividades que um ou mais usuários executam na Plataforma. Esta entidade contém as permissões para os recursos da Plataforma.

**Grupos:** Os Grupos associam um conjunto de usuários, com um ou mais papéis. Os usuários só terão acesso aos recursos da Plataforma se estiverem listados em um ou mais grupos.

## Como funciona? <a href="#h_043a5cc89f" id="h_043a5cc89f"></a>

A figura abaixo apresenta os principais componentes do novo controle de acesso da Digibee HIP:

![](<../../.gitbook/assets/Imagem 2 (3).png>)

Um grupo é uma associação entre um conjunto de usuários (membros) e os vínculos. Um vínculo é uma associação entre um papel (e seus respectivos acessos) e um ambiente (podendo ser teste, produção ou ambos).

Para dar permissão a um novo usuário, o administrador do _realm_ deve criar papéis com seus respectivos acessos, criar usuários (que não terão nenhum acesso por padrão) e criar grupos, os quais vão associar os usuários, aos seus papéis e ambientes.

Há também a opção de utilizar papéis e grupos pré-definidos pela Plataforma. Para saber mais sobre esse assunto, leia o artigo sobre [Papéis de Sistemas e Grupo Padrão](https://intercom.help/godigibee/pt-BR/articles/5811758-papeis-de-sistema-e-grupos-padrao).

## Como começar? <a href="#h_3abe341103" id="h_3abe341103"></a>

Para saber mais sobre como implementar o novo controle de acesso, siga o passo a passo abaixo:

1. Primeiramente, o administrador do _realm_ deve definir quais papéis serão utilizados pelos usuários que terão acesso à Plataforma. Para saber mais sobre a criação de papéis, leia o artigo [Papéis do Controle de Acesso](https://intercom.help/godigibee/pt-BR/articles/5810244-papeis-do-controle-de-acesso)
   1. Para facilitar a definição dos papéis do controle de acesso, a Plataforma fornece um conjunto de papéis de sistemas (pré-definidos) que podem ser utilizados duplicados para facilitar a criação de novos papéis. Para saber mais sobre Papéis de Sistemas, leia o artigo[ Papéis de Sistema e Grupos Padrão](https://intercom.help/godigibee/pt-BR/articles/5811758-papeis-de-sistema-e-grupos-padrao)
2. O administrador do _realm_ também deve criar o cadastro dos usuários que terão acesso à Plataforma. Clique aqui para entender mais sobre[ Conceitos básicos sobre Usuários](https://intercom.help/godigibee/pt-BR/articles/5808313-conceitos-basicos-sobre-usuarios)
3. Por fim, após ter definido os papéis e usuários, o administrador do _realm_ deve criar os grupos que associam um usuário e um ou mais papéis e seu respectivo ambiente. Para saber mais sobre grupos, leia o artigo [Grupos do Controle de Acesso.](https://intercom.help/godigibee/pt-BR/articles/5810361-grupos-do-controle-de-acesso)
4. Após criar Grupos, Usuários e Papéis, acesse a tela de Usuários para verificar se todos os usuários estão aptos à transição. Os usuários que ainda não tiveram seus acessos replicados no novo modelo aparecerão com um ícone de atenção. Para saber, leia o artigo [Transição do novo Controle de Acesso](https://intercom.help/godigibee/pt-BR/articles/5810530-transicao-do-novo-controle-de-acesso).
