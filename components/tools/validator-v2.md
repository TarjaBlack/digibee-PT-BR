---
description: Conheça o componente e saiba como utilizá-lo.
---

# Validator V2

O **Validator V2 (JSON Schema)** valida um conteúdo JSON com base em um JSON Schema.

JSON Schema é uma linguagem padrão de mercado usada para anotar e validar documentos JSON, que funciona como um “contrato” a ser seguido pelo componente. Para saber mais, visite a [documentação oficial do JSON Schema](https://json-schema.org/).

Dê uma olhada nos parâmetros de configuração do componente:

* **Schema Draft version:** versão do _Schema Draft_. Versões suportadas: v4, v6, v7, v2019-09 e v2020-12.
* **Detect Draft version:** se esta opção estiver ativada, a versão do _Schema Draft_ será baseada na versão inserida no parâmetro **JSON Schema**.
* **JSON Payload:** conteúdo JSON a ser validado. Esse campo aceita [expressões Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/double-braces).
* **JSON Schema:** JSON Schema que será usado como base para a validação do conteúdo JSON. Esse campo aceita [expressões Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/double-braces).
* **Simplify validation results:** se esta opção estiver ativada, os erros de validação serão exibidos de forma simplificada; caso contrário, serão exibidos de forma detalhada.
* **Fail on Error:** se a opção estiver ativada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".

## Fluxo de mensagens

### Saída

Se o **Validator V2** validar com sucesso o conteúdo JSON, terá como saída o JSON configurado no parâmetro **JSON Payload**.

Já em casos de erro, o componente terá como saída um conteúdo JSON com a seguinte estrutura por padrão:

```
{
    "success": false,
    "validation": [
        {
            "type": "type",
            "code": "1029",
            "path": "$.code",
            "schemaPath": "#/properties/code/type",
            "arguments": [
                "string",
                "integer"
            ],
            "details": null,
            "message": "$.code: string found, integer expected"
        },
        {
            "type": "required",
            "code": "1028",
            "path": "$",
            "schemaPath": "#/required",
            "arguments": [
                "field"
            ],
            "details": null,
            "message": "$.field: is missing but it is required"
        }
    ]
}

```

O array "validation" contém um objeto JSON para cada validação realizada. Cada objeto JSON tem as seguintes propriedades:

* **type:** o tipo de validação aplicada.
* **code:** código interno da validação.
* **path:** caminho no qual a propriedade validada está configurada no conteúdo JSON.
* **schemaPath:** caminho no qual a propriedade validada está configurada no JSON Schema.
* **arguments:** dados da propriedade analisada durante a validação.
* **details:** detalhes adicionais da validação.
* **message:** mensagem referente ao erro encontrado.

Se a opção **Simplify validation results** estiver ativada, o _array_ "validation" irá conter apenas mensagens de erro, como esta:\


```
{
    "success": false,
    "validation": [
        "$.code: string found, integer expected",
        "$.field: is missing but it is required"
    ]
}

```
