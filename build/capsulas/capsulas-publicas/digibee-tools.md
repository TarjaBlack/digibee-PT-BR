---
description: Saiba quais são as Cápsulas disponíveis nessa Coleção.
---

# Digibee Tools

A Coleção de Cápsulas Digibee Tools disponibiliza, de modo padronizado, recursos que são comumente utilizados em _pipelines_. Assim, também por meio das melhores práticas, a construção de _pipelines_ se torna mais produtiva.

#### CPF CNPJ Validator <a href="#h_8e45a34869" id="h_8e45a34869"></a>

Com essa Cápsula é possível validar o valor de números de documentos brasileiros que identificam uma pessoa de forma única: CPF (Cadastro de Pessoas Físicas) e CNPJ (Cadastro Nacional da Pessoa Jurídica).

Para isso, a Cápsula _**CPF CNPJ Validator**_ utiliza cálculos matemáticos e garante que o dígito verificador esteja correto. É importante ressaltar que não faz parte das funções da Cápsula validar a situação cadastral dos mencionados documentos na Receita Federal Brasileira.

Veja um exemplo de resultado de validação:

```
{
  "libOutPut": {
    "isCpfValid": true,
    "isCnpjValid": false,
    "noMask": "12345678909",
    "withMask": "123.456.789-09"
  }
}
```

Em caso de erro na execução do algoritmo _javascript_, será lançado um erro de execução:

```
{
  "timestamp": 1620665936661,
  "error": "Capsule capsule-v1-digibee-collection-name-test-capsule-name-test-1.0 failed execution. Error: com.digibee.pipelineengine.exception.PipelineEngineRuntimeException: Error during validation of Cpf/Cnpj.",
  "code": 500
}
```

#### Digibee Publish Error <a href="#h_fb4e77bea7" id="h_fb4e77bea7"></a>

Utilize essa Cápsula para padronizar o modo com o qual o seu _pipeline_ publica as mensagens de erro. A Cápsula _**Digibee Publish Error**_ não envia as mensagens diretamente para seus _dashboards_ de monitoramento ou aplicativos (Slack, e-mail, etc). O comportamento da Cápsula consiste em padronizar informações que são chave no monitoramento da integração. Além disso, detalhes técnicos referentes à execução são disponibilizados. O próximo passo é criar um _pipeline_ responsável por receber tais mensagens e optar por ações como, por exemplo, enviar e-mail agrupado com os erros.

A Cápsula também garante que todas as notificações de erros sejam padronizadas, permitindo flexibilidade no envio de informações adicionais através do campo “payload”.

Os campos “Subject” ou “Error Code” podem ser utilizados no critério de agrupamento dos erros. Por exemplo:

* Em uma integração de pedidos, os erros gerados em determinado intervalo de tempo devem ser agrupados e um único ticket deve ser gerado para o time responsável pela avaliação do incidente.
* No fluxo de integração de produtos, é necessário separar os erros com ERP e dos erros com a plataforma _e-commerce_. Nesse caso, cada grupo possui um valor de agrupamento diferente e as notificações podem ser tratadas de forma descentralizada.

{% hint style="info" %}
**IMPORTANTE**: a Cápsula _**Digibee Publish Error**_ padroniza as informações que devem ser preenchidas pelo desenvolvedor nos tratamentos de erros, sendo que tais informações são publicadas pelo componente [Pipeline Executor](../../../components/tools/pipeline-executor.md). Logo, é necessário que o _pipeline_ ‘_error-handling-group-and-notify_‘ seja construído e publicado no mesmo ambiente. Para obter um exemplo dele, entre em contato com a equipe de suporte da Digibee.
{% endhint %}

Veja uma ilustração de uso da Cápsula:

![](<../../../.gitbook/assets/01 (11).png>)

#### **Parallel Execution List to Objects** <a href="#h_5f4ec17e37" id="h_5f4ec17e37"></a>

