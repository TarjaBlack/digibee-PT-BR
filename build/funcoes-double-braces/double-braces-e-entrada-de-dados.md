---
description: Conheça a nova maneira de passar informações para os componentes.
---

# Double Braces e Entrada de Dados

Atualmente, quando é necessário passar parâmetros de forma dinâmica para os componentes, você pode utilizar o _**Transformer**_ antes de cada _step_. Mas é com o recurso Double Braces que você tem acesso direto aos elementos do objeto JSON ou repassa o objeto inteiro.

### Acesso ao elemento do JSON <a href="#acesso-ao-elemento-do-json" id="acesso-ao-elemento-do-json"></a>

Veja o exemplo a seguir, que demonstra como ocorre a passagem do parâmetro “cep” em uma chamada padrão do REST.

Se você tem um { "cep": "" }, um novo objeto com “url” como base deve ser criado:

```
{ 
    "url" : { 
        "cep": "" 
    } 
}
```

Com isso, é necessário adicionar o _**Transformer**_:

![](<../../.gitbook/assets/01 (25).png>)

Além de utilizar o _**Transformer**_, você também precisa conhecer a sintaxe de cada componente, assim como “url.cep”, “body.cep” ou “parameters.cep”.

Ao utilizar _Double Braces_ quando o campo do formulário indica suporte a esse recurso, o que você precisa fazer é simplesmente inserir a descrição do elemento desejado para que os dados sejam passados adiante:

![](<../../.gitbook/assets/02 (10).png>)

Note que nesse caso não foi necessário utilizar o _**Transformer**_, o que diminui a quantidade de passos para a construção do seu _pipeline_.

Dê uma olhada nos exemplos de JSON abaixo, que mostram como acessar o elemento desejado com o novo recurso:

**JSON A**

```
{
    "cliente": {
        "endereco": {
            "cep": "04547-130"
        }
    }
}
```

_**Double Braces**_

```
https://viacep.com.br/ws/{{ message.cliente.endereco.cep }}/json/
```

**JSON B**

```
{
    "clientes": [
    {
        "nome": "João",
        "endereco": {
            "cep": "04547-130"
        }
    },
    {
        "nome": "Pedro",
        "endereco": {
            "cep": "04547-130"
        }
    }]
}
```

**\{{ Double Braces \}}**

```
https://viacep.com.br/ws/{{ message.clientes[0].endereco.cep }}/json/
```

### Acesso ao objeto JSON <a href="#acesso-ao-objeto-json" id="acesso-ao-objeto-json"></a>

Com este exemplo, você poderá entender a atual passagem do parâmetro “body” (objeto) em uma chamada padrão do REST.

Digamos que você tenha { "nome": "", "endereco": { "cep": ""} } e deva criar o novo objeto { "body" : { "nome": "", "endereco": { "cep": ""} } }. Para isso, você precisa adicionar o _**Transformer**_. Olha só:

![](<../../.gitbook/assets/03 (4).png>)

Agora veja como fica se você utilizar Double Braces quando o campo do formulário indicar o suporte a esse recurso. Tudo o que você precisa fazer é descrever o elemento desejado para que os dados sejam passados adiante:

![](<../../.gitbook/assets/04 (12).png>)

### Utilização de funções em elementos <a href="#utilizao-de-funes-em-elementos" id="utilizao-de-funes-em-elementos"></a>

Agora que você já conhece as vantagens da utilização de _Double Braces_, fique sabendo de outra dica: esse recurso pode ser combinado com a utilização de funções.

Acompanhe este exemplo simples:

```
{
    "cep": " 04547-130 "
}
```

Você pode aplicar uma função para remover os espaços:

```
https://viacep.com.br/ws/{{ TRIM(message.cep) }}/json/
```

Clique [aqui](./) para conhecer todas as nossas funções.

### Escopos do Double Braces <a href="#escopos-do-double-braces" id="escopos-do-double-braces"></a>

Até agora você viu o escopo principal de uso de _Double Braces_, que se aplica às mensagens e resolve expressões específicas. Conheça outros contextos nos quais expressões com _Double Braces_ podem ser utilizadas.

