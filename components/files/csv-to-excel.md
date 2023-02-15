---
description: Conheça o componente e saiba como utilizá-lo.
---

# CSV to Excel

O **CSV to Excel** transforma arquivos em formato CSV em arquivos XLSX.

Você pode gerar apenas 1 arquivo de Excel por execução.

Dê uma olhada nos parâmetros de configuração do componente:

![](<../../.gitbook/assets/ezgif.com-gif-maker (7).gif>)

* **Multiple Sheets:** se “true”, múltiplos arquivos CSV vão resultar em múltiplas planilhas; do contrário, apenas 1 arquivo Excel vai ser criado.
* **Excel File Name:** nome do arquivo que será salvo - se o campo estiver vazio, será considerada a propriedade "fileName".
* **Maximum File Size:** tamanho máximo permitido para o arquivo (em _bytes_).

{% hint style="info" %}
**IMPORTANTE:** Esta configuração é opcional e deve ser usada somente se o usuário desejar mais controle sobre o arquivo gerado. Lembre-se que o arquivo Excel a ser gerado provavelmente será maior do que os dados CSV de entrada.
{% endhint %}

* **Charset:** codificação do nome para a leitura do arquivo - veja mais sobre _**java.nio.charset.Charset**_.
* **CSV File Name:** nome do arquivo ou caminho completo do arquivo (ex.: tmp/processed/file.txt) - expressões em _Double Braces_ são suportadas.
* **Sheet Name:** nome da planilha de Excel - se o campo estiver vazio, a planilha será salva como "Sheet1".
* **Delimiter:** delimitador no qual o CSV está configurado.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Set Password:** se esta opção estiver habilitada, você poderá definir uma senha para proteger o arquivo de saída Excel.
* **Password:** Senha do arquivo Excel. Este parâmetro fica disponível apenas quando a opção **Set Password** estiver habilitada. Este campo suporta caracteres de texto e expressões em _Double Braces_.

Note que alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso artigo clicando [aqui](https://intercom.help/godigibee/pt-BR/articles/3185881-double-braces-e-entrada-de-dados).

## CSV to Excel em Ação <a href="#csv-to-excel-em-ao" id="csv-to-excel-em-ao"></a>

### Utilizando múltiplos arquivos CSV de uma só vez <a href="#utilizando-mltiplos-arquivos-csv-de-uma-s-vez" id="utilizando-mltiplos-arquivos-csv-de-uma-s-vez"></a>

Você deve habilitar a opção _Multiple Sheets_ para que seja possível especificar múltiplos arquivos CSV na geração de novas planilhas. Isso vale tanto para arquivos de Excel existentes ou inexistentes.

Se você precisar criar novas planilhas dentro de um arquivo Excel existente, não deixe de informar o nome desse arquivo no campo _Excel File Name_. Assim, o arquivo é atualizado com as novas planilhas.

\
Mas se você quiser criar um novo arquivo de Excel com essas planilhas, então não preencha o campo _Excel File Name_ (ou preencha com o nome de um arquivo inexistente).

### Utilizando um arquivo CSV <a href="#utilizando-um-arquivo-csv" id="utilizando-um-arquivo-csv"></a>

Insira o nome do arquivo CSV a ser utilizado na criação de uma nova planilha no campo _Excel File Name_.

\
Se você precisar criar novas planilhas dentro de um arquivo Excel existente, não deixe de informar o nome desse arquivo no campo _Excel File Name_. Assim, o arquivo é atualizado com as novas planilhas.

\
Mas se você quiser criar um novo arquivo de Excel com essas planilhas, então não preencha o campo _Excel File Name_ (ou preencha com o nome de um arquivo inexistente).

**IMPORTANTE:** desaconselhamos a criação de uma nova planilha em um arquivo de Excel já existente e grande (com uma ou mais planilhas com alta quantidade de dados), já que para criar as novas planilhas é necessário abrir o arquivo de Excel inteiro e isso consome muita memória. Por outro lado, isso não acontece quando um novo arquivo de Excel é criado de uma vez só com múltiplas planilhas - nesse caso, utiliza-se um _stream_ no processo de criação.

### **Exemplos de configuração** <a href="#exemplos-de-configurao" id="exemplos-de-configurao"></a>

**1.** O exemplo que você vê abaixo vai resultar na geração de um arquivo XLXS e todas as colunas e linhas do CSV serão lidas como _string_:

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

&#x20;    \
**IMPORTANTE**: a manipulação de arquivos dentro de um _pipeline_ é feita de maneira protegida. Todos os arquivos podem ser acessados apenas em um diretório temporário, onde cada KEY do _pipeline_ tem acesso ao seu próprio conjunto de arquivos.
