---
description: 'FAQ: Erro Test mode'
---

# ERRO: Network error: Failed to fetch (test-mode)

Para as execuções em [Test mode](./), o front-end aguarda até 60 segundos por uma resposta. Se isso não ocorrer, é apresentado esse erro, porém, **a execução continua em **_**background**_ podendo ser analisada nos logs, no menu **dashboard**. (Usando o filtro test-mode).

Isso também pode ocorrer se o seu computador perder conexão com a internet.

Nos casos de execuções um pouco mais longas, o _pipeline_ ainda continua em execução por até 5 minutos.

Caso seu pipeline esteja focado em longas execuções, dê uma olhada em nosso documento de padrões de integração, no item: [Migração e sincronização de dados entre sistemas](../../../tutoriais-e-melhores-praticas/padroes-de-integracao-digibee.md).\
