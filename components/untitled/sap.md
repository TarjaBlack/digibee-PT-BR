---
description: Conheça o componente e saiba como utilizá-lo.
---

# SAP

O **SAP** permite que você se conecte ao SAP (apenas RFC) para enviar requisições.

&#x20;  \
Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** é necessário criar uma conta tipo BASIC para utilizar as credenciais SAP (usuário e senha).
* **SAP Operation**: **** método de conexão no SAP - o componente suporta acesso via RFC ou IDOC.
* **Host:** _hostname_ do sistema SAP - para que "IP" e "Porta" sejam suportados, é necessário ter conectividade por VPN (você pode definir o VPN através do SAP GUI). Para resolver o nome do host para um endereço IP, você deve adicionar uma entrada de mapeamento ao arquivo do host da máquina na qual o agente está instalado.
* **RFC:** nome da RFC utilizado para se conectar ao sistema SAP - esse campo é informado pelo cliente (os parâmetros de importação da função do SAP devem ser mapeados).
* **Language:** linguagem a ser utilizada na conexão ao sistema SAP (ex.: "EN" para inglês).
* **Client ID:** SAP Client ID, normalmente com 3 dígitos, utilizado para se conectar ao SAP.
* **System Number**: normalmente com 2 dígitos, utilizado para se conectar ao sistema SAP (você pode encontrar essa informação no SAP GUI).
* **Template (XML):** _template_ Apache FreeMarker para a mensagem SOAP enviada na requisição.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

&#x20;  \
Recomendamos que você configure GLOBALS para o AMBIENTE SAP, conforme o exemplo a seguir:

* Globals:
* environment = Ambiente SAP\
  &#x20;  &#x20;

Veja o exemplo dos itens listados abaixo, que devem ser substituídos de acordo com sua necessidade:

* \[rfc] = Nome da RFC
* \[table] = Tabela relacionada a RFC
* \[columns] = Colunas da Tabela

&#x20;   Para mais informações sobre conectividade relacionadas ao SAP, leia o [artigo](https://docs.digibee.com/documentation/build/capsulas/public-capsules/sap-collection#h\_16dfe961b3).&#x20;

### RECOMENDAÇÃO DE USO <a href="#recomendao-de-uso" id="recomendao-de-uso"></a>

#### Estrutura do componente para conexões RFC <a href="#estrutura-do-componente-para-conexes-rfc" id="estrutura-do-componente-para-conexes-rfc"></a>

Para conexões RFC, utilize a cápsula "SAP Json to RFC" antes do componente SAP. Com isso, a chamada já é transformada no formato esperado pelo SAP. Segue abaixo um exemplo de sintaxe de chamada RFC dentro do SAP:\
&#x20;     &#x20;

_**Chamada da função (RFC) BAPI\_BUPA\_ADDRESS\_GETDETAIL dentro do componente JSON Generator**_

```
{
  "sid": "{{sap-test-sid}}",
  "rfc": "BAPI_BUPA_ADDRESS_GETDETAIL",
  "importParameters": {
    "attributes": {
      "BUSINESSPARTNER": {{ message.BUSINESSPARTNER }},
      "VALID_DATE": {{FORMATDATE(NOW(), "timestamp", "yyyy-MM-dd", null , "GMT-3") }}
    }
  }
```

&#x20;      \
Para uma chamada RFC, é importante dar atenção aos seguintes pontos:

* sempre informar o Sid - campo **Enviroment/SystemName/System Id** mencionado anteriormente.
* Campo RFC -  pode constar tanto no arquivo JSON, quanto ser informado dentro do componente.&#x20;
* importParameters - chamada da função dentro do SAP. Especifique apenas os campos que devem ser preenchidos na chamada.

&#x20;       &#x20;

#### Sobre o SAP IDOC              <a href="#sobre-o-sap-idoc" id="sobre-o-sap-idoc"></a>

* **IDOC:** significa _Intermediate Document_
* **IDOC Type:** possui estrutura específica, que coloca em sequência os dados transferidos de um sistema para outro.
* **IDOC TYPE EXTENSION (opcional):** especifica o tipo de extensão IDOC, caso exista, de um IDOC produzido por esse _endpoint_.
* **SYSTEM RELEASE (opcional):** especifica o SAP Basis Release associado, caso exista, a um IDOC produzido por esse _endpoint_.
* **APPLICATION RELEASE (opcional):** especifica o Application Release associado, caso exista, a um IDOC produzido por esse _endpoint_.&#x20;

{% hint style="info" %}
**IMPORTANTE:** Lembre-se que IDOCs são processados assincronamente via SAP. Quando um IDOC é enviado, não há indicação de sucesso ou falha. Em caso de erro, é necessário que o usuário reprocesse o IDOC.
{% endhint %}

### Estrutura do componente para utilização do campo Template XML       <a href="#estrutura-do-componente-para-utilizao-do-campo-template-xml" id="estrutura-do-componente-para-utilizao-do-campo-template-xml"></a>

Veja um exemplo de _template_ (XML):

