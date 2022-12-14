# Dezembro

## Novidades 14/12/2022

### MONITOR

* Visão geral: agora, a tabela de visão geral exibe o número de erros e de execuções de _pipeline_ em conjunto. Também omitimos a coluna “dinâmica” e trocamos a posição da tabela e do gráfico nesta página.



### NOVO CANVAS (Beta restrito)

Melhoramos a performance do novo Canvas, dando mais rapidez para a navegação entre subníveis de um _pipeline_.

**IMPORTANTE**: para participar do programa de [Beta restrito](../../geral/programa-beta.md), fale com o seu _Customer Success Manager (CSM)_.

### &#x20; COMPONENTES

* **RPA**: o componente RPA foi descontinuado. A documentação relacionada ainda está disponível, mas foi sinalizada no título como descontinuada.
* **Suporte SQL Server 2019**: atualizamos nossa lista de [Bancos de Dados suportados](../../plataforma/bancos-de-dados-suportados.md) com a inclusão do Microsoft SQL Server 2019.
* **S3 Storage (AWS):** uma evolução do S3 Storage permite o uso de um _endpoint_ customizado via URL no componente.

### &#x20;RUN

* **Reimplantar:** a reimplantação do _pipeline_ ficou mais fácil e rápida: basta selecionar a opção REIMPLANTAR no _pipeline card_, que irá abrir um painel lateral com as informações já preenchidas. Então, selecione o novo tamanho, execuções simultâneas e réplicas e finalize clicando em IMPLANTAR.
* _**Status**_** de implantação do **_**pipeline**_**:** ficou mais fácil acompanhar o _status_ da implantação do _pipeline_. O novo _design_ do _pipeline card_ inclui o _status_ do _pipeline_ em tempo real.
* _**Auto refresh**_**:** essa nova funcionalidade permite selecionar o intervalo de atualização da página e, consequentemente, a atualização do _status_ do _card_ dos _pipelines_, facilitando obter informações do _pipeline_ em tempo real.
* **Aviso de conflito de rotas:** temos um novo aviso que ajuda a prevenir e solucionar o problema de conflitos de rota durante a implantação. _Pipelines_ com rotas iguais ou que começam com parâmetros que recebem o valor de ":id" através do "queryAndPath" geram erros e substituem _pipelines_ devido a essas definições.

### &#x20;MEU CONSUMO

* **Lista de contatos:** liberamos em nossa página “Meu Consumo” os nomes e e-mails das pessoas que prezam pelo sucesso da sua jornada com a Digibee Integration Platform. Entre em contato com o seu _Customer Success Manager_ (CSM) em caso de dúvidas sobre seu plano.

\


### DOCUMENTAÇÃO

Visando melhorar nossa documentação, atualizamos o artigo abaixo:

* [Pipeline](../../build/pipelines/)
* [Conceitos básicos sobre usuários](../../administration/novo-controle-de-acesso/conceitos-basicos-sobre-usuarios.md#h\_d16f6c5450)
* [Subpipelines](../../build/pipelines/subpipelines.md)\
  \
  \
  &#x20;

Nós também solucionamos alguns _bugs_:

* **Pipeline logs:** corrigimos o _bug_ no qual o nome LIMPAR no botão de limpar mudava para BUSCAR quando o tamanho da página era reduzido.
* **Expiração de senha:** corrigimos o _bug_ em que o botão CONFIRMAR ficava carregando por tempo indeterminado quando o usuário solicitava o cadastro de uma nova senha informando a antiga incorretamente.
* **Simulação de integração de grupos:** corrigimos o _bug_ que atrasava a contagem do temporizador quando o usuário minimizava a página de teste.
* **Blob Storage (Azure):** corrigimos o _bug_ que exibia tela branca no novo Canvas quando o formulário de configuração do componente Blob Storage (Azure) era aberto.
* **Flow tree:** corrigimos o _bug_ que impedia o usuário de redimensionar o tamanho da lista de componentes quando a estrutura do _Flow tree_ estivesse aberta no novo Canvas.
* **Remoção de um Parallel Execution:** corrigimos o _bug_ que exibia uma página branca ao remover ou reconectar o componente Parallel Execution ao fluxo de um _pipeline_ no novo Canvas.
* **Remoção de um Choice:** corrigimos o _bug_ que exibia uma página branca ao remover os parâmetros “_when”_ ou “_otherwise”_ do componente Choice __ quando no novo Canvas_._
* _**Test mode**_** na interpretação de HTML:** corrigimos o _bug_ que fazia o _Test mode_ renderizar textos em HTML e não exibí-los simplesmente como _plain text_ nos _logs_ do __ Canvas V1 e novo Canvas.

\
