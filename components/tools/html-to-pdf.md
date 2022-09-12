---
description: Conheça o componente e saiba como utilizá-lo.
---

# HTML to PDF

O **HTML to PDF** permite a criação de arquivos no formato PDF a partir de um HTML.

Além disso, o componente utiliza _templates_ Apache FreeMaker para gerar o HTML através da mensagem JSON do _pipeline_.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name**: nome do arquivo em PDF que será gerado na saída da execução do componente.
* **Body**: _template_ em HTML a ser interpretado para gerar o arquivo em PDF (esse campo suporta o template FreeMarker).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".
* **Secured PDF:** se a opção estiver habilitada, é permitida a inclusão de senha no arquivo em PDF para gerar um documento protegido.
* **Password:** senha para proteger o arquivo em PDF.
* **Custom permissions:** se a opção estiver habilitada, diversas opções de permissão de acesso no arquivo em PDF ficam disponíveis; do contrário, o arquivo em PDF será gerado com todas as permissões.
* **Read only:** permissão de acesso que define o arquivo em PDF como "somente leitura". Se a opção estiver habilitada, todas as outras permissões de acesso serão desabilitadas.
* **Assemble document:** permite que páginas sejam adicionadas, rotacionadas e removidas do arquivo.
* **Modify:** permite modificar o arquivo.
* **Modify annotations:** permite adicionar ou modificar anotações de texto no arquivo.
* **Extract content:** permite extrair textos e imagens do arquivo.
* **Extract for accessibility:** permite extrair textos e imagens do arquivo para fins de acessibilidade.
* **Print:** permite a impressão do arquivo.
* **Print degraded:** permite a impressão _degraded_ do arquivo.
* **Fill in Form:** permite o preenchimento de formulários com campos interativos.

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

O componente aceita qualquer mensagem de entrada, podendo utilizá-la por meio de _Double Braces_.

#### Saída <a href="#sada" id="sada"></a>

* com sucesso

```
{  
    "success": true,  
    "fileName": "pdf_gerado.pdf",  
}
```

* com erro

```
{  
    "success": false,  
    "message": "Could not generate the pdf file",  
    "error": "java.net.IOException"
}
```

#### Exemplo de resposta de requisição contendo erro <a href="#exemplo-de-resposta-de-requisio-contendo-erro" id="exemplo-de-resposta-de-requisio-contendo-erro"></a>

```
{  
    "success": false,  
    "message": "Could not generate the pdf file",  
    "error": "java.net.IOException:"
}
```

* **success:** “false” quando a operação falha
* **message:** mensagem sobre o erro
* **exception:** informação sobre o tipo de erro ocorrido

**Exemplo:**

Body

```
<p>We have these animals:
<table border=1>
  <#list animals as animal>
    <tr><td>${animal.name}<td>${animal.price} Euros
  </#list>
</table>
```

Portanto, na mensagem de entrada é recebido um _array_ de objetos que contêm as propriedades “name” e “price”:

```
[
    { "name": "Dog", "price": 100},
    { "name": "Cat", "price": 100},
    { "name": "Bird", "price": 30},
]
```

O _template_ fará a iteração nesse _array_ recebido e preencherá o HTML:

```
<p>We have these animals:
<table border=1>
      <tr><td>Dog<td>$100 Euros
<tr><td>Cat<td>$100 Euros
<tr><td>Bird<td>$30 Euros
  </table>
```

**IMPORTANTE:**

* **SVG**

Para utilizar o SVG como _tag_ HTML, aplique a seguinte propriedade dentro da _tag_ SVG (**xmlns="**[**http://www.w3.org/2000/svg**](http://www.w3.org/2000/svg)**"**):

```
<svg xmlns="http://www.w3.org/2000/svg" width="400" height="180">
  <rect x="50" y="20" rx="20" ry="20" width="150" height="150" style="fill:red;stroke:black;stroke-width:5;opacity:0.5" />
  Sorry, your browser does not support inline SVG.
</svg>
```

* **CSS**

Não há suporte para versões acima de 2.1.

* **IMAGENS**

Não é suportada a utilização de imagens em formato base64 dentro de _tags_ HTML.

**Ex.:** \<img src="data:image/png;base64, iVBORw0KGgoAAAANSUhEUgAA…>

Você pode utilizar imagens com referência local e remota:

* **Imagem Local**

```
<img src="image.jpg" alt="IMAGE2" >
```

No exemplo acima, deve existir um arquivo de imagem exatamente com o nome especificado dentro da _tag_ src (image.jpg)

* **Imagem Remota**

```
<img src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_92x30dp.png" alt="IMAGE2" >
```

\
