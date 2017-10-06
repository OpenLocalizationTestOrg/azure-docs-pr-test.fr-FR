---
title: "Azure Active Directory B2C : Demande de jetons d’accès | Microsoft Docs"
description: "Cet article vous indiquent comment toosetup une application cliente et acquérir un jeton d’accès."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C : Demande de jetons d’accès

Un jeton d’accès (notée **accès\_jeton** dans les réponses hello à partir d’Azure AD B2C) est une forme de jeton de sécurité qu’un client peut utiliser les ressources tooaccess est sécurisé par une [le serveur d’autorisation](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), telle qu’une API web. Les jetons d’accès sont représentés en tant que [jetons Web JSON](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) et contiennent des informations sur le serveur de ressources prévue de hello et le serveur de toohello d’autorisations accordées hello. Lorsque vous appelez le serveur de ressources hello, jeton d’accès hello doit être présent dans la demande HTTP hello.

Cet article explique comment tooconfigure une application cliente et l’API web dans l’ordre de tooobtain un **accès\_jeton**.

> [!NOTE]
> **Les chaînes d’API web (pour le compte de) ne sont pas prises en charge par Azure AD B2C.**
>
> Bon nombre d’architectures inclure une API qui doit toocall web une autre API web en aval, les deux sécurisés par Azure AD B2C. Ce scénario est courant dans les clients natifs qui ont une API web principale, qui à son tour appelle un service en ligne Microsoft tels que hello API Azure AD Graph.
>
> Ce scénario chaînées web API peut être pris en charge à l’aide de hello octroi des informations d’identification du support OAuth 2.0 JWT, sinon appelé hello sur à la place de flux. Toutefois, hello sur à la place de flux n’est pas actuellement implémentée dans Azure AD B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Inscrire une API web et publier des autorisations

Avant de demander un jeton d’accès, vous tout d’abord besoin tooregister une API web et publiez les autorisations (étendues) qui peuvent être accordées application cliente de toohello.

### <a name="register-a-web-api"></a>Inscrire une API web

1. Dans Panneau de fonctionnalités hello B2C sur hello portail Azure, cliquez sur **Applications**.
1. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
1. Entrez un **nom** pour l’application hello qui décrire votre tooconsumers d’application. Par exemple, vous pouvez entrer « API Contoso ».
1. Hello de bascule **incluent l’application web / web API** basculer trop**Oui**.
1. Entrez une valeur arbitraire pour hello **URL de réponse**. Par exemple, entrez : `https://localhost:44316/`. valeur de Hello est sans importance, car une API ne doit-elle pas recevoir le jeton de hello directement à partir d’Azure Active Directory B2C.
1. Entrez un **URI ID d’application**. Il s’agit d’identificateur hello utilisé pour votre API web. Par exemple, entrez « Remarques » dans la zone de hello. Hello **URI ID d’application** serait alors `https://{tenantName}.onmicrosoft.com/notes`.
1. Cliquez sur **créer** tooregister votre application.
1. Cliquez sur l’application hello que vous venez de créer et de copier hello globalement unique **identifiant Client d’Application** que vous utiliserez ultérieurement dans votre code.

### <a name="publishing-permissions"></a>Publication des autorisations

Étendues de toopermissions analogues, sont nécessaires lorsque votre application appelle une API. « Lecture » ou « écriture » sont des exemples d’étendues. Supposons que vous souhaitez que votre web ou une application native trop « lecture » à partir d’une API. Appelez votre application Azure AD B2C et demande de jeton d’accès qui donne accès toohello étendue « lecture ». Pour Azure AD B2C tooemit telle un jeton d’accès, application hello doit toobe accordé l’autorisation trop « lecture » à partir de l’API spécifique de hello. toodo, votre API doit tout d’abord toopublish hello « lecture » étendue.

1. Dans Azure AD B2C de hello **Applications** panneau, web de hello ouvrir l’application API (« API Contoso »).
1. Cliquez sur **Étendues publiées**. Il s’agit où vous définissez les autorisations de hello (étendues) qui peuvent être accordées tooother applications.
1. Ajoutez les **valeurs d’étendue** si nécessaire (par exemple, « lecture »). Par défaut, l’étendue « user_impersonation » hello sera défini. Vous pouvez l’ignorer si vous le souhaitez. Entrez une description de l’étendue de hello dans hello **nom de l’étendue** colonne.
1. Cliquez sur **Enregistrer**.

> [!IMPORTANT]
> Hello **nom de l’étendue** description hello Hello **valeur étendue**. Lorsque vous utilisez l’étendue de hello, assurez-vous que toouse hello **valeur étendue**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Accorder native ou web application autorisations tooa web API

