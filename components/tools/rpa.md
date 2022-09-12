---
description: Conheça o componente e saiba como utilizá-lo.
---

# RPA

O **RPA** é configurado para navegar nas páginas da _web_ e interagir com elas, realizando um processo de automação remota.

Dê uma olhada nos parâmetros de configuração do componente:

* **Code:** código _javascript_ necessário para que o serviço RPA Crawler seja executado.
* **Timeout:** tempo máximo de execução do _script_ RPA.
* **Allow Insecure HTTPS Connections:** quando ativada, a opção permite que conexões não seguras de HTTPS sejam estabelecidas.

### RPA em Ação <a href="#rpa-em-ao" id="rpa-em-ao"></a>

Você pode colocar algumas variáveis dentro do "código" que será alterado.

```
{ 
    ...
    code: '.goto(#{url}).wait(#{condition}).end()',
    ...
}
```

O corpo da solicitação deve conter estas variáveis:

```
{
    url: 'www.slack.com',
    condition: '#r1-0 a.result__a'
}
```

Veja o exemplo abaixo:

```
    .goto('https://duckduckgo.com')
    .type('#search_form_input_homepage', 'github nightmare')
    .click('#search_button_homepage')
    .wait('#r1-0 a.result__a')
    .evaluate(() => document.querySelector('#r1-0 a.result__a').href)
    .end()
```

* **goto:** URL a ser acessada
* **type:** digite qualquer coisa dentro de um ID de _input dome_
* **click:** função utilizada para clicar em algum botão
* **wait:** espera para que propriedade/botões sejam carregados
* **evaluate:** avaliar alguma propriedade
* **end:** obrigatório ao final do seu código

Para mais exemplos, clique [aqui](https://github.com/segmentio/nightmare#usage).

\
