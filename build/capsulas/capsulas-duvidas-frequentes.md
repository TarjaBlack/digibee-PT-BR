---
description: Tire suas dúvidas sobre as Cápsulas.
---

# Cápsulas - Dúvidas Frequentes

Para te ajudar a aproveitar ainda mais as Cápsulas, separamos as perguntas mais frequentes sobre esse novo recurso da Plataforma Digibee HIP.&#x20;

### O que são Cápsulas?

Cápsulas são uma nova e grande funcionalidade da Digibee, parte integrante da Plataforma Digibee HIP.

As **Cápsulas Digibee** são componentes reutilizáveis que podem ser utilizados ou criados por qualquer usuário da Plataforma ao aplicar o mesmo modelo de desenvolvimento visual concebido na criação do _pipeline_, provendo uma lógica de negócio reutilizável, segura, validada e evolutiva.

Uma Cápsula permite que a integração de fluxos seja publicada na paleta de componentes para ser utilizada em outro momento, de maneira simplificada e ainda mais rápida

****

### **Quais funcionalidades são resolvidas pelas Cápsulas?**

A essência da Cápsula Digibee é apresentar conjuntos de integrações prontos, testados e validados para o mercado se conectar melhor internamente ou externamente de forma documentada. Isso permite a uma empresa modernizar a sua TI e que suas empresas parceiras possam utilizar as ofertas com segurança e simplicidade.

Pense, por exemplo, em uma organização onde existem diversos fluxos de dados relevantes para todas as áreas - autenticação, consulta de clientes, consulta de estoque, entre outros. Para esses fluxos é possível criar _pipelines_ que distribuem os serviços, porém são necessários também os processos de documentação, catalogação e manutenção do _pipeline_ implantado.

Tornar os fluxos de qualquer parte de um _pipeline_ mais acessíveis permite que você defina objetivos mais amplos para o negócio. Por isso, criamos essa funcionalidade que reúne fluxos e os torna reutilizáveis e auto documentados assim como os nossos componentes _core._ Assim, os fluxos se tornam mais fáceis de serem utilizados e ficam conhecidos por toda a sua organização, bastando consultar diretamente a paleta de componentes.

As Cápsulas possuem os componentes _core_ da Plataforma Digibee HIP, ou seja, têm todas as funcionalidades entregues por eles.



### Como as Cápsulas são construídas?

\
As Cápsulas podem ser construídas pela própria organização, que define de forma documentada todos os parâmetros e o fluxo de dados e negócio dentro do contexto do seu projeto. As Cápsulas também podem ser criadas pela Digibee e pelos seus parceiros e disponibilizadas para uso.

Quando o cliente constrói a Cápsula, ele pode definir parâmetros, documentação e interface, além de conseguir orientar o uso. A liberdade de construir as Cápsulas vem com todas essas funcionalidades e a documentação fica dentro do próprio componente.



### Posso usar a Cápsula no meu ecossistema de parceiros e clientes?

Sim. É possível ter Cápsulas com integrações prontas entre o sistema de uma empresa e do seu parceiro. As Cápsulas também podem ser reaproveitadas para outros parceiros com casos de uso semelhantes.

Por exemplo, um banco pode utilizar uma Cápsula de microcrédito já pronta para uso com PDVs de diferentes redes de farmácias.

\


### A Cápsula é segura para compartilhar os meus dados sensíveis?&#x20;

Sim. As Cápsulas e a Plataforma Digibee possuem uma série de recursos para proteger os seus dados em trânsito e em repouso quando estão sob a nossa responsabilidade.

Por serem incorporadas dentro do _pipeline_ de uma organização, as Cápsulas são executadas isoladamente, mesmo dentro da sua própria organizaçã



### As Cápsulas são compatíveis com a demanda de informação do meu legado?&#x20;

Sim. As Cápsulas são construídas a partir dos componentes _core_ da Plataforma Digibee HIP, que são utilizados nos _pipelines_. É neles que todas as suas funcionalidades ficam registradas.

### As Cápsulas ajudam na migração de sistemas para nuvem?&#x20;

Sim. Quando acontece um processo de migração para nuvem, é muito importante ter estratégias de convivência com _on premise_. Ao incorporar as Cápsulas nessa estratégia, é possível, por exemplo, desenvolver soluções que cadastrem dados no _on premise_, na nuvem ou em ambos.

Além disso, a Digibee conta com uma grande variedade de Cápsulas de soluções _cloud native_ à sua disposição.

### As Cápsulas Digibee oferecem suporte para ampliar o meu sistema de negócios?&#x20;

Sim. A Digibee conta com o time de Delivery, especialista em Cápsulas, e irá apoiar todos os clientes durante o processo de construção e desenvolvimento de projetos para cada organização, incluindo a criação de Cápsulas públicas (feitas de acordo com a solicitação da empresa).

### Qual é o limite de utilização das Cápsulas nos meus pipelines?&#x20;