```
<?xml version="1.0" encoding="ASCII"?>
<idoc:Document
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:FLCUSTOMER_CREATEFROMDATA01---="http://sap.fusesource.org/idoc/{_YOUR_ENVIRONMENT_}/FLCUSTOMER_CREATEFROMDATA01///"
    xmlns:idoc="http://sap.fusesource.org/idoc"
    creationDate="2015-01-28T12:39:13.980-0500"
    creationTime="2015-01-28T12:39:13.980-0500"
    iDocType="FLCUSTOMER_CREATEFROMDATA01"
    iDocTypeExtension=""
    messageType="FLCUSTOMER_CREATEFROMDATA"
    recipientPartnerNumber="QUICKCLNT"
    recipientPartnerType="LS"
    senderPartnerNumber="QUICKSTART"
    senderPartnerType="LS">
  <rootSegment xsi:type="FLCUSTOMER_CREATEFROMDATA01---:ROOT" document="/">
    <segmentChildren parent="//@rootSegment">
      <E1SCU_CRE parent="//@rootSegment" document="/">
        <segmentChildren parent="//@rootSegment/@segmentChildren/@E1SCU_CRE.0">
          <E1BPSCUNEW parent="//@rootSegment/@segmentChildren/@E1SCU_CRE.0"
              document="/"
              CUSTNAME="Fred Flintstone" FORM="Mr."
              STREET="123 Rubble Lane"
              POSTCODE="01234"
              CITY="Bedrock"
              COUNTR="US"
              PHONE="800-555-1212"
              EMAIL="fred@bedrock.com"
              CUSTTYPE="P"
              DISCOUNT="005"
              LANGU="E"/>
        </segmentChildren>
      </E1SCU_CRE>
    </segmentChildren>
  </rootSegment>
</idoc:Document>
```

{% hint style="info" %}
**Importante:** {_YOUR\_ENVIRONMENT_} deve ser substituído pelo seu SAP SID.
{% endhint %}

\
Caso seja uma consulta única, você pode utilizar a seguinte sintaxe:\
&#x20;       &#x20;

_**Elementary fields/Import Parameters**_

```
<?xml version="1.0" encoding="ASCII"?>
<[rfc]:Request 
   xmlns:[rfc]="http://sap.fusesource.org/rfc/{{global.environment}}/[rfc]" 
   [columns]="20180801" 
   [columns]="20180806" 
   [columns]="050" />
   
EXEMPLO:

<?xml version="1.0" encoding="ASCII"?>
<ABCD_RFC_ORDEM_FATURA:Request 
   xmlns:ABCD_RFC_ORDEM_FATURA="http://sap.fusesource.org/rfc/QAS/ABCD_RFC_ORDEM_FATURA" 
   P_ERDAT_INI="2018-07-01T00:00:00.000" 
   P_ERDAT_FIM="2018-08-01T00:00:00.000" 
   CLIENTE="" 
   VKORG="0010" 
   AUART="" />    
```

Caso seja uma consulta a uma tabela, utilize a seguinte sintaxe:&#x20;

_**Table fields**_

```
<?xml version="1.0" encoding="ASCII"?>
<[rfc]:Request ">xmlns:[rfc]="http://sap.fusesource.org/rfc/{{global.environment}}/[rfc]">
 <[table]>
  <row>
   <[columns]>${VBELN}</[columns]>
   <[columns]>${ABDC}</[columns]>
  </row>
 </[table]>
</[rfc]:Request>
```

**Exemplo:**

```
<?xml version="1.0" encoding="ASCII"?>
<ABCD_RFC_MATERIAIS:Request ">xmlns:ABCD_RFC_MATERIAIS:Request="http://sap.fusesource.org/rfc/{{global.environment}}/ABCD_RFC_MATERIAIS:Request">
 <T_TIPO>
  <row>
   <MTART>${type}</MTART>
  </row>
 </T_TIPO>
</ABCD_RFC_MATERIAIS:Request>
```

\
**Entrada**

```
{  
    "body":{    
        "type": "S"  
    }
}
```

&#x20;

* **${type}:** variável que deve ser passada dentro de uma tag "body".

\
Para a variável _**sapRequestTemplate**_, é importante dar atenção aos seguintes pontos:

* o nome da variável pode conter sinal de menos (-), ponto (.), e dois pontos (:) em qualquer posição. Mas esses caracteres precisam ser escapados com _backslash_ (\\). Do contrário, eles serão interpretados como operadores.
* Caso seja necessário, trabalhe com substituição de números:

```
<#assign x=42>
${x}
${x?string} <#-- o mesmo que ${x} -->
${x?string.number}
${x?string.currency}
${x?string.percent}
${x?string.computer}
```

\
**Saída**

```
42
42
42
$42.00
4,200%
42
```

### Fluxo de Mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

#### Entrada <a href="#entrada" id="entrada"></a>

O componente espera uma mensagem em qualquer formato. Porém, ele vai procurar por um caminho dentro da propriedade de configuração "modelPath".

#### Saída <a href="#sada" id="sada"></a>

A mensagem de saída será igual à mensagem de entrada, mas substituindo a propriedade do modelo conforme definida pelo _template_ (como uma _string_). Caso ocorra um erro, a propridade "property\_error" será criada no mesmo nível da propriedade original.

&#x20; &#x20;
