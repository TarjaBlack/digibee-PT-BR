---
description: Conheça o componente e saiba como utilizá-lo.
---

# Email V1

O **Email V1** invoca o servidor SMTP em um _pipeline_.

\
Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** conta a ser utilizada pelo componente.
* **From:** configura o e-mail remetente a ser enviado pelo componente.

```
example@examplo.com.br
```

* **Subject:** configura o assunto a ser enviado pelo componente.

```
Example: ${subject}
```

* **Content Type:** configura o _Content Type_ e a codificação.

```
text/html; charset=UTF-8
```

* **Template:** _template body_ que pode ser utilizado para preparar _templates_ de e-mail (em HTML).

```
<html><body><strong>${firstname} ${lastname}</strong></body></html>
```

{% hint style="info" %}
**IMPORTANTE:** para poder utilizar o **Email V1** , você precisa criar uma _account_ do tipo SMTP.
{% endhint %}

Fluxo de Mensagens\
Entrada <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>
------------------------------------------------------------------

O componente espera uma mensagem no seguinte formato:

```
{
    to  : ["abc1@gmail.com","abc2@gmail.com"]
    cc  : ["abc1@gmail.com","abc2@gmail.com"],
    bcc : ["abc1@gmail.com","abc2@gmail.com"],
	   params: { 
                     // Template body replacement parameters
			"paramA":"valueA",
			"paramB":"valueB",
			...
			"paramN":"valueN"
		}
}
```

### Saída <a href="#sada" id="sada"></a>

Quando ocorre um erro, esta é a mensagem que é mostrada na saída do componente:

```
{
    timestamp: 1503608693745,
    code: 999,
    message:  "error message"
}
```

\
Note que, para alguns erros, _body_ e _header_ estão indisponíveis.

Para ler um tutorial de utilização do _**Email V1**_, clique [aqui](email-v1-exemplos-de-uso.md).
