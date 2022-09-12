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

### Cassandra DB em Ação&#x20;

O CQL (Cassandra Query Language), como já diz o nome, é a linguagem de consulta para o Cassandra, ele usa variáveis em suas consultas envolvendo-as em _Double Braces_, como \{{id\}}. Para ler o nosso artigo sobre _Double Braces_, clique [aqui](https://intercom.help/godigibee/pt-BR/articles/3185881-double-braces-e-entrada-de-dados).

### Operação _INSERT_

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.34.40 (1) (2).png>)

### Saída&#x20;

```
{ "data": {},
 "insertCount": 1 
}
```

### **Operação **_**UPDATE**_

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.35.00 (1) (1) (1).png>)

### Saída

```
{ "data": {},
 "updateCount": 1
}
```

### Operação _SELECT_

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.35.21 (1) (1).png>)

### **Saída**

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

![](<../../.gitbook/assets/Screen Shot 2022-05-09 at 17.39.07 (1).png>)

### Saída

```
{
	"data": {},
	"deleteCount": 1
}

```

### Opção _Advanced_

![](<../../.gitbook/assets/Screenshot\_1 (1).png>)
