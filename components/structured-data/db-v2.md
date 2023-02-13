---
description: Conheça o componente e saiba como utilizá-lo.
---

# DB V2

O **DB V2** efetua operações de SELECT, INSERT, DELETE e UPDATE e também faz chamadas em PROCEDURES, retornando os valores para uma estrutura JSON.

{% hint style="info" %}
**IMPORTANTE:** em casos onde um banco de dados Apache Hive é usado, os dados de _Updatecount_ podem estar indisponíveis devido a uma característica do sistema. Essa informação estará disponível apenas se o controle do _updated row count_ estiver habilitado no servidor Apache Hive. [Para mais informações sobre suporte Apache Hive para a Digibee Integration Platform, leia o artigo Banco de dados suportados.](https://docs.digibee.com/documentation/v/pt-br/plataforma/bancos-de-dados-suportados#apache-hive)
{% endhint %}

## Pool de conexão <a href="#h_f90a8ac5f6" id="h_f90a8ac5f6"></a>

Por padrão, utilizamos um _pool_ de tamanho baseado nas configurações do _pipeline_ implantado. Por exemplo, caso seja um _pipeline_ SMALL, então o tamanho do _pool_ será de 10. Para o MEDIUM o tamanho seria de 20 e para o LARGE seria de 40.

É possível gerenciar o tamanho do _pool_ na hora da implantação também. Para isso, é necessário habilitar a propriedade “Pool Size By Actual Consumers” no componente. Com isso, é utilizado o que for configurado manualmente na tela de implantação.

Veja na figura abaixo a configuração de um _pipeline_ SMALL com 5 _consumers_. Se você quiser que o _pool_ dos componentes de banco de dados (_**DB V2**_ e _**Stream DB V3**_) utilize esse tamanho, será preciso habilitar a propriedade “Pool Size By Actual Consumers” em todos os componentes existentes:

![](../../.gitbook/assets/dbv2-2.png)

{% hint style="info" %}
**IMPORTANTE:** atenção ao configurar o tamanho do _pool_ manualmente para que não ocorra nenhum _deadlock_ em chamadas concorrentes ao mesmo banco.
{% endhint %}

O nosso _pool_ é compartilhado entre os componentes de banco de dados que acessam o mesmo banco de dados dentro do _pipeline_. Caso seja necessário um _pool_ exclusivo para determinado componente, habilite a propriedade “Exclusive Pool”.

## DB V2 em Ação <a href="#db-v2-em-ao" id="db-v2-em-ao"></a>

### Batch mode <a href="#batch-mode" id="batch-mode"></a>

Quando for necessário realizar um processamento em lote de algumas instruções, você pode realizar chamadas em modo _batch_ nas _queries_.

\
**Exemplo**

Digamos que você precise informar no componente um _array_ de objetos, que serão utilizados nessa execução em _batch_:

**ITENS**

```
[   { 
    "name": "Mathews", "type":"A"
    }, { 
    "name": "Jules", "type":"A"
    }, { 
    "name": "Raphael", "type":"B"
    } 
]
```

E na instrução SQL, você deverá informá-lo da seguinte maneira:

**SQL**

INSERT INTO TABLE VALUES ( \{{ item.name \}}, \{{ item.type \}} )

Quando você utiliza expressões em _Double Braces_ \{{ item.name \}}, uma iteração é feita dentro do _array_ (informado em itens) e uma propriedade correspondente é buscada dentro do objeto. Nesse caso, a propriedade é "name".

Após a execução, 3 registros são inseridos. O retorno esperado é:

```
{ 
    "totalSucceeded":3, 
    "totalFailed":0 
}
```

Caso uma das execuções falhe, será retornado um objeto com a propriedade "error":

```
{ 
    "totalSucceeded":1, 
    "totalFailed":1 
}
```

Caso uma das execuções falhe, será retornado um objeto com a propriedade "errors":

```
{ 
    "totalSucceeded":1, 
    "totalFailed":1,
    "errors": ["erro1", "error2"]
}
```

{% hint style="info" %}
**IMPORTANTE:** os erros retornados na propriedade “errors” variam conforme o _driver_ do banco. Alguns _drivers_ não retornam todos os erros ocorridos durante a execução em modo _batch_.
{% endhint %}

### Rollback On Error <a href="#rollback-on-error" id="rollback-on-error"></a>

Se essa opção estiver ativada, os _commits_ das operações serão realizados apenas se todas elas forem bem sucedidas. Do contrário, será feito o _rollback_ de todas as operações _batch_.

Se a opção estiver inativa, então o _commit_ e as alterações bem sucedidas por _commit_ serão feitas __ mesmo que ocorra alguma falha entre as execuções.

**IMPORTANTE:** para alguns bancos de dados, principalmente para o Oracle, não é possível retornar o número consolidado execuções bem ou mal sucedidas. Caso algum erro ocorra, um objeto contendo todos os erros será retornado (dentro da propriedade "errors") e consolidado com o valor -1 também será retornado:

```
{ 
    "totalSucceeded":-1, 
    "totalFailed":-1,
    "errors": ["erro1", "error2"], 
    "success": false
}
```

Para outros bancos, como o Firebird, a ocorrência de erros não é informada. Portanto, um objeto sem nenhum erro pode ser retornado mesmo que tenha ocorrido uma falha:

```
{ 
    "totalSucceeded":0, 
    "totalFailed":3,
    "errors": ["erro1", "error2"], 
    "success": false
}
```

Para esses casos de erro no _Batch Mode_, não deixe de analisar a propriedade "success". Se ela retornar "false", significa que pelo menos um erro ocorreu durante a execução.

## DB V2 via Kerberos&#x20;

Veja na coleção a seguir como usar o DB V2 via Kerberos em diferentes cenários:

{% content-ref url="db-v2/db-v2-via-kerberos.md" %}
[db-v2-via-kerberos.md](db-v2/db-v2-via-kerberos.md)
{% endcontent-ref %}

### &#x20;<a href="#h_f90a8ac5f6" id="h_f90a8ac5f6"></a>
