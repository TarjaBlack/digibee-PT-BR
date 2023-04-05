---
description: Conheça o componente e saiba como utilizá-lo.
---

# Email V2

O _**Email V2**_ permite o envio de emails simples, no formato HTML ou até mesmo contendo anexos.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** necessário para o componente fazer a autenticação ao servidor de email a ser utilizado no envio, caso esse serviço de email seja requisitado na autenticação. Deve-se selecionar a conta do tipo BASIC.
* **SMTP Host:** _host_ SMTP do servidor de email. Ex.: (GMail: smtp.gmail.com).
* **SMTP Port:** porta SMTP do servidor de email. Geralmente utiliza-se a porta 587, mas pode haver variação dependendo do servidor de email utilizado.
* **From:** remetente do email.
* **To:** destinatários do email. Caso existam múltiplos destinatários, eles devem ser separados por vírgula. Ex: a@a.com,b@b.com,....
* **CC:** destinatários que receberão a cópia do email. Caso existam múltiplos destinatários, eles devem ser separados por vírgula. Ex: a@a.com,b@b.com,....
* **BCC:** destinatários que receberão a cópia oculta do email. Caso existam múltiplos destinatários, eles devem ser separados por vírgula. Ex: a@a.com,b@b.com,....
* **Content:** corpo do email. Aceita o uso de _templates_ Freemarker para a geração de HTML dinâmicos.
* **Charset:** _charset_ que será utilizado no envio do corpo do email.
* **Subject:** assunto do email.
* **Authenticated:** se a opção estiver habilitada, é obrigatório passar uma conta com email e senha a serem utilizados para autenticação. Se os envios não precisarem de autenticação, a opção deve ficar desabilitada.
* **Is Over SSL:** se a opção estiver habilitada, o envio é feito via SSL.
* **SSL Port:** se a opção _**Is Over SSL**_ estiver habilitada, então é obrigatório informar qual porta será utilizada para trafegar a mensagem via SSL.
* **Is Over TLS:** se a opção estiver habilitada, o envio é feito via TLS.
* **Force TLSv1.2:** define como obrigatória a conexão com o protocolo TLSv1.2.
* **Use Attachment As Raw**: se a opção estiver habilitada, o formulário para adicionar anexos será ocultado e o envio em modo RAW poderá ser utilizado, por meio do qual você informa o _array_ de anexos. Mas se a opção estiver desabilitada, será utilizada a abordagem do formulário para a especificação de anexos.
* **Attachments**: anexos da mensagem. A especificação ocorre via formulário.

{% hint style="info" %}
**IMPORTANTE**: para adicionar imagens dentro do corpo do email, deve ser informado o prefixo "cid:" antes do nome da imagem. Ex.: \<img src"cid: image.png" />
{% endhint %}

* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "_success_".

## Fluxo de mensagens <a href="#fluxo-de-mensagens" id="fluxo-de-mensagens"></a>

### Entrada <a href="#entrada" id="entrada"></a>

Esse componente não espera nenhuma mensagem de entrada específica, somente se for informada uma expressão em _Double Braces_ em algum dos seus campos.

### Saída <a href="#sada" id="sada"></a>

Ao executar um componente _**Email V2**_, a seguinte estrutura de JSON será gerada:

```
{
    "from": "a@a.com",
    "to": "a@a.com,a@a.com.br",
    "cc":"a@a.com,a@a.com.br",
    "bcc": "a@a.com,a@a.com.br",
    "subject": "Subject",
    "content": "<html>Test Email!</html>",
    "charset": "UTF-8",
    "success": true,
    "attachments": [{
        "type": "ATTACHMENT",
        "attachment": "attachment.extension"
    }]
}
```

* **from:** remetente.
* **to:** destinatários.
* **cc:** destinatários em cópia.
* **bcc:** destinatários em cópia oculta.
* **subject:** assunto.
* **content:** corpo da mensagem. Caso o corpo da mensagem exceda 256 caracteres, esse resultado será truncado.
* **charset:** _charset._
* **success:** se a chamada foi bem sucedida.
* **attachments:** _array_ contendo os anexos enviados.

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.
{% endhint %}

