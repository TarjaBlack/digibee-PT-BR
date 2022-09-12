---
description: Conheça o componente e saiba como utilizá-lo.
---

# DB V1

O **DB V1** efetua operações de SELECT, INSERT, DELETE e UPDATE, retornando os valores para uma estrutura JSON.

{% hint style="info" %}
**IMPORTANTE:** cuidado com o consumo de memória para _datasets_ grandes. Se preferir, você pode utilizar o Stream DB. Para acessar o artigo sobre ele, clique [aqui](stream-db-v3.md).
{% endhint %}

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Database URL:** _string_ de conexão ao banco de dados no formato JBDC.
* **SQL Statement:** instrução SQL a ser executada.
* **Coalesce:** quando ativada, essa opção controla se os objetos de dados são fundidos em uma sequência ou se um erro é gerado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Custom Connection Properties:** propriedades de conexão específicas definidas pelo usuário.
* **Keep Connections:** se estiver ativada, a opção vai manter as conexões com a base de dados por no máximo 30 minutos; do contrário, será por apenas 5 minutos.
* **Advanced:** configurações avançadas.
* **Connection Test Query:** instrução SQL a ser utilizada antes que cada conexão seja estabelecida - esse parâmetro é opcional e deve ser aplicado a bancos de dados que não possuem informações confiáveis sobre o status da conexão.

**Exemplo**

```
{     
    "parameters": {         
        "field1": {         
            "a": "b"         
        }    
    }
}
```

* coalesce = true => field1 = "{\\"a\\": \\"b\\"}"
* coalesce = false => exception
* coalesce = true => field1 = "{\\"a\\": \\"b\\"}"
* coalesce = false => exception

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

**Entrada**

```
{    
    "parameters": {        
        "name": "value"            
        ...    
    }
}        
```

**Saída**

```
{    
    "data": [        
        {"column1":"data1", "column2":"data2", ... }    
    ],
    "rowCount": number_of_returned_rows,
    "updateCount": number_of_rows_updated
}
```

### Saída com erro <a href="#sada-com-erro" id="sada-com-erro"></a>

```
{    
    "code": error_code,    
    "error": error_message,    
    "cause": cause_of_the_error,    
    "sqlState": the_driver_specific_sql_state,    
    "vendorCode": the_driver_specific_error_code
}
```

Para conhecer funções e utilidades para bancos de dados, clique [aqui](../../tutoriais-e-melhores-praticas/funcoes-e-utilidades-para-banco-de-dados.md).
