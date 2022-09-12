---
description: Conheça a funcionalidade Test mode da Digibee Integration Plaform
---

# Test mode

O _Test mode_ é uma funcionalidade da Digibee Integration Plaform muito utilizada na construção de _pipelines_ por possibilitar uma maneira de executar e testar o _pipeline_ diretamente da sua área de desenvolvimento. Ele é muito utilizado para avaliar a lógica de implementação, depurar e solucionar problemas de integrações antes de implantar o _pipeline_ em produção.

## Informações iniciais <a href="#h_675b51f516" id="h_675b51f516"></a>

O _Test mode_ executa o _pipeline_ no ambiente _test_. Ou seja, utilizamos do ambiente _test_ da Digibee Integration Plaform para que seu _pipeline_ seja executado e a lógica de integração validada. Além disso, o _Test mod_e utiliza de valores de _test_ registrados nos serviços de _Globals_, Contas, Relacionamento e Multi-Instância.

**IMPORTANTE:** Dependendo da quantidade de transações de dados a ser executada, o _Test mode_ poderá exibir a mensagem “_Out of memory_”.

## Como testar seu _pipeline_ através do _Test mode_? <a href="#h_7970a1ec07" id="h_7970a1ec07"></a>

### Aba Teste <a href="#h_6cf0165d96" id="h_6cf0165d96"></a>

Na aba TESTE, é possível inserir dados de entrada na coluna da esquerda para a realização do teste, clicar em “EXECUTAR”, e visualizar o resultado da execução no _payload_ de saída (coluna da direita).

![](../../../.gitbook/assets/01.gif)

**Por exemplo:** O componente REST V2, que realiza chamadas para _endpoints_ de HTTP, possibilita buscas e consultas em bases de dados de _web services_ como o ViaCEP. No exemplo acima, o _payload_ de entrada `“cep”: 22460050` gerou como resultado o _payload_ de saída contendo diferentes informações relacionadas ao dado de entrada.

#### _**Pipelines**_** multi-instância**

Caso o _pipeline_ a ser executado seja [multi-instância](../../../configurations/multi-instancia.md), a primeira coluna da aba TESTE permitirá que você informe a instância a qual pretende executar, como no exemplo abaixo:

![](<../../../.gitbook/assets/02 (1).gif>)

Desse modo, o _Test mode_ utilizará os dados da instância selecionada para prosseguir com a execução.

### Aba Logs <a href="#h_273d39100c" id="h_273d39100c"></a>

A aba LOGS traz informações a respeito dos registros de eventos que ocorrem durante a execução de um _pipeline_ no _Test mode_, permitindo a visualização dos logs individuais em uma seção dedicada. As informações de cada log estão dispostas no relatório conforme as seguintes colunas:

* **Timestamp:** A data e o horário em que o passo foi executado no _pipeline_;
* **Nível do log:** A classificação do log, ou seja, o nível do mesmo, podendo ser:
  * **INFO:** Logs informativos;
  * **ERROR:** Logs que apresentaram erro em sua execução;
  * **WARN:** Logs com propósito de aviso.
* **Mensagens do log:** As mensagens de cada log, ou seja, os registros de eventos referentes à execução do _pipeline_.

#### **Ações**

É possível copiar os detalhes de determinado log através da opção Botão Copiar presente em Ações.

![](<../../../.gitbook/assets/03 (5).gif>)

#### **Botão “Ver mais logs”**

Ao clicar em “Ver mais logs”, são carregados mais logs de registro para serem consultados.

### Aba Mensagens <a href="#h_d99b8de4f9" id="h_d99b8de4f9"></a>

Nesta aba, é possível visualizar as mensagens de execução do _pipeline_. _C_ada mensagem exibida é referente ao resultado da execução do respectivo componente. Um componente sempre receberá o _payload_ produzido pelo componente anterior, processará esse _payload_ com base em sua função e produzirá um novo _payload_ como resposta. No entanto, serão mostrados somente os 50 primeiros passos do _pipeline_ quando este for executado em _Test mode_.

![](<../../../.gitbook/assets/04 (3).gif>)

É possível copiar para a área de transferência determinada mensagem através do botão localizado no canto superior direito de cada bloco.

#### **Botão “Atualizar”**

Ao clicar em “Atualizar”, todo o conteúdo desta aba é atualizado trazendo mais mensagens do _pipeline_ executado.

## Informações adicionais <a href="#h_003e842391" id="h_003e842391"></a>

### Teclas de atalho <a href="#h_8d34a69ea1" id="h_8d34a69ea1"></a>

* Para abrir ou fechar o _Test mode_: ctrl+D; _command_ + D.
* Para executar o _Test mode_: ctrl + _Enter_; _command_ + _Enter_.
