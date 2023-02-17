---
description: Aprenda a criar, editar e arquivar um grupo
---

# Grupos

{% hint style="info" %}
Para realizar cada ação descrita nesta página, você deve ter sua respectiva permissão.
{% endhint %}

{% hint style="info" %}
Quando você cria, edita ou arquiva um grupo, essas ações são registradas no histórico de alterações na página Auditoria.
{% endhint %}

### A página de Grupos <a href="#_w5vdysfjsn4u" id="_w5vdysfjsn4u"></a>

A página Grupos exibe uma tabela que mostra os grupos ativos em seu domínio. Esta tabela mostra o **nome**, **descrição** e **número de membros** de cada grupo.

![](<../../.gitbook/assets/0 (1).png>)

## Ações <a href="#_1l3n9ay3fmff" id="_1l3n9ay3fmff"></a>

### Como criar um grupo <a href="#_ic4qogmxjd77" id="_ic4qogmxjd77"></a>

Para criar um grupo:

1. Clique no botão **CRIAR**, no canto superior direito;
2. Preencha o nome e a descrição do grupo;
3. Clique no ícone **+** para atribuir membros ao novo grupo (opcional);

{% hint style="info" %}
Você pode adicionar ou remover membros de um grupo a qualquer momento.
{% endhint %}

4. Clique em **SALVAR** para criar o novo grupo.

### Como vincular um papel a um grupo <a href="#_ui1k2pip8u4q" id="_ui1k2pip8u4q"></a>

{% hint style="info" %}
Você deve criar o papel desejado antes de vinculá-lo a um grupo. Aprenda mais sobre papéis aqui.
{% endhint %}

Para vincular um papel a um grupo:

1. Use a barra de pesquisa ou pesquise na tabela o grupo ao qual deseja atribuir um papel;
2. Clique no ícone de lápis na coluna Ações;
3. Na aba **Permissões**, clique em **+VÍNCULO**;
4. Selecione o papel desejado e o ambiente ao qual deseja atribuir as permissões do papel;
5. Clique em **SALVAR**;
6. Escreva uma nota descrevendo os motivos das alterações que você acabou de fazer;
7. Clique em **EDITAR** para confirmar a ação.

### Como arquivar um grupo <a href="#_9p3yo68cnrdj" id="_9p3yo68cnrdj"></a>

Se você arquivar um grupo, ele ficará inativo. Os membros de um grupo arquivado perderão as permissões concedidas por ele.

Para arquivar um grupo:

1. Use a barra de pesquisa ou procure na tabela o grupo que deseja arquivar;
2. Clique no ícone da caixa na coluna Ações;
3. Escreva uma nota descrevendo os motivos do arquivamento do grupo;
4. Clique em **ARQUIVAR**.

## Grupos padrão <a href="#_4qxm4nw2dj56" id="_4qxm4nw2dj56"></a>

Além de criar seus próprios grupos, você também pode usar os grupos padrão do Digibee. Cada grupo padrão é vinculado a um conjunto de papéis de sistema. Esses grupos cobrem os tipos de usuários mais comuns da Digibee Integration Platform.

Ao contrário dos [papéis de sistema,](papeis-do-controle-de-acesso.md#papeis-de-sistema) os grupos padrão podem ser modificados, excluídos e arquivados.

| Group name          | System roles                                                                                                                                                                                                                                   |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Developers          | Pipeline Builder, Capsule Builder, Pipeline Manager e Deployment Viewer                                                                                                                                                                        |
| Deployer            | Deployment Manager e Deployment Viewer                                                                                                                                                                                                         |
| Access managers     | Users Manager, Roles Manager, Groups Manager e Projects Manager                                                                                                                                                                                |
| Governance managers | Account Viewer, Global Manager, Global Viewer, Capsule Manager, Capsule Publisher, Pipeline Manager, Audit Viewer, Multi instance Manager, Multi instance Viewer, API Key Manager, API Key Viewer, Relationship Manager e Relationship Viewer. |
| Credential managers | Account Manager e API Key Manager                                                                                                                                                                                                              |
| Support             | Pipeline Logs Viewer, Pipeline Metrics Viewer, Running Executions Manager, Running Executions Viewer e Pipeline Executor                                                                                                                       |
