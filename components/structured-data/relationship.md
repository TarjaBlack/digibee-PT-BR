---
description: Conheça o componente e saiba como utilizá-lo.
---

# Relationship

O **Relationship** cria relações entre 1 ou mais entidades para que sejam feitas buscas em bases diferentes.

{% hint style="info" %}
**IMPORTANTE: o componente não suporta acessos simultâneos enquanto está tentando atualizar ou salvar novas relações.**
{% endhint %}

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** operação a ser executada (MATCH, CREATE, UPDATE, GET BY FIELD AND VALUE, TRANSLATE e DELETE EXACT).
* **Relation Name:** nome dado à relação criada.
* **Translate Path:** caminho pelo qual o componente busca os IDs a serem traduzidos.
* **From:** origem da busca.
* **To:** destino da busca.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Operações <a href="#operaes" id="operaes"></a>

* **MATCH:** busca por uma equivalência entre 2 campos e o valor declarado.
* **CREATE:** cria uma relação através do campo.
* **UPDATE:** atualiza uma relação existente através do campo.
* **GET BY FIELD AND VALUE:** busca por uma relação entre o campo e o seu valor.
* **TRANSLATE:** traduz uma lista de IDs com base no caminho especificado em "Translate Path".
* **DELETE EXACT:** exclui a relação exata em todos os campos declarados.

{% hint style="info" %}
**IMPORTANTE:** é preciso declarar a _query_ dentro do objeto de relação:
{% endhint %}

```
{
    relation : {
            field1: value
            field2: value
    }
 }
```
