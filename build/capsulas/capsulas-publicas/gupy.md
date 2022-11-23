---
description: Saiba quais são as Cápsulas disponíveis nessa Coleção.
---

# Gupy

## O que é Gupy? <a href="#h_8d1147ece8" id="h_8d1147ece8"></a>

Gupy é uma ferramenta de seleção e admissão de candidatos. Com a Gupy você agiliza a requisição de vagas, divulga as suas oportunidades nos principais portais de emprego do Brasil e qualifica os seus candidatos com dezenas de testes online prontos. Além disso, você simplifica a admissão digital dos novos colaboradores.

### Pré-requisitos <a href="#h_54bb08168f" id="h_54bb08168f"></a>

Para utilizar as Cápsulas dos serviços Gupy, é necessário possuir um token de autorização, que deve estar cadastrado em uma _account_ do tipo ‘oauth-bearer’ na Digibee Integration Platform.

#### **Cápsulas Gupy** <a href="#h_e04c742e16" id="h_e04c742e16"></a>

* **Configuring Webhook**

Por meio dessa Cápsula, é possível configurar as requisições enviadas pela Gupy para a Digibee. É preciso configurar os diferentes tipos de notificações que devem ser enviadas ao _pipeline_ sempre que ocorrer uma atualização no ambiente Gupy.

A Cápsula _**Configuring Webhook**_\*\* \*\* permite criar, atualizar ou remover inscrições de eventos de notificações.

Para configurar um novo _webhook_, basta escolher um dos eventos listados, inserir as informações do seu _pipeline_ e da respectiva API key para então executar a Cápsula.

{% hint style="info" %}
**IMPORTANTE:** a configuração deve ser realizada uma única vez para cada ambiente e tipo de evento desejado.
{% endhint %}

* **Listing Webhooks Configurations**

Utilize essa Cápsula para consultar os _webhooks_ que já foram configurados anteriormente.

A _**Listing Webhooks Configurations**_ lista os eventos e os _pipelines_ configurados para receber as notificações via _webhook_. Caso seja necessário atualizar ou remover algumas das informações, o campo “id” retornado na consulta servirá como campo chave na identificação do registro a ser alterado. Para alterar as configurações, utilize a Cápsula _**Configuring Webhook**_.

* **Upsert Department**

Essa Cápsula permite a atualização ou criação de novos departamentos dentro da plataforma Gupy.

Um novo registro é criado apenas se não for encontrado um departamento já existente através dos parâmetros de busca informados no campo “search”. Se o registro já existir, então o departamento será atualizado na plataforma Gupy. As informações que serão atualizadas são: “name”, “external\_code” e “similar\_to”.

* **Gupy Business Flow JOB**

Essa Cápsula possui um fluxo completo de criação da posição de trabalho na Gupy, possibilitando a automatização do processo de requisição para a abertura de vagas.

O fluxo contempla a criação da vaga, bem o vínculo ao departamento e ao cargo.

Veja a seguir as explicações das entidades gerenciadas e como elas são tratadas ao longo do fluxo de negócio dentro da Cápsula:

![](<../../../.gitbook/assets/01pt (2).png>)

Para facilitar o seu primeiro uso da Cápsula, veja os campos requisitados para a criação de um novo registro. No exemplo abaixo, o formato utilizado é JSON:

```
{
    "job":{"roleName":"role_example: Developer",
        "roleCode":"code_dev","roleSimilarTo":"trainee",
        "departmentName":"Department test",
        "departmentCode":"dep_code_eg",
        "departmentSimilarTo":"technology",
        "branchName":"filial xpto",
        "branchCode":"branch_code_xpto",
        "branchPaths":"01;02;03;04;05;06",
        "code":"my_code_job",
        "name":"Job name - Developer JR",
        "type":"vacancy_type_trainee",
        "publicationType":"internal",
        "hiringDeadline":"2021-04-20",
        "numVacancies":10,
        "description":"jobDescription - Work  text text text",
        "responsibilities":"responsibilities - text text text",
        "prerequisites":"prerequisites  - logical",
        "additionalInformation":"additionalInformation text text",
        "notes":"notes text text text",
        "disabilities":false,
        "remoteWorking":true,
        "salaryCurrency":"R$",
        "salaryStartsAt":1100.01,
        "salaryEndAt":null,
        "reason":"staff_increase",
        "recruiterEmail":null,
        "managerEmail":null,
        "careerPageId":null,
        "customFields":[{"id":99,"value":"xpto"}],
        "jobRatingCriterias":[],
        "templateId":757624
    }
} 
```

\\
