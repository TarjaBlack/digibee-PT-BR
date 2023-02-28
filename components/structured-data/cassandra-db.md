---
description: >-
  O Cassandra DB realiza operações em uma conexão de database Apache Cassandra.
  Dê uma olhada em alguns dos parâmetros de configuração do componente:
---

# Cassandra DB

* **Account:** conta a ser utilizada pelo componente para conectar na AWS. Pode ser do tipo AWSv4, com _access key_ e _secret_ ou _Basic_ para acesso a servidor do cassandra em uma _data center_, com usuário e senha.&#x20;
* **Operation:** operação a ser executada (INSERT, UPDATE, SELECT, DELETE).&#x20;
* **Connection String:** ‘string’ de conexão com host, porta e _keyspace_ a ser utilizado.
* **Query:** especificação CQL, conforme a operação selecionada. Este parâmetro aceita _Double Braces._&#x20;
* **Max Wait For Operation (in ms):** tempo (em ms) em que a aplicação deve aguardar até a _query_ ser finalizada.&#x20;
* **Heartbeat Connection Timeout (in ms): **_**** dummy request_ para manter conexões vivas no pool.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, e o resultado mostrará o valor false para a propriedade "success".
* **Advanced:** Abre para posteriores opções de configuração.&#x20;
* **Pool Size By Actual Consumers:** Se "verdadeiro", o número de conexões agrupadas será equivalente ao número de consumidores configurados durante a implantação do gasoduto, se "falso", então o tamanho do pool é dado pelo tamanho da implantação do pipeline, independentemente do número de consumidores

## Cassandra DB em Ação&#x20;

O CQL (Cassandra Query Language), como já diz o nome, é a linguagem de consulta para o Cassandra, ele usa variáveis em suas consultas envolvendo-as em _Double Braces_, como \{{id\}}. Leia mais no nosso artigo sobre [Funções Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/funcoes-double-braces).&#x20;

### Operação _INSERT_

#### Entrada

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.34.40 (1) (2).png>)

#### Saída&#x20;

```
{ "data": {},
 "insertCount": 1 
}
```

### **Operação **_**UPDATE**_

#### **Entrada**

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.35.00 (1) (1) (1).png>)

#### Saída

```
{ "data": {},
 "updateCount": 1
}
```

### Operação _SELECT_

{% hint style="info" %}
**Nota:** Os bancos de dados Cassandra ou Keyspaces da AWS podem retornar automaticamente os resultados de forma paginada caso possuam um número considerável de registros. A Digibee Integration Platform trata essa paginação de forma automática, para que o resultado seja consolidado na mensagem de saída do componente como uma consulta atômica. Isso elimina a necessidade de qualquer configuração ou ações adicionais por parte do usuário para obter esses resultados.
{% endhint %}

#### Entrada

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.35.21 (1) (1).png>)

#### **Saída**

```
{
	"data": [{
		"id": "5095e726-d790-4f93-9a71-10ecf2cdd72f",
		" firstName": "Rafael",
		" lastName": "Garbin"
	}],
	"rowCount": 1
}

```

### Operação _DELETE_

#### Entrada

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.39.07 (1).png>)

#### Saída

```
{
	"data": {},
	"deleteCount": 1
}

```