A Plataforma não impõe um limite quantitativo de componentes que podem ser utilizados no _pipeline_, sejam eles componentes _core_ ou Cápsulas. Já o _pipeline_ possui limites como quantidade de execuções concorrentes, _timeout_ e capacidade controlada na implantação quando se escolhe SMALL, MEDIUM ou LARGE.

### Quantas Cápsulas podem ser criadas?

É possível criar quantas Cápsulas for preciso.&#x20;

### Por que é preciso informar um contrato de saída da Cápsula?

Como as Cápsulas são componentes reutilizáveis em _pipelines,_ recorremos ao contrato de saída com especificação _JSON Schema_ para garantir que os _pipelines_ tenham clareza e segurança nas informações de resposta.

Além disso, o contrato de saída também apoia na automação do versionamento das Cápsulas (veja a resposta da pergunta [**Como funciona o versionamento e a manutenção das Cápsulas? Como eu posso garantir que o meu negócio não será afetado?**](https://intercom.help/godigibee/pt-BR/articles/4860435-como-funciona-o-versionamento-e-a-manutencao-das-capsulas-como-eu-posso-garantir-que-o-meu-negocio-nao-sera-afetado)).

### **Como eu faço para utilizar **_**Accounts**_** dentro das Cápsulas?**

_Accounts_ são funcionalidades utilizadas por componentes _core (_como o SAP, por exemplo) para realizar autenticação nos _endpoints_. Para recorrer a uma _Account_, basta encontrar a lista de _Accounts_ na tela _pipeline canvas_, que vêm direto do _Realm_ e são gerenciados no menu _Configurações_ > _Accounts_.

Nas Cápsulas, essa funcionalidade possui uma pequena diferença em relação ao _pipeline_ que irá utilizá-la, já que nem sempre _Accounts_ e _pipelines_ estão no mesmo _Realm_ de construção. Por isso, é necessário definir previamente uma lista de _Placeholder_ de _Accounts_. Essa lista pode ser definida na tela de Cápsulas clicando em:

**`Configurações na tela > aba Con`**`tas`

Na tela descrita acima serão definidas as _Accounts_ com _Label_ e a descrição para orientar sobre o tipo de _Account_ que deve ser selecionado dentro do _pipeline_ _canvas_.

![](<../../.gitbook/assets/01 (24).png>)



### **Como eu posso identificar quais Cápsulas são criadas pela Digibee?**

As Cápsulas criadas pela Digibee são identificadas por meio do ícone _Certificated_ (símbolo de verificação na cor azul). Veja abaixo como identificá-lo:

![](<../../.gitbook/assets/02 (8).png>)



### **Quais são as diferenças entre as Cápsulas e as Bibliotecas?**

As Bibliotecas foram uma versão experimental criada pela Digibee para aprender sobre reutilização utilizando a Plataforma Digibee HIP.

As Cápsulas contemplam todos os aprendizados coletados na experiência com as bibliotecas e estão disponíveis nos modos de:

* Edição
* Versionamento
* Estratégia para utilização de _Accounts_
* Documentação
* Formulário de configurações parametrizáveis

### **As Cápsulas podem ser publicadas para outros clientes?**

Não. As Cápsulas possuem uma série de permissões que são administradas pela Digibee. Essas permissões determinam quais usuários podem tornar uma Cápsula pública.

### &#x20;**Parceiros de clientes podem publicar Cápsulas públicas?**&#x20;

Não. Essa configuração ainda não está disponível, mas está sendo avaliada para oportunidades futuras. ****&#x20;

****

### Cápsulas com a mesma funcionalidade sendo utilizadas por diferentes clientes/empresas ficam restritas?&#x20;

Sim. As Cápsulas ficam restritas a cada empresa que as estiver utilizando.

### **Como funciona o versionamento e a manutenção das Cápsulas? Como eu posso garantir que o meu negócio não será afetado?**

Para garantir confiabilidade nas atualizações das Cápsulas, a Digibee adotou um controle de versionamento composto por 3 níveis. Quando as versões precisam ser atualizadas, a Plataforma Digibee HIP analisa uma Cápsula automaticamente e determina quais serão os valores dos níveis.

Estes são os 3 níveis de versionamento:

* **Major:** versão da Cápsula quando um item de configuração (entrada ou saída) é removido ou se torna obrigatório. Essa versão também se aplica quando o contrato da Cápsula é totalmente modificado. O direcionamento para essa versão é feito automaticamente pela própria Plataforma.
* **Minor:** versão da Cápsula quando um item de configuração (entrada ou saída) é acrescentado ou se torna opcional. Essa alteração ainda não é considerada “Major”.
* **Fix:** versão da Cápsula quando ocorrem alterações nada impactantes para os _pipelines_ que a utilizam. Essa alteração não é considerada “Major” nem “Minor”.

É importante saber que essas alterações serão realizadas somente se a versão passando por alteração tiver sido publicada anteriormente. Por exemplo, se você criar uma Cápsula, ela receberá inicialmente a versão "1.0.0". Enquanto não for publicada, essa versão nunca será modificada quando forem feitas atualizações nela.

Após a publicação da Cápsula, a versão “1.0.0” será definida como não editável. Então, quando uma nova atualização for realizada na mesma Cápsula, a Plataforma irá analisar o que foi alterado para determinar se o número da versão será acrescido na versão Major, Minor ou Fix.

### &#x20;**Como funciona o processo de atualização das Cápsulas nos meus **_**pipelines**_**?**&#x20;

A Plataforma Digibee nunca realiza alterações diretas na estrutura ou informação de _pipelines_ implantados. Com isso, jamais afetamos um _pipeline_ sem que um usuário autorizado na sua organização faça uma nova implantação.

Como precisamos ajudar na distribuição simplificada das Cápsulas, adotamos a seguinte estratégia:

Ao incluir uma Cápsula no seu _pipeline_, você está o associando a versão "Major" ou "Minor" da Cápsula (conforme citado no exemplo da pergunta [**Como funciona o versionamento e a manutenção das Cápsulas? Como eu posso garantir que o meu negócio não será afetado?**](https://intercom.help/godigibee/pt-BR/articles/4860435-como-funciona-o-versionamento-e-a-manutencao-das-capsulas-como-eu-posso-garantir-que-o-meu-negocio-nao-sera-afetado)).

Mas se você se perguntar onde foi parar a versão "Fix”, saiba que um _pipeline_ sempre recebe automaticamente a versão "Fix” mais recente quando uma nova implantação é realizada ou quando o _test-mode_ é executado na tela do _pipeline_ _canvas_. Conforme mencionado anteriormente, a versão "Fix" é alterada apenas quando a modificação não for impactante para o _pipeline_.

Os _pipelines_ não são afetados ou atualizados por versões "Major" ou "Minor" de uma Cápsula que faz parte das suas composições. Para utilizar essa Cápsula, um Analista de Integração responsável pelo _pipeline_ deverá realizar a aplicação manualmente.\


### **O que significa publicar uma Cápsula?**

Ao concluir a construção de uma Cápsula, é preciso publicá-la para que se torne acessível na tela _pipeline canvas_. Para realizar essa ação na lista de Cápsulas, siga estes passos:

* Acesse o Menu _Cápsula_;
* Clique no ícone do foguete ou na tela de _Capsule Canvas_;
* Clique no botão Publicar;
* Clique no botão Salvar.

**Obs.:** se nenhuma das opções acima for exibida, consulte o gestor de acesso de sua empresa e solicite a inclusão da permissão _CAPSULE:UPDATE:PUBLISH_.

****

### **Existe um processo de governança para as Cápsulas da Digibee?**

Sim. Todos os componentes abertos passam pelos processos de qualidade e segurança que garantem os mesmos padrões aplicados nos componentes _core_ da Plataforma Digibee HIP.

### **Como eu controlo o acesso às Cápsulas dentro da minha organização?**

Criamos um conjunto de permissões dedicado a essa funcionalidade, por meio do qual é possível controlar as funções específicas, permitindo a gestão completa do ciclo de vida das suas Cápsulas.

Estas são as divisões das permissões:

* **Permissões de criação**

CAPSULE:CREATE:HEADER - permite o cadastro de novos headers para serem utilizados na criação de Coleções.

CAPSULE:CREATE:GROUP - permite o cadastro de novos grupos para serem utilizados na criação de Cápsulas.

CAPSULE:CREATE - permite a criação de novas Cápsulas e Coleções.

* **Permissões de Edição**

CAPSULE:DELETE - permite o arquivamento de Cápsulas existentes.

CAPSULE:UPDATE - permite a edição de Cápsulas existentes.

* **Permissões Especiais**

TEST-MODE:EXECUTE:CAPSULE - permite a execução de testes em Cápsulas na tela de Cápsulas.

CAPSULE:UPDATE:PUBLISH - permite a publicação de Cápsulas a serem utilizadas por outros usuários.

* **Permissões de Leitura**

CAPSULE:READ - permite a visualização das Cápsulas no Menu Cápsula.

CAPSULE:READ:GROUP - permite a visualização e escolha de um grupo para o cadastro de uma nova Cápsula.

CAPSULE:READ:HEADER - permite a visualização e escolha de um _header_ para o cadastro de uma nova coleção.

CAPSULE:READ:CONSUMER - permite a utilização das Cápsulas dentro do _Pipeline canvas_.

### **Por que eu não posso usar Object Store e Digibee Storage dentro de uma Cápsula?**&#x20;

\
Esses componentes são recursos nativos do seu _Realm._ Portanto, são __ autorizados automaticamente por estarem dentro do contexto controlado do _Realm_. Como uma Cápsula pode ser construída para ser utilizada por outros _Realms,_ não é possível autorizar o acesso a dados desses componentes dentro da Cápsula.

\
