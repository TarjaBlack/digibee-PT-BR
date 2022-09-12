---
description: Conheça o componente e saiba como utilizá-lo.
---

# Throw Error

O _**Throw Error**_ emite um erro dentro de um _pipeline_ ou _subpipeline_. Ele pode ser usado para:

* interromper um _pipeline_ com erro
* interromper um componente que utilize _subpipelines_ para processamento

Dê uma olhada nos parâmetros de configuração desse componente:

* **Error Code:** define o código do erro (utilizamos como base códigos de erro HTTP).
* **Error Message:** define a mensagem de erro que acompanha o código de erro.
* **Custom Error Enabled**: define que o usuário deseja utilizar um erro customizado.
* **Custom Error:** pode ser usado para definir uma mensagem customizada de erro (nesse caso, “Error Code” e “Error Message” são ignorados).
* **Fail on Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

### Throw Error em Ação <a href="#throw-error-em-ao" id="throw-error-em-ao"></a>

#### Tratamento de erros padrão (customErrorEnabled) <a href="#tratamento-de-erros-padro-customerrorenabled" id="tratamento-de-erros-padro-customerrorenabled"></a>

O _**Throw Error**_ pode ser utilizado para o tratamento de erros padrão. Erro padrão é aquele que segue as definições da Plataforma Digibee e que contém um código e uma mensagem.

Quando esse tipo de erro resulta na interrupção do _pipeline_, então a seguinte saída é produzida:

```
{
  "timestamp": <um número longo informando o timestamp de quando o erro foi gerado>,
  "error": <a mensagem configurada>,
  "exception": "PipelineEngineRuntimeException",
  "code": <o código configurado>
}
```

#### Tratamento de erros customizados <a href="#tratamento-de-erros-customizados" id="tratamento-de-erros-customizados"></a>

O _**Throw Error**_ também pode ser utilizado para o tratamento de erros customizados. Nesse caso, um objeto JSON completo é informado na configuração do componente e posteriormente informado na saída do _pipeline_ que resultou em erro.

**IMPORTANTE:** alguns _triggers_, como por exemplo REST, HTTP e HTTP File, necessitam receber uma propriedade _code_ e uma propriedade _error_ na saída do _pipeline_ para preparar o código de retorno da chamada HTTP.

#### Componentes que utilizam _subpipelines_ <a href="#componentes-que-utilizam-subpipelines" id="componentes-que-utilizam-subpipelines"></a>

Quando o _**Throw Error**_ é utilizado em um componente que utiliza o _subpipeline_ “onProcess”, o erro configurado é informado como entrada do _subpipeline_ “onException”. Se a opção “Custom Error” for preenchida, então o conteúdo do objeto JSON é igual ao descrito na seção "Utilização do _**Throw Error**_ para o tratamento de erros padrão" ou "Utilização do _**Throw Error**_ para o tratamento de erros customizados".

Para entender melhor o conceito de _subpipelines_, clique [aqui](../../build/pipelines/subpipelines.md).
