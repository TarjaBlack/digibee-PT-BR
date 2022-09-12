---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream DB V1

O **Stream DB V1** efetua operações através da conexão com um banco de dados, transmitindo dados para um _subpipeline_ que os processa.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Database URL:** _string_ de conexão ao banco de dados.
* **SQL Statement:** instrução SQL a ser executada.
* **Column Name:** nome da coluna a ser lida.
* **Coalesce:** quando ativada, essa opção controla se os objetos de dados são fundidos em uma sequência ou se um erro é gerado.
* **Parallel Execution Of Each Iteration:** ocorre em paralelo com a execução do _loop_.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do _pipeline_ apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro "Fail On Error" não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines_ (onProcess e onException).
* **Custom Connection Properties:** propriedades de conexão específicas definidas pelo usuário.
* **Keep Connections:** se ativada, a opção vai manter as conexões com a base de dados por no máximo 30 minutos; do contrário, será por apenas 5 minutos.
* **Advanced:** configurações avançadas.
* **Connection Test Query:** instrução SQL a ser utilizada antes que cada conexão seja estabelecida - esse parâmetro é opcional e deve ser aplicado a bancos de dados que não possuem informações confiáveis sobre o status da conexão.

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem no seguinte formato:

```
{
	"parameters": {
		"name": "value"
		...
	}
}
```

#### Estrutura de mensagem "onProcess" <a href="#estrutura-de-mensagem-onprocess" id="estrutura-de-mensagem-onprocess"></a>

```
{	
    "column1":"data1", "column2":"data2", ... 
}
```

#### Saída com erro <a href="#sada-com-erro" id="sada-com-erro"></a>

```
{	
    "code": error_code,	
    "error": error_message,	
    "processedId": the_id_column_value
}
```

#### Saída <a href="#sada" id="sada"></a>

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
**IMPORTANTE:** quando as linhas são processadas corretamente, os seus respectivos _subpipelines_ retornam { "success": true } para cada uma delas.
{% endhint %}

Este componente realiza processamento em lote. Para entender melhor o conceito, clique [aqui](../../tutoriais-e-melhores-praticas/processamento-em-lote.md).
