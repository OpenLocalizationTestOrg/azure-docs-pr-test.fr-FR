---
title: "applications à page unique à l’aide de flux implicites de hello Azure AD v2.0 aaaSecure | Documents Microsoft"
description: "Génération d’applications web à l’aide de la mise en œuvre de la version 2.0 d’Azure AD de flux implicites de hello pour les applications de la même page."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# v2.0 protocoles - SPAs à l’aide de flux implicites de hello
Avec le point de terminaison hello v2.0, vous pouvez signer les utilisateurs dans vos applications de page unique avec des comptes personnels et de travail/school à partir de Microsoft.  Page unique et autres applications JavaScript qui exécutent principalement dans un type de navigateur quelques exemples intéressants défis quand il est fourni tooauthentication :

* caractéristiques de sécurité Hello de ces applications sont considérablement différentes à partir d’applications web traditionnelles server en fonction.
* De nombreux serveurs d’autorisation et fournisseurs d’identité ne prennent pas en charge les demandes CORS.
* Redirections du navigateur pleine page en dehors de l’application hello deviennent toohello INVASIF en particulier l’expérience utilisateur.

Pour ces applications (pensez : AngularJS, Ember.js, React.js, etc.) Azure AD prend en charge les flux de OAuth 2.0 Implicit Grant hello.  les flux implicites Hello sont décrite dans hello [OAuth 2.0 spécification](http://tools.ietf.org/html/rfc6749#section-4.2).  Le principal avantage est qu’il permet des jetons de tooget application hello d’Azure AD sans effectuer un échange d’informations d’identification du serveur principal.  Ainsi, hello application toosign utilisateur de hello, maintenir la session et d’obtenir des jetons tooother web API dans du code JavaScript client hello.  Il existe quelques tootake de considérations de sécurité importantes en compte lors de l’utilisation de flux implicites de hello - spécifiquement environ [client](http://tools.ietf.org/html/rfc6749#section-10.3) et [l’emprunt d’identité utilisateur](http://tools.ietf.org/html/rfc6749#section-10.3).

Si vous souhaitez que le flux implicite de toouse hello et Azure AD tooadd authentification tooyour JavaScript application, nous vous recommandons d’utiliser notre bibliothèque JavaScript open source, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Il existe peu de didacticiels AngularJS [ici](active-directory-appmodel-v2-overview.md#getting-started) toohelp commencer.  

Toutefois, si vous préférez pas toouse une bibliothèque dans les messages de protocole unique page application et envoyer vous-même, procédez comme suit général hello.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## Schéma de protocole
Hello entière connexion implicite dans le flux ressemble à ceci : hello étapes sont décrites en détail ci-dessous.

![Couloirs OpenId Connect](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Envoyer la demande de connexion hello
signe de tooinitially hello utilisateur dans votre application, vous pouvez envoyer un [OpenID Connect](active-directory-v2-protocols-oidc.md) demande d’autorisation et obtenir un `id_token` à partir du point de terminaison hello v2.0 :

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Cliquez sur lien hello tooexecute cette demande ! Une fois connecté, votre navigateur doit être redirigé trop`https://localhost/myapp/` avec un `id_token` dans la barre d’adresses hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |required |Hello Id d’Application ce portail d’inscription hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) attribué de votre application. |
| response_type |required |Doit inclure `id_token` pour la connexion à OpenID Connect.  Il peut également inclure hello response_type `token`. À l’aide de `token` ici autorise votre tooreceive application un jeton d’accès immédiatement à partir de hello autoriser un point de terminaison sans avoir toomake une deuxième toohello de demande autoriser point de terminaison.  Si vous utilisez hello `token` response_type, hello `scope` paramètre doit contenir une étendue qui indique quel jeton de hello ressource tooissue pour. |
| redirect_uri |recommandé |Bonjour redirect_uri de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application.  Il doit correspondre exactement à celle de redirect_uris hello que vous inscrit dans le portail hello, à ceci près qu’il doit être codée url. |
| scope |required |Une liste d’étendues séparées par des espaces.  Pour OpenID Connect, elle doit inclure l’étendue de hello `openid`, ce qui se traduit par toohello les autorisations « Connexion vous » dans l’interface utilisateur de consentement hello.  Si vous le souhaitez, vous pouvez également utiliser tooinclude hello `email` ou `profile` [étendues](active-directory-v2-scopes.md) pour obtenir un utilisateur de tooadditional accéder aux données.  Vous pouvez également inclure les autres étendues dans cette demande de demander des ressources toovarious de consentement. |
| response_mode |recommandé |Spécifie la méthode hello qui doit être utilisés toosend hello résultant tooyour précédent jeton application.  Doit être `fragment` pour les flux implicites hello. |
| state |recommandé |Une valeur incluse dans la demande hello qui s’affichera dans la réponse du jeton hello.  Il peut s’agir d’une chaîne du contenu de votre choix.  Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| nonce |required |Une valeur incluse dans la demande hello, généré par l’application hello, qui est incluse dans id_token résultant de hello en tant que revendication.  application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur.  Hello valeur est généralement une chaîne aléatoire unique qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| prompt |facultatif |Indique le type hello d’intervention de l’utilisateur qui est requise.  Hello uniquement à ce stade, les valeurs valides sont « login », « none » et « ».  `prompt=login`force sera hello utilisateur tooenter leurs informations d’identification sur cette demande, la négation de l’authentification unique sur.  `prompt=none`est hello opposé garantit que hello ne s’affiche avec une invite interactive que ce soit.  Si la demande de hello ne peut pas être effectuée en mode silencieux via l’authentification unique, point de terminaison hello v2.0 retournera une erreur.  `prompt=consent`sera hello de déclencheur OAuth consentement dialogue après le signe d’utilisateur hello, demandant hello utilisateur toogrant autorisations toohello application. |
| login_hint |facultatif |Peut être champ d’adresse utilisé toopre-remplissage hello nom d’utilisateur et de messagerie de hello page de connexion pour l’utilisateur de hello, si vous connaissez le nom d’utilisateur à l’avance.  Fréquence à laquelle les applications utilisent ce paramètre au cours de la réauthentification, ayant déjà extrait le nom d’utilisateur hello à partir d’une connexion précédente sign-in à l’aide de hello `preferred_username` de revendication. |
| domain_hint |facultatif |Peut être `consumers` ou `organizations`.  Si inclus, il ignore les processus de détection d’un e-mail hello que l’utilisateur parcourt sur la page, de connexion v2.0 hello début tooa rationalisé légèrement plus expérience utilisateur.  Fréquence à laquelle les applications utilisent ce paramètre au cours de la réauthentification, en extrayant hello `tid` hello id_token de revendication.  Si hello `tid` est de valeur de revendication `9188040d-6c67-4c5b-b112-36a304b66dad`, vous devez utiliser `domain_hint=consumers`.  Sinon, utilisez `domain_hint=organizations`. |

À ce stade, l’utilisateur de hello sera demandé tooenter leurs informations d’identification et l’authentification de hello terminée.  Hello v2.0 le point de terminaison garantit également que l’utilisateur hello a consenti autorisations toohello indiquées Bonjour `scope` paramètre de requête.  Si l’utilisateur de hello a consenti pas tooany de ces autorisations, il vous demande hello utilisateur tooconsent toohello requis autorisations.  Les détails sur les [autorisations, les consentements et les applications mutualisées sont disponibles ici](active-directory-v2-scopes.md).

Une fois que l’utilisateur de hello s’authentifie et donne son consentement, point de terminaison hello v2.0 retournera une application tooyour de réponse à hello indiqué `redirect_uri`, à l’aide de la méthode hello spécifié dans hello `response_mode` paramètre.

#### Réponse correcte
Une réponse correcte à l’aide de `response_mode=fragment` et `response_type=id_token+token` ressemble à hello suivants, avec des sauts de ligne pour une meilleure lisibilité :

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Paramètre | Description |
| --- | --- |
| access_token |Inclus si `response_type` inclut `token`. jeton d’accès Hello hello application demandée, dans ce cas pour hello Microsoft Graph.  jeton d’accès Hello ne doit pas être décodé ou inspecté, il peut être traitée comme une chaîne opaque. |
| token_type |Inclus si `response_type` inclut `token`.  Sera toujours `Bearer`. |
| expires_in |Inclus si `response_type` inclut `token`.  Indique le nombre hello de secondes pendant lesquelles le jeton de hello est valide pour la mise en cache. |
| scope |Inclus si `response_type` inclut `token`.  Indique l’ou les étendues hello pour le hello access_token sera valide. |
| id_token |Bonjour id_token qui hello application demandée. Vous pouvez utiliser l’identité de l’utilisateur hello hello id_token tooverify et démarrer une session avec l’utilisateur de hello.  Plus de détails sur id_tokens et leur contenu est inclus dans hello [référence de jeton de point de terminaison v2.0](active-directory-v2-tokens.md). |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |

#### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin de l’application hello peut gérer de façon appropriée :

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

## Valider hello id_token
Seulement recevoir un id_token n’est pas suffisant tooauthenticate hello ; Vous devez valider les signatures d’id_token hello et vérifier les revendications hello dans le jeton hello selon les besoins de votre application.  point de terminaison Hello v2.0 utilise [des jetons Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) et public jetons toosign de chiffrement de clé et vérifiez qu’ils sont valides.

Vous pouvez choisir toovalidate hello `id_token` dans le code client, mais une pratique courante consiste à toosend hello `id_token` tooa du serveur principal et effectuer une validation hello il.  Une fois que vous avez validé la signature hello de hello id_token, il existe quelques revendications que vous serez tooverify requis.  Consultez hello [référence de jeton v2.0](active-directory-v2-tokens.md) pour plus d’informations, y compris [validation des jetons](active-directory-v2-tokens.md#validating-tokens) et [Important d’informations sur la signature de substitution des clés](active-directory-v2-tokens.md#validating-tokens).  Nous vous recommandons d’utiliser une bibliothèque pour analyser et valider les jetons. Il en existe au moins une pour la plupart des langages et plateformes.
<!--TODO: Improve hello information on this-->

Vous pouvez également y toovalidate des revendications supplémentaires en fonction de votre scénario.  Voici quelques validations courantes :

* Assurer hello / l’organisation de l’utilisateur a inscrit pour l’application hello.
* Garantie qu’utilisateur de hello dispose des privilèges / d’autorisation
* S’assurer de l’utilisation d’une force certaine d’authentification, comme une authentification multifacteur.

Pour plus d’informations sur les revendications hello dans un id_token, consultez hello [référence de jeton de point de terminaison v2.0](active-directory-v2-tokens.md).

Une fois que vous avez complètement validé hello id_token, vous pouvez démarrer une session avec l’utilisateur de hello et utiliser les revendications hello dans hello id_token tooobtain informations hello utilisateur dans votre application.  Ces informations peuvent être utilisées pour l’affichage, les enregistrements, les autorisations, etc.

## Obtenir des jetons d’accès
Maintenant que vous avez connecté les utilisateur hello dans votre application à page unique, vous pouvez obtenir des jetons d’accès pour le web appelant API sécurisé par Azure AD, par exemple hello [Microsoft Graph](https://graph.microsoft.io).  Même si vous avez déjà reçu d’un jeton à l’aide de hello `token` response_type, vous pouvez utiliser ce procédé tooacquire jetons tooadditional les ressources sans avoir à nouveau les tooredirect hello utilisateur toosign.

Dans le flux OpenID Connect/OAuth normal hello, vous faites cela en effectuant un v2.0 toohello de demande `/token` point de terminaison.  Toutefois, le point de terminaison hello v2.0 ne pas les demandes CORS prise en charge, AJAX appels tooget et jetons d’actualisation est en dehors de la question de hello.  Au lieu de cela, vous pouvez utiliser les flux implicites hello dans un iframe masqué tooget nouveaux jetons pour les autres API web : 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Essayez de copier et coller hello ci-dessous demande un onglet de navigateur ! (N’oubliez pas tooreplace hello `domain_hint` et hello `login_hint` valeurs hello avec des valeurs correctes pour votre utilisateur)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |required |Hello Id d’Application ce portail d’inscription hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) attribué de votre application. |
| response_type |required |Doit inclure `id_token` pour la connexion à OpenID Connect.  Il peut inclure d’autres types de réponses, comme `code`. |
| redirect_uri |recommandé |Bonjour redirect_uri de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application.  Il doit correspondre exactement à celle de redirect_uris hello que vous inscrit dans le portail hello, à ceci près qu’il doit être codée url. |
| scope |required |Une liste d’étendues séparées par des espaces.  Pour obtenir des jetons, inclure tous les [étendues](active-directory-v2-scopes.md) vous avez besoin pour la ressource hello dignes d’intérêt. |
| response_mode |recommandé |Spécifie la méthode hello qui doit être utilisés toosend hello résultant tooyour précédent jeton application.  Peut être `query`, `form_post` ou `fragment`. |
| state |recommandé |Une valeur incluse dans la demande hello qui s’affichera dans la réponse du jeton hello.  Il peut s’agir d’une chaîne du contenu de votre choix.  Une valeur unique générée de manière aléatoire est généralement utilisée pour empêcher les falsifications de requête intersite.  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| nonce |required |Une valeur incluse dans la demande hello, généré par l’application hello, qui est incluse dans id_token résultant de hello en tant que revendication.  application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur.  Hello valeur est généralement une chaîne aléatoire unique qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| prompt |required |Pour l’actualisation et l’obtention de jetons dans un iframe masqué, vous devez utiliser `prompt=none` tooensure qui hello iframe ne soit pas bloquée sur la page de connexion v2.0 hello et retourne immédiatement. |
| login_hint |required |Pour l’actualisation et l’obtention de jetons dans un iframe masqué, vous devez inclure hello les nom d’utilisateur de l’utilisateur de hello dans cet indicateur dans l’ordre des toodistinguish entre plusieurs sessions utilisateur de hello peut-être à un moment donné dans le temps. Vous pouvez extraire le nom d’utilisateur hello à partir d’une connexion précédente sign-in à l’aide de hello `preferred_username` de revendication. |
| domain_hint |required |Peut être `consumers` ou `organizations`.  Pour l’actualisation et l’obtention de jetons dans un iframe masqué, vous devez inclure hello domain_hint dans la demande hello.  Vous devez extraire hello `tid` de revendication d’id_token hello d’une précédente connexion toodetermine le toouse de valeur.  Si hello `tid` est de valeur de revendication `9188040d-6c67-4c5b-b112-36a304b66dad`, vous devez utiliser `domain_hint=consumers`.  Sinon, utilisez `domain_hint=organizations`. |

Merci toohello `prompt=none` paramètre, cette demande soit réussissent ou échouent immédiatement et retournent tooyour application.  Une réponse correcte recevront tooyour application à hello indiqué `redirect_uri`, à l’aide de la méthode hello spécifié dans hello `response_mode` paramètre.

#### Réponse correcte
Une réponse correcte utilisant `response_mode=fragment` se présente ainsi :

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Paramètre | Description |
| --- | --- |
| access_token |jeton Hello hello application demandée. |
| token_type |Sera toujours `Bearer`. |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| scope |étendues de Hello hello du jeton d’accès est valide pour. |

#### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin de l’application hello peut gérer de façon appropriée.  Dans les cas de hello de `prompt=none`, une erreur attendue sera :

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

Si vous recevez cette erreur dans la demande iframe hello, hello utilisateur doit interactivement se connecter à nouveau tooretrieve un nouveau jeton.  Vous pouvez choisir toohandle ce cas dans la façon de sens pour votre application.

## Actualisation des jetons
Les deux `id_token`s et `access_token`s va expirer après une courte période de temps, afin de votre application doit être préparée toorefresh ces jetons régulièrement.  toorefresh soit de type de jeton, vous pouvez effectuer hello même demande iframe masqué supérieure à l’aide de hello `prompt=none` paramètre comportement de toocontrol d’Azure AD.  Si vous voulez tooreceive un nouveau `id_token`, être vraiment toouse `response_type=id_token` et `scope=openid`, ainsi qu’un `nonce` paramètre.

## Envoi d’une demande de déconnexion
Hello OpenIdConnect `end_session_endpoint` permet à un tooend de point de terminaison demande toohello v2.0 session et l’effacer cookies d’un utilisateur définies par le point de terminaison hello v2.0 toosend de votre application.  toofully se connecter à un utilisateur en dehors d’une application web, votre application doit mettre fin à sa propre session avec l’utilisateur de hello (généralement en désactivant un cache de jeton ou la suppression des cookies), puis rediriger hello navigateur :

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client.  Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | recommandé | URL de Hello hello utilisateur doit être retourné tooafter déconnexion se termine. Cette valeur doit correspondre à l’un de redirection hello Qu'uri inscrits pour l’application hello. Si ne pas inclus, utilisateur de hello s’affichera un message générique par point de terminaison hello v2.0. |
