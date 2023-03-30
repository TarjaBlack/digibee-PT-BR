---
description: Saiba como criar, editar e arquivar um papel
---

# Papéis

{% hint style="info" %}
Para realizar cada ação descrita nesta página, você deve ter sua respectiva permissão.
{% endhint %}

{% hint style="info" %}
Quando você cria, edita ou arquiva uma papel, essas ações são registradas no histórico de alterações na página Auditoria.
{% endhint %}

Um papel é um conjunto de permissões que podem ser atribuídas a grupos. Essas permissões podem mudar de acordo com o ambiente no qual o usuário está: **test** ou **production**.

## A página de papéis <a href="#_9d3g2kn3fxhi" id="_9d3g2kn3fxhi"></a>

A página **Papéis** exibe uma tabela com papéis ativos em seu _realm_.

Esta tabela mostra o **nome** e **descrição** do papel, assim como botões para visualizá-los, editá-los ou arquivá-los.

<figure><img src="../../.gitbook/assets/0 (2) (1).png" alt=""><figcaption><p>Página de papéis</p></figcaption></figure>

## Ações <a href="#_ppjl1sjz4utb" id="_ppjl1sjz4utb"></a>

### Como criar um papel <a href="#_wnbbosntxrbv" id="_wnbbosntxrbv"></a>

Para criar um papel:

1. Clique no botão **CRIAR**, no canto superior direito;
2. Preencha o nome e a descrição do papel;
3. Clique nos pontos nas colunas CREATE, READ, UPDATE, DELETE e SPECIFIC para ativar ou desativar uma permissão para o serviço descrito em cada linha. As permissões ativadas são representadas por pontos verdes;
4. Clique em **SALVAR**.

### Como visualizar ou editar um papel <a href="#_77hw1b3qlr82" id="_77hw1b3qlr82"></a>

Para visualizar um papel:

1. Pesquise na tabela o papel que deseja editar ou use a barra de pesquisa;
2. Clique no ícone de lápis ou olho na coluna Ações;

Para editar o papel:

1. Faça as alterações desejadas no papel;
2. Clique em **SALVAR**.

