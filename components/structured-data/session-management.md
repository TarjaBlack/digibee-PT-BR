---
description: Conheça o componente e saiba como utilizá-lo.
---

# Session Management

O _**Session Management**_ implementa o gerenciamento de sessão tradicional e a sua função principal para construção de _pipelines_ é bastante utilizada no armazenamento de dados semelhantes às variáveis em desenvolvimento tradicional.\


Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** operação a ser executada (Get Data, Put Data, Delete Data).
* **Session Type:** sessão para inserir o objeto especificado em _"Fields"_ (Local ou Global)
* **Fields:** objeto a ser especificado - ex. _body, data,_ id.
* **Scoped:** Quando esta opção está habilitada, a sessão é isolada de outro subprocesso. Nesse caso, os subprocessos veem sua própria versão dos dados da sessão.

## **Operation**

Esse componente pode ser configurado nas seguintes operações:

* **Get Data:** busca na sessão os objetos especificados no parâmetro _"Fields"_, que serão inseridos em seguida no corpo da solicitação.&#x20;
* **Put Data:** insere na sessão (Local ou Global) os objetos especificados no parâmetro _"Fields"_.
* **Delete Data:** apaga da sessão os objetos especificados no parâmetro _"Fields"_.

## **Session Type**

### Local <a href="#local" id="local"></a>

Lida com uma sessão onde os valores armazenados estão disponíveis apenas no _pipeline_ em execução corrente.               &#x20;

**Exemplo:** As _tags_ "body" e "data" da etapa _"Fields"_ são armazenadas na sessão **Local**.

### Global <a href="#global" id="global"></a>

Lida com uma sessão baseada no _token_ JWT do usuário autenticado, permitindo que _pipelines_ e execuções distintas tenham acesso seguro aos dados armazenados na sessão global do usuário.

Somente será permitido armazenar e acessar dados em sessão **Global** quando o _pipeline_ possuir o REST ou o HTTP Trigger e tiver o _token_ JWT como critério de segurança.

Para executar um _pipeline_ com esse critério de segurança, é necessário que você crie um _pipeline_ de _login_ e utilize o componente JWT para obter um _token_ JWT_._

&#x20;        \
**Exemplo**

* **Step Name:** Session-Management
* **Operation:** Get Data
* **Session Type:** Global - has a global scope controlled by the JWT token injected by a REST Trigger
* **Fields:** object

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela declarando os valores do JSON no campo _"Fields"_.

### Saída <a href="#sada" id="sada"></a>

O componente não altera nenhuma informação da mensagem de entrada. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se este componente for o último passo do _pipeline_.&#x20;

Ao manter a operação **Get Data** selecionada, os itens especificados no campo "_Fields"_ serão adicionados à mensagem de saída (caso existam na sessão).
