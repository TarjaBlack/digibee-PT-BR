---
description: Saiba mais sobre o fluxo de login da Digibee.
---

# Fluxo de login

O acesso à Digibee Integration Platform pode acontecer de duas formas:

## **Login através da plataforma:**

Neste modelo, as ações são feitas diretamente na plataforma. Para acessar a Digibee Integration Platform, é necessário ter passado pelos passos do primeiro acesso:

### **Primeiro Acesso:**

**1.Criar usuário na plataforma**

Para que o usuário comece a utilizar a plataforma, o gestor de acesso deve primeiro criar o usuário. Para saber mais, leia a nossa documentação sobre [como criar um usuário](https://docs.digibee.com/documentation/v/pt-br/administration/novo-controle-de-acesso/conceitos-basicos-sobre-usuarios#h\_465025ea56).

**2.Definir senha de acesso**

Assim que o usuário for criado, um email com a solicitação para criar uma senha de acesso é enviado para o email cadastrado pelo gestor de acesso.

Clique em **CREATE A PASSWORD** para definir a senha de acesso.

**3.Login na Digibee Integration Platform**

Após definir a senha de acesso, o usuário é direcionado para a tela de login, onde será necessário preencher o seu _realm_, email e senha de acesso e realizar o seu primeiro login.

### **Login recorrente:**

Logo que tenha passado pelos passos do primeiro acesso, o usuário já pode fazer o login direto pela plataforma utilizando este [link](https://godigibee.io/login). Será necessário preencher o _realm_, email e senha. Caso tenha habilitado a verificação em duas etapas, o login é o momento de colocar o código de verificação.

<figure><img src="../../.gitbook/assets/Tela de login.png" alt=""><figcaption></figcaption></figure>

**IMPORTANTE:** Para alguns usuários, a plataforma já consegue identificar o _realm_. Nesta situação, só será necessário preencher o usuário e senha.

Caso venha a ter algum problema com o seu login, acesse a nossa documentação sobre [problemas para fazer login na Digibee Integration Platform.](https://intercom.help/godigibee/pt-BR/articles/6618894-problemas-para-fazer-o-login-na-digibee-integration-platform)

### **Senha expirada:**

Por motivos de segurança, a cada 15 dias a plataforma solicitará a troca de senha. Assim que uma tentativa de login for realizada com a senha atual após o prazo de 15 dias, o usuário será direcionado para um tela de redefinição de senha.

<figure><img src="../../.gitbook/assets/Redefinição de senha.png" alt=""><figcaption></figcaption></figure>

Após preencher as informações solicitadas e clicar em **CONFIRMAR**, o usuário poderá efetuar o login normalmente com a nova senha.

## **Login via provedor de identidade (IdP)**

Outra forma de efetuar o login na Digibee Integration Platform é através de um provedor de identidade, porém é necessário que o IdP já tenha sido integrado à Digibee. Para mais informações, acesse a nossa documentação sobre [integração de provedor de identidade](https://docs.digibee.com/documentation/v/pt-br/administration/integracao-de-provedor-de-identidades)**.**

Caso o seu provedor de identidade já tenha sido integrado à Digibee Integration Platform, o usuário poderá efetuar o login direto via IdP. Assim que o fizer, será direcionado para uma tela na Digibee Integration Platform para escolher o provedor pelo qual está efetuando o login.

<figure><img src="../../.gitbook/assets/Login IdP.png" alt=""><figcaption></figcaption></figure>

Após clicar no respectivo provedor de identidade, o usuário será direcionado para a Digibee Integration Platform.
