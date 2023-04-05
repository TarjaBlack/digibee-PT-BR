---
description: Conheça o componente e saiba como utilizá-lo.
---

# SQS (AWS) V2

O componente SQS (AWS) permite o envio de mensagens para filas do serviço da AWS SQS, tanto do tipo standard como do tipo FIFO.

Dê uma olhada nos parâmetros de configuração do componente:

* **Account:** necessário para o componente se autenticar na cloud da AWS. Este deve ser do tipo BASIC.
* **Message:** corpo da mensagem que deseja enviar. Este parâmetro aceita _Double Braces_.\

* **Name of the Queue:** nome da fila na AWS.
* **Connection String:** URL de destino da fila SQS na AWS.\

* **Region:** região na qual a fila está registrada no serviço na AWS.
* **Queue Type:** tipo de fila que receberá a mensagem. Este pode ser do tipo STANDARD ou FIFO. Ao selecionar FIFO, outro parâmetro é necessário\
  \
  \- **Message Group ID:** em filas do tipo FIFO, este é o ID do _message group_ desta fila.\

* **failOnError:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia o nosso artigo clicando [aqui](broken-reference).

## Fluxo de mensagens <a href="#h_7d8a20883e" id="h_7d8a20883e"></a>

**1. Fila AWS SQS Standard (envio sem erro):**

### **Entrada** <a href="#h_f47f2b4130" id="h_f47f2b4130"></a>

```
{
"url": "https://sqs.sa-east-1.amazonaws.com/123456789012/digibee-test",
"typeQueue":"STANDARD",
"queue": "digibee-test",
"messageBody": "{
"test": "Test encryption"
}",
"region": "sa-east-1",
"failOnError": false
}
```

### **Saída** <a href="#h_33eecc5cff" id="h_33eecc5cff"></a>

```
{
"messageId":"c959b1da-6650-46c2-8baf-62302789dd61",
"messageBodyMD5":"c35f05f412ea94ef45bf103ba96b7b0e",
"sequenceNumber":null,
"success":true,
"requestId":"6c950c3a-d081-5685-893b-55cf8c1b51e0"
}
```

**2. Fila AWS SQS FIFO (envio sem erro):**

### **Entrada** <a href="#h_a181151f54" id="h_a181151f54"></a>

```
{
"url": "https://sqs.sa-east-1.amazonaws.com/123456789012/digibee-test.fifo",
"typeQueue":"FIFO",
"messageGroupId":"mygroup",
"queue": "digibee-test.fifo",
"messageBody": "{
"test": "Test encryption"
}",
"region": "sa-east-1",
"failOnError": false
}
```

### **Saída** <a href="#h_e59fa72a49" id="h_e59fa72a49"></a>

```
{
"messageId":"c959b1da-6650-46c2-8baf-62302789dd61",
"messageBodyMD5":"c35f05f412ea94ef45bf103ba96b7b0e",
"sequenceNumber":"18865425420279279616",
"success":true,
"requestId":"6c950c3a-d081-5685-893b-55cf8c1b51e0"
}
```

**3. Fila AWS SQS FIFO (envio sem messageGroupId):**

### **Entrada** <a href="#h_56aeaf2f0c" id="h_56aeaf2f0c"></a>

```
{
"url": "https://sqs.sa-east-1.amazonaws.com/123456789012/digibee-test.fifo",
"typeQueue":"FIFO",
"queue": "digibee-test.fifo",
"messageBody": "{
"test": "Test encryption"
}",
"region": "sa-east-1",
"failOnError": false
}
```

### **Saída** <a href="#h_85799e02a3" id="h_85799e02a3"></a>

```
{
"success":false,
"message":"There is an invalid pipeline configuration",
"error":"com.digibee.pipelineengine.exception.PipelineEngineConfigurationException: Configuration parameter 'messageGroupId' cannot be null for connector sqs-connector"

}
```

**4. Fila AWS SQS (envio com região inválida):**

### **Entrada** <a href="#h_b9b07d042e" id="h_b9b07d042e"></a>

```
{
"url": "https://sqs.sa-east-1.amazonaws.com/123456789012/digibee-test",
"typeQueue":"STANDARD",
"queue": "digibee-test",
"messageBody": "{
"test": "Test encryption"
}",
"region": "wrong-region",
"failOnError": false
}
```

### **Saída** <a href="#h_bb57f09bd6" id="h_bb57f09bd6"></a>

```
{
"success":false,
"message":"Something went wrong while trying to execute SQS CONNECTOR",
"error":"com.amazonaws.services.sqs.model.AmazonSQSException: Credential should be scoped to a valid region, not 'wrong-region'. (Service: AmazonSQS; Status Code: 403; Error Code: SignatureDoesNotMatch; Request ID: bf47d091-2129-5320-a332-89647ef0d86b)"
}
```

Para entender melhor o fluxo das mensagens na Plataforma, clique [aqui ](../../build/pipelines/processamento-de-mensagens.md)e leia o nosso artigo.
