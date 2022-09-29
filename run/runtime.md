---
description: Entenda os conceitos relacionados a Run.
---

# Conceitos de Run

### **O que é “implantação”?** <a href="#h_cd9a478525" id="h_cd9a478525"></a>

Implantação (_deployment_) é o processo de disponibilização dos _pipelines_ que já possuem _triggers_ configurados.

Essa disponibilização pode acontecer tanto no ambiente de teste (_test_) quanto no ambiente de produção (_prod_), como mostrado na figura a seguir:

<figure><img src="../.gitbook/assets/1 - Run - Tela Principal.jpg" alt=""><figcaption></figcaption></figure>

O fluxo de trabalho dentro da _Digibee Integration Platform_ é composto por três fases. Entenda melhor cada uma delas:

* **Build**

Fase na qual os [_pipelines_](https://docs.digibee.com/documentation/v/pt-br/build/pipelines) são construídos.

_Pipelines_ são constituídos por **componentes**, os quais são organizados em uma estrutura lógica, sequencial ou paralela para que se possa realizar uma integração (ex: transformar dados e enviar ao ERP, API ou DB).

**Componentes** são unidades de processamento com papéis bem definidos, por exemplo, realizar uma chamada REST para um endereço HTTP. Eles podem fazer uso de recursos externos ao _pipeline_, assim como __ [_accounts_](https://docs.digibee.com/documentation/v/pt-br/configurations/contas-accounts) e [_globals_](https://docs.digibee.com/documentation/v/pt-br/configurations/conceitos-basicos), que além de armazenar uma ou mais informações, também garantem maior segurança e reaproveitamento.

* **Run**

Segunda fase, caracterizada pelo processo de implantação do _pipeline_. É nesse momento que o _pipeline_ é preparado e disponibilizado para consumo ou execução.&#x20;

O _pipeline_ executa de acordo com as configurações previamente definidas, que determinam o controle e a capacidade de processamento no ambiente (teste ou produção).

* **Monitor**

Na terceira e última fase é possível acompanhar os _pipelines_ implantados para analisar, verificar e rastrear o andamento das execuções.&#x20;

Dessa maneira, os dados sobre o comportamento dos seus _pipelines_ estarão disponíveis para dar suporte à gestão e operação.

Isso permite saber, por exemplo, a quantidade de solicitações executadas com sucesso ou com falha, o tempo de resposta e os logs.

### Conceitos de Run <a href="#h_f2ce24e96f" id="h_f2ce24e96f"></a>

Entenda melhor detalhes sobre os conceitos principais de Run.

A implantação abrange três partes. Saiba quais são elas:

* **Réplicas**

A função das réplicas é determinar a quantidade de réplicas que serão disponibilizadas para atender às suas integrações com alta disponibilidade. Isto garante autonomia, quantidade de execuções simultâneas e redundância .

<figure><img src="../.gitbook/assets/Réplicas - port.jpg" alt=""><figcaption></figcaption></figure>

* **Consumer**

_Consumer_ (ou consumidor) contempla o conceito de execuções simultâneas que cada réplica implantada suporta.

A quantidade máxima de _consumers_ é definida com base em três faixas de tamanho de implantação.

<figure><img src="../.gitbook/assets/Execucoes simul.jpg" alt=""><figcaption></figcaption></figure>

* **Tamanho**

O tamanho da implantação está diretamente relacionado ao poder de processamento e memória de cada uma das réplicas.

<figure><img src="../.gitbook/assets/Tamanho.jpg" alt=""><figcaption></figcaption></figure>

As três faixas de tamanho de implantação são:

* **SMALL:** 1 a 10 _consumers_
* **MEDIUM:** 1 a 20 _consumers_
* **LARGE:** 1 a 40 _consumers_

Por exemplo, se você configurar 10 _consumers_ (SMALL) para a execução do seu _pipeline_, isso significa que 10 mensagens poderão ser processadas simultaneamente.

* **Ambiente**

Os ambientes de execução dos _pipelines_ podem ser teste (_test_) e produção (_prod_):

<figure><img src="../.gitbook/assets/seletordeambiente.png" alt=""><figcaption></figcaption></figure>

O propósito do ambiente de teste é avaliar a construção do _pipeline_ e, por isso, não possui as mesmas características de atendimento do ambiente de produção. Consequentemente, você tem um ambiente de trabalho que permite a livre construção, onde as aplicações podem ser testadas e validadas.

Quando um _pipeline_ está em ambiente de produção e precisar de uma alteração evolutiva ou apresentar alguma falha, sugerimos que as suas alterações sejam feitas no ambiente de teste para que, somente então, volte à produção.
