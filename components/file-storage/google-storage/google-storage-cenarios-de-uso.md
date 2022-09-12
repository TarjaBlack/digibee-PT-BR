---
description: Conheça os cenários de uso suportados.
---

# Google Storage: Cenários de Uso

### Cenário 1: LIST de arquivos <a href="#cenrio-1-list-de-arquivos" id="cenrio-1-list-de-arquivos"></a>

Digamos que você tenha 1 ou mais arquivos no _**Google Storage**_ e que você queira invocar o _**Google Storage**_ em modo de lista. Dessa maneira, você terá acesso à lista de arquivos existentes e às suas respectivas pastas.

Veja um exemplo de como tornar isso viável:

1\. Crie um _pipeline_ e adicione o _**Google Storage**_.

2\. Abra as configurações do componente e escolha uma _ACCOUNT_ (note que esse campo é obrigatório). Caso não possua uma conta configurada para acessar o Google Storage, primeiro você deve gerar uma chave primária através do serviço do Google. Clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br) para fazer isso.

**IMPORTANTE:** O Account suportado é do tipo **Private Key.** O campo key do account deverá conter o _Json_ **completo** gerado pelo Google.

3\. Configure os outros campos obrigatórios do componente (Project ID e Bucket Name) e os opcionais também (Remote Directory, Page Size e Page Token).

4\. Clique em CONFIRMAR.

5\. Ligue o _trigger_ ao _**Google Storage**_.

6\. Execute um teste no _pipeline_ (CTRL + ENTER).

7\. Você verá uma lista dos arquivos disponíveis no Google Storage de acordo com as suas especificações determinadas:

```

  "content": [
    {
      "name": "DGB-413/",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552394033410,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 11
    },
    {
      "name": "DGB-413/iso-8859-1-test.txt",
      "contentType": "application/octet-stream",
      "contentEncoding": null,
      "createTime": 1579552641265,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 65
    }
  ],
  "pageToken": "ChtER0ItNDEzL2lzby04ODU5LTEtdGVzdC50eHQ=",
  "fileName": null,
  "remoteFileName": null,
  "remoteDirectory": "DGB-413",
  "success": true
}
```

Como você pode ver no exemplo acima, a opção escolhida foi _PageSize_ 2, ou seja, apenas 2 arquivos serão listados. Se nenhum valor for especificado nesse campo, então todos os arquivos serão listados. No entanto, não recomendamos que você deixe de especificar esse valor, já que isso pode atrapalhar o desempenho e o tempo de recuperação dos dados. Dê uma olhada no cenário a seguir e aprenda a iterar múltiplos arquivos sem afetar a segurança e o desempenho.

### &#x20;Cenário 2: LIST de vários arquivos usando paginação <a href="#cenrio-2-list-de-vrios-arquivos-usando-paginao" id="cenrio-2-list-de-vrios-arquivos-usando-paginao"></a>

Digamos que você tenha uma grande quantidade de arquivos no Google Storage e que você queira invocar o _**Google Storage**_ em modo de lista. Dessa maneira, você consegue listar os arquivos usando paginação.

Para fazer isso, você deve:

1. Criar um _pipeline_ e adicionar o _**Google Storage**_, escolhendo a opção "List" no campo Step Name.
2. Abrir as configurações do componente e escolher uma _ACCOUNT_ (note que esse campo é obrigatório). Caso não possua uma conta configurada para acessar o Google Storage, primeiro você deve gerar uma chave primária através do serviço do Google. Clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br) para fazer isso. Em seguida, configure uma _Account_ na plataforma da Digibee.
3. Configurar os outros campos obrigatórios do componente (Project ID e Bucket Name) e os opcionais também (Remote Directory, Page Size e Page Token).
4. Clicar em CONFIRMAR.
5. Adicionar mais um _**Google Storage**_, definindo o Step Name como "List-2".
6. Configurar mais uma vez os outros campos obrigatórios do componente (Project ID, Bucket Name, Page Size e Page Token) e o opcional também (Remote Directory).

**IMPORTANTE:** defina o Page Token com _Double Braces_:

```
{{ message.pageToken }}
```

_Double Braces_ dão acesso à saída do componente anterior. Logo, o Page Token gerado pelo _**Google Storage**_ com a configuração "List" permite que a próxima página de listagem de arquivos seja puxada para o _**Google Storage**_ com a configuração "List-2".

7\. Ligar o _trigger_ e os componentes:

![](<../../../.gitbook/assets/google storage.png>)



8\. Executar um teste no _pipeline_ (CTRL + ENTER).\
9\. Você verá uma lista dos arquivos disponíveis no Google Storage de acordo com as suas especificações determinadas:

