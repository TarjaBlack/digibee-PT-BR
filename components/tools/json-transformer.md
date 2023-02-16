---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON Transformer

O _**JSON Transformer**_ possibilita a aplicação de transformações no JSON que está sendo processado dentro do seu _pipeline_.

Você pode realizar uma série de ações utilizando um formulário de configurações.

Dê uma olhada nos parâmetros de configuração do componente:

* **Actions:** adiciona ou remove diferentes ações.
* **Description:** este campo é usado para documentar a ação.
* **Type:** define a ação que será executada, como: _Rename property, Edit property, Remove property e Remove property with Condition_. Veja abaixo mais detalhes sobre cada ação.
* **Rename Property:** renomeia a chave JSON para uma nova chave que pode ser composta por um valor estático ou dinâmico composto por _Double Braces_.
* **Edit Property:** permite a transformação de valores em uma propriedade por meio de _Double Braces_.
* **Remove Property:** remove propriedades em qualquer estrutura do JSON.&#x20;
* **Remove Property With Condition:** usando os operadores lógicos das funções, você pode definir uma condição para que "_true_" seja retornado, indicando quando a propriedade deve ser removida.&#x20;
* **Action Settings:** configurações adicionais relacionadas à ação selecionada.
* **Root path:** deve ser preenchido quando a propriedade JSON estiver na raiz do objeto. Quando esta opção é ativada, **Path (Dot Notation)** não estará disponível.
* **Path (Dot notation):** deve ser preenchido quando a propriedade JSON não estiver na raiz do objeto. Esse campo permite indicar _dot notation_, o que torna mais simples o acesso a diferentes níveis do JSON, incluindo atravessar _array_ e _object_ do JSON.
* **Properties to be renamed**: este parâmetro é mostrado apenas quando a ação **Rename property** estiver selecionada. Deve ser preenchida com a chave e valor que você deseja renomear.
* **Values to be edited:** este parâmetro é mostrado apenas quando a ação **Edit property** is selected. estiver selecionada. Deve ser preenchida com a chave e valor que você deseja editar.
* **Properties to be removed:** este parâmetro é mostrado apenas quando as ações **Remove property** ou **Remove property with Condition** estiverem selecionadas. Deve ser preenchida com o nome chave exato do JSON (no caso de **Remove property**) ou chave e valor (no caso de **Remove property with Condition**) que você deseja remover.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade _"success"._

Ao utilizar _Double Braces,_ os valores das propriedades que serão transformadas deverão ser acessados utilizando a palavra "item". Com a palavra "item" é possível obter valores de todas as propriedades contidas no mesmo nível do JSON que está sendo acessado.

**Exemplos:**

```
{{ item.keyName }} 
```

```
{{ CONCAT(item.customer.id, item.customer.name) }} 
```

```
{{ FORMATDATE( item.orders.dateAdded, "dd-MM-yyyy", "dd MMM yyyy") }}
```

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

## Entrada <a href="#entrada" id="entrada"></a>

Esse componente não espera nenhuma mensagem de entrada específica, somente se for informada uma expressão em _Double Braces_ em algum dos seus campos.

### Saída <a href="#sada" id="sada"></a>

Por se tratar de um componente que transforma o JSON de entrada, a saída é resultado das configurações definidas por você.

Se nenhuma propriedade definida nas configurações do componente for encontrada no JSON, o resultado será exatamente o mesmo JSON da entrada.

Para entender melhor o fluxo das mensagens na Digibee Integration Platform, consulte o artigo [Processamento de mensagens](https://docs.digibee.com/documentation/v/pt-br/build/pipelines/processamento-de-mensagens).

## JSON Transformer em Ação <a href="#json-transformer-em-ao" id="json-transformer-em-ao"></a>

Veja abaixo como o componente se comporta em determinadas situações e as suas respectivas configurações.

### **Renomeando propriedades**

As propriedades podem ser renomeadas utilizando valores estáticos ou dinâmicos composto por _Double Braces_. Essas propriedades podem estar em um _object_, _array_ ou na raiz.

Neste exemplo, veja como renomear "a" para "id" e "b" para "name". As configurações do componente deverão ser:

#### **Entrada**

```
{
   "products": [
           {
            "a": 1,
            "b": "Table"
           },
           {
            "a": 2,
            "b": "Chair"
           }
   ]
}
```

#### **Configurações**

![](../../.gitbook/assets/json-transformer.png)

#### **Saída**

```
{
   "products": [
           {
            "id": 1,
            "name": "Table"
           },
           {
            "id": 2,
            "name": "Chair"
           }
   ]
}
```

### **Editando propriedades**

Os valores podem ser transformados aplicando o _Double Braces_ e funções contidas na Digibee Integration Platform. Essa propriedade pode estar em um _object_, _array_ ou na raiz.

É possível aplicar as funções como _FORMATDATE, CONCAT, REPLACE, FORMATNUMBER_, dentre outras.

Para entender melhor como funcionam esses recursos, leia o artigo [Funções Double Braces](../../build/funcoes-double-braces/).

Neste exemplo, veja como transformar o "id" de _Number_ para _String_. As configurações do componente deverão ser:

#### **Entrada**

```
{
   "products": [
           {
            "id": 1,
            "name": "Table"
           },
           {
            "id": 2,
            "name": "Chair"
           }
   ]
}
```

#### **Configurações**

![](../../.gitbook/assets/json-transformer1.png)

#### **Saída**

```
{
   "products": [
           {
            "id": "1",
            "name": "Table"
           },
           {
            "id": "2",
            "name": "Chair"
           }
   ]
}
```

### **Removendo propriedades com condições de decisão**

As propriedades podem ser removidas utilizando os operadores lógicos das funções _Double Braces_. É possível definir uma condição que, quando for resolvida para _**true**_, indicará que a propriedade deverá ser removida. Essas propriedades podem estar em um _object_, _array_ ou na raiz.

Neste exemplo, veja como remover "description" com valor _null_. As configurações do componente deverão ser:

#### **Entrada**

```
{
   "products": [
           {
            "id": 1,
            "name": "Table",
            "description": "Tea Table",    
},
           {
            "id": 2,
            "name": "Chair",
            "description": null
           }
   ]
}
```

#### **Configurações**

![](../../.gitbook/assets/json-transformer2.png)

#### **Saída**

```
{
   "products": [
           {
            "id": 1,
            "name": "Table",
            "description": "Tea Table",      
},
           {
            "id": 2,
            "name": "Chair"
           }
   ]
}
```

### **Removendo propriedades apenas pelo nome**

As propriedades podem ser removidas apenas declarando seus nomes no campo **Properties to be removed.** Essas propriedades podem estar em um _object_, _array_ ou na raiz.

### **Informações adicionais**

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o o artigo [Como referenciar dados usando Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/como-referenciar-dados-usando-double-braces).
