---
description: Conheça o componente e como usá-lo.
---

# Secure PDF

O SecurePDF permite definir uma senha ou configurações específicas (read only, print, fill in form, etc.), para um arquivo PDF já existente.

Dê uma olhada nos parâmetros de configuração do componente:

* **File Name:** nome ou caminho do arquivo PDF que deverá receber a eventual senha ou permissões.
* **Set password:** se a opção estiver habilitada, é permitida a inclusão de senha no arquivo em PDF para gerar um documento protegido.
* **Password:** senha para proteger o arquivo em PDF.
* **Custom permissions:** se a opção estiver habilitada, diversas opções de permissão de acesso no arquivo em PDF ficam disponíveis; do contrário, o arquivo em PDF será gerado com todas as permissões.
* **Read only:** permissão de acesso que define o arquivo em PDF como "somente leitura". Se a opção estiver habilitada, todas as outras permissões de acesso serão desabilitadas.
* **Assemble document:** permite que páginas sejam adicionadas, rotacionadas e removidas do arquivo.
* **Modify**: permite modificar o arquivo.
* **Modify annotations:** permite adicionar ou modificar anotações de texto no arquivo.
* **Extract content:** permite extrair textos e imagens do arquivo.
* **Extract for accessibility**: permite extrair textos e imagens do arquivo para fins de acessibilidade.
* **Print:** permite a impressão do arquivo.
* **Print degraded:** permite a impressão “degraded” do arquivo.
* **Fill in Form:** permite o preenchimento de formulários com campos interativos.
* **Fail On Error:** se a opção estiver habilitada, a execução do pipeline com erro será interrompida; do contrário, a execução do pipeline continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Alguns dos parâmetros acima, aceitam Double Braces. Para entender melhor como funciona essa linguagem, leia o artigo [Double Braces e Entrada de Dados](../../build/funcoes-double-braces/double-braces-e-entrada-de-dados.md).
