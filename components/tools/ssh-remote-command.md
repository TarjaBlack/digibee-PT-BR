---
description: Conheça o componente e saiba como utilizá-lo.
---

# SSH Remote Command

O _**SSH Remote Command**_ permite que se estabeleça uma conexão com um servidor SSH e que _shell scripts_ sejam executados.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** para o componente fazer a autenticação a um serviço SFTP, é necessário usar uma _account_ do tipo BASIC ou PRIVATE KEY. Este parâmetro aceita _Double Braces_.
* **Username:** deve ser usado apenas quando o _account type_ for PRIVATE KEY.
* **Host:** nome do _host_ ou endereço IP para realizar a conexão. Este parâmetro aceita _Double Braces_.
* **Port:** número da porta - geralmente 22. Este parâmetro aceita _Double Braces_.
* **Custom Environment Variables:** se a opção estiver habilitada, você deverá informar as variáveis de ambiente de forma customizada no campo Environment Variables (ex: \[{"key": "MYVAR", "value": "VAR\_VALUE"}])\

* **Environment Properties:** nome e valor das variáveis de ambiente a serem passadas para execução no servidor de SSH remoto. Essas variáveis devem ser cadastradas no _sshd\_config_. Exemplo do cadastro no _ssh\_config_: AcceptEnv MYVAR
* **Command:** campo utilizado para especificar os comandos a serem executados no servidor SSH.
* **Ignore Output:** se a opção estiver habilitada, a execução do _pipeline_ ignora as respostas exibidas no _stdout_ ou _stderr_ no servidor SSH. Caso contrário, serão exibidos os campos _stdout_ e _stderr_ na saída do componente.
* **Stdout As File:** se a opção estiver habilitada, a resposta do resultado _stdout_ será gravada em um arquivo. Caso contrário, será exibida como _string_ na saída do componente.
* **Stdout File Name**: nome do arquivo a ser criado com as informações do _stdout_.
* **Stderr As File:** se a opção estiver habilitada, a resposta do resultado _stderr_ será gravada em um arquivo. Caso contrário, será exibida como _string_ na saída do componente.
* **Stderr File Name**: nome do arquivo a ser criado com as informações do _stderr_.
* **Connection Timeout:** tempo de expiração da conexão com o servidor (em milissegundos).
* **Server Alive Interval:** tempo que o componente vai manter a conexão ativa (em milissegundos).
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

{% hint style="info" %}
**IMPORTANTE:** note que alguns dos parâmetros acima suportam _Double Braces_. Para entender como essa linguagem funciona, leia o nosso artigo clicando [aqui](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).
{% endhint %}

### Fluxo de mensagens <a href="#h_e854786965" id="h_e854786965"></a>

#### Entrada <a href="#h_0de720fbcf" id="h_0de720fbcf"></a>

Não se espera nenhuma mensagem específica de entrada.

#### Saída <a href="#h_9908e4ffaa" id="h_9908e4ffaa"></a>

Ao executar um componente SFTP utilizando as operações _download, upload_ ou _move_, a seguinte estrutura de JSON será gerada:

```
{
    "stdout": "xpto",
    "stderr": "xpto_err",
    "stdoutFileName": "stdout.txt",
    "stderrFileName": "stderr.txt",
    "success": "true"
}
```

* **stdout: resposta com sucesso da execução do script**
* **stderr:** resposta com erros da execução do script
* **stdoutFileName:** caminho do arquivo salvo contendo as informações exibidas no stdout. Essa propriedade só será exibida caso a flag **Stdout As File** esteja habilitada
* **stderrFileName:** caminho do arquivo salvo contendo as informações exibidas no stderr. Essa propriedade só será exibida caso a flag **Stderr As File** esteja habilitada
* **success:** "true" se houve uma conexão e o script foi executado mesmo se retornar erros no stderr

**Saída com erro:**

```
{
  "success": false,
  "message": "Could not execute the SSH remote command",
  "error": "java.net.SocketTimeoutException: connect timed out"
}
```

* **success:** “false” quando a operação falha
* **message:** mensagem sobre o erro
* **exception:** informação sobre o tipo de erro ocorrido

{% hint style="info" %}
**IMPORTANTE:** a manipulação de arquivos dentro de um _pipeline_ ocorre de forma protegida. Os arquivos ficam disponíveis em diretório temporário que somente o _pipeline_ sendo executado tem acesso.
{% endhint %}

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](../../build/pipelines/processamento-de-mensagens.md) e leia o nosso artigo.

### SSH Remote Command em Ação <a href="#h_9a8cd2b071" id="h_9a8cd2b071"></a>

* **Executando um script e recebendo as informações no JSON de resposta do componente**

**Hostname:** \<HOST>

**Port:** \<PORT>

**Command:** echo $MYNAME && echo error output >&2

**Environment** Variables: \[{"key":"MYNAME", "value":"TEST"}]

**Stdout As File:** desabilitado

**Stderr As File:** desabilitado

**Fail On Error:** desabilitado

**Resultado:**

```
{
    "stdout": "TEST",
    "stderr": "error output",
    "success": "true"
}
```

* **Executando um script e salvando as informações em arquivos**

**Hostname:** \<HOST>

**Port:** \<PORT>

**Command:** echo $MYNAME && echo error output >&2

**Environment Variables:** \[{"key":"MYNAME", "value":"TEST"}]

**Stdout As File:** habilitado

**Stdout File** Name: stdout.txt

**Stderr As File:** habilitado

**Stderr File Name:** stderr.txt

**Fail On Error:** desabilitado

**Resultado:**

```
{
    "stdoutFileName": "stdout.txt",
    "stderrFileName": "stderr.txt",
    "success": "true"
}
```

\
