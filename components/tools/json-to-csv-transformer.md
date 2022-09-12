---
description: Conheça o componente e saiba como utilizá-lo.
---

# JSON to CSV Transformer

O **JSON to CSV Transformer** tem a função de receber um objeto em JSON e, a partir dele, gerar um _array_ contendo os dados para o CSV já formatado.

Dê uma olhada nos parâmetros de configuração do componente:

* **Headers:** configura os _headers_ que o componente utilizará para o processamento do texto. Os itens são separados por vírgula e podem conter mais de uma entrada. É um parâmetro obrigatório e deve ser configurado de acordo com o que você deseja processar.
* **Delimiter:** símbolo delimitador a ser utilizado no processamento do texto. Por padrão, essa opção vem configurada como uma vírgula (","). É um parâmetro obrigatório, podendo utilizar diversos símbolos como separador.
* **Print Headers:** se estiver ativada, a opção insere no resultado os _headers_ previamente configurados como sendo o primeiro elemento do _array_ resultante.
* **Coalesce:** se estiver ativada, e um valor da mensagem de entrada for correspondente à algum objeto/_array_, a entrada será processada e a execução acontecerá normalmente; do contrário, ao receber um valor como objeto/_array_, um erro será apresentado como resultado e será atribuído “false” para a propriedade “success”.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

O componente espera uma mensagem com a propriedade "data" no JSON. O valor dessa propriedade pode ser um _array_ ou um objeto. Veja a seguir um exemplo simples que demonstra a funcionalidade do _**JSON to CSV Transformer**_:

### Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

Você precisa configurar um JSON de entrada em um _pipeline_ com o componente **JSON to CSV Transformer.** Após adicioná-lo ao _pipeline_, é preciso configurar os _headers_ como **product,price** ou o exemplo não vai funcionar.

```
{
   "data": [
       {
           "product": "Samsung 4k Q60T 55",
           "price": 3278.99
       },
       {
           "product": "Samsung galaxy S20 128GB",
           "price": 3698.99
       }
   ]
}
```

#### Saída <a href="#sada" id="sada"></a>

Com as configurações feitas conforme as especificações acima, o resultado será:

```
{
   "data": [
       "Samsung 4k Q60T 55,3278.99",
       "Samsung galaxy S20 128GB,3698.99"
   ]
}
```

### JSON to CSV Transformer em Ação <a href="#json-to-csv-transformer-em-ao" id="json-to-csv-transformer-em-ao"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

#### Informando um valor sendo objeto com a configuração "Coalesce: false" e "Fail On Error: false" <a href="#informando-um-valor-sendo-objeto-com-a-configurao-coalesce-false-e-fail-on-error-false" id="informando-um-valor-sendo-objeto-com-a-configurao-coalesce-false-e-fail-on-error-false"></a>

Com as configurações indicadas, o JSON não será processado e o resultado será uma mensagem de erro e com a propriedade **success: false**

**Entrada**

```
{
   "data": [
       {
           "product": {
               "name": "Samsung 4k Q60T 55"
           },
           "price": 3278.99
       },
       {
           "product": {
               "name": "Samsung galaxy S20 128GB"
           },
           "price": 3698.99
       }
   ]
}
```

**Saída**

```
{   
    "success": false,   
    "message": "Property product is an object"
}
```

#### Informando um valor sendo objeto com a configuração "Coalesce: true" e "Fail On Error: false" <a href="#informando-um-valor-sendo-objeto-com-a-configurao-coalesce-true-e-fail-on-error-false" id="informando-um-valor-sendo-objeto-com-a-configurao-coalesce-true-e-fail-on-error-false"></a>

Com as configurações indicadas, o JSON será processado e o resultado será um csv com o objeto tratado corretamente.

**Entrada**

```
{
   "data": [
       {
           "product": {
               "name": "Samsung 4k Q60T 55"
           },
           "price": 3278.99
       },
       {
           "product": {
               "name": "Samsung galaxy S20 128GB"
           },
           "price": 3698.99
       }
   ]
}
```

**Saída**

```
{
   "data": [
       "product,price",
       "\"{\"\"name\"\":\"\"Samsung 4k Q60T 55\"\"}\",3278.99",
       "\"{\"\"name\"\":\"\"Samsung galaxy S20 128GB\"\"}\",3698.99"
  ]
}
```

#### Informando um valor sendo objeto com a configuração "Coalesce: false" e "Fail On Error: true" <a href="#informando-um-valor-sendo-objeto-com-a-configurao-coalesce-false-e-fail-on-error-true" id="informando-um-valor-sendo-objeto-com-a-configurao-coalesce-false-e-fail-on-error-true"></a>

Com as configurações indicadas, o JSON não será processado e a execução será interrompida imediatamente.

**Entrada**

```
{
   "data": [
       {
           "product": {
               "name": "Samsung 4k Q60T 55"
           },
           "price": 3278.99
       },
       {
           "product": {
               "name": "Samsung galaxy S20 128GB"
          },
           "price": 3698.99
       }
   ]
}
```

**Saída**

```
{
   "timestamp": 1603812645143,
   "error": "Property product is an object",
   "exception": "com.digibee.pipelineengine.exception.PipelineEngineRuntimeException",
   "code": 500
}
```

\
