---
description: >-
  Saiba quais são os itens que devem estar presentes na construção de qualquer
  pipeline.
---

# Pipelines: checklist de construção

### SEGURANÇA <a href="#segurana" id="segurana"></a>

Itens de segurança que devem ser considerados para todos **** os projetos desenvolvidos na nossa Plataforma.\


**a) Trigger / apikey**

Ao utilizar os _triggers_ HTTP, API REST e HTTP File, serviços serão expostos na Internet. Por configuração nativa (e não opcional) da nossa Plataforma, esses _triggers_ podem ser utilizados, publicados e acessados somente com a utilização de API Key.

**API Key** é uma credencial de acesso fornecida para consultas em _pipelines_ que utilizam os _triggers_ mencionados acima. Essa é a garantia mínima de segurança exigida. Recomendamos que você utilize a API Key sempre que possível e que reforce a segurança com o uso de JWT (JSON Web Token).

Para gerar uma chave (API Key) na nossa Digibee Integration Platform, acesse "_Configurações > Consumers_", escolha o ambiente e clique em _CRIAR:_

![](<../.gitbook/assets/img1 (1).png>)

\
**RECOMENDAÇÃO:** gere uma API Key diferente para cada sistema consumidor da sua API, restringindo o acesso somente aos _pipelines_ desejados. Essa chave deverá ser enviada no _header_, com o parâmetro "apikey" e seu respectivo valor. Informe também o Content-Type esperado pelo pipeline (_ex.: application/json)._

**IMPORTANTE:** não recomendamos a utilização de _pipelines_ sem API Key. Manter um _endpoint_ aberto enfraquece a segurança e pode tornar seu ambiente vulnerável a ataques e vazamento de dados. A nossa Plataforma, por padrão, não permite a publicação de _pipelines_ que utilizem _triggers_ HTTP, API REST e HTTP Files sem API Key. Clientes que estejam dispostos a assumir esse risco devem enviar uma solicitação via Intercom utilizando o modelo abaixo:

_Solicito a inclusão do/s pipeline/s abaixo descritos em whitelist para a não utilização de API Key._

* _Nome do realm:_
* _Nome do(s) pipeline(s) que deve(m) ser incluído(s) em whitelist dentro deste realm:_
* _Motivo da solicitação:_

\
**b) Armazenamento de credenciais**

Sempre armazene as credenciais de autenticação dos serviços acessados no cofre de senhas da Plataforma (_contas_).  Você é responsável pela criação da conta.&#x20;

Ao menos um dos _headers_ utilizados para autenticação deve o _account_.

\
**c) Campos sensíveis**

Defina campos sensíveis nas configurações do _pipeline_ para mascarar essas informações em mensagens e _logs_.

![](<../.gitbook/assets/img2 (1).png>)

\
**d) Protocolo HTTPS**

SEMPRE utilize o **** protocolo HTTPS nas chamadas aos serviços acessados via _pipeline_; chamadas HTTP aos _pipelines_ são permitidas somente via VPN.

\
**e) Object Store**

Todo e qualquer dado é armazenado com o máximo de segurança na nossa Plataforma. Ainda assim, recomendamos que dados sensíveis armazenados no Object Store sejam criptografados. Para isso, utilize nossos conectores de criptografia.

Object Store é uma base de dados auxiliar para integração.&#x20;

Os dados inseridos no fluxo de integração não devem crescer infinitamente. Dados antigos devem ser apagados e exceções devem ser avaliadas particularmente.

O campo indexado na _collection_ é o "_\_oId_", ao realizar buscas/atualizações/exclusões, utilize sempre este campo, mesmo que seja complementares com outros. Caso não seja possível, um novo index deverá ser criado para a collection.

\
**f) Script**&#x20;

O Objetivo do Javascript é resolver problemas quando não existirem conectores ou funções existentes dentro da Digibee.

Caso seja necessário utilizá-lo, informe à nossa equipe para que possamos encontrar alternativas e trabalhar na melhoria da Plataforma.

\


### TRATAMENTO DE ERROS <a href="#tratamento-de-erros" id="tratamento-de-erros"></a>

Após se conectar a qualquer serviço (API / Banco de dados / _Storages_), valide se o retorno foi conforme o esperado antes de seguir com o fluxo normal de integração. Em casos de erros, garanta que um evento será disparado e que o mesmo irá gerar algum tipo de alerta.

Defina regras de reprocessamento para erros gerados.

Defina regras de notificação para erros gerados (abertura de _tickets_ em ferramentas de ITSM, envio de e-mails, gravação de logs, etc.).

Para mais detalhes sobre construção de fluxos de tratamento de erros, clique [aqui](https://drive.google.com/file/d/1yoqGnz8UmBruMiMtG6CiqG8aBn9jIwRs/view) para acessar o documento de Padrões de Integração.\
