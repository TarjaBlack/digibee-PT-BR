---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stored Procedure

O **Stored Procedure** realiza operações através de uma conexão com um banco de dados e retorna dados de procedimento como um único objeto de JSON.

{% hint style="info" %}
**IMPORTANTE:** cuidado com o consumo de memória para _datasets_ grandes. BLOB e CLOB ainda não são suportados.
{% endhint %}



Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Database URL:** _string_ de conexão ao banco de dados.
* **SQL Statement:** instrução SQL a ser executada.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Custom Connection Properties:** Propriedades de conexão definidas pelo usuário e específicas do banco de dados.
* **Keep Connections:** se ativada, a opção vai manter as conexões com a base de dados por no máximo 30 minutos; do contrário, será por apenas 5 minutos.
* **Advanced:** configurações avançadas.
* **Connection Test Query:** instrução SQL a ser utilizada antes que cada conexão seja estabelecida - esse parâmetro é opcional e deve ser aplicado a bancos de dados que não possuem informações confiáveis sobre o status da conexão.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

```
{
    "parameters": {
        "variable1": "value"
    }
}
```

:?{in;variable1}

* **in:** tipo de parâmetro (obrigatório)
* **variable1:** nome da variável que veio com a entrada de JSON no corpo da solicitação (obrigatório)

**Exemplo**

Digamos que você queira realizar uma chamada a um procedimento com um parâmetro de entrada (Oracle, MySql, etc.):

* call proc (:?{in; variable})
* SQL Server:
* exec proc :?{in; variable}

**IMPORTANTE:** ainda não é possível configurar o tipo IN (VARCHAR, FLOAT, INTEGER, etc.).

### Saída <a href="#sada" id="sada"></a>

* :?{out;propertyToOutput;Type;java\_type\_library}
* **out:** tipo de parâmetro (obrigatório)
* **propertyToOutput:** nome da propriedade que o componente mostrará no resultado (obrigatório)
* **Tipo:** CURSOR, VARCHAR, NUMERIC, FLOAT, etc. (obrigatório)
* **java\_type\_library:** caso você precise utilizar um procedimento em que OUT seja um Oracle CURSOR, será necessário especificar a seguinte Biblioteca: oracle.jdbc.OracleTypes (opcional)

**Exemplo**

Digamos que você queira realizar uma chamada a um procedimento com um parâmetro de entrada e saída (Oracle, MySql, etc.):

* call proc (:?{in; variable}, :?{out; nameResultOut;VARCHAR})

### SQL Server <a href="#sql-server" id="sql-server"></a>

* exec proc :?{in; variable}, :?{out; nameResultOut;VARCHAR}

### INOUT <a href="#inout" id="inout"></a>

* :?{in; variable|out;propertyToOutput;Type;java\_type\_library}
* **in:** tipo de parâmetro (obrigatório)
* **variable1:** nome da variável que veio com a entrada de JSON no corpo da solicitação (obrigatório)
* **out:** tipo de parâmetro (obrigatório)
* **propertyToOutput:** nome da propriedade que o componente mostrará no resultado (obrigatório)
* **Tipo:** CURSOR, VARCHAR, NUMERIC, FLOAT, etc. (obrigatório)
* **java\_type\_library:** caso você precise utilizar um procedimento em que OUT seja um Oracle CURSOR, será necessário especificar a seguinte Biblioteca: oracle.jdbc.OracleTypes (opcional)
* propertyToOutput: the property's name that this connector will show in the result (mandatory)

**Exemplo**

Digamos que você queira realizar uma chamada a um procedimento com um parâmetro de entrada e saída (Oracle, MySql, etc.):

* call proc (:?{in; variable|out; nameResultOut;VARCHAR})

### SQL Server <a href="#sql-server" id="sql-server"></a>

* exec proc :?{in; variable|out; nameResultOut;VARCHAR}

### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem no seguinte formato:

```
{
    "parameters": {
        "name": "value"
        ...
    }
}
```

### Saída <a href="#sada" id="sada"></a>

```
{
	"out": {
		"rs-1": [
			{
				"column1": "admin",
				"column2": 1
			},
			{
				"column1": "jose",
				"column2": 2
			}
		]
	},
	"success": true
}
```

### Saída com erro <a href="#sada-com-erro" id="sada-com-erro"></a>

```
{
	"success": false,
	"error": error_message,
	"message": cause_of_the_error
}
```
