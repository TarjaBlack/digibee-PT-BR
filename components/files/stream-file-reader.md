---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream File Reader

O **Stream File Reader** lê um arquivo local em um estrutura JSON, que atualmente suporta apenas CSV, e dispara _subpipelines_ para processar cada mensagem. Isso deve ser utilizado para arquivos grandes.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** nome do arquivo local.
* **Charset:** nome do código de caracteres para a leitura do arquivo (padrão UTF-8).
* **Element Identifier:** atributo que será enviado em caso de erros.
* **Paralell Execution Of Each Iteration:** ocorre em paralelo com a execução do _loop_.
* **Ignore Invalid Charset:** se a opção estiver ativada, o _charset_ inválido configurado no componente será ignorado juntamente com o arquivo recebido.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Advanced:** definição de parâmetros avançados.
* **Skip:** número de linhas a serem puladas antes da leitura do arquivo.
* **Limit:** número máximo de linhas a serem lidas.

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem no seguinte formato:

```
{
"filename": "fileName"
}
```

O **Local File Name** substitui o arquivo local padrão.

### Saída <a href="#sada" id="sada"></a>

```
{
"total": 0,
"success": 0,
"failed": 0
}
```

* **total:** número total de linhas processadas
* **success:** número total de linhas processadas com sucesso
* **failed:** número total de linhas cujo processamento falhou

{% hint style="warning" %}
**IMPORTANTE:** para saber se uma linha foi processada corretamente, deve haver o retorno { "success": true } para cada linha processada.
{% endhint %}

O componente joga uma exceção se o _**File Name**_ não existir ou não puder ser lido.

A manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

Este componente realiza processamento em lote. Para entender melhor o conceito, leia o artigo sobre [Processamento em lote](https://docs.digibee.com/documentation/v/pt-br/tutoriais-e-melhores-praticas/processamento-em-lote).&#x20;
