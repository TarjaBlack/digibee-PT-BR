---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON Generator

O **JSON Generator** gera um JSON com um formato específico. Em outras palavras, ele funciona como um _template_ para montar um objeto JSON para que você possa fazer referência a variáveis através do uso de _Double Braces_.

Dê uma olhada nos parâmetros de configuração do componente:

* **JSON:** especificação do JSON a ser gerado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

```
{  
    "abc": {    
        "teste": "algumValor"  
    }
}
```

Você pode usar a seguinte configuração no componente:

```
{  
    "propriedade": {{ message.abc.teste }}
}
```

#### Saída <a href="#sada" id="sada"></a>

```
{  
    "propriedade": "algumValor"
}
```

\
Para saber mais sobre funções, clique [aqui](../../build/funcoes-double-braces/).
