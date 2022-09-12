---
description: Visualize logs de execução
---

# Pipeline Logs

Na aba Pipeline Logs,você pode acompanhar os _logs_ de eventos que são registrados durante a execução de um _pipeline_.

## Seleção de Ambiente <a href="#h_26d49df614" id="h_26d49df614"></a>

Você pode selecionar o ambiente desejado no canto superior esquerdo. O histórico de _logs_ expira após 3 dias no ambiente de teste e após 10 dias no ambiente de produção (prod).

Quando você seleciona um ambiente, a página inteira atualiza e mostra os dados correspondentes.

![](<../.gitbook/assets/seletordeambiente (2).png>)

## Campos de Busca <a href="#h_00048f8780" id="h_00048f8780"></a>

Você pode filtrar os _logs_ de _pipeline_ utilizando os seguintes parâmetros:

* **Período do tempo** : o horário em que um _pipeline_ foi executado. Filtre os _pipelines_ executados nos últimos 5, 15 ou 60 minutos ou selecione um período de tempo específico
* **Mensagem do **_**log**_**:** informação enviada por um componente que retorna _logs_ durante a execução de um _pipeline_. Você deve buscar por palavras inteiras quando utilizar esse campo
* **Nome do **_**pipeline**_**:** o nome do _pipeline_, como informado durante sua criação. Você deve buscar por palavras inteiras quando utilizar esse campo
* **Versão do **_**pipeline**_
* _**Pipeline Key**_**:** um identificador único de uma execução de um _pipeline_
* **Nível do **_**log**_**:** a classificação da mensagem do _log_, conforme o seguinte critério:
  * INFO : informação acerca de eventos ordinários durante a execução do _pipeline_
  * WARN : informação acerca de possíveis problemas durante a execução do _pipeline_
  * ERROR : informação acerca de erros durante a execução do _pipeline_
  * ALL : qualquer tipo de informação

Os _logs_ são mostrados abaixo de acordo com os parâmetros especificados. Você pode clicar no ícone de olho para ver os detalhes do _log_ em um modal ou no ícone de cópia para copiar a mensagem do _log_.

![](<../.gitbook/assets/pasted image 0.png>)
