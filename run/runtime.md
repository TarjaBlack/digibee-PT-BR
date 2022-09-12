---
description: Entenda os conceitos relacionados a RUNTIME.
---

# Runtime

### **O que é “implantação”?** <a href="#h_cd9a478525" id="h_cd9a478525"></a>

Implantação (_deployment_) é o processo de disponibilização dos _pipelines_ que já possuem _triggers_ configurados.

Essa disponibilização pode acontecer tanto no ambiente de teste (_test_) quanto no ambiente de produção (_prod_). Veja:

![](<../.gitbook/assets/1 - Tela principal.jpg>)

O fluxo de trabalho dentro da Plataforma é composto por 3 fases. Entenda melhor cada uma delas:

* **Build**

Fase na qual os [_pipelines_](../build/pipelines/) são construídos.

_Pipelines_ são constituídos por “componentes”, os quais são organizados em uma estrutura lógica, sequencial ou paralela para que se possa realizar uma integração (ex.: transformar dados e enviar ao ERP, API ou DB.)

Componentes são unidades de processamento com papéis bem definidos (ex.: realizar uma chamada REST para um endereço HTTP). Os componentes da Plataforma podem fazer uso de recursos externos ao _pipeline_, assim como "accounts" e "globals", que além de armazenarem uma ou mais informações, também garantem maior segurança e reaproveitamento.

* **Run**

Segunda fase, caracterizada pelo processo de implantação do _pipeline_. É nesse momento que o _pipeline_ é preparado e disponibilizado para consumo ou execução. Formado por componentes e utilizando recursos externos (_accounts_ e _globals_), o _pipeline_ é atrelado a um serviço que garante a sua execução conforme as configurações determinadas. Essas configurações, por sua vez, determinam o controle e a capacidade de processamento do _pipeline_ no ambiente (produção ou teste).

* **Monitor**

Na terceira e última fase é possível acompanhar os _pipelines_ implantados para analisar, verificar e rastrear o andamento das execuções. Dessa maneira, dados sobre o comportamento dos seus _pipelines_ estarão disponíveis para dar suporte à gestão e operação, possibilitando que você saiba, por exemplo, a quantidade de solicitações executadas com sucesso ou com falha, o tempo de resposta e os logs.

### Conceitos de Runtime <a href="#h_f2ce24e96f" id="h_f2ce24e96f"></a>

Entenda melhor detalhes sobre os conceitos principais de Runtime.

A implantação abrange 3 partes. Saiba quais são elas:

* **Réplicas**

A função das réplicas é determinar a quantidade de réplicas que serão disponibilizadas para atender às suas integrações, garantindo autonomia, quantidade de execuções simultâneas e redundância com alta disponibilidade.

* **Consumer**

_Consumer_ (ou consumidor) contempla o conceito de execuções simultâneas que cada réplica implantada suporta.

A quantidade máxima de _consumers_ é definida com base em 3 faixas de tamanho de implantação.

* **Tamanho**

O tamanho da implantação está diretamente relacionado ao poder de processamento e memória de cada uma das réplicas.

As 3 faixas de tamanho de implantação são:

* **SMALL:** 1 a 10 _consumers_
* **MEDIUM:** 1 a 20 _consumers_
* **LARGE:** 1 a 40 _consumers_

Por exemplo, se você configurar 10 _consumers_ (SMALL) para a execução do seu _pipeline_, isso significa que 10 mensagens poderão ser processadas simultaneamente.

* **Ambiente**

Os ambientes de execução dos _pipelines_ podem ser:

\- produção (prod)

\- teste (test)

Quando um _pipeline_ é executado em ambiente de teste, isso significa que as suas aplicações podem ser testadas e alteradas. Consequentemente, você tem um ambiente de trabalho que permite a livre construção e a validação dos _pipelines_ antes de irem à produção de fato. O propósito do ambiente de teste é avaliar a construção do _pipeline_ e, por isso, não possui as mesmas características de atendimento do ambiente de produção.

Quando um _pipeline_ está em ambiente de produção e precisa de uma alteração evolutiva ou apresenta alguma falha, sugerimos que as suas alterações sejam feitas no ambiente de teste para que, somente então, volte à produção.
