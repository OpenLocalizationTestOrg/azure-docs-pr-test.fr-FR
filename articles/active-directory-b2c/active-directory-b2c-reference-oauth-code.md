---
title: "Flux de code d’autorisation - Azure AD B2C | Microsoft Docs"
description: "Découvrez comment toobuild web des applications à l’aide du protocole d’authentification Azure AD B2C et OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C : flux de code d’autorisation OAuth 2.0
Vous pouvez utiliser l’octroi d’un code d’autorisation hello OAuth 2.0 dans les applications installées sur un appareil toogain accès tooprotected des ressources, telles que les API web. À l’aide de mise en œuvre de hello Azure Active Directory B2C (Azure AD B2C) de OAuth 2.0, vous pouvez ajouter d’abonnement, connectez-vous et les tâches de gestion d’identité tooyour des applications mobiles et de bureau. Cet article est indépendant du langage. Dans l’article hello, nous décrivons comment toosend et recevoir des messages HTTP sans utiliser les bibliothèques open source.

<!-- TODO: Need link toolibraries -->

Hello flux de code d’autorisation OAuth 2.0 est décrit dans [section 4.1 de spécification de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). Vous pouvez l’utiliser pour les activités d’authentification et d’autorisation avec la plupart des types d’applications, notamment les [applications web](active-directory-b2c-apps.md#web-apps) et les [applications installées de façon native](active-directory-b2c-apps.md#mobile-and-native-apps). Vous pouvez utiliser hello OAuth 2.0 toosecurely de flux de code d’autorisation acquérir *jetons d’accès* pour vos applications, ce qui peut être utilisé tooaccess les ressources qui sont sécurisés par une [serveur d’autorisation](active-directory-b2c-reference-protocols.md#the-basics).

Cet article se concentre sur hello **clients publics** flux de code d’autorisation OAuth 2.0. Un client public est toute application cliente qui ne peut pas être approuvée toosecurely préserver l’intégrité des hello de mot de passe secret principal. Cela inclut les applications mobiles, les applications de bureau et essentiellement n’importe quelle application qui s’exécute sur un appareil et nécessite des jetons d’accès tooget. 

> [!NOTE]
> application tooadd identity management tooa web à l’aide d’Azure AD B2C, utilisez [OpenID Connect](active-directory-b2c-reference-oidc.md) au lieu de OAuth 2.0.

Azure AD B2C étend standard hello Qu'oauth 2.0 flux toodo plus de l’autorisation et d’authentification simple. Il introduit hello [paramètre de stratégie](active-directory-b2c-reference-policies.md). Avec les stratégies intégrées, vous pouvez utiliser OAuth 2.0 tooadd utilisateur rencontre tooyour application, telles que d’abonnement, connectez-vous et gestion des profils. Dans cet article, nous vous indiquons comment toouse tooimplement OAuth 2.0 et les stratégies de chacun de ces expériences dans vos applications natives. Nous vous montrons également comment tooget les jetons d’accès pour l’accès aux API web.

Dans les requêtes d’exemple HTTP hello dans cet article, nous utilisons notre répertoire Azure AD B2C d’exemple, **fabrikamb2c.onmicrosoft.com**. Nous utilisons également nos exemples d’application et de stratégies. Vous pouvez essayer de demandes de hello vous-même à l’aide de ces valeurs, ou vous pouvez les remplacer par vos propres valeurs.
Découvrez comment trop[obtenir votre propre annuaire Azure AD B2C, application et des stratégies](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Obtention d’un code d’autorisation
flux de code d’autorisation Hello commence par client hello dirigeant hello utilisateur toohello `/authorize` point de terminaison. Il s’agit partie interactive de hello du flux de hello, où les utilisateurs hello intervient. Dans cette demande, les clients hello indique Bonjour `scope` autorisations hello de paramètre qu’il nécessite de tooacquire à partir de l’utilisateur de hello. Bonjour `p` paramètre, il indique hello stratégie tooexecute. Hello trois chacun des exemples suivants (avec les sauts de ligne pour une meilleure lisibilité) utilisent une stratégie différente.

### <a name="use-a-sign-in-policy"></a>Utilisation d’une stratégie de connexion
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Utilisation d’une stratégie d’inscription
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Utilisation d’une stratégie de modification de profil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| client_id |Requis |ID de l’application Hello affecté application tooyour Bonjour [portail Azure](https://portal.azure.com). |
| response_type |Requis |type de réponse Hello, qui doit inclure `code` pour les flux de code d’autorisation hello. |
| redirect_uri |Requis |Hello URI de redirection de votre application, où les réponses d’authentification sont envoyés et reçus par votre application. Il doit correspondre exactement à celle de redirection de hello URI que vous avez enregistré dans le portail hello, sauf qu’il doit être encodé en URL. |
| scope |Requis |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure Active Directory (Azure AD) à la fois des autorisations de hello sont demandées. À l’aide du client hello ID de la portée de hello indique que votre application a besoin d’un jeton d’accès qui peut être utilisé avec votre propre service ou d’une API web, représenté par hello même ID de client.  Hello `offline_access` étendue indique que votre application a besoin d’un jeton d’actualisation pour l’accès à long terme tooresources. Vous pouvez également utiliser hello `openid` étendue toorequest un jeton d’ID à partir d’Azure Active Directory B2C. |
| response_mode |Recommandé |méthode Hello utiliser tooyour précédent code d’autorisation qui en résulte toosend hello application. Il peut s’agir de `query`, `form_post` ou `fragment`. |
| state |Recommandé |Une valeur incluse dans la demande hello qui est retourné dans la réponse du jeton hello. Il peut être une chaîne de contenu que vous souhaitez toouse. En règle générale, une valeur unique générée de manière aléatoire est utilisée, les attaques par falsification de tooprevent demande entre sites. état de Hello est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite. Par exemple, utilisateur de hello page hello a eu lieu ou hello stratégie était en cours d’exécution. |
| p |Requis |stratégie de Hello est exécutée. Son hello nom d’une stratégie qui est créée dans votre répertoire Azure Active Directory B2C. valeur de nom de stratégie Hello doit commencer par **b2c\_1\_**. toolearn en savoir plus sur les stratégies, consultez [stratégies intégrées d’Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Facultatif |type de Hello d’intervention de l’utilisateur qui est requise. Actuellement, hello seule valeur valide est `login`, qui force hello utilisateur tooenter leurs informations d’identification pour cette demande. L’authentification unique ne prendra pas effet. |

À ce stade, les flux de travail de la stratégie toocomplete hello est demandé à utilisateur de hello. Cela peut également impliquer l’utilisateur de hello entrer leur nom d’utilisateur et un mot de passe, vous connecter avec une identité sociale, souscrire hello répertoire ou tout autre nombre d’étapes. Actions de l’utilisateur dépendent de la stratégie de hello est définie.

Utilisateur de hello après la stratégie de hello, Azure AD renvoie une application tooyour de réponse à la valeur hello vous avez utilisé pour `redirect_uri`. Il utilise la méthode hello spécifié dans hello `response_mode` paramètre. réponse de Hello est exactement hello même pour chacun des hello action scénarios utilisateur, indépendamment de la stratégie de hello qui a été exécutée.

Une réponse correcte utilisant `response_mode=query` se présente ainsi :

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Paramètre | Description |
| --- | --- |
| code |code d’autorisation Hello hello application demandée. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour une ressource cible. Les codes d’autorisation ont des durées de vie très courtes. Généralement, ils expirent au bout de 10 minutes. |
| state |Consultez la description complète de hello dans table hello hello précédant la section. Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |

Réponses d’erreur peuvent également être envoyés l’URI de redirection toohello afin que hello application peut gérer de façon appropriée :

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser les types de hello tooclassify d’erreurs qui se produisent. Vous pouvez également utiliser hello chaîne tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |
| state |Consultez la description complète de hello Bonjour tableau précédent. Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |

## <a name="2-get-a-token"></a>2. Obtention d’un jeton
Maintenant que vous avez acquis un code d’autorisation, vous pouvez échanger hello `code` pour un jeton toohello prévu des ressources en envoyant un toohello de la demande POST `/token` point de terminaison. Dans Azure AD B2C, hello uniquement les ressources que vous pouvez demander un jeton sont votre site web principal de l’application API. convention de Hello est utilisée pour demander un jeton tooyourself est toouse l’ID de client de votre application en tant qu’étendue de hello :

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| p |Requis |Hello stratégie qui a été utilisé tooacquire hello autorisation code. Vous ne pouvez pas utiliser une autre stratégie dans cette demande. Notez que vous ajoutez ce paramètre toohello *chaîne de requête*, et non dans hello corps POST. |
| client_id |Requis |ID de l’application Hello affecté application tooyour Bonjour [portail Azure](https://portal.azure.com). |
| grant_type |Requis |type Hello d’octroi. Pour les flux de code d’autorisation hello, type d’octroi hello doit être `authorization_code`. |
| scope |Recommandé |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD à la fois des autorisations de hello sont demandés. À l’aide du client hello ID de la portée de hello indique que votre application a besoin d’un jeton d’accès qui peut être utilisé avec votre propre service ou d’une API web, représenté par hello même ID de client.  Hello `offline_access` étendue indique que votre application a besoin d’un jeton d’actualisation pour l’accès à long terme tooresources.  Vous pouvez également utiliser hello `openid` étendue toorequest un jeton d’ID à partir d’Azure Active Directory B2C. |
| code |Requis |code d’autorisation Hello que vous avez obtenue dans la première branche de hello du flux de hello. |
| redirect_uri |Requis |Hello URI de redirection d’application hello où vous avez reçu le code d’autorisation de hello. |

Un jeton de réponse correct se présente ainsi :

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Paramètre | Description |
| --- | --- |
| not_before |heure de Hello à quels hello jeton est considéré comme valide dans le temps de l’époque. |
| token_type |valeur de type de jeton Hello. Hello tapez uniquement que prend en charge d’Azure AD est porteur. |
| access_token |Hello signé le jeton Web JSON (JWT) que vous avez demandé. |
| scope |étendues de Hello hello jeton est valide pour. Vous pouvez également utiliser des jetons de toocache étendues pour une utilisation ultérieure. |
| expires_in |Durée Hello de hello jeton est valide (en secondes). |
| refresh_token |Un jeton d’actualisation OAuth 2.0. application Hello peut utiliser ce jeton tooacquire des jetons supplémentaires après l’expiration du jeton actuel de hello. Les jetons d’actualisation sont de longue durée. Vous pouvez utiliser les tooretain accès tooresources pendant de longues périodes de temps. Pour plus d’informations, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Les réponses d’erreur ressemblent à ceci :

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser les types de hello tooclassify d’erreurs qui se produisent. Vous pouvez également utiliser hello chaîne tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |

## <a name="3-use-hello-token"></a>3. Utilisation du jeton hello
Maintenant que vous avez acquis avec succès d’un jeton d’accès, vous pouvez utiliser le jeton de hello dans l’API web principale tooyour de demandes en l’incluant dans hello `Authorization` en-tête :

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Actualiser le jeton de hello
Les jetons d’accès et les jetons d’ID ont une courte durée de vie. Une fois qu’ils expirent, vous devez actualiser les toocontinue tooaccess ressources. toodo, envoyer un autre toohello de demande POST `/token` point de terminaison. Cette fois-ci, fournir hello `refresh_token` au lieu de hello `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| p |Requis |stratégie Hello qui était le jeton d’actualisation d’origine utilisé tooacquire hello. Vous ne pouvez pas utiliser une autre stratégie dans cette demande. Notez que vous ajoutez ce paramètre toohello *chaîne de requête*, et non dans hello corps POST. |
| client_id |Recommandé |ID de l’application Hello affecté application tooyour Bonjour [portail Azure](https://portal.azure.com). |
| grant_type |Requis |type Hello d’octroi. Pour cette branche du flux de code d’autorisation hello, type d’octroi hello doit être `refresh_token`. |
| scope |Recommandé |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD à la fois des autorisations de hello sont demandés. À l’aide du client hello ID de la portée de hello indique que votre application a besoin d’un jeton d’accès qui peut être utilisé avec votre propre service ou d’une API web, représenté par hello même ID de client.  Hello `offline_access` étendue indique que nécessaires à votre application un jeton d’actualisation pour l’accès à long terme tooresources.  Vous pouvez également utiliser hello `openid` étendue toorequest un jeton d’ID à partir d’Azure Active Directory B2C. |
| redirect_uri |Facultatif |Hello URI de redirection d’application hello où vous avez reçu le code d’autorisation de hello. |
| refresh_token |Requis |Hello d’origine jeton d’actualisation que vous avez obtenue dans la branche de deuxième hello du flux de hello. |

Un jeton de réponse correct se présente ainsi :

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Paramètre | Description |
| --- | --- |
| not_before |heure de Hello à quels hello jeton est considéré comme valide dans le temps de l’époque. |
| token_type |valeur de type de jeton Hello. Hello tapez uniquement que prend en charge d’Azure AD est porteur. |
| access_token |Hello signé JSON que vous avez demandé. |
| scope |étendues de Hello hello jeton est valide pour. Vous pouvez également utiliser des jetons de toocache hello étendues pour une utilisation ultérieure. |
| expires_in |Durée Hello de hello jeton est valide (en secondes). |
| refresh_token |Un jeton d’actualisation OAuth 2.0. application Hello peut utiliser ce jeton tooacquire des jetons supplémentaires après l’expiration du jeton actuel de hello. Actualiser les jetons sont de longue durées et peut être utilisé tooretain accès tooresources pendant de longues périodes de temps. Pour plus d’informations, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Les réponses d’erreur ressemblent à ceci :

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser les types de tooclassify d’erreurs qui se produisent. Vous pouvez également utiliser hello chaîne tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Utiliser votre propre annuaire Azure AD B2C
tootry ces demandes vous-même, hello complet suivant les étapes. Remplacez les valeurs d’exemple hello que nous avons utilisé dans cet article avec vos propres valeurs.

1. [Créez un annuaire Azure AD B2C](active-directory-b2c-get-started.md). Utiliser le nom hello de votre annuaire dans les demandes hello.
2. [Créer une application](active-directory-b2c-app-registration.md) tooobtain un ID d’application et un URI de redirection. Incluez un client natif dans votre application.
3. [Créer vos stratégies](active-directory-b2c-reference-policies.md) tooobtain vos noms de stratégie.