Para entender melhor o fluxo das mensagens na Digibee Integration Platform, leia o artigo sobre [Processamento de mensagens](../../build/pipelines/processamento-de-mensagens.md).

## Email V2 em Ação <a href="#email-v2-em-ao" id="email-v2-em-ao"></a>

Veja abaixo como o componente se comporta em determinada situação e a sua respectiva configuração.

### Enviando um arquivo de texto (xpto.txt) como anexo em modo RAW e o corpo do email contendo imagens também <a href="#enviando-um-arquivo-de-texto-xptotxt-como-anexo-em-modo-raw-e-o-corpo-do-email-contendo-imagens-tamb" id="enviando-um-arquivo-de-texto-xptotxt-como-anexo-em-modo-raw-e-o-corpo-do-email-contendo-imagens-tamb"></a>

* **SMTP Host:** smtp.gmail.com
* **SMTP Port:** 587
* **From:** [email@gmail.com](mailto:email@gmail.com) (esse email deve ser o mesmo configurado na conta especificada neste componente)
* **To:** [some\_other\_email@gmail.com](mailto:some\_other\_email@gmail.com),[second\_email@gmail.com](mailto:second\_email@gmail.com)
* **Subject:** Hello
* **Content:**

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
 <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <title>Demystifying Email Design</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
</head>
<body>
<img src="cid:myImage.png" />
</body>
</html>
```

* **Authenticated:** habilitado
* **Is Over TLS:** habilitado
* **Attachment As Raw:** habilitado
* **Attachments:**

```
[
{"type": "INLINE", "attachment": "myImage.png" },
{"type": "ATTACHMENT", "attachment": "xpto.txt" }
]
```

O resultado será:

```
{
    "from": "email@gmail.com",
    "to": "some_other_email@gmail.com,second_email@gmail.com",
    "cc":"",
    "bcc": "",
    "subject": "Hello",
    "content": "<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"><html xmlns="http://www.w3.org/1999/xhtml"> <head> <meta http-equiv ...TRUNCATED",
    "charset": "UTF-8",
    "success": true,
    "attachments": [
        {"type": "INLINE", "attachment": "myImage.png" },
        {"type": "ATTACHMENT", "attachment": "xpto.txt" }
    ]
}
```

Veja como passar valores de forma dinâmica usando o conector:

![](<../../.gitbook/assets/ezgif.com-gif-maker (20) (1).gif>)

Neste exemplo de uso dinâmico, passamos variáveis indicando a emissão de notas fiscais `<a href='${NF}' com uma segunda variável indicando o vencimento ${M_VENC}.`

```
<!DOCTYPE html>
<html>
<head>
 </head>
<body>
 
Boa tarde, <br/>
Segue a nota fiscal <a href='${NF}'>(Clique aqui)</a> referente a mensalidade de licenciamento da plataforma – com vencimento para <b> ${M_VENC}</b>. <br/>
O pagamento será via <b>transferência bancária</b> - dados no corpo da nota fiscal.   <br/><br/>


Por favor, confirmar o recebimento. <br/>
Qualquer dúvida, estamos à disposição. <br/><br/>
 <br/>
 <br/>
Att.,
Relacionamento com o Cliente
</body>
</html>

```

Observe que o conector _permite o uso de_ D_ouble Braces:_



![](<../../.gitbook/assets/ezgif.com-gif-maker (19).gif>)

#### Dados do _JSON_

```
{
    "remetente": "digibee@gmail.com",
    "destinatario" : "digi@gmail.com",
    "destinatario_cc" : "digi1@gmail.com",
    "destinatario_bcc" : "digi2@gmail.com",
    "port" : "587",
    "host": "smtp.gmail.com",
    "NF": "98787979789",
    "M_VENC" : "13/01/2023"
}
```

## Tecnologia <a href="#tecnologia" id="tecnologia"></a>

Utilizamos o Freemarker para realizar as nossas conversões e transformações no _template_ do corpo do email. Leia a [documentação externa do Freemarker](https://freemarker.apache.org/docs/dgui\_template\_exp.html) para saber como utilizá-lo.
