---
description: Conheça os próximos lançamentos do time de Produto
---

# Roadmap de Produto, Q3/22

Este artigo destaca o futuro roadmap de _features_ a serem lançadas durante o Q3/22 (3º trimestre de 2022).

**Observação**: As informações apresentadas sobre as próximas _features_ servem apenas como referência. Todos os itens aqui mencionados estão sujeitos a alterações ou atraso, e o desenvolvimento, lançamento e a periodicidade das _features_ são determinados exclusivamente pela Digibee.

## Build <a href="#h_49f9930331" id="h_49f9930331"></a>

O time Build é responsável por acelerar o tempo dos desenvolvedores até a obtenção de valor (_time to value_) ao criar a melhor experiência de construção de _pipeline_.

Destacamos as seguintes _features_ a serem lançadas em Q3/22:

**Novo Canvas:**

Desenvolvemos uma arquitetura totalmente nova para o Canvas.

O objetivo é dar mais agilidade ao time Digibee para desenvolver novas _features_ no Canvas e facilitar sua manutenção.

Devido à nova arquitetura, o Novo Canvas é capaz de mostrar validações em tempo real durante o processo de construção do _pipeline_ e oferecer uma nova experiência de navegação. Agora o Novo Canvas possibilitará ao time construir _features_ como um _Outline_ para a navegação, ações de Desfazer e Refazer, além de uma experiência de _Debugging_.

**Validações durante a construção do **_**pipeline**_**:**

Os usuários verão alertas para ajudá-los a identificar e corrigir problemas comuns mais rapidamente.

Esses alertas são categorizados como Erros ou Avisos para indicar a gravidade de um problema.

Exemplo: se um componente _Choice_ não tiver a opção _Otherwise_, os usuários verão um alerta vermelho indicando um erro e uma mensagem, além de um link para documentação com detalhes sobre como corrigi-lo.

Durante o 3º trimestre, o time Build vai explorar mais regras a serem implementadas bem como gerenciar o uso de cada regra. Exemplo: desabilitar os Avisos ou transformá-los em Erros para se tornarem obrigatórios.

## Platform Governance: <a href="#h_ec65e1f7bc" id="h_ec65e1f7bc"></a>

O time Platform Governance é responsável pelo escopo de Gestão de Identidade e Acessos na Digibee Integration Plaform.

Nosso objetivo para o 3º trimestre é aumentar a confiança do gestor de acesso ao realizar o gerenciamento de identidade e acessos para _realms_ integrados a um provedor de identidade.

Destacamos as seguintes _features_ a serem lançadas em Q3/22:

**Classificação de acesso à Plataforma:** Essa iniciativa oferecerá ferramentas ao gestor de acesso para classificar o acesso dos usuários em termos de características de autenticação e autorização para melhorar o _troubleshooting_ e apoiar a tomada de decisões relacionadas ao gerenciamento de identidade e de acesso.

**Teste de Mapeamento de Grupos:** O gestor de acesso poderá testar o mapeamento de grupos (integrando grupos IdP aos grupos Digibee) antes de ativar a autorização federada ao _realm_, prevenindo a perda de acesso para os usuários da Plataforma.

## Components <a href="#h_74fef86296" id="h_74fef86296"></a>

O time Components é responsável por criar e atualizar _Triggers_ e Componentes da Digibee Integration Plaform.

Destacamos as seguintes _features_ a serem lançadas em Q3/22:

**Componente Parquet:** É um formato de arquivo projetado para suportar o processamento rápido de dados complexos. Ao usar este componente, os usuários podem escrever e ler o arquivo Parquet dentro de seus _pipelines_ e cápsulas.

**Melhoria do componente SAP:** Esta melhoria no componente SAP permitirá que os usuários se conectem a um sistema SAP através de uma conexão com _Load Balancer,_ além de conexões diretas.

**Novos componentes:** O time Componentes trabalha continuamente no desenvolvimento de componentes solicitados por nossos clientes para atender suas necessidades.

## Core Platform <a href="#h_b0fff13d78" id="h_b0fff13d78"></a>

O time Core Platform é responsável por criar _features_ internas para acelerar as entregas dos demais times da Digibee.

Destacamos as seguintes _features_ a serem lançadas em Q3/22:

**Implementação de performance:** Nosso objetivo é reduzir o uso de _memory heap_ em até **5x** na JVM (Java Virtual Machine) ao carregar o _pipeline_ durante o _runtime_. Isso resolverá problemas no _Test-mode_ para _pipelines_ grandes e durante o uso de várias cápsulas em um mesmo _pipeline_.

## Monitor <a href="#h_981328b301" id="h_981328b301"></a>

O time Monitor é responsável por criar a melhor experiência de Monitoramento e _Troubleshooting_ na Digibee Integration Plaform.

Destacamos as seguintes _features_ a serem lançadas em Q3/22:

**Nova experiência do Monitor**: O time Monitor começará a revisar a experiência atual do usuário, oferecendo melhorias de curto e médio prazo.

## Growth and Licensing <a href="#h_d9b45b3b12" id="h_d9b45b3b12"></a>

O time Growth and Licensing é responsável por melhorar a experiência do usuário ao gerenciar e adquirir licenças e por ajudar os clientes a ampliar o uso da Plataforma por conta própria.

Destacamos a seguinte _feature_ a ser lançada em Q3/22:

**Gestão do novo modelo de subscrição SaaS**: Nosso objetivo é construir uma nova experiência visual e _self-service_ para os clientes que contrataram o novo modelo de subscrição SaaS (após abril/2022).
