---
description: Este guia descreve como configurar o uso da sua conta pessoal do Gmail.
---

# Utilizando sua conta Gmail com o componente de e-mail da Digibee (SMTP)

É bastante útil dispor da sua própria conta no Gmail para realizar envios através do componente de e-mail da Digibee, o SMTP.

{% hint style="info" %}
**IMPORTANTE:** a abordagem descrita não é recomendada para ambientes produtivos.
{% endhint %}

Leve em consideração que este artigo trata de um tipo de _account_ depreciado. Clique [aqui](../components/web-protocols/email-v2.md) para ler o artigo sobre o componente _**Email V2**_ e entender o novo modelo de envio de e-mail.

### Configurando a conta (_account_) <a href="#h_fc54f2134b" id="h_fc54f2134b"></a>

Insira as configurações de sua conta Gmail conforme imagem abaixo:

![](<../.gitbook/assets/img1 (3).png>)

* observe a configuração do nome da Conta (Label) e do tipo (Type);
* defina um nome para a conta que depois será utilizada pelo componente de e-mail;
* escolha o tipo _smtp-auth-and-properties_.

### Autorizando o Gmail <a href="#h_74cf14b45a" id="h_74cf14b45a"></a>

Envios são realizados através do SMTP, considerado pelo Gmail um canal menos seguro. Por isso, é preciso autorizar o Gmail a suportar aplicações não seguras.

Clique [aqui](https://support.google.com/accounts/answer/6010255?hl=pt-BR) para saber como autorizar o Gmail a suportar aplicações não seguras.



### Obtendo o link de autorização <a href="#h_a08765b7d7" id="h_a08765b7d7"></a>

É possível que o Gmail envie um link de autorização na primeira execução do componente de e-mail. Se isso acontecer, você receberá um erro na primeira execução do seu _pipeline_.

### Conta com duplo fator de autenticação <a href="#h_2100257aae" id="h_2100257aae"></a>

É recomendável que você utilize o duplo fator de autenticação na sua conta. Para isso, é necessário criar uma senha de aplicativo.

Clique [aqui](https://support.google.com/accounts/answer/185833?hl=pt-BR) para saber como criar uma senha de aplicativo.
