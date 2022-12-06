---
description: Saiba o que há de novo e como isso pode te beneficiar.
---

# Nova interface de configuração e rotas personalizáveis

Temos novidades que se aplicam aos seguintes _triggers_:

* REST
* HTTP
* HTTP File

## ANTES E DEPOIS <a href="#antes-e-depois" id="antes-e-depois"></a>

A seguir você pode ver algumas das configurações mais comuns dos _triggers_ na versão anterior e na versão nova:\
&#x20; &#x20;

\- _**Padrão com API Key**_

![](<../../../../.gitbook/assets/nova interface 2.png>)

&#x20;      \
\- _**Com API Key e JWT**_

![](https://downloads.intercomcdn.com/i/o/192892166/7a99b228f4faa2e9d9e9932f/Screen+Shot+2020-03-16+at+18.39.13.png)

&#x20;  \
\- _**Sem segurança (API Key ou JWT)**_

![](https://downloads.intercomcdn.com/i/o/192892167/cde5e3240fc0623b88f10534/Screen+Shot+2020-03-16+at+18.40.15.png)

Entenda o que significa cada campo nas configurações do _trigger_:

* **METHODS:** métodos do protocolo HTTP (GET, PUT, POST, PATCH e DELETE)
* **Maximum Timeout:** tempo máximo de resposta da chamada
* **External API:** publica o API em um _gateway_ externo
* **Internal API:** publica o API em um _gateway in_terno
* **API Key:** necessário quando o API for consumido
* **Token JWT:** necessário quando o API for consumido
* **Custom URI Path:** campo onde é inserida a rota editável\
  &#x20;  &#x20;

Note que com o surgimento dos formulários você:

* tem acesso a todas as configurações de antes&#x20;
* pode visualizar todas as opções de configuração possíveis
* realiza os preenchimentos com mais rapidez e praticidade

## QUAIS SÃO AS NOVIDADES? <a href="#quais-so-as-novidades-afinal" id="quais-so-as-novidades-afinal"></a>

### Exposição Interna/Externa de APIs <a href="#exposio-internaexterna-de-apis" id="exposio-internaexterna-de-apis"></a>

Agora é possível publicar APIs escolhendo se serão expostas externamente ou apenas internamente. Veja algumas possibilidades que esta nova funcionalidade proporciona:

* Exposição externa: permite que os endpoints sejam acessados via internet. Ideal para implementação de estratégias de open API, para integrações com parceiros e sistemas externos.
* Exposição interna: publicação de APIs acessíveis exclusivamente em seu Realm, permite que seus ambientes On premise utilizem APIs dentro da Rede através da VPN (Cloud Privada). Ideal para integrações que envolvam apenas sistemas internos.

#### Benefícios da mudança <a href="#benefcios-da-mudana" id="benefcios-da-mudana"></a>

* Maior isolamento e segurança para integrações com sistemas internos
* Possibilidade de versões externas e internas com diferentes níveis de funcionalidadeCustomização das URIs

### Customização das URIs <a href="#customizao-das-uris" id="customizao-das-uris"></a>

A grande novidade está na customização das URIs. Além disso, o uso que antes era somente externo, agora fica disponível também no seu Realm.    &#x20;

Depois que os _pipelines_ são implantados, as suas URLs adquirem a seguinte estrutura:\
_**https://{env}.godigibee.io/pipeline/{realm}/v{n}/{pipeline-name}**_

* **{env}:** pode ser tanto o ambiente de produção quanto de teste
* **{realm}:** corresponde ao Realm
* **v{n}:** versão do _pipeline_
* **{pipeline-name}:** nome dado ao _pipeline_

Vamos supor que criamos o _pipeline_ "lista-produto".  Levando em consideração o que comentamos acima, a sua URL terá a seguinte aparência:

[_**https://test.godigibee.io/pipeline/empresa/v1/lista-produto**_](https://test.godigibee.io/pipeline/empresa/v1/lista-produto)

&#x20;  \
O que vem depois de "v1" é a parte editável. No caso, escolhemos "lista-produto", que nos trará todos os produtos de uma lista disponibilizada pela empresa em questão. Agora você tem a liberdade de definir novas rotas. Acompanhe como:\
&#x20; &#x20;

**1.** Ative a opção "Additional API Routes".\
**2.** Digite "/produtos" e aperte ENTER.

![](<../../../../.gitbook/assets/nova interface 5.png>)

**3.** Pronto! Você tem uma rota alternativa, com um novo endereço:\
[_**https://test.godigibee.io/pipeline/empresa/v1/produtos**_](https://test.godigibee.io/pipeline/empresa/v1/produtos)

![](<../../../../.gitbook/assets/nova interface 6.png>)

Você também pode acrescentar uma rota que recebe um parâmetro - por exemplo, "/produto/:id".&#x20;

[_**https://test.godigibee.io/pipeline/empresa/v1/produtos/1234**_](https://test.godigibee.io/pipeline/empresa/v1/produtos/1234)

Se a URL acima for chamada, o seu _pipeline_ receberá o valor de ":id" através do "queryAndPath", conforme este código:\
&#x20;

```
{
  "body": {},
  "headers": {
    "Host": "lista-produto:8080",
    "apikey": "xxxxxxxxxxxxxxxxxxxxxxx",
  },
  "queryAndPath": {
    "id": "1234"
  },
  "method": "GET"
}
```

&#x20;    \
Fique atento ao definir suas rotas adicionais. Conflitos dentro do mesmo Realm fazem com que seja difícil prever qual _pipeline_ será executado. Por exemplo:

* A (/produto)
* B (/produto)
* C (/:produto)

Quando _pipelines_ diferentes têm URIs iguais (assim como os _pipelines_ A e B), apenas um deles é executado. O mesmo acontece quando o _request_ vem com o valor “produto” (_pipeline_ C). Para evitar que isso aconteça, sugerimos que você adote um padrão de nomenclatura, inclusive para os _requests_.\
&#x20; &#x20;

Se você utilizar _**/:produto**_ (conforme indicado no exemplo C), o caminho original de acesso ao _pipeline_ será substituído.

Digamos que você crie um _pipeline_ e o chame de _**pipeline-1**_. Assim que o ocorrer o _deploy_, a plataforma vai criar a seguinte URL: [https://staging-test.godigibee.io/pipeline/digibee/v1/pipeline-1](https://staging-test.godigibee.io/pipeline/digibee/v1/pipeline-1)

E caso você utilize rotas adicionais e configure a rota _**/:mensagem**_, a URL [http://staging-test.godigibee.io/pipeline/digibee/v1/](http://staging-test.godigibee.io/pipeline/digibee/v1/) vai disparar o _**pipeline-1**_ considerando _**/:mensagem**_.&#x20;

Nós recomendamos que você tenha cuidado redobrado nesse momento, pois essa rota vai sobrescrever qualquer outro _pipeline_ que esteja no ar na versão 1 (v1). Com isso, por exemplo, o _pipeline_ [https://staging-test.godigibee.io/pipeline/digibee/v1/meu-novo-pipeline](https://staging-test.godigibee.io/pipeline/digibee/v1/meu-novo-pipeline) ficaria inacessível, pois _**/:mensagem**_ o sobrescreveria.&#x20;

O que nós aconselhamos é cautela na criação de rotas adicionais. Caso isso não seja necessário de fato, então sugerimos que você utilize algum prefixo. Por exemplo, _**/minha-rota/:mensagem**_. Assim, a URL original é preservada e os outros _pipelines_ não são prejudicados.\
&#x20; &#x20;

Recomendamos também que você siga as boas práticas de REST. Clique [aqui](https://blog.caelum.com.br/rest-principios-e-boas-praticas/) para conhecê-las.

#### Benefícios da mudança <a href="#benefcios-da-mudana" id="benefcios-da-mudana"></a>

* Mais controle e segurança nesses tipos de _trigger_ (REST, HTTP e HTTP File)
* Rotas adicionais dão mais flexibilidade aos _pipelines_
* O usuário evita retrabalho caso utilize legados com menos flexibilidade em termos de URI
