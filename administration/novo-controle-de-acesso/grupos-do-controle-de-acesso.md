---
description: Aprenda a criar, editar e arquivar um grupo
---

# Grupos

{% hint style="info" %}
Para realizar cada ação descrita nesta página, você deve ter sua respectiva permissão.
{% endhint %}

{% hint style="info" %}
Quando você cria, edita ou arquiva um grupo, essas ações são registradas no histórico de alterações da página Auditoria.
{% endhint %}

## Como criar um grupo

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Grupos**, na aba no canto esquerdo;
3. Clique no botão **CRIAR**, no canto superior direito;
4. Preencha o nome e a descrição do grupo;
5. Clique no ícone **+** para atribuir membros ao novo grupo (opcional);

{% hint style="info" %}
Você pode adicionar ou remover membros de um grupo a qualquer momento.
{% endhint %}

6. Clique em **SALVAR** para criar o novo grupo.

<figure><img src="https://i.imgur.com/Bih9Upn.gif" alt=""><figcaption><p>Criando um grupo</p></figcaption></figure>

## Como vincular um papel a um grupo

{% hint style="info" %}
Você deve criar o papel desejado antes de vinculá-lo a um grupo. Aprenda mais sobre papéis aqui.
{% endhint %}

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Grupos**, na aba no canto esquerdo;
3. Pesquise na tabela o grupo ao qual você deseja atribuir um vínculo ou use a barra de pesquisa;
4. Clique no ícone de lápis, na coluna Ações;
5. Na aba Permissões, clique em **+VÍNCULO**;
6. Selecione o papel desejado e o ambiente ao qual deseja atribuir as permissões do papel;
7. Clique em **SALVAR**;
8. Escreva uma nota descrevendo o motivo das alterações que você acabou de fazer;
9. Clique em **EDITAR** para confirmar a ação.

<figure><img src="https://i.imgur.com/ETLpnzE.gif" alt=""><figcaption><p>Vinculando um papel a um grupo</p></figcaption></figure>

## Como arquivar um grupo

Se você arquivar um grupo, ele ficará inativo. Os membros de um grupo arquivado perderão as permissões concedidas por ele.

Para arquivar um grupo, siga esses passos:

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Grupos**, na aba no canto esquerdo;
3. Use a barra de pesquisa ou procure na tabela o grupo que deseja arquivar;
4. Clique no ícone de caixa, na coluna Ações;
5. Escreva uma nota descrevendo os motivos do arquivamento do grupo;
6. Clique em **ARQUIVAR**.

<figure><img src="https://i.imgur.com/iIE8nPz.gif" alt=""><figcaption><p>Arquivando um grupo</p></figcaption></figure>

## Grupos padrão

Além de criar seus próprios grupos, você também pode usar os grupos padrão do Digibee. Cada grupo padrão é vinculado a um conjunto de [papéis de sistema](papeis-do-controle-de-acesso.md#papeis-de-sistema). Esses grupos cobrem os tipos de usuários mais comuns da Digibee Integration Platform.

Ao contrário dos papéis de sistema, os grupos padrão podem ser modificados, excluídos e arquivados.

| Group name          | System roles                                                                                                                                                                                                                                   |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Developers          | Pipeline Builder, Capsule Builder, Pipeline Manager e Deployment Viewer                                                                                                                                                                        |
| Deployer            | Deployment Manager e Deployment Viewer                                                                                                                                                                                                         |
| Access managers     | Users Manager, Roles Manager, Groups Manager e Projects Manager                                                                                                                                                                                |
| Governance managers | Account Viewer, Global Manager, Global Viewer, Capsule Manager, Capsule Publisher, Pipeline Manager, Audit Viewer, Multi instance Manager, Multi instance Viewer, API Key Manager, API Key Viewer, Relationship Manager e Relationship Viewer. |
| Credential managers | Account Manager e API Key Manager                                                                                                                                                                                                              |
| Support             | Pipeline Logs Viewer, Pipeline Metrics Viewer, Running Executions Manager, Running Executions Viewer e Pipeline Executor                                                                                                                       |
