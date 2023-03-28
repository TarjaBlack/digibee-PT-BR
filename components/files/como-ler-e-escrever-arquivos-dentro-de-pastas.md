---
description: Exemplos com os componente File Reader e File Writer.
---

# Como ler e escrever arquivos dentro de pastas

### _**Cenário 1: Lendo um arquivo dentro de uma pasta**_

Digamos que você tenha um arquivo 'file.txt' na pasta 'folder' disponível no seu _pipeline_. Para poder ler esse arquivo dentro de uma pasta, você pode invocar um _**File Reader**_ que indique o caminho 'folder/file.txt'. Dessa forma, você consegue acessar o arquivo 'file.txt'.

#### **Exemplo**

<figure><img src="https://i.imgur.com/29yULHk.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://i.imgur.com/lr1MbY9.png" alt=""><figcaption></figcaption></figure>

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

### Cenário 2: escrevendo arquivos dentro de uma pasta

Digamos que você tenha um arquivo 'file.txt' na pasta 'folder' disponível no seu pipeline. Para poder escrever esse arquivo dentro de uma pasta, você pode invocar um File Writer que indique o caminho 'folder/file.txt'. Dessa forma, você consegue acessar o arquivo 'file.txt'.

#### **Exemplo**

<figure><img src="https://i.imgur.com/29yULHk.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://i.imgur.com/lr1MbY9.png" alt=""><figcaption></figcaption></figure>

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
