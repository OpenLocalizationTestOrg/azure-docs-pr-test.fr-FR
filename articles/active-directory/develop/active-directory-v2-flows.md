---
title: "types d’aaaApp pour le point de terminaison v2.0 hello Azure Active Directory | Documents Microsoft"
description: "types Hello des applications et des scénarios pris en charge par le point de terminaison v2.0 hello Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Types d’application pour le point de terminaison v2.0 hello Azure Active Directory
Hello point de terminaison Azure Active Directory (Azure AD) version 2.0 prend en charge l’authentification pour différentes architectures d’applications modernes, tous basés sur des protocoles standard [OAuth 2.0 ou OpenID Connect](active-directory-v2-protocols.md). Cet article décrit les types de hello d’applications que vous pouvez générer à l’aide d’Azure AD v2.0, quel que soit votre plateforme ou la langue par défaut. informations de cet article Hello sont conçue toohelp vous comprenez les scénarios de haut niveau avant que vous [commencer à travailler avec le code de hello](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory. toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>principes de base Hello
Vous devez inscrire chaque application qui utilise le point de terminaison hello v2.0 Bonjour [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com). processus d’inscription d’application Hello collecte et affecte ces valeurs pour votre application :

* un **ID d’application** qui identifie de manière unique votre application ;
* A **URI de redirection** que vous pouvez utiliser toodirect réponses arrière tooyour application
* quelques valeurs spécifiques au scénario.

Pour plus d’informations, découvrez comment trop[inscrire une application](active-directory-v2-app-registration.md).

Après l’inscription de l’application hello, application hello communique avec Azure AD en envoyant le point de terminaison v2.0 demandes toohello Azure AD. Nous fournissons les infrastructures open source et les bibliothèques qui gèrent les détails de hello de ces demandes. Vous avez également la logique d’authentification hello hello option tooimplement vous-même en créant des points de terminaison toothese demandes :

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>les applications web
Pour les applications web (.NET, PHP, Java, Ruby, Python, nœud) qui hello d’accès des utilisateurs via un navigateur, vous pouvez utiliser [OpenID Connect](active-directory-v2-protocols.md) pour la connexion d’utilisateur. OpenID Connect, l’application hello web reçoit un jeton d’ID. Un jeton d’ID est un jeton de sécurité qui vérifie l’identité de l’utilisateur hello et fournit des informations sur l’utilisateur hello sous forme de hello de revendications :

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Vous pouvez en savoir plus sur tous les types hello de jetons et les revendications qui sont d’application disponibles tooan Bonjour [v2.0 jetons référence](active-directory-v2-tokens.md).

Dans les applications de serveur web, le flux d’authentification de connexion de hello prend ces étapes :

![Flux d’authentification d’application web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Vous pouvez garantir l’identité de l’utilisateur hello en validant le jeton d’ID hello avec une clé de signature publique qui est reçue à partir du point de terminaison hello v2.0. Un cookie de session est défini, ce qui peut être utilisateur de hello tooidentify utilisé sur les demandes de page suivante.

exemples de ce scénario en action, essayez l’une des code hello web application connectez-vous toosee dans notre v2.0 [mise en route](active-directory-appmodel-v2-overview.md#getting-started) section.

En outre toosimple connectez-vous, une application de serveur web peut être nécessaire de tooaccess un autre service web, par exemple une API REST. Dans ce cas, l’application serveur hello web s’engage dans un flux combiné OpenID Connect et OAuth 2.0, à l’aide de hello [flux de code d’autorisation OAuth 2.0](active-directory-v2-protocols.md). Pour en savoir plus sur ce scénario, découvrez comment [la bien démarrer avec les applications web et des API web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>API Web
Vous pouvez utiliser hello v2.0 point de terminaison toosecure web services, tels que les API Web RESTful de votre application. Au lieu d’ID et de jetons de cookies de session, une API Web utilise un toosecure de jeton OAuth 2.0 accès ses données et tooauthenticate les demandes entrantes. appelant Hello d’une API Web ajoute un jeton d’accès dans l’en-tête d’autorisation de hello d’une requête HTTP, comme suit :

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello API Web utilise identité et tooextract informations d’hello accès tooverify jeton hello appelant de l’API hello appelant à partir des revendications qui sont codés dans le jeton d’accès hello. toolearn sur tous les types hello de jetons et les revendications qui sont disponibles tooan application, consultez hello [v2.0 jetons référence](active-directory-v2-tokens.md).

Une API Web peut donner aux utilisateurs hello power tooopt ou désactiver des fonctionnalités spécifiques ou des données en exposant les autorisations, également appelé [étendues](active-directory-v2-scopes.md). Pour une étendue de tooa appelant application tooacquire autorisation, utilisateur de hello doit donner son accord toohello étendue pendant un flux. point de terminaison Hello v2.0 demande l’autorisation utilisateur de hello et enregistre ensuite les autorisations dans tous les jetons d’accès que hello que reçoit des API Web. Hello API Web valide les jetons d’accès hello il reçoit sur chaque appel et effectue des vérifications d’autorisation.

Une API web peut recevoir des jetons d’accès de tous types d’applications, notamment des applications de serveur web, des applications de bureau et mobiles, des applications de page unique, des démons côté serveur, et même d’autres API web. flux de haut niveau de Hello pour une API Web ressemble à ceci :

![Flux d’authentification d’API web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn comment toosecure une API Web à l’aide des jetons d’accès OAuth2, extraction hello code de l’API Web des exemples dans notre [mise en route](active-directory-appmodel-v2-overview.md#getting-started) section.

Dans de nombreux cas, API web doivent également les demandes sortantes toomake tooother en aval web API sécurisées par Azure Active Directory.  toodo par conséquent, les API web peut tirer parti de Azure AD **sur place de** flux, ce qui permet à un jeton d’accès entrant pour un autre toobe jeton d’accès utilisé dans les demandes sortantes hello web API tooexchange.  Hello v2.0 point de terminaison pour le compte de flux est décrit dans [décrit en détail ici](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Applications mobiles et natives
Périphérique installé des applications, telles que des applications mobiles et de bureau, doivent souvent des services de back-end tooaccess ou API Web qui stockent des données et effectuer des fonctions pour le compte d’un utilisateur. Ces applications peuvent ajouter des services en tooback dans l’authentification et l’autorisation à l’aide de hello [flux de code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

Dans ce flux, application hello reçoit un code d’autorisation à partir du point de terminaison v2.0 hello lorsque hello utilisateur se connecte. Bonjour les services de l’application hello d’autorisation code représente autorisation toocall principaux pour le compte d’utilisateur hello qui s’est connecté. application Hello peut échanger le code d’autorisation de hello en arrière-plan hello pour un jeton d’accès OAuth 2.0 et un jeton d’actualisation. application Hello utilisez hello accès jeton tooauthenticate tooWeb API dans les demandes HTTP et utilisez hello actualisation jeton tooget nouveaux jetons d’accès lors de l’expirent des jetons d’accès plus anciens.

![Flux d’authentification d’applications native](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Applications à page unique (Javascript)
De nombreuses applications modernes disposent d’un frontend d’application à page unique écrit principalement en JavaScript. Souvent, il est écrit à l’aide d’une infrastructure telle qu’AngularJS, Ember.js ou Durandal.js. point de terminaison v2.0 Hello Azure AD prend en charge ces applications à l’aide de hello [flux implicite OAuth 2.0](active-directory-v2-protocols-implicit.md).

Dans ce flux, application hello reçoit les jetons directement à partir de hello v2.0 autoriser le point de terminaison, sans tout échange de serveur à serveur. Tous les logique d’authentification et de gestion prend de session placent entièrement hello JavaScript client, sans les redirections de pages supplémentaires.

![Flux d’authentification implicite](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee ce scénario en action, essayez l’une des exemples de code d’application une seule page hello dans notre [mise en route](active-directory-appmodel-v2-overview.md#getting-started) section.

## <a name="daemons-and-server-side-apps"></a>Applications démons et côté serveur
Les applications qui ont des processus longs ou qui ne fonctionne pas sans interaction avec un utilisateur également besoin de tooaccess des ressources, telles que les API Web sécurisées. Ces applications peuvent s’authentifier et obtenir des jetons à l’aide d’identité de l’application hello, plutôt que d’un utilisateur délégué identité, le transfert des informations d’identification client hello OAuth 2.0.

Dans ce flux, application hello interagit directement avec hello `/token` points de terminaison de point de terminaison tooobtain :

![Flux d’authentification d’applications démons](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild une application démon, consultez la documentation sur les informations d’identification client hello dans notre [mise en route](active-directory-appmodel-v2-overview.md#getting-started) section ou essayez un [exemple d’application .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
