---
description: Exemplos com os componente File Reader e File Writer.
---

# Como ler e escrever arquivos dentro de pastas



_**Cenário 1: Ler um arquivo dentro de uma pasta**_\
Digamos que você tenha um arquivo 'file.txt' na pasta 'folder' disponível no seu _pipeline_. Para poder ler esse arquivo dentro de uma pasta, você pode invocar um _**File Reader**_ que indique o caminho 'folder/file.txt'. Dessa forma, você consegue acessar o arquivo 'file.txt'.\


**Exemplo:**

[![](https://downloads.intercomcdn.com/i/o/184674084/c4bcd395d62667ef534e697a/image.png)](https://downloads.intercomcdn.com/i/o/184674084/c4bcd395d62667ef534e697a/image.png)[![](https://downloads.intercomcdn.com/i/o/184674164/75f7dd37d4e81d84944ba681/image.png)](https://downloads.intercomcdn.com/i/o/184674164/75f7dd37d4e81d84944ba681/image.png)

1. Crie um _pipeline_ e adicione um componente _**File Reader**_
2. Abra as configurações do componente
3. Defina o _FILE NAME_ como 'folder/file.txt'
4. Clique em CONFIRMAR para salvar as configurações do componente
5. Conecte o _trigger_ com o _File Reader_
6. Execute um teste no _pipeline_ (CTRL + ENTER)

O resultado será apresentado:

```
{
  "data": [
    "my sample content"
  ],
  "fileName": "folder/file.txt",
  "lineCount": 1
}
```

* **data:** vetor com o conteúdo do arquivo lido pelo _**File Reader**_
* **fileName:** apresenta o caminho completo do arquivo que foi lido
* **lineCount:** identifica a quantidade de linhas contidas no arquivo lido pelo _**File Reader**_

\
_**Cenário 2: Escrever um arquivo dentro de uma pasta**_\
Digamos que você tenha um arquivo 'file.txt' na pasta 'folder' disponível no seu _pipeline_. Para poder escrever esse arquivo dentro de uma pasta, você pode invocar um _**File Writer**_ que indique o caminho 'folder/file.txt'. Dessa forma, você consegue acessar o arquivo 'file.txt'.

**Exemplo:**

[![](https://downloads.intercomcdn.com/i/o/184682211/efd73f7cadef4cae6666cdbe/image.png)](https://downloads.intercomcdn.com/i/o/184682211/efd73f7cadef4cae6666cdbe/image.png)[![](https://downloads.intercomcdn.com/i/o/184682176/ad58e87dd18d0471b4edc364/image.png)](https://downloads.intercomcdn.com/i/o/184682176/ad58e87dd18d0471b4edc364/image.png)

1. Crie um _pipeline_ e adicione um componente _**File Writer**_
2. Abra as configurações do componente
3. Defina o _FILE NAME_ como 'folder/file.txt'
4. Defina o campo _DATA como \{{ message.data \}}._\
   Note que usamos a expressão em _Double Braces: \{{ message.data \}}_ para acessar o resultado do último componente. Nesse caso, acessamos _data_ com o conteúdo do arquivo a ser escrito.
5. Clique em CONFIRMAR para salvar as configurações do componente
6. Conecte o _trigger_ com o _**File Writer**_
7. Execute um teste no _pipeline_ (CTRL + ENTER)

O resultado será apresentado:

```
{
 "fileName": "folder/file.txt",
 "success": true
}
```

* **fileName:** apresenta o caminho completo do arquivo que foi escrito
* **success:** quando apresenta _true_ no resultado, indica que a execução foi bem sucedida

### Diversos outros componentes possuem as funcionalidades acima: <a href="#diversos-outros-conectores-usufruem-das-funcionalidades-acima-veja-a-lista-a-seguir" id="diversos-outros-conectores-usufruem-das-funcionalidades-acima-veja-a-lista-a-seguir"></a>

* **Ler e Escrever Arquivos**\
  File Reader\
  File Writer\
  CSV File Writer\
  CSV to Excel\
  Excel\
  Stream Excel\
  Stream File Reader V2
* **Upload, Download e Remoção (**_**Delete**_**) de Arquivos de Data Storage**\
  Digibee Storage\
  S3 Storage\
  Google Storage\
  Dropbox\
  SFTP\
  FTP\
  One Drive\
  WebDAV
* **Outros componentes**\
  WGet\
  Zip File\
  REST V2\
  PGP
