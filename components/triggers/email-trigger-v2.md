---
description: Conheça o trigger e saiba como utilizá-lo.
---

# Email Trigger V2

#### **IMPORTANTE: Este **_**trigger**_** suporta apenas o protocolo **_**IMAP**_**.**

O Email Trigger permite o recebimento dos dados de uma conta de e-mail no _pipeline_. Veja os parâmetros a serem configurados com o exemplo abaixo:

**1.** Abra as configurações de _trigger_ e selecione o tipo _**email-v2**_.

**2.** Preencha os campos das configurações:

* **Account:** especifique a conta para que o _trigger_ acesse o e-mail correto.
* **Operation:** escolha a opção "_mark as read_" (existem outras opções, que serão explicadas mais à frente).
* **Hostname:** insira o nome do _host_ do servidor IMAP _(ex.: imap.uol.com)_.
* **Port:** determine qual é a porta.
* **Email Folder:** defina o nome da pasta / caixa de entrada que o _trigger_ deve ler (ex.: inbox). Nessa pasta não podem existir mais que 100 mensagens (lidas/não lidas).
* **Destination Email Folder:**  aponte para qual pasta a mensagem deve ser movida. \
  Note que **este campo aparece apenas quando é escolhida a opção "**_**move to another folder**_**"** em "_Operation"_. Como neste exemplo a opção _"mark as read"_ foi escolhida, ele **não ficará visível** entre os parâmetros de configuração.
* **Maximum Timeout:** preencha o tempo máximo de execução do _trigger_.
* **Allow Redelivery Of Messages:** se ativada, a opção permite que as mensagens sejam entregues novamente caso o _Pipeline Engine_ falhe.

**3.** Clique em "Confirmar".

**4.** Continue a construção do _pipeline_.

**5.** Conecte os seus componentes.

**6.** Faça o _deploy_ do pipeline:

* Clique em "Run", localizado na parte superior da tela.
* Selecione o ambiente, que pode ser _**test**_ ou _**prod**_.
* Clique em "Criar uma nova implantação".
* Selecione o _pipeline_ com a sua versão e capacidade.
* Clique em "Confirmar".

**7.** Quando for disparado, o _pipeline_ receberá um _payload_ similar ao seguinte:

```
{ 
 "textMessage": "",
 "htmlMessage": "Olá, Pedro\r\nAinda não recebi o relatório deste mês. 
     Você poderia enviá-lo até o final do dia?",
 "attachments": ["attachment_fileName1", "attachment_fileName2", 
     "attachment_fileName3"]
  "subject": "Relatório mensal",
  "from": ["Renato Peixe Junior <renato.peixe@gmail.com>"],
  "to": ["pedro.gomes@gmail.com"],
  "cc": [],
  "bcc": [],
  "replyTo": ["Renato Peixe Junior <renato.peixe@gmail.com>"],
  "sentDate": "2020-02-10T17:54:40Z[UTC]",
  "receivedDate": "2020-02-10T17:54:52Z[UTC]"
} 
```

* **data:** conteúdo da mensagem
* **subject:** assunto da mensagem
* **from:** e-mail do remetente
* **to:** e-mail do destinatário
* **cc:** destinatários em cópia
* **bcc:** destinatários em cópia oculta
* **replyTo:** e-mail de destino da resposta
* **sentDate:** data de envio da mensagem
* **receivedDate:** data de recebimento da mensagem

### Campo "Operation" <a href="#h_7f01d390b4" id="h_7f01d390b4"></a>

* _**mark as read**_**:** selecione essa opção se, após processada, você deseja que a mensagem seja marcada como “lida”.
* _**move to another folder**_**:** selecione essa opção se, após processada, você deseja que a mensagem seja movida para uma pasta pré-determinada. O destino é especificado no campo "_Destination e-mail folder"_, que só aparece nas configurações quando "_move to another folder"_ é selecionada.
* _**delete**_**:** selecione essa opção se, após processada, você deseja que a mensagem seja excluída.

### Anexos <a href="#h_ed7b1075bc" id="h_ed7b1075bc"></a>

Caso haja algum anexo no corpo da mensagem recebida pelo _trigger_, ele vai baixá-las e disponibilizá-las dentro do diretório de execução do _pipeline_. Os nomes dos anexos estarão contidos dentro da propriedade _**attachments** _ e essa propriedade será um _array_ de _strings_ contendo os nomes dos anexos.

****

{% hint style="info" %}
**IMPORTANTE:** caso haja 2 anexos com o mesmo nome na mensagem, um identificador único será adicionado no nome do anexo baixado.
{% endhint %}

#### **Exemplo:**

Há 2 anexos com nome "file.csv" dentro da mensagem. Portanto, o conteúdo da propriedade _**attachments** _ será:

```
{
"attachments": ["file.csv", "0072e485-8ba2-4f79-bba5-8068e37ee792_file.csv"]
}
```

O identificador varia a cada execução.

{% hint style="info" %}
**Nota:** Se você utilizar o Gmail como _host_ do servidor IMAP, será necessário autorizar o suporte de aplicações não seguras. Clique [aqui](https://support.google.com/accounts/answer/6010255?hl=pt-BR) para ver o passo-a-passo.
{% endhint %}
