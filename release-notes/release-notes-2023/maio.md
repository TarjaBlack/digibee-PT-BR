# Maio

## Novidades 09/05/2023

### COMPONENTES

* **Validator V2 (General Availability):** criamos uma nova versão do componente que valida conteúdo JSON de forma dinâmica via Double Braces, com base em um JSON Schema. Saiba mais na [documentação do Validator V2](https://docs.digibee.com/documentation/v/pt-br/components/tools/validator-v2).
* **HL7 Trigger (Beta Restrito):** criamos um novo trigger que recebe mensagens no formato HL7 (Health Level 7) na Digibee Integration Platform. Este trigger está atualmente em [fase Beta Restrito](https://docs.digibee.com/documentation/v/pt-br/geral/programa-beta#h\_d59e60e1bd) e disponível somente para clientes específicos.
* **CassandraDB, CSV to Excel e Zip File (General Availability):** os componentes estão em fase General Availability e disponíveis para todos os usuários.

### &#x20;NOVO CANVAS - TEST MODE

Fizemos algumas melhorias no Test mode do Novo Canvas. Agora, é possível redimensionar o tamanho da janela e também das colunas de Input e Output na aba de Teste. Além disso, o Test mode exibirá até 1000 mensagens de uma execução no Novo Canvas. Saiba mais na [documentação de Test mode](https://docs.digibee.com/documentation/v/pt-br/build/canvas/test-mode).



### MONITOR - EXECUÇÕES CONCLUÍDAS

Adicionamos um link em Detalhes da execução que redireciona o usuário ao Canvas do pipeline cuja execução está sendo analisada. Esta _feature_ está em fase Beta. Saiba mais sobre o [programa Beta da Digibee aqui](https://docs.digibee.com/documentation/v/pt-br/geral/programa-beta).

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### PÁGINA DE GRUPOS

Adicionamos à página de Grupos um _tooltip_ que exibe a descrição completa do grupo ao passar o cursor do mouse sobre a descrição do grupo.\
\
\


Nós também solucionamos alguns bugs:

#### NOVO CANVAS

* **Test mode:** corrigimos o bug que removia o conteúdo do Payload e Output do Test mode caso a página fosse atualizada.
* **Atalhos:** corrigimos o bug que impedia o uso dos atalhos para selecionar todos os componentes do novo Canvas de uma só vez (CTRL+A ou CMD+A).
* **Barra de tarefas:** corrigimos o bug onde o título da barra lateral esquerda do novo Canvas sumia ao rolar a barra para a lateral.
* **Configurações do pipeline:** corrigimos o bug que ativava a ação de salvar ao usar a tecla TAB para navegar entre os campos Name e Description nas configurações do pipeline.&#x20;
* **Componentes desconectados não são exibidos:** corrigimos o bug onde os componentes de subnível que tinham Choice ou Parallel desconectados sumiam no novo Canvas.
* **Flow tree:** corrigimos o bug onde a navegação pelo Flow tree não funcionava ao tentar voltar de um subnível do pipeline.
* **Cápsulas:** corrigimos o bug onde as Cápsulas apareciam sem os ícones quando eram arrastadas para o novo Canvas.
* **Breadcrumb do pipeline:** corrigimos o bug onde não era possível voltar para o nível principal do pipeline usando o breadcrumb.\


#### OUTROS

* Corrigimos um bug onde, às vezes, os filtros de nome e versão do pipeline não eram aplicados quando o usuário clicava no ícone de lupa na página de Visão geral.
* Corrigimos um bug onde a interface gráfica da página de Visão geral exibia a seleção incorreta do filtro de tempo quando o usuário alternava entre a aba de Monitor e outras abas.
