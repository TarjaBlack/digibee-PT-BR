---
description: Conheça o componente e saiba como utilizá-lo.
---

# XML Transformer

O _**XML Transformer**_ transforma um objeto JSON em uma _string_ XML.

Dê uma olhada nos parâmetros de configuração do componente:

* **Output JSON Property:** define o nome do atributo do JSON de saída que receberá como valor o resultado da transformação para XML.
* **Generate Root Element On XML:** define o valor do elemento _root_ que será adicionado no XML gerado.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

É esperado que um objeto JSON seja transformado, desde que os parâmetros do componente sejam preenchidos corretamente.

### **Saída** <a href="#h_1154f08e69" id="h_1154f08e69"></a>

Uma _string_ XML que é o resultado da conversão do objeto JSON de entrada.

## XML Transformer em Ação <a href="#h_fd0d375710" id="h_fd0d375710"></a>

### Entrada <a href="#h_fbe63e5574" id="h_fbe63e5574"></a>

&#x20;Considerando as configurações:

* **Output JSON Property:** output
* **Generate Root Element On XML:** customers

Quando a seguinte mensagem é recebida:

```
{
    "customer": {
        "id":1,
        "name":"Paul"
    }
} 
```

### Saída <a href="#h_84cf6390e0" id="h_84cf6390e0"></a>

A seguinte estrutura de saída é gerada:

```
{
   "output": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><customers><customer><id>1</id><name>Paul</name></customer></customers>"
}
```
