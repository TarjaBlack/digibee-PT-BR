---
description: Conheça o componente e saiba como utilizá-lo.
---

# Stream Excel



O _**Stream Excel**_ lê um arquivo local de Excel linha por linha em uma estrutura JSON e dispara _subpipelines_ para processar cada linha. Esse recurso costuma ser indicado em situações nas quais há a necessidade de processamento de arquivos grandes.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** determina o nome do arquivo local que será lido.
* **Sheet Name:** nome da planilha de Excel a ser lida.
* **Sheet Index:** _index_ da planilha de Excel a ser lida.
* **Use Sheet Index Instead Of Name:** se ativada, a opção permite que o index da planilha seja informado no lugar do nome.
* **Max Fractional Digits:** determina o número preciso de dígitos fracionários em uma célula numérica no momento da leitura do arquivo Excel (padrão = 10).
* **Read Specific Columns As String:** indica quais colunas o componente deve ler em forma de _string_ ao invés do seu formato original. Cada coluna desejada deve ser informada separadamente por uma vírgula (ex.: A,B,X,AA).
* **Read All Columns As String:** se selecionada, a opção fará com que todas as colunas sejam lidas como _string_.
* **Parallel Execution Of Each Iteration:** se selecionada, a opção fará com que o componente realize a leitura de linhas do arquivo em paralelo.
* **Fail On Error:** a habilitação desse parâmetro suspende a execução do _pipeline_ apenas quando há uma ocorrência grave na estrutura da iteração, impedindo a sua conclusão por completo. A ativação do parâmetro "Fail On Error" não tem ligação com erros ocorridos nos componentes utilizados para a construção dos _subpipelines_ (onProcess e onException).
* **Advanced:** quando selecionada, a opção solicita a definição de parâmetros avançados.
* **Skip:** número de linhas a serem puladas antes da leitura do arquivo.
* **Limit:** número máximo de linhas a serem lidas.

O _**Stream Excel**_ realiza processamento em lote. Para entender melhor o conceito, clique [aqui](../../tutoriais-e-melhores-praticas/processamento-em-lote.md).

{% hint style="info" %}
**IMPORTANTE:** o _**Stream Excel**_ não é capaz de ler arquivos no formato .xls, mas apenas no formato .xlsx.
{% endhint %}

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada, podendo utilizá-la por meio de _Double Braces_.

### Saída <a href="#sada" id="sada"></a>

O componente retorna um JSON contendo o total de execuções, total de sucesso e total de falhas.

* **sem erro**

```
{
    "total": 5,
    "success": 5,
    "failed": 0
}
```

* **com erro**

```
{
    "total": 5,
    "success": 3,
    "failed": 2
}
```

* **Total:** número total de linhas processadas
* **Success:** número total de linhas processadas com sucesso
* **Failed:** número total de linhas cujo processamento falhou

{% hint style="info" %}
**IMPORTANTE:** para saber se uma linha foi processada corretamente, deve haver o retorno { "success": true } para cada linha processada.
{% endhint %}

O componente joga uma exceção se o arquivo não existir ou não puder ser lido. Do contrário, uma mensagem é produzida na saída com a exceção ocorrida.

Você também pode encontrar um erro ao fazer o upload de um arquivo .xlsx no Google Drive e, em um _pipeline_, usar o componente _**Google Drive**_ para fazer o download e o componente _**Stream Excel**_ para ler este arquivo.

Quando você faz essa ação, um comportamento inesperado do Google Sheets altera o arquivo .xlsx. Isso faz com que o _**Stream Excel**_ leia todas as linhas da planilha (incluindo aquelas em branco) ao invés de ler apenas as linhas com conteúdo. Este comportamento não está relacionado com a Digibee Integration Platform.

Como solução alternativa, você pode copiar o conteúdo da planilha e colar em uma nova guia no mesmo arquivo .xlsx. Se você fizer esse procedimento, não copie as linhas em branco ou o mesmo erro irá ocorrer.

A manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Todos os arquivos podem ser acessados apenas por um diretório temporário, no qual cada _pipeline key_ dá acesso ao seu próprio conjunto de arquivos.

## Stream Excel em Ação

Abaixo será demonstrado como o componente se comporta em determinada situação e a sua respectiva configuração.

### Ler arquivo de Excel e analisar resultado

Para esse exemplo, vamos considerar que já possuímos um arquivo Excel no fluxo do _pipeline_ que foi baixado através de componentes como: [_**Google Drive**_](https://docs.digibee.com/documentation/v/pt-br/components/file-storage/google-drive), [_**OneDrive**_](https://docs.digibee.com/documentation/v/pt-br/components/file-storage/onedrive) e assim por diante. O arquivo em questão possui uma planilha com os nomes dos 100 bilionários selecionados pela Forbes.

O componente _**Stream Excel**_ será configurado da seguinte forma:

* **Step Name:** Stream Excel
* **File Name:** file.xlsx
* **Sheet Name:** Plan1
* **Max Fractional Digits:** 5
* **Read Specific Columns As String:** B,D,F
* **Column Identifier:** A

Todas as demais opções ficarão desabilitadas para esse exemplo.&#x20;

<figure><img src="https://lh4.googleusercontent.com/-pvA8z_G3T8rofRlazUGDrfundDYQCHBgD-rVX__a61rRz6kQ6T291S4kYbtnkzTPu-ZrlKt-q5EE62XuMlO-x-oZtekm1kYKC5iDUCek0dMIBMsfCyOThcLHSy-RhW7QnTzpHB-xFQWcSxsAa8xgOg" alt=""><figcaption></figcaption></figure>

#### **Entrada**

```
{
"fileName": "sheets.xlsx"
}
```

#### **Saída**

```
{
"total": 102,
"success": 0,
"failed": 102
}
```

#### **Resultado do log**

Para visualizar esse _log_, será utilizada a aba de **Mensagens** do _pipeline_. Conforme demonstrado na imagem abaixo, todas as linhas da planilha foram lidas individualmente pelo componente, incluindo até o nome das colunas.

<figure><img src="https://lh4.googleusercontent.com/5Y91LjptJR4okSCt_P2b6R7mdULdExZCwUW2kyXJwBipJZFwKa7qbWzje-c0Zw-J5lLEYPWfjj6UCg46u-DaTEUUUPC2l4u1BK6GJ2f9bCPKx8PPIFObYyptQq703gApRtIcBRxvveVhg1LP3qVChpE" alt=""><figcaption></figcaption></figure>

### Ler arquivo de Excel e analisar uma planilha inexistente no arquivo

Para esse exemplo, considere a mesma planilha analisada anteriormente. No entanto, será selecionada uma planilha que não existe.

O componente _**Stream Excel**_ irá retornar a seguinte mensagem de erro (**Fail On Error** está desativado):

```
{
"success": false,
"message": "Sheet 'InvalidSheetName' does not exist",
"exception": "com.monitorjbl.xlsx.exceptions.MissingSheetException"
}
```

### **Ler arquivo de Excel inválido**

Para esse exemplo, considere um arquivo inexistente no fluxo do _pipeline_.

O componente _**Stream Excel**_ irá retornar a seguinte mensagem de erro (**Fail On Error** está desativado):

```
{
"success": false,
"message": "File invalidsheets.xlsx does not exist.",
"exception": "com.digibee.pipelineengine.exception.PipelineEngineRuntimeException"
}
```
