---
description: Conheça a funcionalidade Relacionamento da Plataforma Digibee
---

# Relacionamento

A funcionalidade Relacionamento, baseada no conceito de Modelagem Relacional de Dados, permite criar modelos de relacionamento entre entidades com base em diferentes tipos de relações, que poderão ser utilizados posteriormente na construção de _pipelines_ através do [componente Relationship](../components/structured-data/relationship.md).

Localizado na página de configurações da Plataforma Digibee, o submenu Relacionamento disponibiliza a listagem de todos os modelos de relacionamento já criados dentro da Plataforma com seus parâmetros de configuração. Além disso, também é possível editar e excluir Relacionamentos existentes, assim como consultar dados de entidades relacionadas através de ações, conforme explicado neste artigo.

![](<../.gitbook/assets/01 (21).png>)

### Tipos de relação <a href="#h_004188821b" id="h_004188821b"></a>

A funcionalidade Relacionamento comporta três diferentes tipos de relação. Ao criar um novo modelo de relacionamento, apenas um tipo deverá ser escolhido a depender da natureza dos atributos das entidades, isto é, dos dados que deseja relacionar no _pipeline_. São eles:

* _**ID translation**_**:** Permite criar relações 1:1 (1 para 1) entre entidades, com possibilidade de sobrescrita de dados;
* _**Parent child**_**:** Permite criar relações 1:N (1 para muitos) entre entidades;
* _**ID translation no overwrite**_**:** Permite criar relações 1:1 (um para 1) entre entidades, sem a possibilidade de sobrescrita de dados.

#### Exemplo de relação <a href="#h_af35c226ef" id="h_af35c226ef"></a>

A título de exemplo, imaginemos duas entidades, Loja e Funcionário. A entidade Loja possui como atributo o dado ‘**id**’, e a entidade Funcionário, por sua vez, possui como atributo o dado ‘**nome**’. Veja:

| **LOJA** | **FUNCIONÁRIO** |
| -------- | --------------- |
| id       | nome            |

Nesse caso, podemos estabelecer as seguintes regras:

* Uma loja, de determinado ‘**id**’ identificador, emprega vários funcionários;
* Um funcionário, de determinado ‘**nome**’, trabalha em apenas uma loja.

Além disso, podemos estabelecer os seguintes relacionamentos:

* A relação entre loja e funcionário é de **1:N** (uma loja para muitos funcionários);
* A relação entre funcionários e loja é **N:1** (muitos funcionários para uma única loja).

Utilizando a funcionalidade Relacionamento, conseguimos relacionar os dados '**id**' e '**nome**', provenientes das entidades Loja e Funcionário, respectivamente, utilizando o tipo de relacionamento ‘**Parent child**’. Exemplificando, ao relacionar esses dados, conseguimos buscar os nomes de todos os funcionários de determinada loja por meio do seu **id**, e buscar o id da loja que determinado funcionário trabalha através do **nome** do mesmo.

Assim, após criado o modelo, conseguiremos incorporá-lo no _pipeline_ para que as entidades relacionadas possam ser manipuladas utilizando o [componente Relationship](../components/structured-data/relationship.md).

### Botão "+ Criar" <a href="#h_9f91acc973" id="h_9f91acc973"></a>

![](<../.gitbook/assets/02 (3).png>)

Para criar um novo modelo de Relacionamento, basta clicar no botão “+ Criar”, no canto superior direito da página, e informar os seguintes parâmetros de configuração:

* **Nome:** Nome do modelo de relacionamento. Este parâmetro atua como referência para o modelo de relacionamento que será utilizado pelo componente Relationship no _pipeline_;
* **Tipo:** O tipo de relacionamento entre entidades. São eles:
  * _**ID translation**_**:** Permite criar relações 1:1 (1 para 1) entre entidades, com possibilidade de sobrescrita de dados;
  * _**Parent child**_**:** Permite criar relações 1:N (1 para muitos) entre entidades;
  * _**ID translation no overwrite**_**:** Permite criar relações 1:1 (um para 1) entre entidades, sem a possibilidade de sobrescrita de dados.
* **Campo A:** Campo identificador de um relacionamento. Representa a origem, isto é, o dado ou atributo identificador.
* **Campo B:** Campo que armazenará o valor referente ao seu identificador (Campo A). Representa o destino, isto é, o dado ou atributo alvo.
* **Descrição:** Descrição do modelo de relacionamento.

### Ação Editar **(botão Lápis)** <a href="#h_986b9e59c0" id="h_986b9e59c0"></a>

![](<../.gitbook/assets/03 (9).png>)

Esta ação permite editar todos os parâmetros de configuração definidos no momento da criação do novo Relacionamento. São eles: **Nome**, **Tipo** (_**ID translation,**_ _**Parent child**_, _**ID translation no overwrite**_), **Campo A**, **Campo B** e **Descrição**.

### Ação Buscar (botão Peça) <a href="#h_e1cf66d669" id="h_e1cf66d669"></a>

![](<../.gitbook/assets/04 (1).png>)

Esta ação permite realizar buscas por dados de entidades relacionadas dentro do modelo de relacionamento em questão. Os parâmetros que auxiliam o usuário a realizar a busca são:

* **Ambiente:** O ambiente em que se encontra o dado relacionado, podendo ser:
  * _test_;
  * _prod_.
* **Campo:** É possível selecionar um campo dentre os configurados na criação do modelo de relacionamento (**Campo A** e **Campo B**);
* **Valor:** Dado cadastrado no modelo de relacionamento, tendo por base o **Campo** supracitado.

**IMPORTANTE**: A inserção, atualização e exclusão de dados de um modelo de relacionamento é feita através do componente **Relationship**, que leva em consideração o ambiente no qual o _pipeline_ foi implantado para realizar essas ações.

**Por exemplo:** para inserir, atualizar e excluir dados de um modelo de relacionamento criado em _**test**_, basta executar o _pipeline_ no próprio _test-mode_ ou implantá-lo __ no ambiente _**test**_; para inserir, atualizar e excluir dados de um modelo de relacionamento criado em **prod**, basta implantá-lo no ambiente **prod**.

### Ação Remover Relacionamento (botão Lixeira) <a href="#h_f95399056d" id="h_f95399056d"></a>

Através desta ação, é possível excluir um modelo de relacionamento caso este não esteja sendo utilizado na Plataforma, seja em _pipelines_ implantados, não implantados ou arquivados.

![](<../.gitbook/assets/05 (13).png>)

**IMPORTANTE:** Ao clicar em “Confirmar”, a ação não poderá ser desfeita.
