---
title: "v2.0 aaaAzure AD flux de Code d’autorisation OAuth | Documents Microsoft"
description: "Génération d’applications web à l’aide de la mise en œuvre d’Azure AD hello OAuth 2.0 du protocole d’authentification."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocoles v2.0 : flux du code d’autorisation OAuth 2.0
octroi d’un code d’autorisation Hello OAuth 2.0 peut servir dans les applications qui sont installées sur un appareil toogain accès tooprotected des ressources, telles que les API web.  À l’aide de la mise en œuvre de v2.0 modèle hello application de OAuth 2.0, vous pouvez ajouter de connexion et API accès tooyour des applications mobiles et de bureau.  Ce guide est indépendant du langage et décrit comment toosend et recevoir des messages HTTP sans utiliser l’un de nos bibliothèques open source.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

Hello flux de code d’autorisation OAuth 2.0 est décrit dans [section 4.1 de spécification de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749).  Il est utilisé tooperform l’authentification et l’autorisation dans la majorité de hello des types d’application, y compris [les applications web](active-directory-v2-flows.md#web-apps) et [installé en mode natif les applications](active-directory-v2-flows.md#mobile-and-native-apps).  Elle permet aux applications toosecurely acquérir access_tokens qui peut être tooaccess utilisées les ressources qui sont sécurisés à l’aide du point de terminaison hello v2.0.  

## Schéma de protocole
À un niveau élevé, le flux d’authentification complète hello pour une application native/mobile ressemble un peu à ceci :

![Flux de code d’authentification OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Demander un code d’autorisation
flux de code d’autorisation Hello commence par client hello dirigeant hello utilisateur toohello `/authorize` point de terminaison.  Dans cette demande, client de hello indique les autorisations hello tooacquire à partir de l’utilisateur de hello :

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Cliquez sur lien hello tooexecute cette demande ! Une fois connecté, votre navigateur doit être redirigé trop`https://localhost/myapp/` avec un `code` dans la barre d’adresses hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |required |Hello Id d’Application ce portail d’inscription hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) attribué de votre application. |
| response_type |required |Doit inclure `code` pour les flux de code d’autorisation hello. |
| redirect_uri |recommandé |Bonjour redirect_uri de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application.  Il doit correspondre exactement à celle de redirect_uris hello que vous inscrit dans le portail hello, à ceci près qu’il doit être codée url.  Pour les applications natives et mobiles, vous devez utiliser la valeur par défaut hello `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| scope |required |Une liste séparée par des espaces de [étendues](active-directory-v2-scopes.md) que vous souhaitez tooconsent d’utilisateur hello pour. |
| response_mode |recommandé |Spécifie la méthode hello qui doit être utilisés toosend hello résultant tooyour précédent jeton application.  Peut être `query` ou `form_post`. |
| state |recommandé |Une valeur incluse dans la demande hello qui s’affichera dans la réponse du jeton hello.  Il peut s’agir d’une chaîne du contenu de votre choix.  Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| prompt |facultatif |Indique le type hello d’intervention de l’utilisateur qui est requise.  Hello uniquement à ce stade, les valeurs valides sont « login », « none » et « ».  `prompt=login`force sera hello utilisateur tooenter leurs informations d’identification sur cette demande, la négation de l’authentification unique sur.  `prompt=none`est hello opposé garantit que hello ne s’affiche avec une invite interactive que ce soit.  Si la demande de hello ne peut pas être effectuée en mode silencieux via l’authentification unique, point de terminaison hello v2.0 retournera une erreur.  `prompt=consent`sera hello de déclencheur OAuth consentement dialogue après le signe d’utilisateur hello, demandant hello utilisateur toogrant autorisations toohello application. |
| login_hint |facultatif |Peut être champ d’adresse utilisé toopre-remplissage hello nom d’utilisateur et de messagerie de hello page de connexion pour l’utilisateur de hello, si vous connaissez le nom d’utilisateur à l’avance.  Fréquence à laquelle les applications utilisent ce paramètre au cours de la réauthentification, ayant déjà extrait le nom d’utilisateur hello à partir d’une connexion précédente sign-in à l’aide de hello `preferred_username` de revendication. |
| domain_hint |facultatif |Peut être `consumers` ou `organizations`.  Si inclus, il ignore les processus de détection d’un e-mail hello que l’utilisateur parcourt sur la page, de connexion v2.0 hello début tooa rationalisé légèrement plus expérience utilisateur.  Fréquence à laquelle les applications utilisent ce paramètre au cours de la réauthentification, en extrayant hello `tid` à partir d’une connexion précédente sign-in.  Si hello `tid` est de valeur de revendication `9188040d-6c67-4c5b-b112-36a304b66dad`, vous devez utiliser `domain_hint=consumers`.  Sinon, utilisez `domain_hint=organizations`. |

À ce stade, l’utilisateur de hello sera demandé tooenter leurs informations d’identification et l’authentification de hello terminée.  Hello v2.0 le point de terminaison garantit également que l’utilisateur hello a consenti autorisations toohello indiquées Bonjour `scope` paramètre de requête.  Si l’utilisateur de hello a consenti pas tooany de ces autorisations, il vous demande hello utilisateur tooconsent toohello requis autorisations.  Les détails sur les [autorisations, les consentements et les applications mutualisées sont disponibles ici](active-directory-v2-scopes.md).

Une fois que l’utilisateur de hello s’authentifie et donne son consentement, point de terminaison hello v2.0 retournera une application tooyour de réponse à hello indiqué `redirect_uri`, à l’aide de la méthode hello spécifié dans hello `response_mode` paramètre.

#### Réponse correcte
Une réponse correcte utilisant `response_mode=query` se présente ainsi :

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Paramètre | Description |
| --- | --- |
| code |Bonjour authorization_code qui hello application demandée. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour la ressource cible de hello.  Les codes d’autorisation présentent une durée de vie très courte. Généralement, ils expirent au bout de 10 minutes. |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |

#### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin de l’application hello peut gérer de façon appropriée :

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

#### Codes d’erreur pour les erreurs de point de terminaison d’autorisation
Hello tableau suivant décrit hello différents codes d’erreur qui peuvent être retournées dans hello `error` paramètre de réponse d’erreur hello.

| Code d'erreur | Description | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| unauthorized_client |Hello application cliente n’est pas autorisé à toorequest un code d’autorisation. |Cela se produit généralement lorsque l’application cliente de hello n’est pas inscrit dans Azure AD ou locataire Azure AD de l’utilisateur toohello n’est pas ajoutée. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| access_denied |Le propriétaire de la ressource n’a pas accordé son consentement. |application cliente de Hello peut avertir l’utilisateur de hello il ne peut pas continuer à moins que hello utilisateur y consent. |
| unsupported_response_type |serveur d’autorisation de Hello ne prend pas en charge le type de réponse hello dans la demande de hello. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| server_error |serveur de Hello a rencontré une erreur inattendue. |Réessayez la demande de hello. Ces erreurs peuvent résulter de conditions temporaires. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison d’une erreur temporaire. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison d’une condition temporaire. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique la ressource de hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |

## Demander un jeton d’accès
Maintenant que vous avez acquis un authorization_code et l’autorisation avez été accordée par l’utilisateur de hello, vous pouvez échanger hello `code` pour un `access_token` toohello souhaité de ressource, en envoyant un `POST` demande toohello `/token` point de terminaison :

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Essayez d'exécuter cette requête dans Postman ! (N’oubliez pas tooreplace hello `code`) [ ![s’exécutent dans Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |required |Hello Id d’Application ce portail d’inscription hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) attribué de votre application. |
| grant_type |required |Doit être `authorization_code` pour les flux de code d’autorisation hello. |
| scope |required |Une liste d’étendues séparées par des espaces.  les étendues de Hello demandées dans cette branche doit être équivalente tooor un sous-ensemble des étendues de hello demandé dans la première branche de hello.  Si les étendues hello spécifiés dans cette requête sont réparties entre plusieurs serveurs de ressources, point de terminaison hello v2.0 retournera un jeton pour la ressource hello spécifiée dans l’étendue première hello.  Pour obtenir une explication plus détaillée des étendues, consultez trop[autorisations consentement et étendues](active-directory-v2-scopes.md). |
| code |required |Bonjour authorization_code que vous avez obtenue dans la première branche de hello du flux de hello. |
| redirect_uri |required |Bonjour la même valeur redirect_uri qui a été utilisé tooacquire hello authorization_code. |
| client_secret |requis pour les applications Web |secret d’application Hello que vous avez créé dans le portail de l’enregistrement d’application hello pour votre application.  Il ne doit pas être utilisé dans une application native, car les clés secrètes client ne peuvent pas être stockées de manière sûre sur les appareils.  Il est requis pour les applications web et des API qui ont hello capacité toostore hello client_secret en toute sécurité sur le côté du serveur hello web. |

#### Réponse correcte
Une réponse de jeton réussie se présente ainsi :

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès demandé Hello. application Hello peut utiliser cette toohello tooauthenticate jeton ressource, telle qu’une API web sécurisée. |
| token_type |Indique la valeur de jeton de type hello. seul le type qui prend en charge par Azure AD Hello est porteur |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| scope |étendues de Hello hello access_token est valide pour. |
| refresh_token |Un jeton d’actualisation OAuth 2.0. Hello application peut utiliser ce jeton acquérir des jetons d’accès supplémentaires après l’expiration du jeton d’accès actuel hello.  Refresh_tokens sont de longue durée et peut être utilisé tooretain accès tooresources pendant de longues périodes de temps.  Pour plus d’informations, consultez toohello [référence de jeton v2.0](active-directory-v2-tokens.md). |
| id_token |Un jeton Web JSON non signé (JWT). Hello application peut base64Url décoder segments hello de ces informations de jeton toorequest sur utilisateur hello connectés. application Hello peut mettre en cache les valeurs hello et les afficher, mais il ne doit pas dépendre les pour toute l’autorisation ou des limites de sécurité.  Pour plus d’informations sur id_tokens consultez hello [référence de jeton de point de terminaison v2.0](active-directory-v2-tokens.md). |

#### Réponse d’erreur
Les réponses d’erreur se présentent comme suit :

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |heure de Hello hello erronée. |
| trace_id |Identificateur unique pour la demande hello qui peut aider dans les diagnostics. |
| correlation_id |Identificateur unique pour la demande hello qui peut vous aider à diagnostics entre les composants. |

#### Codes d’erreur pour les erreurs de point de terminaison de jeton
| Code d'erreur | Description | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez et soumettez à nouveau la demande de hello |
| invalid_grant |code d’autorisation de Hello n’est pas valide ou a expiré. |Essayez une nouvelle toohello de demande `/authorize` point de terminaison |
| unauthorized_client |Hello client authentifié n’est pas autorisé toouse type d’accorder cette autorisation. |Cela se produit généralement lorsque l’application cliente de hello n’est pas inscrit dans Azure AD ou locataire Azure AD de l’utilisateur toohello n’est pas ajoutée. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| invalid_client |Échec d’authentification du client. |informations d’identification du client Hello ne sont pas valides. toofix, administrateur de l’application hello met à jour les informations d’identification hello. |
| unsupported_grant_type |serveur d’autorisation de Hello ne prend pas en charge le type d’octroi d’autorisation hello. |Hello de modification accorder le type de demande de hello. Ce type d’erreur doit se produire uniquement lors du développement et doit être détecté lors du test initial. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique la ressource de hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |
| interaction_required |demande de Hello nécessite une interaction utilisateur. Par exemple, une étape d’authentification supplémentaire est nécessaire. |Nouvelle tentative de demande hello avec hello même ressource. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison d’une condition temporaire. |

## Utilisation du jeton d’accès hello
Maintenant que vous avez acquis avec succès une `access_token`, vous pouvez utiliser le jeton de hello dans les demandes tooWeb API en l’incluant dans hello `Authorization` en-tête :

> [!TIP]
> Exécutez cette requête dans Postman ! (Remplacez hello `Authorization` en-tête première) [ ![s’exécutent dans Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Actualiser le jeton d’accès hello
Access_tokens est courte durée de vie, et vous devez les actualiser après l’expiration des toocontinue l’accès aux ressources.  Vous pouvez le faire en envoyant un autre `POST` demande toohello `/token` point de terminaison, cette fois en fournissant hello `refresh_token` au lieu de hello `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Essayez d'exécuter cette requête dans Postman ! (N’oubliez pas tooreplace hello `refresh_token`) [ ![s’exécutent dans Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |required |Hello Id d’Application ce portail d’inscription hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) attribué de votre application. |
| grant_type |required |Doit être `refresh_token` pour cette branche du flux de code d’autorisation hello. |
| scope |required |Une liste d’étendues séparées par des espaces.  les étendues de Hello demandées dans cette branche doit être équivalente tooor un sous-ensemble des étendues de hello demandé dans le tronçon de requête authorization_code hello d’origine.  Si les étendues hello spécifiés dans cette requête sont réparties entre plusieurs serveurs de ressources, point de terminaison hello v2.0 retournera un jeton pour la ressource hello spécifiée dans l’étendue première hello.  Pour obtenir une explication plus détaillée des étendues, consultez trop[autorisations consentement et étendues](active-directory-v2-scopes.md). |
| refresh_token |required |Bonjour refresh_token que vous avez obtenue dans la branche de deuxième hello du flux de hello. |
| redirect_uri |required |Bonjour la même valeur redirect_uri qui a été utilisé tooacquire hello authorization_code. |
| client_secret |requis pour les applications Web |secret d’application Hello que vous avez créé dans le portail de l’enregistrement d’application hello pour votre application.  Il ne doit pas être utilisé dans une application native, car les clés secrètes client ne peuvent pas être stockées de manière sûre sur les appareils.  Il est requis pour les applications web et des API qui ont hello capacité toostore hello client_secret en toute sécurité sur le côté du serveur hello web. |

#### Réponse correcte
Une réponse de jeton réussie se présente ainsi :

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès demandé Hello. application Hello peut utiliser cette toohello tooauthenticate jeton ressource, telle qu’une API web sécurisée. |
| token_type |Indique la valeur de jeton de type hello. seul le type qui prend en charge par Azure AD Hello est porteur |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| scope |étendues de Hello hello access_token est valide pour. |
| refresh_token |Un nouveau jeton d’actualisation OAuth 2.0. Vous devez remplacer l’actualisation hello ancien jeton avec cette tooensure de jeton d’actualisation récemment acquis vos jetons d’actualisation restent valides aussi longtemps que possible. |
| id_token |Un jeton Web JSON non signé (JWT). Hello application peut base64Url décoder segments hello de ces informations de jeton toorequest sur utilisateur hello connectés. application Hello peut mettre en cache les valeurs hello et les afficher, mais il ne doit pas dépendre les pour toute l’autorisation ou des limites de sécurité.  Pour plus d’informations sur id_tokens consultez hello [référence de jeton de point de terminaison v2.0](active-directory-v2-tokens.md). |

#### Réponse d’erreur
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |heure de Hello hello erronée. |
| trace_id |Identificateur unique pour la demande hello qui peut aider dans les diagnostics. |
| correlation_id |Identificateur unique pour la demande hello qui peut vous aider à diagnostics entre les composants. |

Pour obtenir une description des codes d’erreur hello et hello client action recommandée, consultez [codes d’erreur pour les erreurs de point de terminaison de jeton](#error-codes-for-token-endpoint-errors).

