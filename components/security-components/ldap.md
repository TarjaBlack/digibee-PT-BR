---
description: Conheça o componente e saiba como utilizá-lo.
---

# LDAP

O _**LDAP**_ realiza operações em um servidor LDAP.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **Operation:** comando a ser acionado (Add, Delete ou Modify).
* **Search Operation:** operação de busca (Object, One level ou Sub trees).
* **Host Name:** nome ou IP do servidor LDAP.
* **Port:** porta do LDAP.
* **Authentication DN:** Distinguished Name (DN) utilizado para conectar o servidor LDAP.
* **Filter:** expressões de filtros.
* **SSL:** protocolo de segurança.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

{% hint style="info" %}
**IMPORTANTE**: o parâmetro **Authentication DN** deve ser configurado com o _path_ completo até o usuário desejado. Com isso, se o **Distinguished Name** for igual a "CN=UserExample,OU=FOLDER1,DC=abc,DC=com,DC=br", o parâmetro Authentication DN ficará configurado com "OU=FOLDER1,DC=abc,DC=com,DC=br". A configuração "CN=UserExample" deve ser utilizada no _username ****_ do _account_ configurado no componente, ou seja, _username_ recebe o valor "UserExample".
{% endhint %}

## LDAP em Ação <a href="#h_b135e18bed" id="h_b135e18bed"></a>

Você pode:

\- utilizar um valor fixo:

_**(dnOperation = "ou=system,cn=users")**_

\- conseguir algum JSON da mensagem, que vai buscar o objeto 'data' da mensagem:

_**(dnOperation = "\{{ message.$.dn \}}**_

\- combinar ambos os exemplos:

_**(dnOperation = " ou=\{{ message.$.dn \}}")**_

* **searchOperation:** integra entre 0 e 2 utilizado para buscar, sendo:

0 -> Base Object

1 -> One Level

2 -> Full Subtree

* **modifyOperation:** integra entre 0 e 3 utilizado para alterar, sendo:

0 -> Adicionar atributo

1 -> Excluir atributo

2 -> Substituir atributo

3 -> Incrementar atributo

* **filter:** filtra configurações para a mesma operação de busca.

Exemplo: filtro "(objectClass=)"

Você pode:

\- utilizar um valor fixo:

filtro = ("objectClass=)"

\- conseguir algum JSON da mensagem, que vai buscar o objeto 'data' da mensagem:

filtro = "\{{ message.$.filter \}}

\- combinar ambos os exemplos:

filtro = "objectClass=\{{ message.$.filter \}}"

* **entries:** o objeto utilizado para adicionar ou alterar as entradas no servidor LDAP.

Você pode:

\- utilizar um valor fixo:

_**filtro = ("objectClass":\["top","person"],"cn":"test\_ad","sn":"test\_sn"}**_

\- conseguir algum JSON da mensagem, que vai buscar o objeto 'data' da mensagem:

_**entries = "\{{ message.$.entries \}}**_

\- combinar ambos os exemplos:

_**entries = {"objectClass":\["top","person"],"cn":"\{{ message.$.entries \}}","sn":"test\_sn"}"**_

* **operation:** a operação que você deseja executar no servidor LDAP: BUSCAR / ADICIONAR / ALTERAR / EXCLUIR
* **useSsl:** se verdadeiro, será conectado utilizando SSL (conexão segura); do contrário, não será conectado
* **failOnError:** se verdadeiro, um erro vai suspender a execução do pipeline

O _**LDAP**_ precisa de autenticação. Para isso, você deve criar uma conta com privilégios de administrador (tipo BASIC) e utilizá-la no componente.

**IMPORTANTE**: o _username_ a ser utilizado no _account_ deve ser o campo "name" configurado no servidor LDAP.

Para converter _Double Braces_, nós utilizamos especificações de JSON Path. Clique [aqui](https://github.com/json-path/JsonPath) para saber mais.

## Fluxo de Mensagens <a href="#h_96698bc8c4" id="h_96698bc8c4"></a>

### Operação SEARCH <a href="#h_019ef5a604" id="h_019ef5a604"></a>

#### **Entrada**

```
{
"type": "connector",
"name": "ldap-connector",
"accountLabel": "ldap",
"stepName": "ldap",
"params": {
"operation": "SEARCH",
"host": "LDAP_IP",
"port": 389,
"dnAuthentication": "DC=digibee,DC=io",
"dnOperation": "DC=digibee,DC=io",
"filter": "(objectClass=)",
"searchOperation": 0,
"useSsl": false,
"failOnError": false
}
}
```

#### **Saída**

```
{
"result": [
{
"pwdhistorylength": "24"
},
{
"msds-alluserstrustquota": "1000"
},
{
"otherwellknownobjects": [
"B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN=Keys,DC=digibee,DC=io",
"B:32:1EB93889E40C45DF9F0C64D23BBB6237:CN=Managed Service Accounts,DC=digibee,DC=io"
]
}
]
}
```

### Operação ADD <a href="#h_ee7e46186d" id="h_ee7e46186d"></a>

#### **Entrada**

```
{
"type": "connector",
"name": "ldap-connector",
"accountLabel": "ldap",
"stepName": "ldap",
"params": {
"operation": "ADD",
"host": "LDAP_IP",
"port": 389,
"dnAuthentication": "DC=digibee,DC=io",
"entries": "{{ message.$.entries }}",
"dnOperation": "DC=digibee,DC=io",
"useSsl": false,
"failOnError": false
}
}
```

#### **Payload**

```
{"entries": {
"objectClass": ["top", "person"],
"cn": "test_ad",
"sn": "test_sn"

}
}
```

#### **Saída**

```
{
"message": "Entry added successfully",
"success": true
}
```

### Operação MODIFY <a href="#h_00ac903a0c" id="h_00ac903a0c"></a>

#### **Entrada**

```
{
"type": "connector",
"name": "ldap-connector",
"accountLabel": "ldap",
"stepName": "ldap",
"params": {
"operation": "MODIFY",
"host": "LDAP_IP",
"port": 389,
"dnAuthentication": "DC=digibee,DC=io",
"entries": "{{ message.$.entries }}",
"dnOperation": "DC=digibee,DC=io",
"modifyOperation": 0,
"useSsl": false,
"failOnError": false
}
}
```

#### **Payload**

```
{"entries": {
"objectClass": ["top", "person"],
"cn": "test_ad",
"sn": "test_sn"

}
}
```

#### **Saída**

```
{
"message": "Entry modified successfully",
"success": true
}
```

### Operação DELETE <a href="#h_8844a54707" id="h_8844a54707"></a>

#### **Entrada**

```
{
"type": "connector",
"name": "ldap-connector",
"accountLabel": "ldap",
"stepName": "ldap",
"params": {
"operation": "DELETE",
"host": "LDAP_IP",
"port": 389,
"dnAuthentication": "DC=digibee,DC=io",
"dnOperation": "DC=digibee,DC=io",
"useSsl": false,
"failOnError": false
}
}
```

#### **Saída**

```
{
"message": "Entry modified successfully",
"success": true
}
```

O _**LDAP**_ suporta _Double Braces_ estáticos nos seguintes parâmetros previamente especificados:

* operation
* host
* dnAuthentication
* port
* modifyOperation
* searchOperation
* useSsl

[Para ler o nosso artigo sobre _Double Braces_, clique aqui.](https://docs.digibee.com/documentation/v/pt-br/build/double-braces)
