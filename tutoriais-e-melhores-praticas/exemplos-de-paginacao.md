---
description: Exemplo de paginação com banco de dados - Oracle, SqlServer
---

# Exemplos de paginação



Neste documento, segue alguns exemplos de query para implementar consultas paginadas no pipeline.

**Exemplo de entrada:**

```
{
    "page" : 1,
    "pageSize" : 50
}
```

## **Oracle** <a href="#h_83a431a13f" id="h_83a431a13f"></a>

```sql
SELECT COL_A, COL_B
  FROM (SELECT COL_A,
               COL_B,
               row_number() over (order by COL_A) rn
          FROM XPTO.MY_TABLE )

WHERE rn BETWEEN {{ TOLONG(SUM(SUBTRACT(MULTIPLY(message.page, message.pageSize), message.pageSize), 1)) }}


AND {{ TOLONG(MULTIPLY(message.page, message.pageSize)) }}
```

## **SQL Server** <a href="#h_7be7d57144" id="h_7be7d57144"></a>

```sql
SELECT col_a, col_b FROM myTabel 
ORDER BY col_a  
OFFSET {{ TOLONG(SUM(SUBTRACT(MULTIPLY(message.page, message.pageSize), message.pageSize), 1)) }} ROWS

FETCH NEXT {{ message.pageSize}} ROWS ONLY 
```

## **Spark** <a href="#h_288d411002" id="h_288d411002"></a>

****

```sparql
WITH CTEResults AS

( 

 SELECT *, ROW_NUMBER() OVER (ORDER BY query.col_1) AS RowNum FROM(

  select distinct

  col_1,

  col_2,

  col_3

  from mytable

 where << YOUR FILTERS HERE>>

 order by col_1) query

)

SELECT * FROM CTEResults

where RowNum > {{ TOLONG(SUBTRACT(MULTIPLY(message.page, message.pageSize), message.pageSize)) }}

 and RowNum <= {{ TOLONG(MULTIPLY(message.page, message.pageSize)) }}Sp
```
