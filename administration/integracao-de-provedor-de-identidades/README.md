---
description: >-
  Saiba mais sobre o que é um provedor de identidade (IdP) e quais as vantagens
  e os requisitos  para integrar o seu IdP à Digibee Integration Platform.
---

# Integração de provedor de identidades

### O que é um provedor de identidade (IdP)?

Um provedor de identidade (IdP) é um serviço de armazenagem e gerenciamento de identidades digitais. A Digibee Integration Platform suporta o serviço de integração com IdP que, uma vez ativado, permite a troca de informações de autenticação e autorização para que o gestor de acessos consiga organizar e controlar acessos de seus usuários (internos e externos) de forma centralizada.

Aqui estão alguns exemplos de IdPs:

* Active Directory (AD)
* Azure AD Native
* G Suite P
* PingFederateSharePoint

### **O que acontece quando o IdP é integrado à Digibee Integration Platform**

Uma vez que seu provedor de identidade esteja integrado à Digibee Integration Platform, será possível ter acesso às seguintes funcionalidades:

* **Single Sign-On:** um logon único que elimina a necessidade de gerenciamento de diversos repositórios de senhas;
* **Autenticação Integrada:** permite que o acesso à plataforma seja verificado pelo próprio IdP, centraliza as informações e facilita a gestão de acesso, podendo ser configurada de uma única vez para um ou mais realms do mesmo cliente;
* **Autorização integrada:** permite fazer a gestão de grupos do provedor de identidade que estão integrados a grupos de acesso da Digibee Integration Platform e, dessa forma, controlar quem tem acesso aos serviços que cada grupo integrado Digibee disponibiliza;

### **Quais são os requisitos para poder integrar um provedor de identidade à Digibee Integration Platform**

Garanta que o provedor de identidade seja compatível com o protocolo SAML 2.0 antes de realizar a integração com a Digibee.&#x20;

Quer saber sobre o passo a passo pra integrar seu provedor de identidades à Digibee Integration Platfom? Leia o artigo [Como integrar seu provedor de identidades](como-integrar-seu-provedor-de-identidades.md)**.**
