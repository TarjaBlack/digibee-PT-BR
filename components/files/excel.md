---
description: Conheça o componente e saiba como utilizá-lo.
---

# Excel

O **Excel** lê e salva arquivos de Excel.

Dê uma olhada nos parâmetros de configuração do componente:

<figure><img src="../../.gitbook/assets/Gif Excel.gif" alt=""><figcaption></figcaption></figure>

* **Operation:** ação a ser executada pelo componente.
* **Excel Full Path:** caminho no qual o arquivo de Excel está localizado.
* **File Name:** nome do arquivo criado.
* **Sheet Name:** nome da planilha.
* **Cell:** especificação da célula da planilha.
* **Cells:** lista de células da planilha.
* **Cell Value:** valor a ser substituído em uma célula específica.
* **Sheets:** lista de nomes das planilhas.
* **JSON Data:** JSON a ser utilizado na geração do arquivo de Excel.
* **Read All Sheets:** se a opção estiver ativada, todas as planilhas do arquivo de Excel serão lidas.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### **Operação READ** <a href="#operao-read" id="operao-read"></a>

Lê um arquivo de Excel e gera um objeto de JSON com planilhas e linhas.

Os seus parâmetros são:

* Read All Sheets (obrigatório)
* Excel Full Path (obrigatório)
* Sheet Name (obrigatório apenas se a opção _**Read All Sheets**_ não estiver ativada)

**Saída**

* Se você quiser ler todas as planilhas

```
{
     "Sheet1": [{"A1": "A1 Content"},{"A2": "A2 Content"} ...],
     "Sheet2": [{"A1": "A1 Content"},{"A2": "A2 Content"} ...],
     ...
}
```

* Se você quiser ler apenas uma planilha específica

```
{
     "Sheet_Specified": [{"A1": "A1 Content"},{"A2": "A2 Content"} ...]
}
```

### Operação READ SPECIFIC SHEETS <a href="#operao-read-specific-sheets" id="operao-read-specific-sheets"></a>

Lê planilhas específicas passadas através de uma lista.

Os seus parâmetros são:

* Excel Full Path (obrigatório)
* Sheets (obrigatório)

**Saída**

```
{
      "Sheet_Specified1": [{"A1": "A1 Content"},{"A2": "A2 Content"} ...],
      "Sheet_Specified2": [{"A1": "A1 Content"},{"A2": "A2 Content"} ...],
      ...
}
```

### Operação READ ONE CELL <a href="#operao-read-one-cell" id="operao-read-one-cell"></a>

Lê uma célula específica de um arquivo de Excel.

Os seus parâmetros são:

* Sheet Name (obrigatório)
* Excel Full Path (obrigatório)
* Cell (obrigatório)

**Saída**

```
{
      "A1": "A1 Content"
}
```

### Operação READ MULTIPLE CELLS <a href="#operao-read-multiple-cells" id="operao-read-multiple-cells"></a>

Lê múltiplas células de uma planilha de um arquivo de Excel passado através de uma lista.

Os seus parâmetros são:

* Sheet Name (obrigatório)
* Excel Full Path (obrigatório)
* Cells (obrigatório)

**Saída**

```
{
     "A1": "A1 Content",
     "B1": "B1 Content",
     "X1": "X1 Content"
}
```

### Operação CREATE <a href="#operao-create" id="operao-create"></a>

Cria um arquivo de Excel a partir do JSON passado.

Os seus parâmetros são:

* Sheet Name
* JSON Data (obrigatório)
* File Name

**Saída**

```
{
     "localFilename": "path/to/the/file",
     "success": true
}
```

### Operação UPDATE ONE CELL <a href="#operao-update-one-cell" id="operao-update-one-cell"></a>

Atualiza uma célula específica de um arquivo de Excel.

Os seus parâmetros são:

* Excel Full Path (obrigatório)
* Cell (obrigatório)
* Cell Value (obrigatório)

**Saída**

```
{
      "localFilename": "path/to/the/file",
      "success": true,
      "cellUpdated": {
           "A1": "A1 new Content"
      }
}
```
