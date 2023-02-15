---
description: Conheça o componente e saiba como utilizá-lo.
---

# Template Transformer

O **Template Transformer** gera XML, HTML, texto e outros dados a partir de um _template_ especificado. O componente pode receber dados para preencher o _template_ dinamicamente a partir de um JSON recebido na sua mensagem de entrada.

Dê uma olhada nos parâmetros de configuração do componente:

* **Model Path:** caminho no qual o _input_ de JSON encontra os modelos a serem utilizados no _template (dotted notation_).
* **Preserve Original:** se ativada, a opção preserva os campos originais recebidos na entrada do componente.
* **Body:** o _template_ (_string_) a ser substituído e transformado durante o tempo de execução com os dados recebidos, via JSON, configurados na propriedade _**Model Path**_.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

Para entender melhor como utilizar o **Template Transformer**, [clique aqui para ler o nosso artigo com exemplos ilustrados.](https://docs.digibee.com/documentation/v/pt-br/components/tools/template-transformer/template-e-suas-utilizacoes)

### Exemplo de resposta de requisição ao Template Transformer contendo erro <a href="#exemplo-de-resposta-de-requisio-ao-template-transformer-contendo-erro" id="exemplo-de-resposta-de-requisio-ao-template-transformer-contendo-erro"></a>

```
{  
    "body": null,  
    "_error": "Can not construct instance of java.util.LinkedHashMap: no String-argument constructor/factory method to deserialize from String value ('')\n at [Source: N/A; line: -1, column: -1]",  
    "_body": ""
}
```

* **body:** _template_ transformado
* **\_error:** descrição do erro que ocorreu na execução
* **\_body:** se a opção _**Preserve Original**_** ** estiver habilitada, a propriedade será exibida na saída contendo o JSON de entrada

### Entrada <a href="#entrada" id="entrada"></a>

Esse componente aceita receber um objeto JSON na sua entrada, utilizando uma linguagem chamada Freemarker para fazer as transformações e gerar o _template_. Ele vai buscar o JSON a ser utilizado dentro da propriedade de configuração _**Model Path**_.

### Saída <a href="#sada" id="sada"></a>

A estrutura será igual a de entrada, porém com outro modelo e outra representação de _template_ como _string_. Em caso de erro, a propriedade "error" será criada no mesmo nível da propriedade original.

A notação com pontos (_dotted notation_) de JSON vai procurar pelo elemento raiz que está sendo processado pelo _pipeline_ e realizar um cruzamento de acordo com as especificações passados na propriedade _**Model Path**_.

## Template Transformer em Ação <a href="#template-transformer-em-ao" id="template-transformer-em-ao"></a>

Em uma representação do _Model Path_ contendo a.b.c.d, "a" será procurado no elemento raiz. Em seguida será o "b", depois o "c" e finalmente o "d". Se um _array_ for encontrado durante o cruzamento, então o algoritmo vai gerar um caminho de cruzamento para cada elemento no _array_. O algoritmo substitui todas as ocorrências do caminho definido em _**Model Path**_.

### **Sem erro**

```
{ 
    "body": "TEMPLATE TRANSFORMADO"
    "_body": {}
}
```

* **\_body:** se a opção _**Preserve Original**_** ** estiver habilitada, a propriedade será exibida na saída contendo o JSON de entrada

### **Com erro**

```
{  
    "body": null,  
    "_error": "Can not construct instance of java.util.LinkedHashMap: no String-argument constructor/factory method to deserialize from String value ('')\n at [Source: N/A; line: -1, column: -1]",  
    "_body": ""
}
```

## Tecnologia <a href="#tecnologia" id="tecnologia"></a>

Utilizamos o Freemarker para realizar nossas conversões e transformações no _template_ dentro desse componente. [Para conhecer mais sobre o Freemaker e como utilizá-lo, clique aqui.](https://freemarker.apache.org/docs/dgui\_template\_exp.html)
