---
description: Conheça mais sobre as URLs utilizadas na Plataforma e seus usos
---

# Sistema de URLs

URL é um acrônimo para Uniform Resource Locator e é uma referência que funciona como um endereço a um recurso na Internet.

A Digibee Integration Plaform utiliza um conjunto de URLs para identificar seus recursos. Os URLs são utilizados desde o Portal Web que pode ser acessado pelos usuários para criar, publicar e monitorar os pipelines, até, por exemplo, o Endpoint Transacional de APIs que pode ser utilizado pelos pipelines para receber requisições.

Este artigo apresenta os detalhes do sistema de URLs da Digibee Integration Plaform.

#### **Sistema de URL Atual** <a href="#h_dfbf424bac" id="h_dfbf424bac"></a>

Todos os realms criados antes de abril/2022 são acessíveis a partir do domínio godigibee.io e seguem o seguinte modelo de URL.

* **Dominio:** [godigibee.io](http://www.godigibee.io/)
* **Portal Web:** [www.godigibee.io](http://www.godigibee.io/)
  * URL do Portal Web que pode ser acessado por usuários para criar, publicar e monitorar pipelines.
* **Back-end:** core.godigibee.io
  * Endpoint voltado para o uso interno, ou seja, pelo _backend_ da Plataforma, para se fazer requisições de componentes internos.
* **Transacional:** api.godigibee.io
  * Endpoint utilizado para realizar requisições aos pipelines no ambiente de produção
* **Static content:** static.godigibee.io
  * Endpoint utilizado que fornece imagens estáticas. Ex.: Miniaturas dos pipelines e as imagens dos componentes (Triggers, Capsules and Component).
* **Test: test.godigibee.io**
  * Endpoint utilizado para identificar o endereço dos Pipelines que estão configurados como APIs, ou seja, REST, HTTP e HTTP-File.

**Nota**: Todos os realms acessíveis a partir do domínio godigibee.io seguem este modelo de URL.

#### **Sistema de URL Novo** <a href="#h_32f30180cf" id="h_32f30180cf"></a>

Realms criados a partir de maio de 2022 que são acessíveis a partir do domínio [digibee.io](http://digibee.io/) utilizarão um novo sistema de URL, conforme descrito abaixo:

* **Dominio:** [**digibee.io**](http://www.godigibee.io/)
* **Portal Web: \<realm>.portal.digibee.io**
* **Back-end: \<realm>.core.digibee.io**
* **Static content: \<realm>.static.digibee.io**
* **Test: \<realm>.test.digibee.io**
* **Prod (Transacional): .\<realm>.api.digibee.io**

**Nota**: Em um futuro próximo, haverá convivência entre o novo modelo de URLs e o modelo antigo para _realms_ criados antes de maio de 2022.
