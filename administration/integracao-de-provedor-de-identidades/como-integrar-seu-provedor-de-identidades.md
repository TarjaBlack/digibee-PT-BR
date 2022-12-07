---
description: >-
  Veja aqui o passo a passo para integrar o seu provedor de identidade à Digibee
  Integration Platform.
---

# Como integrar seu provedor de identidades

Uma vez confirmado que seu provedor de identidade é compatível com o protocolo SAML 2.0, já será possível iniciar os passos para integrá-lo à Digibee Integration Platform. Com a conclusão da integração, a habilitação da autenticação integrada e a funcionalidade de Integração de Grupos, que possibilita a autorização federada ao Realm, já estarão disponíveis.

A funcionalidade Integração de Provedor de Identidade também suporta a integração para múltiplos _realms_ na Digibee Integration Platform para o mesmo provedor de identidade, isto é, habilitar o logon único para todos os _realms_ (do mesmo cliente) simultaneamente a partir de uma única integração.

**IMPORTANTE:** essa capacidade está disponível apenas para _realms_ existentes na mesma regiões, clusters e instalação.

Para saber mais sobre o que é um provedor de identidade e as vantagens de integrá-lo a Digibee Integration Platform, leia nosso[ artigo](./).

## **Como integrar um realm à Digibee Integration Platform**

### **1.Solicitar a integração do IdP à plataforma**

Para iniciar o processo de integração, o primeiro passo é fazer a solicitação da intenção para a Digibee. É possível fazer isso de duas formas:

* Solicitar ao time de suporte através do chat da Digibee HIP ou por e-mail suporte@digibee.com;
* Mediante o seu ponto de contato no time de Customer Service Management (CSM);

**IMPORTANTE:** caso haja o interesse em integrar mais de um _realm_ ao mesmo IdP, basta informar para a Digibee nesta etapa.

### **2.Enviar informações essenciais para a integração**

Na solicitação da integração é necessário informar as chaves dos endpoints SAML 2.0. É possível enviar um arquivo XML com o conteúdo ou a URL do XML.

Caso tenha alguma dúvida, segue um exemplo de URL que poderá ser enviado:

**https://login.microsoftonline.com/\{{UUID\}}/FederationMetadata/2007-0 6/FederationMetadata.xml.**

**IMPORTANTE:** Existem casos de ADFS que são segmentados e, se aplicável, é importante informar junto a URL de metadata o appid correspondente, no seguinte formato:

**“…Federationmetadata.xml?appid=2a954093-fd61-469d-861e-704236a96bd5”**

### **3.Configurar ambiente SAML 2.0 do provedor de identidades**

Após receber os endpoints e realizar as devidas configurações internas, a Digibee envia uma nova URL com o nome da empresa solicitante e alguns dados extras para que seja configurado o próprio ambiente SAML V2 do provedor de identidade:

* **URL do Assertion Consumer Service (ACS):** conhecido como URL de retorno (callback) e que tem o seguinte formato: **https://{cliente}.auth.godigibee.io/samlv2/acs**
* **Issuer:** também conhecido como entityId do provedor de serviço: e possui a seguinte forma: **https://{cliente}.auth.godigibee.io/samlv2/sp/\{{UUID\}}**
* **Metadata URL:** identifica os atores envolvidos em vários perfis, tal como o SSO do provedor de identidade e do provedor de serviço: **... https://{cliente}.auth.godigibee.io/samlv2/sp/metadata/\{{UUID\}}**

### **4.Confirmar dados do Firewall**

Logo em seguida, será essencial realizar a configuração dos endpoints enviados pela Digibee e, se necessário, liberar regras de Firewall para os endpoints.

**IMPORTANTE:** Verifique com o seu time de segurança se há algum tipo de restrição de acesso às URLs fornecidas pela Digibee.

### **5.Validar ambiente**

Uma vez que todas as configurações foram realizadas, o acesso a Digibee Integration Platform por este fluxo de integração, deverá ser realizado através da URL fornecida pela Digibee que possui o seguinte formato:

**"https://{cliente}.auth.godigibee.io/oauth2/authorize?client\_id={cliente-id}\&response\_type=code\&redirect\_uri=%2Flogin"**

Por fim, o cliente valida o ambiente e o libera para os usuários, desde que as regras de conformidade tenham sido seguidas.
