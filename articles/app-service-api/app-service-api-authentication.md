---
title: aaaAuthentication et une autorisation pour API Apps dans Azure App Service | Documents Microsoft
description: "En savoir plus sur les services d’authentification et d’autorisation hello du Service d’applications Azure fournit des applications de l’API."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Authentification et autorisation pour API Apps dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
> [!NOTE]
> Cette rubrique sera migré tooa consolidé [App Service authentification / autorisation](../app-service/app-service-authentication-overview.md) rubrique, qui couvre les applications API Web et Mobile.
> 
> 

Azure App Service offre des services d’authentification et d’autorisation intégrés qui implémentent [OAuth 2.0](#oauth) et [OpenID Connect](#oauth). Cet article décrit les services hello et options sont disponibles pour les applications API dans Azure App Service.

Hello suivant le diagramme illustre certaines caractéristiques clés de l’authentification du Service d’application :

* Il prétraite les demandes entrantes de l’API, ce qui signifie qu’il est compatible avec n’importe quel langage ou framework pris en charge par App Service.
* Elle vous offre plusieurs options pour l’authentification de la quantité de travail vous souhaitez toodo dans votre propre code.
* Il fonctionne aussi bien pour l’authentification de l’utilisateur final que pour celle du compte de service. 
* Il prend en charge cinq fournisseurs d’identité : Azure Active Directory, Facebook, Google, Twitter et Compte Microsoft.
* Elle fonctionne même hello pour les applications API, les applications Web et les applications mobiles.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Langage non spécifié
Traitement de l’authentification du Service d’applications se produit avant que les requêtes parviennent à votre application d’API, ce qui signifie que les fonctionnalités d’authentification hello fonctionnent pour les applications d’API écrites dans n’importe quel langage ou le framework.  Votre API peut être basée sur ASP.NET, Java, Node.js ou une infrastructure prise en charge par App Service.

Service de l’application passe sur le jeton de web hello JSON (JWT) dans l’en-tête d’autorisation de hello d’une requête HTTP et le code écrit dans n’importe quel langage ou le framework peut obtenir informations hello que nécessaires de hello jeton. En outre, du Service d’applications vous donne plus facilement accès les revendications toohello couramment utilisé en définissant certains en-têtes spéciaux, tels que les suivants hello :

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Dans une API .NET, vous pouvez utiliser hello `Authorize` d’attribut et pour une autorisation, vous pouvez écrire facilement du code en fonction des revendications, car les informations de revendications sont remplies pour vous dans les classes .NET.

## <a name="multiple-protection-options"></a>Plusieurs options de protection
App Service peut empêcher les requêtes HTTP anonymes d’atteindre votre application API ; il peut également transmettre toutes les demandes et valider les jetons pour les demandes dans lesquelles ils sont inclus, ou bien acheminer toutes les demandes sans aucune action :

1. Autoriser uniquement les demandes authentifiées tooreach votre application API.
   
    Si une demande anonyme est reçue depuis un navigateur, Service de l’application redirige tooa page de connexion pour le fournisseur d’authentification hello (Azure AD, Google, Twitter, etc.) que vous choisissez. 
   
    Avec cette option, vous n’avez pas besoin toowrite n’importe quel code d’authentification du tout dans votre application et code d’autorisation est simplifiée car les revendications plus importantes hello sont fournies dans les en-têtes HTTP de hello.
2. Autoriser toutes les demandes tooreach votre application API, mais valider les demandes authentifiées et transmettre les informations d’authentification dans les en-têtes HTTP de hello.
   
    Cette option vous donne plus de souplesse dans la gestion des demandes anonymes, mais que vous avez toowrite code si vous souhaitez que les utilisateurs anonymes tooprevent à partir de l’aide de votre API. Étant donné que les demandes les plus populaires hello sont passés dans les en-têtes de hello de requêtes HTTP, code d’autorisation est relativement simple.
3. Autoriser toutes les demandes tooreach votre API, effectuer aucune action sur les informations d’authentification dans les demandes de hello.
   
    Cette option laisse tâches hello d’authentification et d’autorisation entièrement des tooyour code de l’application.

Bonjour [portail Azure](https://portal.azure.com/), vous activez l’option hello sur hello **l’authentification / autorisation** panneau.

![](./media/app-service-api-authentication/authblade.png)

Pour les options 1 et 2, activer **l’authentification du Service application**et Bonjour **tootake Action lors de la demande n’est pas authentifiée** liste déroulante, choisissez **connecter** ou **Autoriser les requêtes (aucune action)**.  Si vous choisissez **connecter**, vous avez toochoose un fournisseur d’authentification et configurer ce fournisseur.

![](./media/app-service-api-authentication/actiontotake.png)

Pour plus d’informations sur la façon tooconfigure l’authentification, consultez [comment tooconfigure votre connexion de Service d’applications application toouse Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). article de Hello applique tooAPI applications ainsi que des applications mobiles, et elle lie les articles tooother hello pour les autres fournisseurs d’authentification.

## <a id="internal"></a> Authentification du compte de service
L’authentification du Service de l’application fonctionne pour les scénarios internes comme appelé à partir d’une application de tooanother API d’application API. Dans ce scénario, vous pouvez obtenir un jeton en utilisant les informations d’identification correspondant à un compte de service au lieu des informations d’identification de l’utilisateur final. Un compte de service est également appelé *principal de service* dans Azure Active Directory, et l’authentification pratiquée avec ce type de compte est également appelée « scénario de service à service ». 

Pour les scénarios de service, protéger hello appelée application API à l’aide d’Azure Active Directory et fournir un jeton d’autorisation de principal du service AAD quand vous appelez l’application hello API. Vous obtenez un jeton en fournissant des ID de client hello et secret principal à partir de l’application AAD de hello du client. Aucun spéciaux code Azure uniquement n’est requis, par exemple, true toobe utilisé pour gérer le jeton de Mobile Services Zumo hello. Un exemple de ce scénario à l’aide d’applications ASP.NET API n’est couverte par un didacticiel de hello [l’authentification principale du Service pour les applications de l’API](app-service-api-dotnet-service-principal-auth.md).

Si vous voulez toohandle un scénario de service sans utiliser l’authentification du Service d’applications, vous pouvez utiliser des certificats de client ou de l’authentification de base. Pour plus d’informations sur les certificats de client dans Azure, consultez [comment tooConfigure l’authentification mutuelle de TLS pour les applications Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Pour plus d’informations sur l’authentification de base dans ASP.NET, consultez [Filtres d’authentification dans ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

L’authentification du compte de service à partir d’une application de Service de l’application logique application tooan API est un cas spécial qui est expliqué dans [à l’aide de votre API personnalisée hébergé sur App Service avec les applications de la logique](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Authentification du client mobile
Pour plus d’informations sur l’authentification toohandle à partir de clients mobiles, consultez hello [documentation sur l’authentification pour les applications mobiles](../app-service-mobile/app-service-mobile-ios-get-started-users.md). L’authentification du Service d’applications fonctionne hello identique pour les applications mobiles et les applications API.

## <a name="more-information"></a>Plus d’informations
Pour plus d’informations sur l’authentification et d’autorisation dans Azure App Service, consultez hello suivant des ressources :

* [Extension de l’authentification/autorisation App Service](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Comment tooconfigure votre connexion d’Azure Active Directory du Service d’applications application toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (inclut des liens pour d’autres fournisseurs d’authentification en hello haut hello.) 

Pour plus d’informations sur OAuth 2.0, OpenID Connect et les jetons Web JSON (JWT), consultez hello suivant des ressources.

* [Prise en main d’OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [Introduction tooOAuth2, OpenID Connect et les jetons Web JSON (JWT) - Pluralsight cours](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Création et sécurisation d’une API RESTful pour plusieurs clients dans ASP.NET (cours PluralSight)](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Pour plus d’informations sur Azure Active Directory, consultez hello suivant des ressources.

* [Scénarios Azure AD](http://aka.ms/aadscenarios)
* [Guide du développeur Azure AD](http://aka.ms/aaddev)
* [Exemples Azure AD](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Étapes suivantes
Cet article a décrit les fonctionnalités d’authentification et d’autorisation d’App Service que vous pouvez utiliser pour API Apps. Hello autre didacticiel de mise en route de hello démarré série montre comment tooimplement [l’authentification des utilisateurs dans les applications API App Service](app-service-api-dotnet-user-principal-auth.md).

