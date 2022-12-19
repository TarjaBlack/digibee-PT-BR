---
description: >-
  Saiba quais são os tipos de bancos de dados e versões suportadas pela Digibee
  Integration Platform.
---

# Bancos de Dados suportados

O acesso aos bancos de dados é feito por meio do uso de componentes próprios para isso, tais como:

* DB ([V1](../components/structured-data/db-v1.md) e [V2](../components/structured-data/db-v2.md))
* Stream DB ([V1](../components/structured-data/stream-db-v1.md) e [V3](../components/structured-data/stream-db-v3.md))
* [Stored Procedure](../components/structured-data/stored-procedure.md)

Se quiser saber mais sobre os componentes acima, basta clicar em cima dos seus nomes ou das suas versões para ler os respectivos artigos.

Atualmente a Digibee Integration Platform suporta os seguintes bancos de dados:

## SQL Server <a href="#sql-server" id="sql-server"></a>

Nas versões:

* Microsoft SQL Server 2019
* Microsoft SQL Server 2017
* Microsoft SQL Server 2016
* Microsoft SQL Server 2014
* Microsoft SQL Server 2012
* Microsoft SQL Server 2008 R2
* Azure SQL Database
* Azure SQL Data Warehouse or Parallel Data Warehouse
* Azure SQL Managed Instance (Extended Private Preview)

{% hint style="info" %}
**IMPORTANTE:** embora a conexão através da versão 2019 do Microsoft SQL Server seja suportada, nem todas as funcionalidades desta versão poderão estar disponíveis.
{% endhint %}

**String de Conexão**

```
jdbc:sqlserver://[serverName[\instanceName][:portNumber]]
```

## Oracle <a href="#oracle" id="oracle"></a>

Nas versões:

* 19.x
* 18.3
* 12.2 ou 12cR2
* 12.1 ou 12cR1
* 11.2 ou 11gR2

**Strings de Conexão**

* Sintaxe Oracle Net

```
jdbc:oracle:thin:@(DESCRIPTION=
(LOAD_BALANCE=on)
(ADDRESS_LIST=
(ADDRESS=(PROTOCOL=TCP)(HOST=host1) (PORT=5221))
(ADDRESS=(PROTOCOL=TCP)(HOST=host2)(PORT=5221)))
(CONNECT_DATA=(SERVICE_NAME=orcl)))
```

* Sintaxe com Nome de Serviço

```
jdbc:oracle:thin:@//localhost:5221/orcl
```

**IMPORTANTE:** leve em consideração que apenas conexões do tipo _thin_ são suportadas. Ao acessar as bases de dados especificadas nessa _string_ de conexão, você concorda que possui as licenças Oracle necessárias.

## Mysql <a href="#mysql" id="mysql"></a>

Nas versões:

* 5.6
* 5.7
* 8.0

**String de Conexão**

```
jdbc:mysql://<host>:<port>/<database>
```

**IMPORTANTE:** a Digibee Integration Platform desabilita a interpretação de _strings_ Maria DB pelo _driver_ Mysql. No entanto, é possível utilizar o _driver_ Maria DB para se conectar a versões mais antigas do Mysql.

## Maria DB <a href="#maria-db" id="maria-db"></a>

Na versão:

* 5.5.3+

**String de Conexão**

```
jdbc:mariadb://<host>:<port>/<database>
```

**IMPORTANTE:** a Digibee Integration Platform desabilita a interpretação de _strings_ Maria DB pelo _driver_ Mysql.

## Progress <a href="#progress" id="progress"></a>

Na versão:

* OpenEdge 10.1.x+

**String de Conexão**

```
jdbc:datadirect:openedge://hostname:port
```

## Sybase <a href="#sybase" id="sybase"></a>

Na versão:

* SAP/Sybase ASE

**String de Conexão**

```
jdbc:sybase:Tds:host:port
```

## PostgreSQL <a href="#postgresql" id="postgresql"></a>

Em todas as versões

**String de Conexão**

```
jdbc:postgresql://host:port/database
```

## OLAP DataSource via MDX <a href="#olap-datasource-via-mdx" id="olap-datasource-via-mdx"></a>

Nas versões:

* Hyperion Essbase 7
* Microsoft Analysis Services 2005
* Mondrian (sem informação de versão)
* SAP BW 3.0a+

**Strings de Conexão**

* MS SQL Server

```
jdbc:jdbc4olap:http://<server>:<port>/OLAP/msmdpump.dll
```

* Mondrian

```
jdbc:jdbc4olap:http://<server>:<port>/mondrian/xmla
```

