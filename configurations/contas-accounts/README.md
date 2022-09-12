---
description: Saiba o que são e como utilizá-las.
---

# Contas (Accounts)

## Contas (Accounts) <a href="#contas-accounts" id="contas-accounts"></a>

Sempre que você precisar utilizar alguma senha, chave privada, _token_ de autenticação, entre outros, recomendamos muito que você recorra a uma conta cadastrada na Plataforma. Assim, os seus dados são criptografados e não ficam expostos durante a execução da integração.

## Tipos de Contas <a href="#tipos-de-contas" id="tipos-de-contas"></a>

### **Basic** <a href="#basic" id="basic"></a>

Recorra a esse tipo de conta quando você utilizar um componente ou serviço que necessite de uma autenticação de usuário/senha.

* **USERNAME:** nome do usuário
* **PASSWORD:** senha

### Custom Auth Header <a href="#custom-auth-header" id="custom-auth-header"></a>

Recorra a esse tipo de conta caso algum _endpoint_ necessite de um _header_ customizado de autenticação.

* **HEADER-NAME:** nome do _header_
* **HEADER-VALUE:** o valor do _header_

### OAuth Bearer <a href="#oauth-bearer" id="oauth-bearer"></a>

Recorra a esse tipo de conta quando precisar armazenar um _token_ do tipo OAuth. O _token_ será atribuído ao parâmetro "Authorization" no _header_ de requisição.

* **TOKEN:** o _token_ OAuth

### Private Key <a href="#private-key" id="private-key"></a>

Tipo de conta que armazena uma chave privada.

**Exemplo:**

```
-----BEGIN RSA PRIVATE KEY-----
MIICWwIBAAKBgF2duc4+xxNKlMO9bUud4bzGnuATkQVX3bM/gzxISrgw7B1AzJwA
OT5UChBoIKfmISaaVVY9+/fTpI1szihSqTyemdHnbC+FcDzoK3p53C5ZJ4pL7s+G
Y7vGEa2Z/6JVder6dwJaaOtwf+DfZYiWQjvh8tfAVjVdONE/XZSxOOofAgMBAAEC
-----END RSA PRIVATE KEY-----
```

* **KEY:** chave privada
* **PASSPHRASE:** senha da chave privada

### Public Key <a href="#public-key" id="public-key"></a>

Esse tipo de conta armazena uma chave pública.

**Exemplo:**

```
-----BEGIN PUBLIC KEY-----
MIGeMA0GCSqGSIb3DQEBAQUAA4GMADCBiAKBgF2duc4+xxNKlMO9bUud4bzGnuAT
kQVX3bM/gzxISrgw7B1AzJwAOT5UChBoIKfmISaaVVY9+/fTpI1szihSqTyemdHn
-----END PUBLIC KEY-----
```

* **KEY:** chave pública

### Certificate Chain <a href="#certificate-chain" id="certificate-chain"></a>

Configura uma cadeia de certificados. Utilizada para _endpoints_ que necessitam de autenticação _2 way SSL_ ou de um certificado do lado cliente. A cadeia de certificado deve ser passada na ordem correta, e no formato pem.

Para converter sua chave, você pode fazer através do OpenSSL via linha de comando, Ex: **openssl pkcs12 -in mycert\_xpto.p12 -out myapp.pem**

Exemplo:

```
-----BEGIN CERTIFICATE-----
MIIEUTCCAzmgAwIBAgIBATANBgkqhkiG9w0BAQUFADBSMQswCQYDVQQGEwJVUzEj
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIEUTCCAAGVDSHVEbjhdbhjsjeiejAQUFADBSMQswCQYDVQQGEwJVUzEj
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
MIICWwIBAAKBgF2duc4+xxNKlMO9bUud4bzGnuATkQVX3bM/gzxISrgw7B1AzJwA
-----END RSA PRIVATE KEY-----
```

* **CHAIN:** cadeia de certificados completa
* **PASSWORD:** senha da chave privada, caso necessário

### Google Key <a href="#google-key" id="google-key"></a>

Chave de serviço para acessar APIs do Google.

**Exemplo:**

```
{
"type": "service_account",
"project_id": "project_id",
"private_key_id": "dfdsfrfr43r43r4refbcceceabf8055a12a",
"private_key": "-----BEGIN PRIVATE KEY-----\n-----END PRIVATE KEY-----\n",
"client_email": "user@DOMAIN.iam.gserviceaccount.com",
"client_id": "123456576788888899",
"auth_uri": "https://accounts.google.com/o/oauth2/auth",
"token_uri": "https://accounts.google.com/o/oauth2/token",
"auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
"client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/storage%40project.iam.gserviceaccount.com"
}
```

* **KEY:** chave do Google
* **SCOPES:** escopos necessários para acessar determinada API (separados por vírgula). Para saber mais sobre escopos do Google, clique [aqui](https://developers.google.com/identity/protocols/oauth2/scopes).

### Kerberos <a href="#kerberos" id="kerberos"></a>

Conta que armazena a _Keytab_ para autenticações em ambientes que utilizam Kerberos.

* **KEYTAB:** base64 do arquivo _Keytab_
* **PRINCIPAL:** usuário dessa _Keytab_ (ex.: user@DOMAIN)

### SMTP Auth And Properties <a href="#smtp-auth-and-properties" id="smtp-auth-and-properties"></a>

Conta utilizada somente para o Mail Connector. Ela configura os dados de acesso ao servidor SMTP para envio de e-mail.

* **HOST:** nome do _host_ do servidor SMTP
* **PORT:** porta de acesso ao servidor SMTP
* **USERNAME:** e-mail do usuário
* **PASSWORD:** senha do e-mail
* **STARTTLS\_ENABLE:** valores “true” ou “false” - se “true”, o acesso será via SSL.
* **AUTH:** tipo de autenticação do servidor de e-mail

### OAuth 2 <a href="#oauth-2" id="oauth-2"></a>

OAuth é um padrão aberto para autorização, comumente utilizado para permitir que os usuários da Internet possam fazer _logon_ em sites de terceiros usando as suas contas do Google, Microsoft, etc. sem expor as senhas. OAuth lhes fornece um "acesso seguro delegado" aos recursos do servidor em nome do proprietário do recurso.

* **PROVEDOR:** provedor OAuth
* **SCOPES:** escopos de acesso do OAuth

Suportamos os seguintes provedores:

* **Microsoft**: é obrigatório o escopo "offline\_access" para utilização na Plataforma Digibee. Também é importante lembrar que esse provedor aceita apenas contas pessoais.
* **Google**
* **Mercado Livre**

### Secret Key <a href="#secret-key" id="secret-key"></a>

Chave secreta utilizada para componentes de criptografia.

* **KEY:** chave secreta

### API Key <a href="#api-key" id="api-key"></a>

Conta que configura uma API Key para ser utilizada em _endpoints_ que necessitam de uma API Key.

* **URL-PARAM-NAME:** nome do _query parameter_ em que a API Key configurada será utilizada
* **API-KEY:** valor da API Key a ser utilizada

**IMPORTANTE**: os provedores abaixo têm um prazo de expiração para seu token de autenticação. Com isso, é necessário atualizar as configurações de suas contas conforme o prazo previsto por eles.

Microsoft - 3 meses\
Google - 6 meses\
Mercado Livre - 6 meses
