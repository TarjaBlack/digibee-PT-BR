---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON Generator

JSON Generator (Mock) cria um objeto JSON. Esse componente aceita qualquer _input_.

Dê uma olhada nos parâmetros de configuração do componente:

* **JSON**: o objeto JSON que será o output do componente. Expressões _Double Braces_ são suportadas.
* **Fail on Error:** se você ativar essa opção, a execução do _pipeline_ será interrompida caso um erro ocorra durante a execução deste componente. Se você desativá-la, quando um erro acontecer, o componente irá gerar uma mensagem de erro em formato JSON como saída, mas a execução do _pipeline_ continuará. O uso indevido dessa opção pode levar a falsas mensagens de sucesso nos passos subsequentes do seu _pipeline_.

### Exemplo de uso

Nesse exemplo, usamos o componente **JSON Generator (Mock)** para modificar os dados de uma pessoa. Aqui, queremos unir as propriedades `primeiroNome` e `sobrenome` em uma única propriedade chamada `nomeCompleto`. Também queremos deletar a propriedade `numeroTelefone` e adicionar uma propriedade chamada `pais`, que sempre assume o valor `“Brasil”`.

#### Entrada

```json
{
“primeiroNome” : “Carlos”,
“sobrenome” : “Silva”,
“numeroTelefone” : “+55(11)99999-8888”
}
```

#### Configurações dos parâmetros

Usamos o componente **JSON Generator (Mock)** com a seguinte configuração no parâmetro JSON:

```json
{
"nomeCompleto" : {{ CONCAT(message.primeiroNome," ", message.sobrenome) }},
"pais" : "Brasil"
}
```

Aqui, usamos a função [**Double Braces CONCAT**](../../build/funcoes-double-braces/funcoes-de-string.md) para concatenar o primeiro nome e o sobrenome, com um espaço entre eles.

#### Saída

```json
{
  "nomeCompleto": "Carlos Silva",
  "pais": "Brazil"
}
```
