---
description: Conheça o componente e saiba como utilizá-lo.
---

# CSV to Excel

O **CSV to Excel** converte arquivos em formato CSV em arquivos XLSX. Você pode gerar apenas um arquivo de Excel por execução.

Dê uma olhada nos parâmetros de configuração do componente:

<figure><img src="../../.gitbook/assets/CSV to Excel.gif" alt=""><figcaption></figcaption></figure>

* **Multiple Sheets:** se “_true_”, múltiplos arquivos CSV vão resultar em múltiplas planilhas; do contrário, apenas um arquivo Excel vai ser criado.
* **Sheet Information:** ao clicar em _**Add**_, você ativa os parâmetros _**CSV File Name**_, _**Sheet Name Destination**_ e _**CSV Delimiter**_. Com esses parâmetros, você pode importar os dados de vários arquivos CSV para as abas um arquivo Excel (isso somente é possível se o arquivo Excel conter diferentes abas).
  * CSV File Name: nome do arquivo CSV a ser importado.
  * Sheet Name Destination: nome da aba que deve receber os dados do arquivo CSV.
  * CSV Delimiter: delimitador do arquivo CSV.&#x20;
* **Excel File Name:** nome do arquivo que será salvo. Se o campo estiver vazio, será considerada a propriedade "_fileName_".
* **Maximum File Size:** tamanho máximo permitido para o arquivo (em _bytes_).

{% hint style="warning" %}
**IMPORTANTE:** a configuração _**Maximum File Size**_ é opcional e deve ser usada somente se o usuário desejar mais controle sobre o arquivo gerado. Lembre-se que o arquivo Excel a ser gerado provavelmente será maior do que os dados CSV de entrada.
{% endhint %}

* **Charset:** codificação do nome para a leitura do arquivo. Veja mais sobre _**java.nio.charset.Charset**_.
* **CSV File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt). Expressões em _Double Braces_ são suportadas.
* **Sheet Name:** nome da planilha de Excel. Se o campo estiver vazio, a planilha será salva como "Sheet1".
* **Delimiter:** delimitador no qual o CSV está configurado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".
* **Column Properties:** ao clicar em _**Add**_, você ativa os parâmetros _**Column**_, _**Date Format**_ e _**Column Type**_. Com esses parâmetros, você pode indicar um tipo de dado a uma coluna específica de um arquivo Excel que será criado.&#x20;
  * **Column:** coluna que contém os dados que serão tratados.
  * **Date Format:** formato de dado a ser usado se o tipo do campo é _Date_ (por exemplo: _Column Type_ = _Date_).&#x20;
  * **Column Type:** tipo de dado da coluna (_Number_, _Date_ ou _Boolean_).&#x20;
* **Set Password:** se esta opção estiver habilitada, você poderá definir uma senha para proteger o arquivo de saída Excel.
* **Password:** Senha do arquivo Excel. Este parâmetro fica disponível apenas quando a opção _**Set Password**_ estiver habilitada. Este campo suporta caracteres de texto e expressões em _Double Braces_.

Note que alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso [artigo sobre Funções Double Braces](https://docs.digibee.com/documentation/v/pt-br/build/double-braces/funcoes-double-braces).

## CSV to Excel em Ação <a href="#csv-to-excel-em-ao" id="csv-to-excel-em-ao"></a>

### Utilizando múltiplos arquivos CSV de uma só vez <a href="#utilizando-mltiplos-arquivos-csv-de-uma-s-vez" id="utilizando-mltiplos-arquivos-csv-de-uma-s-vez"></a>

Você deve habilitar a opção _**Multiple Sheets**_ para que seja possível especificar múltiplos arquivos CSV na geração de novas planilhas. Isso vale tanto para arquivos de Excel existentes ou inexistentes.

Se você precisar criar novas planilhas dentro de um arquivo Excel existente, informe o nome desse arquivo no campo _**Excel File Name**_. Dessa forma, o arquivo será atualizado com as novas planilhas.

No entanto, se você quiser criar um novo arquivo de Excel com essas planilhas, então não preencha o campo _**Excel File Name**_ (ou preencha com o nome de um arquivo inexistente).

### Utilizando um arquivo CSV <a href="#utilizando-um-arquivo-csv" id="utilizando-um-arquivo-csv"></a>

No campo _**Excel File Name**_, insira o nome do arquivo CSV a ser utilizado na criação de uma nova planilha.

Se você precisar criar novas planilhas dentro de um arquivo Excel existente, informe o nome desse arquivo no campo _**Excel File Name**_. Assim, o arquivo será atualizado com as novas planilhas.

No entanto, se você quiser criar um novo arquivo de Excel com essas planilhas, então não preencha o campo _**Excel File Name**_ (ou preencha com o nome de um arquivo inexistente).

{% hint style="warning" %}
**IMPORTANTE:** desaconselhamos a criação de uma nova planilha em um arquivo de Excel já existente e grande (com uma ou mais planilhas com alta quantidade de dados), porque para criar as novas planilhas é necessário abrir o arquivo de Excel inteiro e isso consome muita memória. Por outro lado, isso não acontece quando um novo arquivo de Excel é criado de uma vez só com múltiplas planilhas - nesse caso, utiliza-se um _stream_ no processo de criação.
{% endhint %}

### **Exemplos de configuração** <a href="#exemplos-de-configurao" id="exemplos-de-configurao"></a>

**1.** O exemplo abaixo vai resultar na criação de um arquivo XLXS. Todas as colunas e linhas do CSV serão lidas como _string_:

```
{
       "type": "connector",
       "name": "csv para excel-connector",
       "stepName": "csv-test",
       "params": {
            "fileName": "{{message.fileName}}",
            "excelFileName": "arquivo",
            "delimiter": ",",
            "failOnError": false
       }
}
```

&#x20;

**2.** Veja quais são os tipos de configuração para algumas colunas:

```
{
       "type": "connector",
       "name": "csv para excel-connector",
       "stepName": "csv-test",
       "params": {
            "fileName": "{{message.fileName}}",
            "excelFileName": "arquivo",
            "cellDefinitions": "[{\" column \ ": \" A \ ", \" type \ ": \" NUMBER \ "}, {\" column \ ": \" B \ ", \" dateFormat \ " : \ "dd-MM-aaaa \", \ "type \": \ "DATE \"}, {\ "column \": \ "C \", \ "type \": \ "BOOLEAN \"}] ",
         "delimiter": ",",
         "failOnError": false
       }
}
```

{% hint style="warning" %}
**IMPORTANTE**: a manipulação de arquivos dentro de um _pipeline_ é feita de maneira protegida. Todos os arquivos podem ser acessados apenas em um diretório temporário, onde cada KEY do _pipeline_ tem acesso ao seu próprio conjunto de arquivos.
{% endhint %}
