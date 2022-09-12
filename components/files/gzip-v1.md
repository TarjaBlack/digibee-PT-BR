---
description: Conheça o componente e saiba como utilizá-lo.
---

# Gzip V1

O **Gzip V1** zipa um objeto JSON inteiro como uma _string_.\


Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** "compress" comprime e "decompress" descomprime.
* **JSON Field:** caminho do JSON a ser zipado.
* **Preserve Original:** se ativada, a opção preserva campos originais que possuem prefixo com _underline_.
* **Binary Content:** se ativada, a opção faz com que o dado seja tratado como binário e uma _string_ base64 será esperada.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Suporta qualquer estrutura, desde que o elemento a ser comprimido seja especificado.

### Saída <a href="#sada" id="sada"></a>

Preserva a mensagem de entrada, com o objeto JSON comprimido no formato base64.

**Exemplo:**

Os passos dentro do componente _**Retry**_ serão executados 3 vezes até que sejam bem sucedidos - "true" deve aparecer na mensagem:

```
"start": [
{
"type": "connector",
"name": "gzip-connector",
"stepName": "test-compress",
"params": {
"operation" : "compress",
"failOnError": false,
"jsonField": "body.test",
"preserveOriginal" : false,
"isBinary" : false
}
}
]
```
