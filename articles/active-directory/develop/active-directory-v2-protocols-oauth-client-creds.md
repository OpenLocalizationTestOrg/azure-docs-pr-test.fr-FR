---
title: "aaaUse Azure AD v2.0 tooaccess sécuriser les ressources sans intervention de l’utilisateur | Documents Microsoft"
description: "Générer des applications web à l’aide d’implémentation hello AD Azure hello OAuth 2.0 du protocole d’authentification."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 hello OAuth 2.0 client informations d’identification et de flux
Vous pouvez utiliser hello [accorder des informations d’identification du client OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), parfois appelées *à deux branches de OAuth*, tooaccess hébergé sur le web de ressources à l’aide d’identité hello d’une application. Ce type d’octroi couramment est utilisé pour les interactions de serveur à serveur qui doivent s’exécuter en arrière-plan hello, sans intervention de l’exécution à un utilisateur. Ces types d’applications sont souvent désignée tooas *démons* ou *comptes de service*.

> [!NOTE]
> point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory. toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

Bonjour plus classique *OAuth de trois phases*, une application cliente est tooaccess de l’autorisation accordée à une ressource pour le compte d’un utilisateur spécifique. autorisation de Hello est déléguée à partir de l’application toohello utilisateur hello, généralement dans le cadre hello [consentement](active-directory-v2-scopes.md) processus. Toutefois, dans le flux des informations d’identification des clients hello, autorisations sont accordées directement application toohello lui-même. Lors de l’application hello présente une ressource de jeton tooa, les ressources hello impose qu’application hello lui-même a une action d’autorisation tooperform et pas cet utilisateur hello a l’autorisation.

## Schéma de protocole
flux d’informations d’identification Hello client entier recherche des diagramme suivant toohello similaire. Nous décrivent chacune des étapes hello plus loin dans cet article.

