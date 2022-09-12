---
description: Conheça o componente e saiba como utilizá-lo.
---

# Session Management

O **Session Management** implementa o gerenciamento de sessão tradicional e a sua função principal para construção de _pipelines_ é bastante utilizada no armazenamento de dados semelhantes às variáveis em desenvolvimento tradicional.\


Esse componente pode ser configurado nas seguintes operações:

* **GET:** vai ser buscado na sessão o objeto especificado no "campo" parâmetro, para ser colocado no corpo da solicitação.
* **PUT:** vai ser colocado na sessão, LOCAL ou GLOBAL, o objeto especificado do "campo" parâmetro do passo anterior.

### LOCAL <a href="#local" id="local"></a>

Lida com uma sessão onde os valores armazenados estão disponíveis apenas no _pipeline_ em execução corrente.              \
&#x20;        &#x20;

**Exemplo:**\
As _tags_ "body" e "data" do passo anterior são armazenadas na sessão local.\


### GLOBAL <a href="#global" id="global"></a>

Lida com uma sessão baseada no _token_ JWT do usuário autenticado, permitindo que _pipelines_ e execuções distintas tenham acesso seguro aos dados armazenados na sessão global do usuário.

Somente será permitido armazenar e acessar dados em sessão GLOBAL quando o _pipeline_ possuir o REST ou o HTTP Trigger e tiver o _token_ JWT como critério de segurança.

Para executar um _pipeline_ com esse critério de segurança, é necessário que você crie um _pipeline_ de _login_ e utilize o componente JWT para obter um _token_ JWT_._

&#x20;        \
**Exemplo**

* **Step Name:** Session-Management
* **Operation:** GET DATA
* **Session Type:** GLOBAL - has a global scope controlled by the JWT token injected by a REST Trigger
* **Fields:** object

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada e pode fazer uso dela declarando os valores do JSON no campo _"fields"_.

### Saída <a href="#sada" id="sada"></a>

O componente não altera nenhuma informação da mensagem de entrada. Portanto, ela é retornada para o componente seguinte ou é utilizada como resposta final se este componente for o último passo do _pipeline_. Ao manter selecionada a operação GET, os itens declarados no campo "_fields"_ serão adicionados à mensagem de saída (caso existam na sessão).