Une fois configuré toopublish étendues, une API application cliente de hello doit toobe accordé ces étendues via hello portail Azure.

1. Accédez toohello **Applications** menu dans le panneau de fonctionnalités hello B2C.
1. Inscrivez une application cliente ([application web](active-directory-b2c-app-registration.md#register-a-web-app) ou [cliente native](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) si vous ne l’avez pas déjà fait. Si vous suivez ce guide comme point de départ, vous devez tooregister une application cliente.
1. Cliquez sur **Accès d’API**.
1. Cliquez sur **Ajouter**.
1. Sélectionnez vos étendues hello et les API web (autorisations) toogrant voulue.
1. Cliquez sur **OK**.

> [!NOTE]
> Azure Active Directory B2C ne demande pas leur consentement aux utilisateurs de votre application cliente. Au lieu de cela, le consentement tous les est fourni par hello admin, en fonction des autorisations hello configurées entre les applications hello décrites ci-dessus. Si une autorisation pour une application est révoquée, tous les utilisateurs qui ont été préalablement tooacquire cette autorisation ne sera plus être en mesure de toodo donc.

## <a name="requesting-a-token"></a>Demande d’un jeton

Lors de la demande un jeton d’accès, application de client hello a besoin d’autorisations de hello souhaité toospecify Bonjour **étendue** paramètre de requête de hello. Par exemple, toospecify hello **étendue valeur** « lecture » pour hello API qui a hello **URI ID d’application** de `https://contoso.onmicrosoft.com/notes`, étendue de hello serait `https://contoso.onmicrosoft.com/notes/read`. Voici un exemple d’un toohello de demande de code d’autorisation `/authorize` point de terminaison.

> [!NOTE]
> Actuellement, les domaines personnalisés ne sont pas pris en charge avec les jetons d’accès. Vous devez utiliser votre domaine tenantName.onmicrosoft.com dans l’URL de demande hello.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire plusieurs autorisations Bonjour même demande, vous pouvez ajouter plusieurs entrées Bonjour unique **étendue** paramètre, séparé par des espaces. Par exemple :

URL décodée :

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

URL encodée :

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

Vous pouvez demander plus d’étendues (autorisations) pour une ressource que ce qui est accordé pour votre application cliente. Si c’est le cas de hello, hello appel réussi si au moins une autorisation est accordée. Hello résultant **accès\_jeton** aura son revendication « scp » renseignée avec les seules autorisations hello qui ont été accordées avec succès.

> [!NOTE] 
> Nous ne prennent pas en charge demandant des autorisations sur les deux ressources de l’autre site web Bonjour même demande. Ce type de demande échoue.

### <a name="special-cases"></a>Cas particuliers

Hello OpenID Connect standard spécifie plusieurs valeurs spéciales « portée ». Hello suivant étendues spéciaux représentent hello autorisation trop « accès hello profil utilisateur » :

* **OpenID** : cette étendue demande un jeton d’ID
* **offline\_access** : cette étendue demande un jeton d’actualisation (à l’aide du [flux de code d’authentification](active-directory-b2c-reference-oauth-code.md)).

Si hello `response_type` paramètre dans un `/authorize` demande inclut `token`, hello `scope` paramètre doit inclure l’étendue d’au moins une ressource (autre que `openid` et `offline_access`) qui est accordée. Dans le cas contraire, hello `/authorize` demande s’arrête avec un échec.

## <a name="hello-returned-token"></a>Hello renvoyé un jeton

Dans un correctement a été réalisé conformément **accès\_jeton** (à partir de deux hello `/authorize` ou `/token` point de terminaison), suivant de hello revendications sera présente :

| Nom | Revendication | Description |
| --- | --- | --- |
|Public ciblé |`aud` |Hello **ID d’application** de ressource hello ce jeton hello accorde l’accès à. |
|Scope |`scp` |Hello autorisations toohello ressource. Plusieurs autorisations octroyées doivent être séparées par une espace. |
|Tiers autorisé |`azp` |Hello **ID d’application** d’application cliente hello qui a initié la demande de hello. |

Lorsque votre API reçoit hello **accès\_jeton**, il doit [valider hello jeton](active-directory-b2c-reference-tokens.md) tooprove hello jeton est authentique et qu’il possède les revendications correct hello.

Nous sommes toujours ouvrir toofeedback ainsi que des suggestions ! Si vous avez des difficultés avec cette rubrique, veuillez la publier sur le débordement de pile à l’aide de la balise de hello ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Étapes suivantes

* Générer une API web à l’aide de [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Générer une API web à l’aide de [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
