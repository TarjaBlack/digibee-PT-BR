---
description: Conheça o componente e saiba como utilizá-lo.
---

# Append Files

O _**Append Files**_ acrescenta um ou mais arquivos textos em um arquivo texto existente.

Dê uma olhada nos parâmetros de configuração do componente:

![](<../../.gitbook/assets/ezgif.com-gif-maker (8).gif>)

* **File Name:** nome do arquivo que recebe o conteúdo de outros arquivos.
* **Charset:** _charset_ do arquivo final.
* **Files to Append**: lista dos arquivos a serem acrescentados ao arquivo original.
* **File Name:** nome do arquivo.
* **Charset:**_charset_ do arquivo.
* **Custom Append Files Specification**: se a opção estiver habilitada, é possível informar a lista de arquivos ao componente de forma dinâmica.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

## Fluxo de mensagens <a href="#h_b57caa312c" id="h_b57caa312c"></a>

### Entrada <a href="#h_1e7f6fb470" id="h_1e7f6fb470"></a>

É necessário ter no diretório corrente do _pipeline_ apenas os arquivos que serão utilizados nesse componente.

### Saída <a href="#h_767373613b" id="h_767373613b"></a>

```
{
"fileName": "pipeline-example",
"success": true
}
```

* **fileName:** nome do arquivo final
* **success:** quando a chamada é feita com sucesso

## Append Files em Ação <a href="#h_d8518c02cf" id="h_d8518c02cf"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

### Realizando o _append_ de vários arquivos <a href="#h_2c4d751949" id="h_2c4d751949"></a>

* **File Name:** arquivo\_final.txt
* **Charset:** "UTF-8"
* **Custom Append Files Specification:** habilitado
* **Files to Append:**

```
[
{"fileName": "file1.txt", "charset": "UTF-8"},
{"fileName": "file2.txt", "charset": "UTF-8"}
]
```

* **Fail On Error:** false
* **Conteúdo do arquivo:** arquivo\_final.txt

```
HEADER
line1
```

* **Conteúdo do arquivo:** file1.txt

```
file1
test
```

* **Conteúdo do arquivo:** file2.txt

```
file2
another test
```

**Saída**

```
{
"fileName": "arquivo_final.txt",
"success": true
}
```

* **Conteúdo final do arquivo:** arquivo\_final.txt

```
HEADER
line1file1
testfile2
another test
```
