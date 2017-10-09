---
title: aaaAzure AD B2C | Documents Microsoft
description: "types Hello d’applications que vous pouvez générer Bonjour Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C : types d’applications
Azure Active Directory (Azure AD) B2C prend en charge l’authentification pour une variété d’architectures d’applications modernes. Tous les reposent sur hello protocoles standard [OAuth 2.0](active-directory-b2c-reference-protocols.md) ou [OpenID Connect](active-directory-b2c-reference-protocols.md). Ce document décrit brièvement les types d’applications que vous pouvez générer hello, indépendant de la langue de hello ou plateforme vous préférez. Il vous permet également de comprendre les scénarios de haut niveau hello avant [démarrer la création d’applications](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>principes de base Hello
Chaque application qui utilise Azure AD B2C doit être inscrit dans votre [B2C active](active-directory-b2c-get-started.md) via hello [Azure Portal](https://portal.azure.com/). processus d’inscription d’application Hello collecte et affecte l’application de tooyour quelques valeurs :

* un **ID d’application** qui identifie de manière unique votre application ;
* A **URI de redirection** qui peut être utilisé toodirect réponses arrière tooyour application.
* n’importe quelle valeur spécifique au scénario. Pour plus d’informations, découvrez comment trop[inscrire une application](active-directory-b2c-app-registration.md).

Après l’inscription de l’application hello, il communique avec Azure AD en envoyant le point de terminaison v2.0 demandes toohello Azure AD :

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Chaque demande envoyée tooAzure AD B2C spécifie un **stratégie**. Une stratégie de contrôle le comportement de hello d’Azure AD. Vous pouvez également utiliser ces points de terminaison de toocreate un ensemble hautement personnalisable d’expériences utilisateur. Les stratégies courantes comprennent les stratégies d’inscription, les stratégies de connexion et les stratégies de modification de profil. Si vous n’êtes pas familiarisé avec les stratégies, vous devez examiner hello Azure AD B2C [infrastructure de stratégie extensible](active-directory-b2c-reference-policies.md) avant de continuer.

interaction Hello de chaque application avec un point de terminaison v2.0 suit un modèle de niveau supérieur similaires :

1. application Hello dirige tooexecute de point de terminaison v2.0 hello utilisateur toohello un [stratégie](active-directory-b2c-reference-policies.md).
2. utilisateur de Hello termine stratégie hello selon la définition de la stratégie toohello.
3. application Hello reçoit un type de jeton de sécurité à partir du point de terminaison hello v2.0.
4. application Hello utilise les informations de jeton tooaccess protégé sécurité hello ou une ressource protégée.
5. serveur de ressources Hello valide tooverify jeton hello sécurité auxquelles l’accès peut être accordé.
6. application Hello actualise régulièrement le jeton de sécurité hello.

<!-- TODO: Need a page for libraries toolink too-->
Ces étapes peuvent différer légèrement en fonction de type hello d’application que vous générez. Bibliothèques Open source peuvent adresser des détails de hello pour vous.

## <a name="web-apps"></a>les applications web
Pour les applications web (notamment .NET, PHP, Java, Ruby, Python et Node.js.) qui sont hébergées sur un serveur et accessibles par le biais d’un navigateur, Azure AD B2C prend en charge [OpenID Connect](active-directory-b2c-reference-protocols.md) pour toutes les expériences utilisateur. Cela inclut la connexion, l’inscription et la gestion des profils. Dans l’implémentation hello Azure AD B2C d’OpenID Connect, votre application web lance ces expériences utilisateur en émettant tooAzure de demandes d’authentification Active Directory. résultat de Hello de demande de hello est un `id_token`. Ce jeton de sécurité représente l’identité de l’utilisateur hello. Il fournit également des informations sur l’utilisateur hello sous forme de hello de revendications :

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

En savoir plus sur les types de revendications et jetons application disponible tooan Bonjour hello [référence de jeton B2C](active-directory-b2c-reference-tokens.md).

Dans les applications web, chaque exécution d’une [stratégie](active-directory-b2c-reference-policies.md) suit la procédure générale ci-après :

![Images de couloirs d’application Web](./media/active-directory-b2c-apps/webapp.png)

Validation de hello `id_token` à l’aide d’une clé de signature publique qui est reçue à partir d’Azure AD est suffisamment d’identité hello tooverify d’utilisateur de hello. Il définit également un cookie de session qui peut être des utilisateurs de hello tooidentify utilisé sur les demandes de page suivante.

toosee ce scénario en action, essayez l’une des exemples de code de connexion hello web app dans notre [section mise en route](active-directory-b2c-overview.md#get-started).

Dans Ajout toofacilitating simple connexion, une application de serveur web peut être nécessaire tooaccess un service web principal. Dans ce cas, l’application web hello peut effectuer légèrement différentes [OpenID Connect de flux](active-directory-b2c-reference-oidc.md) et acquérir des jetons à l’aide des codes d’autorisation et les jetons d’actualisation. Ce scénario est représenté dans suivant de hello [section de l’API Web](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>API Web
Vous pouvez utiliser les services web Azure AD B2C toosecure telles que les API de web RESTful de votre application. API Web peut utiliser OAuth 2.0 toosecure leurs données, en authentifiant les requêtes HTTP entrantes à l’aide de jetons. appelant Hello d’une API web ajoute un jeton dans l’en-tête d’autorisation de hello d’une requête HTTP :

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello web API peut ensuite utiliser tooextract des identités et des informations l’appelant hello API hello jeton tooverify de hello appelant à partir des revendications qui sont codés dans le jeton de hello. En savoir plus sur les types de revendications et jetons application disponible tooan Bonjour hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Actuellement, Azure AD B2C prend uniquement en charge les API web qui sont accessibles par leurs clients connus. Par exemple, votre application dans son ensemble peut inclure une application iOS, une application Android et une API web principale. Cette architecture est entièrement prise en charge. Permettre à un client partenaire, par exemple une autre application iOS, tooaccess hello même web QU'API n’est pas prise en charge. Tous les composants hello de votre application complète doivent partager un ID d’application unique.
>
>

Une API web peut recevoir des jetons de tous types de clients, notamment des applications web, des applications de bureau et mobiles, des applications de page unique, des démons côté serveur, et même d’autres API web. Voici un exemple de flux de hello complète pour une application web qui appelle une API web :

![Images de couloirs d’API Web d’application Web](./media/active-directory-b2c-apps/webapi.png)

toolearn en savoir plus sur les codes d’autorisation, les jetons d’actualisation et les étapes de hello pour obtenir des jetons, en savoir plus sur hello [protocole OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

toolearn comment toosecure une API web à l’aide d’Azure AD B2C, extraction hello web didacticiels API dans notre [section mise en route](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Applications mobiles et natives
Les applications qui sont installées sur les appareils, tels que des applications mobiles et de bureau, doivent souvent des services du back-end tooaccess ou API web pour le compte d’utilisateurs. Vous pouvez ajouter une identité personnalisée gestion expériences tooyour applications natives et appeler en toute sécurité des services principaux à l’aide d’Azure AD B2C et hello [flux de code d’autorisation OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

Dans ce flux, application hello exécute [stratégies](active-directory-b2c-reference-policies.md) et reçoit un `authorization_code` à partir d’Azure AD une fois l’utilisateur de hello termine la stratégie de hello. Hello `authorization_code` représente hello services du back-end du toocall autorisation de l’application pour le compte d’utilisateur de hello qui est actuellement connecté. application Hello échanger hello `authorization_code` en arrière-plan hello pour un `id_token` et un `refresh_token`.  application Hello peut utiliser hello `id_token` tooauthenticate tooa principal API web dans les demandes HTTP. Il peut également utiliser hello `refresh_token` tooget une nouvelle `id_token` lorsqu’un ancien arrive à expiration.

> [!NOTE]
> Azure AD B2C prend actuellement en charge que les jetons qui sont utilisés tooaccess à un service web principal de l’application. Par exemple, votre application dans son ensemble peut inclure une application iOS, une application Android et une API web principale. Cette architecture est entièrement prise en charge. Autoriser votre tooaccess d’application iOS une API web des partenaires à l’aide des jetons d’accès OAuth 2.0 n’est pas pris en charge actuellement. Tous les composants hello de votre application complète doivent partager un ID d’application unique.
>
>

![Images de couloirs d’application native](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Limitations actuelles
Azure AD B2C ne prend pas en charge hello les types d’applications suivants, mais ils se trouvent sur la feuille de route hello. 

### <a name="daemonsserver-side-apps"></a>Démons/applications côté serveur
Les applications qui contiennent les processus longs ou qui ne fonctionne pas sans la présence de hello d’un utilisateur également besoin de tooaccess des ressources telles que les API web sécurisées. Ces applications peuvent s’authentifier et obtenir des jetons en utilisant l’identité de l’application hello (plutôt qu’une identité déléguée d’un utilisateur) et à l’aide de flux d’informations d’identification du client hello OAuth 2.0.

Ce flux n’est pas actuellement pris en charge par Azure AD B2C. Ces applications peuvent uniquement obtenir des jetons après l’exécution d’un flux interactif utilisateur.

### <a name="web-api-chains-on-behalf-of-flow"></a>Chaînes d’API web (flux On-Behalf-Of)
Bon nombre d’architectures inclure une API qui doit toocall web à une autre API web en aval, où les deux sont sécurisées par Azure AD B2C. Ce scénario est courant chez les clients natifs disposant d’une API web principale. Il appelle ensuite un service en ligne Microsoft tels que hello API Azure AD Graph.

Ce scénario chaînées web API peut être pris en charge à l’aide d’octroi d’informations d’identification PORTEUR hello OAuth 2.0 JWT, également appelé hello sur à la place de flux.  Toutefois, hello sur à la place de flux n’est pas actuellement implémentée Bonjour Azure Active Directory B2C.