* SAP BW

```
jdbc:jdbc4olap:http://<server>:<port>/sap/bw/soap/xmla?sap-client=number
```

**IMPORTANTE:** esse modo de conexão utiliza o padrão XMLA (XML for Analysis), que deve estar habilitado no servidor de OLAP a ser acessado.

## JTOpen for AS/400 <a href="#jtopen-for-as400" id="jtopen-for-as400"></a>

Sem informação de compatibilidade

**String de Conexão**

```
jdbc:as400://<server>[:port];prompt=false
```

**IMPORTANTE:**

* A porta de Database Access (padrão 8471) deve ser mapeada conforme a documentação da IBM. Clique [aqui](https://www.ibm.com/support/pages/tcpip-ports-required-ibm-i-access-and-related-functions) para acessá-la.
* Especifique o parâmetro “prompt=false” para que o _driver_ não tente solicitar credenciais, que são passadas automaticamente.

## SAP HANA <a href="#sap-hana" id="sap-hana"></a>

Sem informação de compatibilidade

**String de Conexão**

```
jdbc:sap://<server>:<port>
```

## Firebird <a href="#firebird" id="firebird"></a>

Nas versões:

* 2.5+

**Strings de Conexão**

```
jdbc:firebirdsql://<HOST>:<PORT>/C:\PATH_TO_DATABASE/DATABASE_FILE.FDB
```

## DB Informix <a href="#h_397032b59c" id="h_397032b59c"></a>

**Ao acessar as bases de dados especificadas nessa \_string**\_\*\* de conexão, você concorda que possui as licenças IBM necessárias.\*\*

Sem informação de compatibilidade

**String de Conexão**

```
jdbc:informix-sqli://<HOST>:<PORT>/<DATABASE>:informixserver=<INFORMIX_SERVER>
```

## Netsuite <a href="#h_c94de6d619" id="h_c94de6d619"></a>

**Ao acessar as bases de dados especificadas nessa \_string**\_\*\* de conexão, você concorda que possui as licenças da Netsuite necessárias.\*\*

**IMPORTANTE:** esse _driver_ de banco de dados suporta somente a operação SELECT.

Sem informação de compatibilidade

**String de Conexão**

```
jdbc:ns://{Server Host}:{Server Port};ServerDataSource={Server Data Source};encrypted=1;Ciphersuites={Cipher Suite};CustomProperties=(AccountID={Account Id};RoleID={Role Id})
```

## Snowflake <a href="#h_abaa247811" id="h_abaa247811"></a>

Ao acessar as bases de dados especificadas nessa _string_ de conexão, você concorda que possui as licenças da Snowflake necessárias.

Nas versões:

* 3.51.x +

**Strings de Conexão**

* **Sintaxe**

```
jdbc:snowflake://<account_name>.snowflakecomputing.com/?<connection_params>
```

* **Exemplo**

```
jdbc:snowflake://wxyz.us-central1.gcp.snowflakecomputing.com/?db=snowflake_sample_data&sfSchema=TPCH_SF100
```

Clique [aqui](https://docs.snowflake.com/en/user-guide/jdbc-configure.html) para obter mais informações sobre a configuração de parâmetros da _string_ de conexão.

**IMPORTANTE:**

**1.** Está sendo utilizada a versão 3.10.3 do _driver_ JDBC devido a uma limitação nas suas versões mais atuais - não é possível trabalhar com micro serviço alocando memória de 64MB, configuração referente a um _pipeline small_ na Digibee Integration Platform. Para mais informações sobre o _change log_ desse _driver_, clique [aqui](https://docs.snowflake.com/en/release-notes/client-change-log-jdbc.html).

**2.** O Snowflake não suporta os campos CLOB ou BLOB. Com isso, a opção “Blob as File” não funcionará nos componentes DB e Stream DB. Clique [aqui](https://docs.snowflake.com/en/sql-reference/data-types-unsupported.html) e [aqui](https://docs.snowflake.com/en/user-guide/binary-input-output.html) para obter mais informações.

**3.** Quando o _batch mode_ é utilizado e ocorre um erro, o _driver_ do Snowflake não retorna a quantidade de transações com sucesso nem a quantidade de erros. Só é retornado o erro da primeira exceção SQL e o _rollback_ de toda a transação é feito mesmo quando a opção “rollbackOnError” não é selecionada.

**4.** O Snowflake não suporta os parâmetros OUT e INOUT, retornando o erro _SQLFeatureNotSupportedException_.

**5.** Quando o _batch mode_ é utilizado, os campos do tipo BINARY e VARBINARY não são suportados.