{% hint style="info" %}
[Papéis de sistema](papeis-do-controle-de-acesso.md#\_7auxts1l679f) não podem ser editados
{% endhint %}

### Como duplicar um papel <a href="#_xulzjx3de8" id="_xulzjx3de8"></a>

Para duplicar um papel:

1. Pesquise na tabela o papel que deseja duplicar ou use a barra de pesquisa;
2. Clique no ícone de lápis ou olho na coluna Ações;
3. Clique em **DUPLICAR PAPEL**;
4. Faça as alterações desejadas no novo papel;
5. Clique em **SALVAR**.

### Como arquivar um papel <a href="#_v6bw27hgycyn" id="_v6bw27hgycyn"></a>

Ao arquivar um papel, as permissões concedidas por esse papel tornam-se inativas. Para arquivar um papel:

1. Pesquise na tabela o papel que deseja arquivar ou use a barra de pesquisa;
2. Clique no ícone de caixa na coluna Ações;
3. Escreva uma nota descrevendo o motivo do arquivamento desse papel;
4. Clique em **CONFIRMAR**.

{% hint style="info" %}
[Papéis de sistema](papeis-do-controle-de-acesso.md#\_7auxts1l679f) não podem ser arquivados
{% endhint %}

## Papéis de sistema <a href="#_7auxts1l679f" id="_7auxts1l679f"></a>

Além de criar seus próprios papéis, você também pode usar os papéis de sistema da Digibee. Os papéis de sistema são papéis predefinidos criados pelo Digibee. Você não pode editar ou excluir os papéis do sistema, mas você pode replicá-los e editar suas réplicas.

Abaixo, você pode ver todos os papéis de sistema e suas respectivas permissões:

| Role Name                  | ACLs                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Account Manager            | <p>ACCOUNT:CREATE</p><p>ACCOUNT:DELETE</p><p>ACCOUNT:READ</p><p>ACCOUNT:UPDATE</p><p>AUDIT:READ</p><p>GLOBAL:CREATE</p><p>GLOBAL:DELETE</p><p>GLOBAL:READ</p><p>GLOBAL:UPDATE</p><p>RELATION:CREATE</p><p>RELATION:DELETE</p><p>RELATION:READ</p><p>RELATION:UPDATE</p><p>USER:READ</p><p>OAUTH:CREATE</p><p>OAUTH:DELETE</p><p>OAUTH:UPDATE</p>                                   |
| Account Viewer             | <p>ACCOUNT:READ</p><p>AUDIT:READ</p><p>GLOBAL:READ</p><p>RELATION:READ</p><p>USER:READ</p>                                                                                                                                                                                                                                                                                         |
| Api Key Manager            | <p>APIKEY:CREATE</p><p>APIKEY:CREATE:ACL</p><p>APIKEY:CREATE:APIKEY</p><p>APIKEY:DELETE</p><p>APIKEY:DELETE:APIKEY</p><p>APIKEY:READ</p><p>APIKEY:UPDATE</p><p>AUDIT:READ</p><p>USER:READ</p>                                                                                                                                                                                      |
| Api Key Viewer             | <p>APIKEY:READ</p><p>AUDIT:READ</p><p>USER:READ</p>                                                                                                                                                                                                                                                                                                                                |
| Audit Viewer               | AUDIT:READ                                                                                                                                                                                                                                                                                                                                                                         |
| Capsule Builder            | <p>ACCOUNT:READ</p><p>CAPSULE:CREATE</p><p>CAPSULE:CREATE:GROUP</p><p>CAPSULE:CREATE:HEADER</p><p>CAPSULE:DELETE</p><p>CAPSULE:DELETE:HEADER</p><p>CAPSULE:READ</p><p>CAPSULE:UPDATE</p><p>CAPSULE:UPDATE:HEADER</p><p>GLOBAL:READ</p><p>RELATION:READ</p><p>TEST-MODE:EXECUTE:CAPSULE</p>                                                                                         |
| Capsule Manager            | <p>CAPSULE:CREATE</p><p>CAPSULE:CREATE:GROUP</p><p>CAPSULE:CREATE:HEADER</p><p>CAPSULE:DELETE</p><p>CAPSULE:DELETE:HEADER</p><p>CAPSULE:READ</p><p>CAPSULE:UPDATE</p><p>CAPSULE:UPDATE:HEADER</p><p>REPLICA:READ</p><p>TEST-MODE:EXECUTE:CAPSULE</p><p>CAPSULE:DELETE:GROUP</p><p>CAPSULE:UPDATE:GROUP</p>                                                                         |
| Capsule Publisher          | CAPSULE:UPDATE:PUBLISH                                                                                                                                                                                                                                                                                                                                                             |
| Deployment Manager         | <p>CONFIGURATION:CREATE</p><p>CONFIGURATION:READ</p><p>CONFIGURATION:UPDATE</p><p>DEPLOYMENT:CREATE</p><p>DEPLOYMENT:CREATE:REDEPLOY</p><p>DEPLOYMENT:DELETE</p><p>DEPLOYMENT:EXECUTE</p><p>DEPLOYMENT:READ</p><p>USER:READ:LIST-JWT</p><p>USER:CREATE:GENERATE-JWT</p><p>USER:DELETE:REVOKE-JWT</p><p>USER:READ:OPEN-AUTH-CONFIG</p>                                              |
| Deployment Viewer          | <p>CONFIGURATION:READ</p><p>DEPLOYMENT:READ</p>                                                                                                                                                                                                                                                                                                                                    |
| Global Manager             | <p>GLOBAL:CREATE</p><p>GLOBAL:DELETE</p><p>GLOBAL:READ</p><p>GLOBAL:UPDATE</p>                                                                                                                                                                                                                                                                                                     |
| Global Viewer              | GLOBAL:READ                                                                                                                                                                                                                                                                                                                                                                        |
| Groups Manager             | <p>GROUP:CREATE</p><p>GROUP:READ</p><p>GROUP:READ:PERMISSION</p><p>GROUP:UPDATE</p><p>GROUP:DELETE</p><p>USER:UPDATE:ASSIGN-GROUP</p><p>USER:READ:PERMISSION</p><p>USER:READ:INACTIVE-PERMISSION</p><p>PERMISSION:READ</p>                                                                                                                                                         |
| Logs Viewer                | <p>LOG:READ</p><p>MESSAGE:READ</p><p>STATS:READ</p>                                                                                                                                                                                                                                                                                                                                |
| Multi instance Manager     | <p>REPLICA:READ</p><p>REPLICA:CREATE</p><p>REPLICA:UPDATE</p><p>REPLICA:DELETE</p>                                                                                                                                                                                                                                                                                                 |
| Multi instance Viewer      | REPLICA:READ                                                                                                                                                                                                                                                                                                                                                                       |
| Metrics Viewer             | METRIC:READ                                                                                                                                                                                                                                                                                                                                                                        |
| Pipeline Builder           | <p>ACCOUNT:READ</p><p>CONFIGURATION:CREATE</p><p>CONFIGURATION:READ</p><p>CONFIGURATION:UPDATE</p><p>APIKEY:READ</p><p>GLOBAL:READ</p><p>PIPELINE:CREATE</p><p>PIPELINE:READ</p><p>PIPELINE:READ:HISTORY</p><p>PIPELINE:UPDATE</p><p>PROJECT:READ</p><p>RELATION:READ</p><p>REPLICA:READ</p><p>TEST-MODE:EXECUTE</p>                                                               |
| Pipeline Executor          | DEPLOYMENT:EXECUTE                                                                                                                                                                                                                                                                                                                                                                 |
| Pipeline Manager           | <p>ACCOUNT:READ</p><p>CONFIGURATION:CREATE</p><p>CONFIGURATION:READ</p><p>CONFIGURATION:UPDATE</p><p>APIKEY:READ</p><p>GLOBAL:READ</p><p>PIPELINE:CREATE</p><p>PIPELINE:DELETE</p><p>PIPELINE:READ</p><p>PIPELINE:READ:HISTORY</p><p>PIPELINE:UPDATE</p><p>PROJECT:READ</p><p>PROJECT:UPDATE:LINK-WITH-PIPELINE</p><p>RELATION:READ</p><p>REPLICA:READ</p><p>TEST-MODE:EXECUTE</p> |
| Projects Manager           | <p>AUDIT:READ</p><p>PROJECT:CREATE</p><p>PROJECT:DELETE</p><p>PROJECT:READ</p><p>PROJECT:UPDATE</p><p>PROJECT:UPDATE:LINK-WITH-PIPELINE</p><p>PERMISSION:READ</p>                                                                                                                                                                                                                  |
| Relationship Manager       | <p>RELATION:READ</p><p>RELATION:CREATE</p><p>RELATION:UPDATE</p><p>RELATION:DELETE</p>                                                                                                                                                                                                                                                                                             |
| Relationship Viewer        | RELATION:READ                                                                                                                                                                                                                                                                                                                                                                      |
| Roles Manager              | <p>ROLE:CREATE</p><p>ROLE:READ</p><p>ROLE:UPDATE</p><p>ROLE:DELETE</p><p>PERMISSION:READ</p>                                                                                                                                                                                                                                                                                       |
| Running Executions Manager | <p>INFLIGHT:CANCEL</p><p>INFLIGHT:READ</p>                                                                                                                                                                                                                                                                                                                                         |
| Running Executions Viewer  | INFLIGHT:READ                                                                                                                                                                                                                                                                                                                                                                      |
| Users Manager              | <p>USER:CREATE</p><p>USER:DELETE</p><p>USER:READ</p><p>USER:UPDATE</p><p>PERMISSION:READ</p>                                                                                                                                                                                                                                                                                       |
