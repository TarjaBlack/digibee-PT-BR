---
description: Entenda como criar e configurar sua integração.
---

# Integração dos grupos IdP com grupos Digibee

O realm da Digibee que possui integração com provedor de identidade (IdP), poderá integrar os grupos do provedor de identidade com os grupos Digibee para aumentar a eficiência da gestão de acessos dos seus usuários. Isso permite escalar as mudanças das permissões, e garantir mais facilidade ao gestor de acessos.

Para evitar possíveis perdas de acesso, o gestor de acesso do realm deve configurar as integrações de grupos e solicitar a sua ativação via solicitação ao time de suporte ou Customer Success da Digibee.

Quando ativada a integração de Grupos IdP, o controle de acesso terá o seguinte comportamento:

* **Usuários nativos** não são afetados pela integração de grupos IdP, assim eles podem ser associados a qualquer grupo Digibee (integrado ou não).
* **Usuários integrados (IdP)** poderão participar apenas de **grupos integrados (IdP)** quando a integração for ativada pelo time de Suporte (após solicitação). Caso não esteja ativa, estes usuários podem ser associados manualmente a grupos Digibee.

<figure><img src="../../.gitbook/assets/Imagem 1 (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/imagem 2.png" alt=""><figcaption></figcaption></figure>

**Nota:** Caso solicitado, a opção de usuários nativos pode ser desativada no realm, após a validação de todo o ambiente.

Todas as etapas descritas abaixo só terão efeito imediato após ativação com o time de suporte.

### **Antes de começar**

Leia os seguintes artigos e conheça mais sobre o funcionamento do Novo Controle de Acesso e da integração com Provedor de Identidade:

* [Novo Controle de Acesso](../novo-controle-de-acesso/)
* [Integração com Provedor Identidade](./)

### **Como criar uma integração**

Para criar uma integração, siga os seguintes passos:

1. Faça login na Plataforma Digibee;
2. Clique no ícone de “Administração”;
3. Entre na opção do menu “Grupos”;

<figure><img src="../../.gitbook/assets/Imagem 3.png" alt=""><figcaption></figcaption></figure>

4\. Selecione a aba “Integração de grupos”;

5 Clique no botão **+ CRIAR** no canto superior direito;

<figure><img src="../../.gitbook/assets/Imagem 4 (2).png" alt=""><figcaption></figcaption></figure>

6\. **** Um formulário solicitando a seguintes informações será exibido:

* **Nome:** nome desejado para a integração.
* **SAML Scheme:** esquema de organização do seu provedor de identidade.
* **Código ID do provedor de identidade:** código identificador do grupo no provedor de identidade.
* **Grupo Digibee:** grupo da Plataforma que será integrado.



Caso seja selecionado “**Custom Scheme**” no campo SAML Scheme, um novo campo será exibido:                                                                                                                                                                                                    &#x20;

* **Xpath:** caminho do XML para obter os IDs do grupo do provedor de identidade.



**Nota:** caso seu provedor de identidade seja apresentado na listagem de SAML Scheme, não é necessário localizar o XPath.

7\. Após preencher os campos, clique em **“SALVAR”**  no canto inferior direito.

8\. Uma caixa de  diálogo de confirmação aparecerá.Digite uma breve explicação da integração que foi criada. Esta informação será adicionada no Registro de Auditoria da Plataforma.

9\. Clique em **“CRIAR INTEGRAÇÃO”**

Após todos estes passos a integração será criada com sucesso.

### **Como editar uma integração**

Para editar uma integração, siga os seguintes passos:

1. Vá para a aba “Integração de grupos”;
2.  Busque a integração desejada na barra de pesquisa;

    **Nota:** É possível buscar a integração por qualquer atributo da integração (nome, código, ID, grupo Digibee, ou SAML)

<figure><img src="../../.gitbook/assets/Imagem 5 (1).png" alt=""><figcaption></figcaption></figure>

3\. Clique no ícone de lápis (“Editar integração”);

<figure><img src="../../.gitbook/assets/Imagem 6 (2).png" alt=""><figcaption></figcaption></figure>

4\. Faça as alterações desejadas.

5\. Após realizar as alterações clique em **“SALVAR"**  no canto inferior direito.

6\. Uma caixa de diálogo de confirmação aparecerá. Digite uma breve explicação do que foi editado. Esta informação será adicionada no Registro de Auditoria da Plataforma.

7\. Clique em **“EDITAR INTEGRAÇÃO”**

Após todos estes passos a integração será editada com sucesso.

**Nota:** As mudanças nos grupos do usuário serão realizadas no momento que for feito o login através da integração.

### **Como arquivar uma integração**

Para arquivar uma integração siga os seguintes passos:

1. Vá para a aba “Integração de grupos”;
2. Busque a integração desejada na barra de pesquisa;

<figure><img src="../../.gitbook/assets/Imagem 7.png" alt=""><figcaption></figcaption></figure>

**Nota:** É possível buscar a integração por qualquer atributo da integração (nome, código, ID, grupo Digibee, ou SAML)

3**.** Clique no ícone de **“**Arquivar integração**”;**

<figure><img src="../../.gitbook/assets/imagem 8.png" alt=""><figcaption></figcaption></figure>

Uma caixa de diálogo de confirmação aparecerá. Digite uma breve explicação do porquê a integração será arquivada. Esta informação será adicionada no Registro de Auditoria da Plataforma.

4\. Clique em **“ARQUIVAR INTEGRAÇÃO”**

**Nota:** Não é possível reverter esta ação, pois pode gerar um conflito de acessos. Será necessário criar uma nova integração.

Após todos estes passos a integração será arquivada com sucesso.

**IMPORTANTE:** Arquivar uma integração pode causar perda de acessos aos membros contidos no grupo da integração em questão.

### **Impactos da integração dos grupos IdP**

A ativação da integração não pode ser desfeita. Os usuários podem ter perda de acesso total ou parcial caso os grupos não estejam mapeados corretamente.

Após a ativação, usuários nativos associados a papéis e grupos podem continuar utilizando a página de login da Plataforma.

Suas configurações somente poderão ser ativadas manualmente pelo time de suporte da Digibee. Portanto, quando considerar que o trabalho de mapeamento está completo e desejar que as integrações configuradas passem a valer no momento do login do usuário entre em contato pelo chat.
