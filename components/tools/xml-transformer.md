---
description: Conheça o componente e saiba como utilizá-lo.
---

# XML Transformer

O _**XML Transformer**_ realiza transformações de uma estrutura no formato JSON para a sua representação na estrutura XML.

Dê uma olhada nos parâmetros de configuração do componente:

* **Output JSON Property:** define o nome do atributo do JSON de saída que receberá como valor o resultado da transformação para XML.
* **Generate Root Element On XML:** define o valor do elemento _root_ que será adicionado no XML gerado.

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

É esperado um objeto na estrutura JSON para ser transformado e o devido preenchimento dos parâmetros do componente.

#### **Saída** <a href="#h_1154f08e69" id="h_1154f08e69"></a>

Ao executar o componente será gerado um JSON contendo a propriedade definida no parâmetro _**Output JSON Property**_ e seu valor será o resultado da transformação da estrutura JSON de entrada para a representação na estrutura XML.

### XML Transformer em Ação <a href="#h_fd0d375710" id="h_fd0d375710"></a>

#### Entrada <a href="#h_fbe63e5574" id="h_fbe63e5574"></a>

**Parâmetros**

**Output JSON Property:** output

**Generate Root Element On XML:** customers

**JSON**

```
{
    "customer": {
        "id":1,
        "name":"Paul"
    }
} 
```

#### Saída <a href="#h_84cf6390e0" id="h_84cf6390e0"></a>

```
{
   "output": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><customers><customer><id>1</id><name>Paul</name></customer></customers>"
}
```
