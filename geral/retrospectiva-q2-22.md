---
description: Relembre os principais destaques do 2º trimestre de 2022
---

# Retrospectiva, Q2/22

Este artigo recapitula as principais funcionalidades lançadas na Plataforma Digibee no segundo trimestre de 2022.

****[**mTLS GA**](../components/triggers/configuracoes-de-triggers/mtls.md)****

O protocolo mútuo TLS (mTLS) já está liberado para todos os clientes (_general availability_). Este protocolo de autenticação reforça a segurança da Plataforma Digibee, expondo APIs com mTLS sem que o cliente precise de um _gateway_ de API próprio.

****[**Response Headers**](../components/triggers/http-trigger.md)****

Essa _feature_ de segurança permite a configuração de _headers_ de resposta direto nos _triggers_ HTTP (HTTP Trigger, HTTP File Trigger e REST Trigger). Isso garante uma camada extra de segurança para transações importantes e procedência de resposta para tomadas de decisão.

****[**Avro Format for Kafka Component**](../components/queues-and-messaging/kafka.md)

O Componente Kafka recebe os dados em JSON, valida esses dados e converte para o formato Avro antes de enviar para o tópico Kafka. Com este formato, é possível manipular grandes tráfegos de dados mais rapidamente e com menos erros.

****[**Avro Format for Kafka Trigger**](../components/triggers/kafka-trigger.md)****

Assim como o Componente Kafka, o Trigger Kafka é caracterizado pela velocidade e alta tolerância a falhas. Esse _trigger_ recebe grande volume de dados no formato Avro e os converte em JSON para que possam ser processados ​​pelo _pipeline_.

[**Auditoria da Plataforma - evolution**](../administration/auditoria.md)

Essa funcionalidade registra toda e qualquer ação que um usuário faz na Plataforma, Portal, API Administrativa ou digibeectl, o que auxilia na governança e mapeamento das ações na Plataforma Digibee.

****[**Cassandra DB Component**](../components/structured-data/cassandra-db.md)****

Com este componente, os clientes Digibee que possuem grandes _workloads_ têm acesso ao Cassandra, um banco de dados NoSQL projetado para gerenciar grande volume de dados em tempo real.

****[**Azure Blob Storage Component**](../components/file-storage/azure-blob-storage.md)****

Este componente permite aos clientes que usam o Blob Storage da Azure manipular os objetos armazenados na nuvem dentro da Plataforma Digibee.
