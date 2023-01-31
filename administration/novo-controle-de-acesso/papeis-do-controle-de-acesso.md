---
description: Saiba como criar, editar e arquivar um papel
---

# Papéis

{% hint style="info" %}
Para realizar cada ação descrita nesta página, você deve ter sua respectiva permissão.
{% endhint %}

{% hint style="info" %}
Quando você cria, edita ou arquiva um papel, essas ações são registradas no histórico de alterações na página Auditoria.
{% endhint %}

## Como criar um papel

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Papéis**, na aba no canto esquerdo;
3. Clique no botão **CRIAR**, no canto superior direito;
4. Preencha o nome e a descrição do papel;
5. Clique nos pontos nas colunas Criar, Ler, Atualizar, Deletar e Específico para ativar ou desativar a permissão para o serviço descrito em cada linha. As permissões ativadas são representado por pontos verdes;
6. Clique em **SALVAR**.

<figure><img src="https://i.imgur.com/3MUwR76.gif" alt=""><figcaption><p>Criando um papel</p></figcaption></figure>

## Como editar um papel

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Papéis**, na aba no canto esquerdo;
3. Pesquise na tabela o papel que deseja editar ou use a barra de pesquisa;
4. Clique no ícone de lápis, na coluna Ações;
5. Faça as alterações desejadas no papel;
6. Clique em **SALVAR**.

<figure><img src="https://i.imgur.com/alpvCzw.gif" alt=""><figcaption><p>Editando um papel</p></figcaption></figure>

## Como duplicar um papel

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Papéis**, na aba no canto esquerdo;
3. Pesquise na tabela o papel que deseja duplicar ou use a barra de pesquisa;
4. Clique no ícone de lápis ou de olho na coluna Ações;
5. Clique em **DUPLICAR PAPEL**;
6. Faça as alterações desejadas no novo papel;
7. Clique em **SALVAR**.

<figure><img src="https://i.imgur.com/LliYgq9.gif" alt=""><figcaption><p>Duplicando um papel</p></figcaption></figure>

## Como arquivar um papel

Ao arquivar um papel, as permissões concedidas por esse papel tornam-se inativas. Para arquivar um papel, siga esses passos:

Depois de fazer login na Digibee Integration Platform:

1. Clique no ícone de **Administração**, no canto superior direito;
2. Clique em **Papéis**, na aba no canto esquerdo;
3. Procure o papel que deseja arquivar na tabela ou use a barra de pesquisa;
4. Clique no ícone de caixa na coluna Ações;
5. Escreva uma nota descrevendo o motivo do arquivamento dessa Papel;
6. Clique em **CONFIRMAR**.

<figure><img src="https://i.imgur.com/9XhFjrZ.gif" alt=""><figcaption><p>Arquivando um papel</p></figcaption></figure>

## Papéis de sistema

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