Essa Cápsula transforma um _array_ em um mapa de objetos, utilizando o campo “_executionId_” existente na raiz do _array_. O uso da _**Parallel Execution List to Objects**_** ** pode ser aplicado ao padrão de saída do componente [Parallel Execution](../../../components/logic/parallel-execution.md) na recuperação de objetos resultantes do processamento paralelo.

Veja um exemplo de uso, no qual se aplica um fluxo de execução em paralelo:

![](<../../../.gitbook/assets/02 (9).png>)

O fluxo acima resulta no seguinte _array_:

```
[
  {
    "executionId": "Examaple-execution-3",
    "result": {
      "message": {
        "year": "2021"
      }
    }
  },
  {
    "executionId": "Address-execution-2",
    "result": {
      "body": {
        "address": "Disney"
      }
    }
  },
  {
    "executionId": "Customer-execution-1",
    "result": {
      "customer": {
        "name": "Mickey Mouse"
      }
    }
  }
]
```

Utilizando a combinação do componente [Block Execution](../../../components/logic/block-execution.md) com o fluxo paralelo (conforme o exemplo acima) e a Cápsula, o resultado é um mapa de objetos para cada _execution Id_. Veja:

```
{
  "Examaple-execution-3": {
    "message": {
      "year": "2021"
    }
  },
  "Address-execution-2": {
    "body": {
      "address": "Disney"
    }
  },
  "Customer-execution-1": {
    "customer": {
      "name": "Mickey Mouse"
    }
  }
}
```

#### **Send Email Alert** <a href="#h_1b1f5eb271" id="h_1b1f5eb271"></a>

O objetivo dessa Cápsula é facilitar o envio de erros por e-mail com base nas informações preenchidas no formulário de configuração. A _**Send Email Alert**_ possibilita o envio de informações complementares em um _template_ de e-mail pré-determinado para que se entenda a causa raiz do erro.

Para utilizar a Cápsula, é preciso configurar uma conta do tipo “_SMTP Auth And Properties_”. Clique [aqui](https://intercom.help/godigibee/pt-BR/articles/4280470-utilizacao-de-accounts) para acessar o nosso artigo completo sobre utilização de _accounts_.

Clique [aqui](https://intercom.help/godigibee/pt-BR/articles/2961109-usando-sua-conta-de-gmail-com-o-conector-de-email-smtp-da-digibee) para visualizar um exemplo de configuração utilizando sua conta Google.

{% hint style="info" %}
**IMPORTANTE:** verifique o limite de mensagens permitidas pela sua conta de e-mail. Para uma melhor confiabilidade na quantidade de e-mails enviados, recomendamos a abordagem apresentada na Cápsula _**Digibee Publish Error**._
{% endhint %}

#### **Sort Array by field** <a href="#h_5690c3c833" id="h_5690c3c833"></a>

O objetivo dessa Cápsula é ordenar o seu _array_ JSON de forma crescente (A-Z) ou de forma decrescente (Z-A).

{% hint style="info" %}
**IMPORTANTE:** a ordenação não leva em consideração o tempo cronológico de campos de datas, mas apenas a ordenação alfabética. Para uma ordenação correta, a data deve estar no formato ‘yyyy-mm-dd’.
{% endhint %}

#### **Validate Consumers** <a href="#h_100b8854f2" id="h_100b8854f2"></a>

Quando o _pipeline_ precisar ser executado com um número máximo de _consumers_ diferente do que consta no padrão de Runtime, utilize a Cápsula _**Validate Consumers**_** ** para impedir que as execuções aconteçam com a configuração incorreta de implantação.

Por exemplo, se o _pipeline_ permite a execução de até 2 requisições simultâneas, mas o Runtime esteja configurado com 10 requisições simultâneas e a Cápsulas com 2, então um erro é lançado nas execuções para que as configurações sejam corrigidas. No entanto, se na configuração da Cápsula constar 2 requisições simultâneas, a implantação deve ser configurada com 1 ou 2 _consumers_ no máximo.

Clique [aqui](../../../run/runtime.md) para saber mais sobre Runtime.
