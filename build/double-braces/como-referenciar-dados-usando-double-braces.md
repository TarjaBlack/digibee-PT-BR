---
description: Aprenda diferentes maneiras de usar Double Braces
---

# Como referenciar dados usando Double Braces

Você pode usar Double Braces de várias maneiras: para acessar os dados recebidos pelo componente no formato JSON, para fazer referência a Globals, contas ou metadados.

Veja como você pode fazer isso:

## Como referenciar dados JSON <a href="#_87tlux10inbm" id="_87tlux10inbm"></a>

Suponha que um componente receba os seguintes dados JSON sobre um funcionário chamado João Silva:

```json
{
"primeiroNome": "João",
"sobrenome": "Silva",
"endereco": {
"rua": "Rua 123",
"cidade": "São Paulo",
"estado": "SP",
"CEP": "11111-111"
},
"telefone": "+5511999999999",
"email": "joaosilva@email.com",
"idade": 30,
"genero": "masculino",
"ocupacao": "Engenheiro de Software"
}
```

### Referenciando todos os dados <a href="#_lx0q7rponynp" id="_lx0q7rponynp"></a>

Para fazer referência a todos os dados JSON recebidos pelo componente, use a seguinte sintaxe:

```
{{ message.$ }}
```

Aqui:

* **message** é uma palavra reservada que se refere aos dados que foram recebidos pelo componente em questão, conhecido como _payload_.
* **$** indica que você está se referindo a todo o _payload_.

### Fazendo referência a propriedades específicas <a href="#_266jiko3l5ec" id="_266jiko3l5ec"></a>

Use a seguinte sintaxe para fazer referência a propriedades específicas de um JSON, substituindo os termos entre símbolos de menor e maior que pelo valor desejado:

```
{{ message.<nome-da-propriedade> }}
```

Aqui:

* **message** é uma palavra reservada que se refere aos dados que foram recebidos pelo componente em questão, também chamado de _payload_.
* **nome-da-propriedade** refere-se ao nome da propriedade desejada.

Por exemplo, se você quiser referenciar o endereço de e-mail de João Silva, use a seguinte notação:

```
{{ message.email }}
```

Para acessar propriedades contidas em outras propriedades, use a notação de maneira recursiva. Por exemplo, para referenciar o CEP de João Silva, use a seguinte notação:

```
{{ message.endereco.CEP }}
```

## Referenciando Globals <a href="#_w40qqx1i9zyi" id="_w40qqx1i9zyi"></a>

Globals são variáveis ​​criadas pelo usuário que podem ser referenciadas em vários pipelines. Para aprender mais sobre Globals, [leia esta documentação](../../configurations/conceitos-basicos.md).

Para fazer referência a um Global usando Double Braces, use a seguinte sintaxe, substituindo os termos entre símbolos de menor e maior que pelo valor desejado:

```
{{ global.<nome-do-global> }}
```

Aqui:

* **global** é uma palavra reservada.
* **nome-do-global** é o nome do Global desejado.

Suponha que você queira referenciar um Global chamado “meu-global”. Use a notação:

```
{{ global.meu-global }}
```

## Referenciando contas <a href="#_6kg4o5xryfbp" id="_6kg4o5xryfbp"></a>

As contas são credenciais definidas pelo usuário que podem ser referenciadas em vários pipelines.Para saber mais, [leia nossa documentação sobre contas](../../configurations/contas-accounts/).

Para fazer referência a uma conta, use a seguinte sintaxe, substituindo os termos entre símbolos de menor e maior que pelo valor desejado:

```
{{ account.<rotulo-da-conta>.<campo> }}
```

Aqui:

* **account** é uma palavra reservada que se refere às contas salvas na Digibee Integration Platform.
* **rotulo-da-conta** refere-se ao rótulo da conta exibido na página de contas.
* **campo** refere-se ao nome do campo da conta na página de contas, como, por exemplo, **username**,**password**, **token**, **header-value**, entre outros.

Suponha que você queira fazer referência ao _username_ de uma conta salva chamada **conta-da-emily**. Para fazer isso, use a seguinte sintaxe:

```
{{ conta.conta-da-emily.username }}
```

## Referenciando metadados <a href="#_ddcmojcg6oul" id="_ddcmojcg6oul"></a>

Metadados podem se referir a vários tipos de dados, tais como informações sobre o próprio pipeline, a execução atual do pipeline, a configuração usada para executar o pipeline e o ambiente no qual o pipeline está sendo executado.

Para referenciar metadados, use a seguinte sintaxe, substituindo os termos entre símbolos de menor e maior que pelo valor desejado:

```
{{ metadata.<dados> }}
```

Aqui:

* **metadata** é uma palavra reservada.
* **dados** refere-se aos metadados que você deseja referenciar.

Por exemplo, use a seguinte sintaxe para referenciar o nome do pipeline no qual este código está sendo executado:

```
{{ metadata.pipeline.name }}
```

Estes são todos os metadados que você pode acessar com Double Braces:

### Metadados de pipeline <a href="#_bnmd222uaqa0" id="_bnmd222uaqa0"></a>

| data                  | Descrição                  |
| --------------------- | -------------------------- |
| pipeline.name         | Nome do pipeline           |
| pipeline.versionMajor | Versão _major_ do pipeline |
| pipeline.versionMinor | Versão _minor_ do pipeline |
| pipeline.realm        | _Realm_ do pipeline        |
| pipeline.description  | Descrição do pipeline      |
| pipeline.id           | ID do pipeline             |

### Metadados de implantação <a href="#_7cp8uzvvzlmg" id="_7cp8uzvvzlmg"></a>

| Descrição                                                                             | data                      |
| ------------------------------------------------------------------------------------- | ------------------------- |
| Quantidade máxima de consumidores, de acordo com o tamanho da implantação do pipeline | runtime.consumers         |
| Quantidade de consumidores, como definido pelo usuário                                | runtime.actualConsumers   |
| Ambiente em que o pipeline está sendo executado                                       | runtime.actualEnvironment |

### Metadados de execução de pipeline <a href="#_wyxvj3wtt377" id="_wyxvj3wtt377"></a>

| data                     | Descrição                                                                                                                                                                                                   |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| execution.key            | ID da execução do pipeline atual                                                                                                                                                                            |
| execution.timeout        | _Timeout_ configurado do pipeline                                                                                                                                                                           |
| execution.startTimestamp | _Timestamp_ do início da execução pipeline (em milissegundos, no formato UNIX Epoch)                                                                                                                        |
| execution.redelivery     | Booleano. _True_ se esta execução for uma nova tentativa de execução. _False,_ se não. Aprenda mais sobre reprocessamento em [nosso artigo sobre o _Pipeline Engine_](../../plataforma/pipeline-engine.md). |