![Flux des informations d’identification du client](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Obtenir l’autorisation directe
Une application reçoit généralement directe d’autorisation tooaccess une ressource de deux manières : via une liste de contrôle d’accès (ACL) au niveau de ressource de hello, ou via une attribution d’autorisation application dans Azure Active Directory (Azure AD). Ces deux méthodes sont hello plus courant dans Azure AD, et nous vous recommandons pour les clients et les ressources qui effectuent le flux d’informations d’identification du client hello. Une ressource peut choisir tooauthorize ses clients d’autres manières, toutefois. Chaque serveur de ressources peut choisir la méthode hello hello plus logique pour son application.

### Listes de contrôle d'accès
Un fournisseur de ressources peut appliquer une vérification d’autorisation basée sur une liste d’ID d’application qu’il connaît et octroyer un niveau d’accès spécifique. Lors de la ressource de hello reçoit un jeton à partir du point de terminaison hello v2.0, il peut décoder le jeton de hello et extraire des ID d’Application du client hello hello `appid` et `iss` revendications. Elle compare ensuite application hello par rapport à une liste ACL qu’il gère. granularité de l’ACL de Hello et méthode peut-être varier considérablement entre les ressources.

Un cas d’usage courant est toouse un toorun ACL teste pour une application web ou d’une API Web. Hello API Web peut accorder uniquement un sous-ensemble de client spécifique de tooa toutes les autorisations. les tests de bout en bout toorun hello API, créez un client de test qui acquiert des jetons à partir du point de terminaison hello v2.0, puis les envoie toohello API. ID d’Application du client pour un accès complet des fonctionnalités entière toohello l’API de test Hello API puis vérifications hello ACL pour hello. Si vous utilisez ce type de liste ACL, veillez à toovalidate hello non seulement l’appelant `appid` valeur. Également valider ce hello `iss` valeur du jeton de hello est approuvé.

Ce type d’autorisation est courant pour les processus et les comptes de service nécessitant des données tooaccess appartienne aux utilisateurs de consommateur qui ont des comptes personnels de Microsoft. Les données appartenant à des organisations, nous recommandons que vous obtenez l’autorisation nécessaire de hello via les autorisations de l’application.

### Autorisations de l’application
Au lieu d’utiliser des ACL, vous pouvez utiliser les API tooexpose un jeu d’autorisations de l’application. Autorisation de l’application est accordée tooan application par l’administrateur d’une organisation, et peuvent être utilisés tooaccess uniquement données détenues par cette organisation et ses employés. Par exemple, Microsoft Graph expose plusieurs applications autorisations toodo hello éléments suivants :

* Lire les messages dans toutes les boîtes aux lettres
* Lire et écrire des messages dans toutes les boîtes aux lettres
* Envoyer des messages en tant que n’importe quel utilisateur
* Lire les données du répertoire

Pour plus d’informations sur les autorisations d’application, accédez trop[Microsoft Graph](https://graph.microsoft.io).

autorisations d’application toouse dans votre application, procédez comme hello suit les sujets abordés dans les sections suivantes hello.

#### Demander des autorisations dans le portail de l’enregistrement d’application hello hello
1. Accédez application tooyour Bonjour [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou [créer une application](active-directory-v2-app-registration.md), si vous n’avez pas encore. Vous devez toouse au moins un Secret d’Application lorsque vous créez votre application.
2. Recherchez hello **autorisations d’Application Direct** section, puis ajoutez les autorisations de hello que votre application requiert.
3. **Enregistrer** hello d’inscription d’une application.

#### Recommandé : Se connecter hello utilisateur dans l’application de tooyour
En règle générale, lorsque vous générez une application qui utilise les autorisations d’application, application hello requiert une page ou un affichage sur le hello administrateur approuve les autorisations de l’application hello. Cette page peut faire partie de flux de connexion l’application hello, dans les paramètres de l’application hello, ou il peut être « se connecter » flux dédié. Dans de nombreux cas, il est logique pour hello application tooshow cela « se connecter » afficher uniquement une fois un utilisateur connecté avec un professionnel ou scolaire compte Microsoft.

Si vous vous connectez utilisateur hello dans tooyour application, vous pouvez identifier les organisation hello utilisateur de hello toowhich appartient avant de vous demandez des autorisations d’application hello hello utilisateur tooapprove. Bien que cela ne soit pas strictement nécessaire, cela peut vous aider à créer une expérience plus intuitive pour vos utilisateurs. toosign hello utilisateur, suivez notre [didacticiels de protocole v2.0](active-directory-v2-protocols.md).

#### Demander des autorisations hello à partir d’un administrateur d’annuaire
Lorsque vous êtes prêt toorequest les autorisations de l’administrateur de l’organisation hello, vous pouvez rediriger hello utilisateur toohello v2.0 *point de terminaison admin consentement*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Paramètre | Condition | Description |
| --- | --- | --- |
| locataire |Requis |locataire d’annuaire Hello toorequest autorisation souhaité. Peut être au format GUID ou sous forme de nom convivial. Si vous ne connaissez pas les utilisateurs qui hello client appartient tooand vous souhaitez toolet les connectez-vous avec n’importe quel client, utilisez `common`. |
| client_id |Requis |Hello Application ID que hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) affecté tooyour application. |
| redirect_uri |Requis |Hello rediriger URI où vous souhaitez hello toobe de réponse envoyé pour toohandle de votre application. Il doit correspondre exactement à celle de redirection de hello URI que vous avez enregistré dans le portail hello, sauf qu’elle doit être codée URL et il peut avoir des segments de chemin d’accès supplémentaire. |
| state |Recommandé |Une valeur qui est incluse dans la demande de hello également retournée dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. l’état Hello est tooencode utilisé plus d’informations sur l’état de l’utilisateur hello dans application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |

À ce stade, Azure AD impose que seul un administrateur client peut se connecter dans la demande toocomplete hello. administrateur de Hello demandera tooapprove que tous hello les autorisations d’application direct que vous avez demandé pour votre application dans le portail de l’enregistrement d’application hello.

##### Réponse correcte
Si hello administrateur approuve les autorisations hello pour votre application, la réponse correcte de hello ressemble à ceci :

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Paramètre | Description |
| --- | --- | --- |
| locataire |locataire d’annuaire Hello votre application hello auquel des autorisations accordées qui il a demandées, au format GUID. |
| state |Une valeur qui est incluse dans la demande de hello également retournée dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. l’état Hello est tooencode utilisé plus d’informations sur l’état de l’utilisateur hello dans application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| admin_consent |Définir trop**true**. |

##### Réponse d’erreur
Si l’administrateur de hello n’approuve pas les autorisations hello pour votre application, hello a échoué présente de réponse comme suit :

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Paramètre | Description |
| --- | --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser les types de tooclassify des erreurs et les, vous pouvez utiliser tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier la cause première hello d’une erreur. |

Une fois que vous avez reçu une réponse correcte à partir du point de terminaison de mise en service d’application hello, votre application a obtenu les autorisations d’application direct hello qu’il a demandée. Maintenant, vous pouvez demander un jeton de ressource hello souhaité.

## Obtention d’un jeton
Une fois que vous avez acquis les autorisations nécessaires hello pour votre application, passez à l’acquisition des jetons d’accès pour les API. tooget un jeton à l’aide d’octroi des informations d’identification du client hello, envoyer un toohello de la demande POST `/token` v2.0 le point de terminaison :

### Premier cas : demande de jeton d’accès avec un secret partagé

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Paramètre | Condition | Description |
| --- | --- | --- |
| client_id |Requis |Hello Application ID que hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) affecté tooyour application. |
| scope |Requis |valeur de Hello passée pour hello `scope` paramètre dans cette demande doit être un identificateur de ressource hello (URI ID d’Application) de ressource hello souhaitée, apposée par hello `.default` suffixe. Par exemple Microsoft Graph de hello, valeur de hello est `https://graph.microsoft.com/.default`. Cette valeur informe le point de terminaison de hello v2.0 que toutes les autorisations d’application directe de hello que vous avez configuré pour votre application, il doit émettre un jeton pour hello associés ressource hello toouse. |
| client_secret |Requis |Hello Secret d’Application que vous avez créé pour votre application dans le portail de l’enregistrement d’application hello. |
| grant_type |Requis |Doit être `client_credentials`. |

### Deuxième cas : demande de jeton d’accès avec un certificat

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Paramètre | Condition | Description |
| --- | --- | --- |
| client_id |Requis |Hello Application ID que hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) affecté tooyour application. |
| scope |Requis |valeur de Hello passée pour hello `scope` paramètre dans cette demande doit être un identificateur de ressource hello (URI ID d’Application) de ressource hello souhaitée, apposée par hello `.default` suffixe. Par exemple Microsoft Graph de hello, valeur de hello est `https://graph.microsoft.com/.default`. Cette valeur informe le point de terminaison de hello v2.0 que toutes les autorisations d’application directe de hello que vous avez configuré pour votre application, il doit émettre un jeton pour hello associés ressource hello toouse. |
| client_assertion_type |required |la valeur Hello doit être`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |required | Une assertion (un jeton Web JSON) que vous avez besoin de toocreate et signe avec hello certificat que vous avez enregistré en tant qu’informations d’identification pour votre application. En savoir plus sur [informations d’identification de certificat](active-directory-certificate-credentials.md) toolearn comment tooregister votre format de certificat et hello d’assertion de hello.|
| grant_type |Requis |Doit être `client_credentials`. |

Notez que les paramètres de hello sont presque identiques, comme dans les cas de hello de demande de hello hello par secret partagé, sauf que le paramètre de client_secret hello est remplacé par deux paramètres : un client_assertion_type et un client_assertion.

### Réponse correcte
Une réponse correcte se présente ainsi :

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès demandé Hello. application Hello peut utiliser cette toohello tooauthenticate jeton ressource, telles que tooa API Web sécurisée. |
| token_type |Indique la valeur de jeton de type hello. Hello uniquement le type qui prend en charge d’Azure AD est `bearer`. |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |

### Réponse d’erreur
Une réponse d’erreur ressemble à ceci :

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Une chaîne de code d’erreur que vous pouvez utiliser tooclassify les types d’erreurs qui se produisent et tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |
| error_codes |Liste des codes d’erreur STS spécifiques pouvant être utiles dans les tests de diagnostic. |
| timestamp |heure de Hello hello erronée. |
| trace_id |Identificateur unique pour la demande hello qui peut vous aider avec les diagnostics. |
| correlation_id |Identificateur unique pour la demande hello qui peut vous aider avec les diagnostics dans des composants. |

## Utilisation d’un jeton
Maintenant que vous avez acquis un jeton, utilisez hello jeton toomake demandes toohello ressource. Lors de l’expiration du jeton de hello, répétez hello demande toohello `/token` tooacquire de point de terminaison un jeton d’accès de nouveau.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Exemple de code
toosee un exemple d’application qu’implémente hello octroi des informations d’identification du client à l’aide du point de terminaison hello admin consentement, consultez notre [exemple de code du démon v2.0](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