* **Account**

No escopo “account” é possível acessar o cofre de credenciais da Digibee por meio das expressões com _Double Braces_.

Os componentes acessam o cofre e obtêm, de forma segura, os valores informados para as credenciais durante fase de configuração. Muitos componentes já possuem uma lógica pré-programada que permite não só o acesso, mas também o uso das credenciais.

**Exemplos:**

O componente de banco de dados _**DB V2**_ sempre recebe credenciais do tipo "basic", acessando nome de usuário e senha utilizados para autenticar na instância de banco de dados.

Por outro lado, o componente _**REST V2**_ utiliza um conjunto credenciais para aplicação na chamada de API a ser executada. Se uma credencial do tipo "basic" é informada ao REST V2, então a chamada de API será feita com autenticação “basic”. Logo, usuário e senha são informados em um campo de cabeçalho (_header_) com o valor em base64.

No entanto, existem cenários em que a chamada de API requer a passagem personalizada de credenciais. Quando isso acontece, expressões _Double Braces_ com _account_ podem ser utilizadas. Veja como fica a estrutura:

```
{{ account.<account label key>.<campo> }}
```

No exemplo acima, \<account label key> é o local onde deve ser informada a chave para o _account label_ desejado e \<campo> é o local onde deve informado o campo da credencial que se deseja utilizar.

Hoje somente 2 conectores suportam esse tipo de expressão: _**REST V2**_ e _**Soap V2**_. Isso acontece porque o acesso ao cofre deve ser feito com segurança, evitando o vazamento de credenciais. Os componentes foram preparados para isso e restringem o acesso ao cofre de credenciais em apenas 2 propriedades configuráveis - “body” e "headers".

![](<../../.gitbook/assets/05 (6).png>)

No exemplo acima, o REST V2 adiciona 2 novos _accounts_ configuráveis, denominados “Custom Account #1” e “Custom Account #2”. Eles podem ser acessados através dos _account label keys_ "custom-1" e "custom-2". Dessa maneira, a expressão com _Double Braces_ para acessar o campo “username” dentro da credencial informada em “Custom 1” é:

```
{{ account.custom-1.username }}
```

Para evitar vazamentos, somente os campos "body" e "headers" dos componentes suportam acesso através de expressões com _Double Braces_ em _Account_. Se você utilizar essas expressões em outros campos, uma mensagem de erro será informada durante a execução do _pipeline_.

* **Metadata**

O escopo “metadata” permite acesso aos metadados do _pipeline_.

Estas são as informações de metadados do _pipeline_ atualmente suportadas:

**Informações sobre o **_**pipeline**_

\- **pipeline.name:** nome do _pipeline_

\- **pipeline.versionMajor:** _version major_

\- **pipeline.versionMinor:** _version minor_

\- **pipeline.realm:** nome do _Realm_

**- pipeline.description:** descrição do _pipeline_

\- **pipeline.id:** ID único do _pipeline_

**Informações sobre a configuração de execução**

**- runtime.consumers:** quantidade de consumidores de acordo com o tamanho do _pipeline_

**- runtime.actualConsumers:** quantidade de consumidores efetivamente configurados

**- runtime.environment:** nome do ambiente onde o _pipeline_ está em execução

**Informações sobre o ambiente de execução**

**- execution.key:** ID único para esta execução do _pipeline_

**- execution.timeout:** _timeout_ configurado para o _pipeline_

**- execution.startTimestamp:** tempo de início da execução do _pipeline_ (em milissegundos, no formato "UNIX Epoch")

**- execution.redelivery:** booleano que especifica se é a primeira execução ou uma nova tentativa (clique [aqui](../../plataforma/pipeline-engine.md) para acessar o artigo sobre _Pipeline Engine_ e entender melhor)

Utilize uma expressão com _Double Braces_ e _metadata_ para acessar informações necessárias. Veja este exemplo:

```
{{ metadata.pipeline.name }}
```

O nome do _pipeline_ será resolvido como uma _string_.

Para saber quais são as funções associadas aos _Double Braces_ e como utilizá-las, clique [aqui](./) para acessar o nosso outro artigo.
