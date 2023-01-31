---
description: Relembre os principais destaques do 4º trimestre de 2022
---

# Retrospectiva, Q4/22

Este artigo recapitula as principais funcionalidades lançadas na Digibee Integration Platform no quarto trimestre de 2022.

## Componentes

### [Componente SAP (Atualização)](https://docs.digibee.com/documentation/v/pt-br/build/capsulas/capsulas-publicas/sap)

A atualização do novo componente facilita a leitura de uma quantidade muito grande de dados, criando um formato de arquivo com as informações dos dados por meio de dois novos parâmetros: Send as File e File Name.

### [Componente Google Big Table](https://docs.digibee.com/documentation/v/pt-br/components/structured-data/google-big-table)

Conecta-se ao serviço Google Bigtable no pipeline e permite que as operações sejam executadas nas instâncias do Bigtable.

### [Teradata Database](https://docs.digibee.com/documentation/platform/supported-databases#teradata-database)

Os componentes DB v2 e Stream DB V3 podem acessar e executar operações no Teradata, um banco de dados relacional usado para grande armazenamento de dados.

### [S3 Custom Endpoint (AWS)](https://docs.digibee.com/documentation/v/pt-br/components/file-storage/s3-storage)

Uma melhoria no componente S3 Storage que permite a adoção de uma URL de endpoint personalizada no pipeline, proporcionando autonomia e liberdade para os usuários de AWS na Digibee Integration Pipeline.

### [Cassandra DB](https://docs.digibee.com/documentation/v/pt-br/components/structured-data/cassandra-db)

O componente Cassandra DB executa operações no Apache Cassandra, um banco de dados NoSQL projetado para gerenciar grandes quantidades de dados em tempo real, permitindo resposta imediata e suporte a pontos de falha.\


### [Conexão TLS no MongoDB](https://docs.digibee.com/documentation/v/pt-br/components/structured-data/mongo-db)

Essa nova atualização fortalece uma conexão segura a uma instância via SSL/TLS, permite a criação de certificados personalizados e também inclui o parâmetro "expire after seconds" que permite especificar o tempo (em segundos) após o qual os documentos com um TTL índice expirar.

## Features

### [Novo Canvas (Beta)](https://docs.digibee.com/documentation/v/pt-br/build/novo-canvas-beta-restrito)

A nova versão do ambiente de criação de pipeline da Digibee Integration Platform já está disponível em Beta. Novos recursos, como [alertas de validação](https://docs.digibee.com/documentation/v/pt-br/release-notes/release-notes-2022/dezembro#novo-canvas-beta), [campo de pesquisa](https://docs.digibee.com/documentation/v/pt-br/release-notes/release-notes-2022/dezembro#novo-canvas-beta), [Flow tree](https://docs.digibee.com/documentation/v/pt-br/release-notes/release-notes-2022/dezembro#novo-canvas-beta), [Auto pan](https://docs.digibee.com/documentation/v/pt-br/release-notes/release-notes-2022/dezembro#novo-canvas-beta) e [minimapa](https://docs.digibee.com/documentation/v/pt-br/release-notes/release-notes-2022/dezembro#novo-canvas-beta), melhoram a experiência do usuário com mais precisão, conexões e navegação mais fáceis.

### [Nova Página de Gestão de Subscriptions (Beta restrito)](https://docs.digibee.com/documentation/v/pt-br/licenciamento/meu-consumo)

A página Meu Consumo permite rastrear facilmente o consumo e a disponibilidade de Pipeline Subscriptions e RTUs disponíveis em seu realm.\


### [Nova operação de redeploy (General Availability, GA)](https://docs.digibee.com/documentation/run/redeploying-a-pipeline)

O recurso de redeploy na página RUN torna o processo de reimplantação do pipeline mais fácil e rápido para os ambientes de Teste e Produção. Isso permite que um pipeline seja reimplantado mais rapidamente quando ocorre um erro.\


### [Informações do pipeline em tempo real (General Availability, GA)](https://docs.digibee.com/documentation/v/pt-br/run/status-de-implantacao-do-pipeline)

Graças ao redesign da página RUN, você pode acompanhar o status da implantação em tempo real com as seguintes informações: Error, Starting, Deployed e Deleting.

### [Execuções Concluídas - Melhorias na página (General Availability, GA) ](https://docs.digibee.com/documentation/v/pt-br/monitor/execucoes-concluidas)

A página onde você acompanha a execução dos pipelines e seus históricos de log agora tem mais melhorias: novos botões, adição da unidade de tempo decorrido e melhorias no campo de busca.\


### [Pipeline Logs - Melhorias na página (General Availability, GA)](https://docs.digibee.com/documentation/v/pt-br/monitor/pipeline-logs)

As melhorias na aba de Pipeline Logs incluem: novos botões, melhorias no campo de busca e ajustes na formatação de data/hora nos detalhes do log.

### [Integração dos grupos IdP com grupos Digibee](https://docs.digibee.com/documentation/v/pt-br/administration/integracao-de-provedor-de-identidades/integracao-dos-grupos-idp-com-grupos-digibee)

Esse recurso melhora a experiência de gerenciamento de acesso a domínios com muitos usuários e também incentiva mais clientes a integrar seu domínio a um provedor de identidade (IdP).

### [Simulação de Integração de Grupos](https://docs.digibee.com/documentation/v/pt-br/administration/integracao-de-provedor-de-identidades/integracao-dos-grupos-idp-com-grupos-digibee#como-simular-uma-integracao)

Essa feature permite que os clientes interessados ​​em ativar a autorização integrada em seus domínios testem as integrações do grupo Digibee com grupos de provedores de identidade (IdP) e simulem o login IdP de um usuário teste.