```
{
  "content": [
    {
      "name": "DGB-413/iso8859-2.txt",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552395963553,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 55
    },
    {
      "name": "DGB-413/utf-16-test.txt",
      "contentType": "text/plain",
      "contentEncoding": null,
      "createTime": 1552394973030,
      "bucket": "digibee-test-digibee-test-bucket",
      "size": 70
    }
  ],
  "pageToken": "ChdER0ItNDEzL3V0Zi0xNi10ZXN0LnR4dA==",
  "fileName": null,
  "remoteFileName": null,
  "remoteDirectory": "DGB-413",
  "success": true
}

```

Como você pode ver no exemplo acima, a saída mostra apenas os arquivos da última página gerada pelo _**Google Storage**_ com a configuração "List-2". No entanto, fica claro como você pode utilizar o Page Token para acessar páginas consecutivas.

### Cenário 3: DOWNLOAD de um arquivo <a href="#cenrio-3-download-de-um-arquivo" id="cenrio-3-download-de-um-arquivo"></a>

Digamos que você tenha um arquivo no _**Google Storage**_ e que você queira invocar o _**Google Storage**_ em modo de _download_. Dessa maneira, você tem acesso a um arquivo específico para ser trabalhado pelo _pipeline_.

Veja como fazer isso:

1. Crie um _pipeline_ e adicione _**Google Storage**_.
2. Abra as configurações do componente e escolher uma _ACCOUNT_ (note que esse campo é obrigatório). Caso não possua uma conta configurada para acessar o Google Storage, primeiro você deve gerar uma chave primária através do serviço do Google. Clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br) para fazer isso. Em seguida, configure uma _Account_ na plataforma da Digibee.
3. Configure os outros campos obrigatórios do componente (Project ID, Bucket Name e Remote File Name) e os opcionais também (File Name e Remote Directory).
4. Clique em CONFIRMAR.
5. Ligue o _trigger_ ao _**Google Storage**_.
6. Execute um teste no _pipeline_ (CTRL + ENTER).
7. Você verá uma confirmação da existência e disponibilidade do arquivo no _pipeline_, com o File Name especificado:

```
{
  "fileName": "iso-8859.txt",
  "remoteFileName": "iso-8859-1-test.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}
```

### &#x20;Cenário 4: UPLOAD de um arquivo <a href="#cenrio-4-upload-de-um-arquivo" id="cenrio-4-upload-de-um-arquivo"></a>

Digamos que você tenha um arquivo no _pipeline_ e que você queira invocar o _**Google Storage**_ em modo de _upload_. Dessa maneira, o arquivo especificado fica disponível no Google Storage.

Saiba como fazer isso:

1. Crie um _pipeline_ e adicione o _**Google Storage**_.
2. Abra as configurações do componente e escolher uma _ACCOUNT_ (note que esse campo é obrigatório). Caso não possua uma conta configurada para acessar o Google Storage, primeiro você deve gerar uma chave primária através do serviço do Google. Clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br) para fazer isso. Em seguida, configure uma _Account_ na plataforma da Digibee.
3. Configure os outros campos obrigatórios do componente (Project ID, Bucket Name e File Name) e os opcionais também (Remote File Name e Remote Directory).
4. Clique em CONFIRMAR.
5. Ligue o _trigger_ ao _**Google Storage**_.
6. Execute um teste no _pipeline_ (CTRL + ENTER).
7. Você verá uma confirmação da criação do arquivo no Google Storage, com o Remote File Name e o Remote Directory especificados:

```
{
  "fileName": "iso-8859.txt",
  "remoteFileName": "iso-8859-upload.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}

```

### &#x20;Cenário 5: DELETE de um arquivo <a href="#cenrio-5-delete-de-um-arquivo" id="cenrio-5-delete-de-um-arquivo"></a>

Digamos que você tenha um arquivo no Google Storage e que você queira invocar o _**Google Storage**_ em modo de _delete_. Dessa maneira, o arquivo é removido do Google Storage.

Para fazer isso, basta você seguir estes passos:

1. Crie um _pipeline_ e adicione o _**Google Storage**_.
2. Abra as configurações do componente e escolher uma _ACCOUNT_ (note que esse campo é obrigatório). Caso não possua uma conta configurada para acessar o Google Storage, primeiro você deve gerar uma chave primária através do serviço do Google. Clique [aqui](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br) para fazer isso. Em seguida, configure uma _Account_ na plataforma da Digibee.
3. Configure os outros campos obrigatórios do componente (Project ID, Bucket Name e Remote File Name) e o opcional também (Remote Directory).
4. Clique em CONFIRMAR.
5. Execute um teste no _pipeline_ (CTRL + ENTER).
6. Você verá uma confirmação da remoção do arquivo do Google Storage:

```
{
  "fileName": null,
  "remoteFileName": "iso-8859-upload.txt",
  "remoteDirectory": "DGB-413",
  "success": true
}
```
