---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream DB V3



O _**Stream DB V3**_ permite estabelecer uma conexão com um serviço que suporta o protocolo JDBC (_Java Database Connectivity_) e executar instruções SQL (_Structured Query Language_).

Diferentemente do componente [DB V1](db-v1.md), o _**Stream DB**_ foi desenvolvido para realizar execução em lotes, ou seja, cada retorno (linha resultante ou _row_) da instrução SQL executada é tratada individualmente através de um _subpipeline_, podendo conter seu próprio fluxo de processamento. Leia o artigo [Subpipelines](../../build/pipelines/subpipelines.md) para saber mais.

{% hint style="info" %}
**IMPORTANTE:** em casos onde um banco de dados Apache Hive é usado, os dados de _Updatecount_ podem estar indisponíveis devido a uma característica do sistema. Essa informação estará disponível apenas se o controle do _updated row count_ estiver habilitado no servidor Apache Hive. Para mais informações sobre suporte Apache Hive para a Digibee Integration Platform, leia o artigo [Banco de dados suportados](https://docs.digibee.com/documentation/v/pt-br/plataforma/bancos-de-dados-suportados#apache-hive).
{% endhint %}

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** para o componente fazer a autenticação a um serviço JDBC, é necessário usar uma _account_ do tipo BASIC ou KERBEROS (veja o tópico [Autenticação via Kerberos](stream-db-v3.md#autenticao-via-kerberos)).
* **Database URL:** URL (_Uniform Resource Locator_) para estabelecer conexão ao servidor de banco de dados com suporte ao protocolo JDBC. Este parâmetro aceita _Double Braces_.
* **SQL Statement:** instrução SQL a ser executada.
* **Column Name:** caso haja um erro no processamento do _subpipeline_ _onProcess_, o valor associado à coluna definida neste campo será adicionado à mensagem de erro, em um novo campo chamado "_processedId_" e que poderá ser manipulado pelo _subpipeline onException_. Veja:

```
{  
    "timestamp": 1600797662733,  
    "error": "Error message",  
    "code": 500,  "processedId": "2"
}
```

* **Parallel Execution Of Each Iteration:** quando ativada, essa opção faz com que cada uma das passagens pelo _subpipeline_ seja feita em paralelo, reduzindo o tempo de execução total. No entanto, não há qualquer garantia de que os itens sejam executados na ordem retornada pelo banco de dados.
* **Blob As File:** se ativada, a opção faz com que os campos do tipo _blob_ sejam armazenados no contexto do _pipeline_ como arquivo; do contrário, os campos são armazenados como textos normais (_strings_) e codificados em base64, conforme a seguir:

```
// "Blob As File" true
{
  "id": 12,
  "blob": "d3X8YK.file",
}

// "Blob As File" false
{
  "id": 12,
  "blob": "iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAIAAACQkWg2AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAeSURBVDhPY1Da6EMSYiBJNVDxqAZiQmw0lAZHKAEAaskfEED3lr0AAAAASUVORK5CYII="
}
```

* **Clob As File:** a opção faz com que os campos do tipo _clob_ sejam armazenados no contexto do _pipeline_ como arquivo; do contrário, os campos são armazenados como textos normais (_strings_), conforme a maneira a seguir:

```
// "Clob As File" true
{
  "id": 15,
  "clob": "f7X9AS.file",
}

// "Clob As File" false
{
  "id": 15,
  "clob": "AAAAABBBBBCCCC”
}
```

* **Charset:** essa opção é exibida apenas quando a opção **Clob As File** for ativada. Esse parâmetro permite configurar o _encoding_ de arquivos _clob_.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do pipeline apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro **Fail On Error** não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines_ (_onProcess_ e _onException_).
* **Custom Connection Properties:** propriedades de conexão específicas definidas pelo usuário.
* **Keep Connections:** se ativada, a opção vai manter as conexões com a base de dados por no máximo 30 minutos; do contrário, será por apenas 5 minutos.
* **Advanced:** se ativada, as seguintes configurações estarão disponíveis:
* **Pool Size By Actual Consumers:** se a opção estiver ativada, o número de _pooled connections_ será equivalente ao número de _consumers_ configurados durante a implantação do _pipeline_. Do contrário, o tamanho do _pool_ é dado pelo tamanho de implantação do _pipeline_, independentemente do número de _consumers_.
* **Exclusive DB Pool:** se a opção estiver ativada, um novo _pool_ não-compartilhado sempre será criado para uso exclusivo deste componente. Do contrário, um _pool_ poderá ser compartilhado entre componentes se a URL for a mesma.
* **Output Column From Label:** para alguns bancos de dados, é importante manter esta opção ativada caso o seu SELECT esteja utilizando algum _alias_, pois dessa maneira garante-se que o nome da coluna será exibido da mesma forma que o _alias_ configurado.
* **Connection Test Query:** instrução SQL a ser executada antes que cada conexão seja estabelecida (i.e. _select 1 from dual_). Esse parâmetro é opcional e deve ser aplicado apenas a bancos de dados que não possuem informações confiáveis sobre o _status_ da conexão.
* **Raw SQL Statement:** se a opção estiver ativada, o parâmetro **SQL Statement** permite o uso de _queries_ dinâmicas através de declarações _Double Braces_. Ao utilizar essa funcionalidade, você deve garantir que o _pipeline_ possua mecanismos de segurança contra instruções SQL indesejadas (_SQL Injection_). Veja mais sobre esse parâmetro na [seção](stream-db-v3.md#raw-sql-statement) abaixo.

## Raw SQL Statement

Para trazer mais flexibilidade ao utilizar o **Stream DB V3**, podemos ativar a opção **Raw SQL Statement**, configurar previamente uma _query_ e referenciá-la via _Double Braces_ no parâmetro **SQL Statement** da seguinte maneira:

#### **Query definida previamente via Template Transformer**

<figure><img src="../../.gitbook/assets/DB V2 - Raw SQL 01 - apr 23.png" alt=""><figcaption></figcaption></figure>

#### **Ativação do Raw SQL Statement**

<figure><img src="../../.gitbook/assets/DB v2 - Raw SQL 02 - apr 23.png" alt=""><figcaption></figcaption></figure>

#### **Query referenciada no parâmetro SQL Statement**

<figure><img src="../../.gitbook/assets/DB V2 - Raw SQL 03 - apr 23.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**IMPORTANTE:** como boa prática, recomendamos fortemente que ao ativar a opção **Raw SQL Statement**, as _queries_ sejam definidas previamente através do componente [**Template Transformer**](https://docs.digibee.com/documentation/components/tools/template-transformer). O uso do **Template Transformer** permite validar parâmetros através da tecnologia FreeMarker e também a declaração de parâmetros via _Double Braces_. Estes parâmetros não são resolvidos pelo **Template Transformer** e sim pelo componente **Stream DB V3**, que por padrão configura e valida os parâmetros da instrução SQL previamente (_PreparedStatement_). Ao aplicar essas medidas de segurança, você diminui os riscos de ataques do tipo _SQL Injection_.
{% endhint %}

Na imagem abaixo, temos à esquerda um exemplo do uso recomendado do componente (com o _Double Braces_ na cláusula _WHERE_, no destaque verde); e à direita um exemplo do uso não recomendado (com o FreeMarker na cláusula _WHERE_, no destaque vermelho) que pode trazer riscos à segurança do _pipeline_:

<figure><img src="../../.gitbook/assets/DB V2 - Raw SQL 04 exp - apr 23.png" alt=""><figcaption></figcaption></figure>

## Tecnologia <a href="#tecnologia" id="tecnologia"></a>

### **Autenticação via Kerberos** <a href="#autenticao-via-kerberos" id="autenticao-via-kerberos"></a>

Para realizar autenticação a um banco de dados via Kerberos é necessário:

* informar uma conta (_account_) do tipo KERBEROS
* configurar um Kerberos principal
* configurar uma _keytab_ (que deve ser a base64 do próprio arquivo _keytab_ gerado)

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Estrutura de mensagem disponível no **_**subpipeline**_** onProcess** <a href="#estrutura-de-mensagem-disponvel-no-subpipeline-onprocess" id="estrutura-de-mensagem-disponvel-no-subpipeline-onprocess"></a>

Uma vez que a instrução SQL é executada, o _subpipeline_ será disparado recebendo o resultado da execução por meio de uma mensagem na seguinte estrutura:

```
{  
    "coluna1": "dado1",   
    "coluna2": "dado2",  
    "coluna3": "dado3"
}
```

### Saída com erro <a href="#erro" id="erro"></a>

```
{   
    "code": error_code,   
    "error": mensagem de erro,   
    "processId": the_id_column_value
}
```

### Saída <a href="#sada" id="sada"></a>

Após a execução do componente, é retornada uma mensagem na seguinte estrutura:

```
{   
    "total": 0,   
    "success": 0,   
    "failed": 0
}
```

* **total:** número total de linhas processadas
* **success:** número total de linhas processadas com sucesso
* **failed:** número total de linhas cujo processamento falhou

{% hint style="info" %}
**IMPORTANTE:** para detectar se uma linha foi processada corretamente, cada _subpipeline_ onProcess deve responder com { "success": true } a cada elemento processado.
{% endhint %}

O _**Stream DB V3**_ realiza processamento em lote. Consulte o artigo [Processamento em lote](../../tutoriais-e-melhores-praticas/processamento-em-lote.md) para saber mais sobre este conceito.

## _Pool_ de conexão <a href="#h_cf06a705b9" id="h_cf06a705b9"></a>

Por padrão, utilizamos um _pool_ com tamanho baseado nas configurações do _pipeline_ implantado. Caso seja um _pipeline_ SMALL, então o tamanho do _pool_ será de 10; para o MEDIUM, será de 20; e para o LARGE, de 40.

É possível gerenciar o tamanho do _pool_ também na hora da implantação. Para isso, será necessário habilitar o parâmetro **Pool Size By Actual Consumers** no componente. Com isso, será utilizado o que for configurado manualmente na tela de implantação.

No exemplo da figura abaixo, foi configurado um _pipeline_ SMALL com 5 _consumers_. Se você quiser que o _pool_ dos componentes de banco de dados ([DB V2](db-v2.md) e Stream DB V3) utilize esse tamanho, é necessário habilitar o parâmetro **Pool Size By Actual Consumers** em todos os componentes existentes.

![](<../../.gitbook/assets/streamdb v3.png>)

Tenha atenção redobrada ao configurar o tamanho do _pool_ manualmente para que não ocorra nenhum _deadlock_ em chamadas concorrentes ao mesmo banco.

O nosso _pool_ é compartilhado entre os componentes de banco de dados que acessam o mesmo banco de dados dentro do _pipeline_. Caso seja necessário um _pool_ exclusivo para um determinado componente, habilite o parâmetro **Exclusive DB Pool**.
