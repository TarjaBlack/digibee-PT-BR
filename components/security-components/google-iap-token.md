---
description: Conheça o componente e saiba como utilizá-lo
---

# Google IAP Token

O componente **Google IAP Token** permite gerar tokens do tipo OpenID para autenticações de proxies IAP (Identity Aware Proxy).

Dê uma olhada nos parâmetros de configuração do componente:

* **IAP Client ID:** informe o OAuth _client ID_, gerado na plataforma GCP, para recursos protegidos por IAP_._
* **Private Key:** Chave para o _account_ com o _private key_ do _Google service account._
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado da propriedade _success_ será _false_ na saída do componente.

**IMPORTANTE:** Para gerar o token, é necessário criar um _service account_ no Google Cloud e utilizar a _private key_ para configurar um Account na Digibee Integration Plaform.

## Fluxo de mensagens <a href="#h_c8faba169d" id="h_c8faba169d"></a>

### **Entrada** <a href="#h_61c4d1a2b4" id="h_61c4d1a2b4"></a>

Não é necessário nenhuma mensagem específica na entrada, bastando apenas configurar os campos necessários para cada operação.

### **Saída** <a href="#h_ec99af231b" id="h_ec99af231b"></a>

Object

```
{
"success": true,
"token": "eyJhbGciOiJSUz",
"refreshToken": "eyJhbGciOiJSUzI1N"
}
```

Erro

```
{
"success": false,
"message": "com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: Error loading connector google-authenticator-connector. Error: com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: Invalid account type received: GOOGLE_KEY"
}
```

* **success:** “false”, pois ocorreu um erro na execução
* **message:** é a mensagem de erro do componente
* **error:** é a mensagem de erro recebida do componente Google Authenticator

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui](https://intercom.help/godigibee/pt-BR/articles/4428887-processamento-de-mensagens) e leia o nosso artigo.
