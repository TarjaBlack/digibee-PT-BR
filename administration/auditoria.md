---
description: Conheça a funcionalidade de auditoria da Plataforma Digibee
---

# Auditoria

Para auxiliar na governança e no mapeamento de ações, toda e qualquer operação realizada dentro da Plataforma Digibee é armazenada em segurança e apresentada no submenu Auditoria, localizado na página de Administração da Plataforma.

## Seletor de Período <a href="#h_e3f6a0edc4" id="h_e3f6a0edc4"></a>

![](../.gitbook/assets/auditoria\_1.png)

No centro da tela “Auditoria”, podemos atualizar os logs de ações ao selecionar o período pretendido entre as opções:

* 5 minutos
* 15 minutos
* 1 hora
* **Específico:** Ao clicar em “Específico”, é possível estabelecer um intervalo de tempo entre duas datas e horas.

## Logs de Ações <a href="#h_a4bc7973c0" id="h_a4bc7973c0"></a>

![](../.gitbook/assets/auditoria\_2.png)

Nesta seção, é mostrado os logs de ações conforme o intervalo de tempo e os parâmetros de busca previamente definidos. As informações de cada log estão dispostas no relatório conforme as seguintes colunas:

* **Data de início:** A data e o horário de início da ação;
* **Usuário:** O nome e o e-mail do usuário que executou a ação;
* _**Action**_**:** O tipo de ação realizada, podendo ser:
  * _**All**_**:** Todos os tipos de ações;
  * _**Viewed**_**:** _Logs_ de ações de visualização;
  * _**Created**_**:** _Logs_ de ações de criação;
  * _**Updated**_**:** _Logs_ de ações de atualização;
  * _**Removed**_**/**_**Archived**_**:** _Logs_ de ações de exclusão ou arquivamento.
* _**Status**_**:** O _status_ da ação, podendo ser:
  * _**Success**_: Ações executadas com sucesso;
  * _**Error**_: Ações que apresentaram erro em sua execução.
* _**Service**_**:** Onde a ação foi realizada.
* _**Reference**_**:** O _id_ do objeto que sofreu a ação. Caso o log da ação se refira a um serviço e não a um objeto em específico, este campo será apresentado em branco.
* **Descrição:** Breve descrição da ação executada.

**IMPORTANTE:** Alguns _logs_ de ação serão apresentados com o campo _Reference_ em branco, pois esses não se referem a ações executadas em um objeto específico, mas sim a serviços, que são as entidades do sistema que englobam os objetos. Os objetos específicos de um serviço possuem _id_ e os serviços, por sua vez, não possuem _id_.

## Campo de Busca <a href="#h_1d19bf926c" id="h_1d19bf926c"></a>

O “Campo de Busca” comporta parâmetros que auxiliam o usuário a encontrar determinado log de ação. Através deles, é possível especificar atributos de determinada ação para localizá-la com maior precisão e rapidez.

### Busca simples <a href="#h_f171f2aa86" id="h_f171f2aa86"></a>

![](../.gitbook/assets/auditoria\_3.png)

* **E-mail:** Este parâmetro filtra os logs pelo e-mail do usuário que realizou ou solicitou a ação.

### Busca avançada <a href="#h_5ea7820720" id="h_5ea7820720"></a>

![](../.gitbook/assets/auditoria\_4.png)

* **Descrição:** Este parâmetro filtra os logs pela descrição da ação;
* _**Action**_**:** Este parâmetro filtra os logs conforme o tipo de ação realizada, podendo ser escolhido dentre as seguintes opções:
  * _**All**_**:** Apresenta todos os tipos de ações;
  * _**View**_**:** Apresenta apenas os logs de ações de visualização;
  * _**Create**_**:** Apresenta apenas os logs de ações de criação;
  * _**Update**_**:** Apresenta apenas os logs de ações de atualização;
  * _**Remove**_**/**_**Archive**_**:** Apresenta apenas os logs de ações de exclusão ou arquivamento.
* _**Reference**_**:** O _id_ do objeto que sofreu a ação.
* _**Services**_**:** Este parâmetro filtra a ação pelo serviço, ou seja, pela funcionalidade onde a ação foi realizada, podendo ser:
  * Account
  * Audit
  * Capsule
  * Capsule Collection
  * Capsule Group
  * Capsule Header
  * Completed Execution
  * Consumer
  * Deployment
  * Global
  * Monitor Overview
  * Multi Instance
  * OAuth Provider
  * Pipeline
  * Pipeline Configuration
  * Pipeline Log
  * Pipeline Metric
  * Platform Permission
  * Project
  * Relationship
  * Running Execution
  * Test Mode
  * User
  * User Group
  * User Role
  * digibeectl
