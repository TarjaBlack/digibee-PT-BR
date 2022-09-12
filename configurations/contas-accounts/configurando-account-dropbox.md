---
description: Aprenda como configurar o Dropbox Connector.
---

# Configurando Account Dropbox

### Obtendo um access token <a href="#obtendo-um-access-token" id="obtendo-um-access-token"></a>

A autenticação no Dropbox é feita através de _access token._

Acesse [https://www.dropbox.com/developers/apps](https://www.dropbox.com/developers/apps).\
Clique em "Create app", selecione um dos tipos de API, um dos tipos de acesso e o nome do seu app:

![](<../../.gitbook/assets/01 (19).png>)

![](<../../.gitbook/assets/02 (4).png>)

Feito isso, ao clicar em "Create app" você será redirecionado à página de configurações do seu novo app:

![](<../../.gitbook/assets/03 (13).png>)

![](<../../.gitbook/assets/04 (14).png>)

Clicando em "Generate" na seção "OAuth 2", você obterá seu _access token:_

![](<../../.gitbook/assets/05 (8).png>)

Agora_,_ na plataforma, precisamos criar um _Account_ com o tipo de conta "oauth-bearer" e inserir o _access token_ gerado:

![](<../../.gitbook/assets/06 (2).png>)

Pronto, temos nosso _access token_ configurado e nossa _account_ criada e pronta para uso no Dropbox Connector:

![](<../../.gitbook/assets/07 (4).png>)
