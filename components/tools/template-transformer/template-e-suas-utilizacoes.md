---
description: Dicas de como utilizar todo potencial desse componente.
---

# Template e suas utilizações

Conheça algumas validações e tratamentos que podem ser feitos com a linguagem _Freemarker_ quando você utiliza o **Template Transformer**. Para saber mais sobre esse componente, clique [aqui](https://intercom.help/godigibee/pt-BR/articles/2950086-template-transformer) e leia o artigo a respeito.

Para os exemplos que você verá a seguir, considere o seguinte JSON de entrada:

```
{
  "pedido": {
    "codigo": 213,
    "valor": 4513423.1322,
    "descricao": "   pedido teste   ",
    "itens": [
      {
        "nome": "item 1",
        "quantidade": 2
      },
      {
        "nome": "item 2",
        "quantidade": 1
      }
    ]
  }
}
```

#### LIST <a href="#list" id="list"></a>

Possibilita que você realize iterações em um _array_ (lista) no JSON. Imagine essa função na criação de uma lista dinâmica de elementos na saída, que transforma o JSON em XML.

**Sintaxe**

```
<#list SuaLista as elemento>
              bloco de informações que será iterado.
</#list>
```

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode criar uma lista dinâmica de itens utilizando o _template_.

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">
<soap:Header/>
    <soap:Body>
        <web:pedido>
            <web:itens>
                <#list itens as item>
                    <web:item>
                        <web:nome>${item.nome}</web:nome>
                        <web:quantidade>${item.quantidade}</web:quantidade>
                    </web:item>
                </#list>
            </web:itens>
        </web:pedido>
    </soap:Body>
</soap:Envelope>
```

**Saída do XML**

```
<soap:Envelope 	xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\"	xmlns:web=\"http://www.webservicex.net/\">
 <soap:Header/>    
 <soap:Body>        
  <web:pedido>            
    <web:itens>                                    
     <web:item>                        
     	<web:nome>item 1</web:nome>                        
     	<web:quantidade>2</web:quantidade>                    
     </web:item>                    
     <web:item>                        
     	<web:nome>item 2</web:nome>                        
     	<web:quantidade>1</web:quantidade>                    
     </web:item>            
    </web:itens>        
  </web:pedido>    
 </soap:Body>
</soap:Envelope>
```

{% hint style="info" %}
**IMPORTANTE:** lembre-se que a saída do **Template** é um XML em uma _string_.
{% endhint %}

#### IF/ELSE <a href="#ifelse" id="ifelse"></a>

Você pode utilizar essa função para a validação de algumas informações. Mesmo quando os seus campos estiverem nulos ou vazios, não há um grande impacto na sua transformação de dados.

**Sintaxe**

```
<#if condição>
             Bloco de informações caso a condição do if seja verdadeira.
<#elseif condição>
              Bloco de informações caso a condição do elseif seja verdadeira.
<#else>
              Bloco de informações caso nenhuma das condições seja tomadas.
</#if>
```

\


Não existe limitação para a quantidade de _elseif_ e também é possível usar apenas um _if_ sem o _else_ - tudo depende da sua necessidade.

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode criar uma validação na qual o campo "código" precise ser maior que 0 (zero).

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">

    <soap:Header/>  
    <so ap:Body> 
       <web:pedido> 
           <web:codigo><#if codigo &gt; 0 >${codigo}</#if></web:codigo>
       </web:pedido> 
    </soap:Body> 
</soap:Envelope>
```

**Saída do XML**\
Caso a condição seja verdadeira:

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\">

   <soap:Header/> 
       <soap:Body>     
          <web:pedido> 
              <web:codigo>213</web:codigo>  
          </web:pedido> 
       </soap:Body> 
</soap:Envelope>
```

Caso a condição seja falsa:

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\"> 
   <soap:Header/> 
       <soap:Body>     
          <web:pedido> 
              <web:codigo></web:codigo>  
          </web:pedido> 
       </soap:Body> 
</soap:Envelope>
```

Sabia que a utilização da função não é limitada a condições simples? Você também pode utilizar expressões para validar se o campo existe (??) e se ele tem conteúdo (has\_content).

**Sintaxe**

```
<#if seuCampo?? && seuCampo?has_content>
             Bloco de informações caso o campo exista e tenha conteúdo.
<#else>
              Bloco de informações caso nenhuma das condições seja tomadas.
</#if>

```

**IMPORTANTE:** é possível utilizar operadores lógicos para uma condição mais avançada.

_**&&**_ - para o E (AND).

_**||**_ - para o OU (OR).

**Exemplo**

Agora veja como melhorar a validação para que o _if_ feito no primeiro caso seja utilizado apenas se o campo "código" existir e tiver conteúdo.

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/"> 
    <soap:Header/>  
    <so ap:Body> 
       <web:pedido>
          <#if codigo?? && codigo?has_content>
              <web:codigo><#if codigo gt 0 >${codigo}</#if></web:codigo>
          </#if>
       </web:pedido> 
    </soap:Body> 
</soap:Envelope>
```

**Saída do XML**\
Caso a condição seja verdadeira:

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\"> 
   <soap:Header/> 
       <soap:Body>     
          <web:pedido> 
              <web:codigo>213</web:codigo>  
          </web:pedido> 
       </soap:Body> 
</soap:Envelope>
```

Caso a condição seja falsa...

... e o campo "código" tenha um valor _null_, vazio ou não venha na entrada:

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\"> 
   <soap:Header/> 
       <soap:Body>     
          <web:pedido> 
          </web:pedido> 
       </soap:Body> 
</soap:Envelope
```

#### TRIM <a href="#trim" id="trim"></a>

Essa função é utilizada para remover os espaços em branco no começo e final de uma _string_.

**Sintaxe**

```
${SeuCampo?trim}
```

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode remover os espaços em branco no começo e final do campo "descrição".

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">

    <soap:Header/>  
    <soap:Body> 
       <web:pedido> 
           <web:descricao>${descricao?trim}</web:descricao> 
       </web:pedido> 
    </soap:Body> 
</soap:Envelope>
```

**Saída do XML**

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\"> 
    <soap:Header/> 
    <soap:Body>    
       <web:pedido> 
           <web:descricao>pedido teste</web:descricao>    
       </web:pedido> 
    </soap:Body> 
</soap:Envelope>
```

#### REPLACE <a href="#replace" id="replace"></a>

Essa função é utilizada para substituir um valor pré-determinado no campo.

**Sintaxe**

```
${SeuCampo?replace}
```

\


**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode substituir o valor "teste" em descrição por "prod".

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/"> 
    <soap:Header/>  
    <soap:Body> 
       <web:pedido> 
           <web:descricao>${descricao?replace("teste","prod")}</web:descricao> 
       </web:pedido> 
    </soap:Body> 
</soap:Envelope>
```

**Saída do XML**

```
<soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\">
     <soap:Header/>
     <soap:Body>
	   <web:pedido>
	       <web:descricao>   pedido prod   </web:descricao>
	   </web:pedido>
     </soap:Body>
</soap:Envelope>
```

#### SLICE (SUBSTRING) <a href="#slice-substring" id="slice-substring"></a>

Essa função é utilizada quando o campo é obrigado a ter um terminado tamanho.

**Sintaxe**

```
${SeuCampo[0..9]} 0 = valor inicial9 = valor final
```

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode determinar que o campo tenha apenas 10 caracteres, mesmo que o tamanho dele seja maior.

**IMPORTANTE:** uma boa prática aplicável à essa função é utilizar IF/ELSE para validar o tamanho desejado do campo. Dessa forma, você evita erros caso o campo seja menor do que o valor de corte.

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">
    <soap:Header/>
    <soap:Body>  
        <web:pedido>
            <#if descricao?length &lt; 10>       
                <web:descricao>${descricao}</web:descricao>
            <#else>
                <web:descricao>${descricao[0..9]}</web:descricao>
            </#if>
       </web:pedido>
    </soap:Body>
</soap:Envelope>
```

**Saída do XML**

```
<soap:Envelope
    xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\"
    xmlns:web=\"http://www.webservicex.net/\">   
    <soap:Header/>   
    <soap:Body>         
         <web:pedido>                           
             <web:descricao>   pedido </web:descricao>      
         </web:pedido>   
    </soap:Body>
</soap:Envelope>
```

#### LOCALE <a href="#locale" id="locale"></a>

Essa função é utilizada no _template_ para configurar a localização de um valor numérico.

**Sintaxe**

```
<#setting locale="en_US">${SeuCampo}<#setting locale="pt_BR">${SeuCampo}
```

Para poder utilizá-lo, você precisa passar a _tag_ antes do campo dinâmico. Veja como fazer isso nos exemplos abaixo.

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode formatar o valor para que ele fique no padrão do sistema legado.

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">     
    <soap:Header/>
    <soap:Body>
        <web:pedido>
            <#setting locale="en_US">
            <web:valor_US>${valor}</web:valor_US>
            <#setting locale="pt_BR">
            <web:valor_BR>${valor}</web:valor_BR>
        </web:pedido>
    </soap:Body>
</soap:Envelope>
```

**Saída do XML**

```
<soap:Envelope
	xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\"
	xmlns:web=\"http://www.webservicex.net/\"> 
	<soap:Header/>
	<soap:Body>       
		<web:pedido>                        
			<web:valor_US>4,513,423.13</web:valor_US>
			<web:valor_BR>4.513.423,13</web:valor_BR>   
		</web:pedido>    
	</soap:Body>
</soap:Envelope>
```

#### Customizado <a href="#customizado" id="customizado"></a>

Caso a formatação desejada não seja aceita pelo seu sistema, você pode definir a formatação necessária do número por meio da _tag "_number\_format". É ela que permite a tratativa personalizada do número.

**Sintaxe**

```
<#setting number_format="0.##">
${seuCampo}
```

**IMPORTANTE:** as _hashtag_ (#) definem a quantidade de casas decimais que serão utilizadas.

**Exemplo**

Utilizando a entrada informada no começo do artigo, você pode formatar o valor para que ele fique no padrão do sistema legado.

O que você deve passar no _template_ é:

```
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://www.webservicex.net/">     
    <soap:Header/>
    <soap:Body>
        <web:pedido>
            <#setting number_format="0.#">
            <web:valor_custom>${valor}</web:valor_custom>
            <#setting locale="pt_BR">
        </web:pedido>
    </soap:Body>
</soap:Envelope>

```

**Saída do XML**

```
<soap:Envelope  xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:web=\"http://www.webservicex.net/\">  
     <soap:Header/> 
     <soap:Body>     
          <web:pedido>                     
	       <web:valor_custom>4513423.1</web:valor_custom>     
	  </web:pedido> 
     </soap:Body> 
</soap:Envelope>
```

\
