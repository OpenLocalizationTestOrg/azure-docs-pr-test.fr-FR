---
title: aaaAzure protocole v2.0 et hello OpenID Connect Active Directory | Documents Microsoft
description: "Générer des applications web à l’aide de mise en œuvre de v2.0 hello AD Azure hello OpenID Connect du protocole d’authentification."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocole de Active Directory Azure v2.0 et hello OpenID Connect
OpenID Connect est un protocole d’authentification basé sur OAuth 2.0 que vous pouvez utiliser l’authentification toosecurely dans une application web de tooa utilisateur. Lorsque vous utilisez la mise en œuvre hello v2.0 du point de terminaison de OpenID Connect, vous pouvez ajouter connectez-vous et API accès tooyour applications web. Dans cet article, nous vous indiquons comment toodo ce indépendante du langage. Nous allons décrire comment toosend et recevoir des messages HTTP sans utiliser les bibliothèques open source de Microsoft.

> [!NOTE]
> point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory. toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) étend hello OAuth 2.0 *autorisation* toouse protocole comme un *authentification* de protocole, afin que vous puissiez effectuer seul l’authentification à l’aide d’OAuth. OpenID Connect d’introduit le concept de hello d’un *le jeton d’ID*, qui est un jeton de sécurité autorisant les clients de hello identité de hello tooverify d’utilisateur de hello. le jeton d’ID Hello obtient également des informations de profil de base sur l’utilisateur de hello. Car OpenID Connect étend OAuth 2.0, les applications peuvent obtenir en toute sécurité *jetons d’accès*, ce qui peut être utilisé tooaccess les ressources qui sont sécurisés par une [serveur d’autorisation](active-directory-v2-protocols.md#the-basics). Nous recommandons d'utiliser OpenID Connect si vous concevez une [application web](active-directory-v2-flows.md#web-apps) hébergée sur un serveur et accessible par le biais d’un navigateur.

## Schéma de protocole : Connexion
Hello plus simple flux de connexion comporte les étapes hello illustrés hello suivant. Nous décrirons en détail chaque étape dans cet article.

![Protocole OpenID Connect : Connexion](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Extraire le document de métadonnées hello OpenID Connect
OpenID Connect décrit un document de métadonnées qui contient la plupart des informations hello requises pour une application tooperform connexion. Ces informations indiquent notamment hello URL toouse et l’emplacement de hello publique de du service hello clés de signature. Pour le point de terminaison hello v2.0, il s’agit de document de métadonnées OpenID Connect hello que vous devez utiliser :

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Hello `{tenant}` peut prendre une des quatre valeurs :

| Valeur | Description |
| --- | --- |
| `common` |Utilisateurs avec un compte Microsoft personnel et un compte professionnel ou scolaire d’Azure Active Directory (Azure AD) peuvent se connecter toohello application. |
| `organizations` |Seuls les utilisateurs disposant de travail ou les comptes d’établissement scolaire d’Azure AD puissent se connecter toohello application. |
| `consumers` |Seuls les utilisateurs avec un compte Microsoft personnel peuvent se connecter toohello application. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` |Seuls les utilisateurs avec un compte professionnel ou scolaire à partir d’une annonce Azure client peut se connecter toohello application. Nom de domaine convivial hello de hello locataire Azure AD ou identificateur GUID du locataire hello peut être utilisé. |

les métadonnées Hello sont un document JavaScript Objet Notation (JSON) simple. Consultez hello suivant extrait de code pour obtenir un exemple. Hello contenu de l’extrait de code est décrites en détail dans hello [OpenID Connect de spécification](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

En règle générale, vous utiliserez ce document de métadonnées tooconfigure une bibliothèque OpenID Connect ou d’un kit de développement ; bibliothèque de Hello utiliseriez hello métadonnées toodo son travail. Toutefois, si vous n’utilisez pas une bibliothèque OpenID Connect de pré-build, vous pouvez suivre les étapes de hello dans reste hello de cet article tooperform signe dans une application web à l’aide du point de terminaison hello v2.0.

## Envoyer la demande de connexion hello
Lorsque l’utilisateur de hello tooauthenticate a besoin de votre application web, il peut diriger hello utilisateur toohello `/authorize` point de terminaison. Cette demande est similaire toohello première branche de hello [flux de code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md), avec ces différences importantes :

* demande de Hello doit inclure hello `openid` étendue Bonjour `scope` paramètre.
* Hello `response_type` paramètre doit inclure `id_token`.
* demande de Hello doit inclure hello `nonce` paramètre.

Par exemple :

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Cliquez sur hello suivant tooexecute de lien de cette demande. Une fois que vous vous connectez, votre navigateur sera redirigé toohttps://localhost/myapp/, avec un jeton d’ID dans la barre d’adresses hello. Notez que cette requête utilise `response_mode=query` (pour les besoins du didacticiel uniquement). Nous vous recommandons d'utiliser `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Paramètre | Condition | Description |
| --- | --- | --- |
| locataire |Requis |Vous pouvez utiliser hello `{tenant}` valeur dans le chemin d’accès de hello de hello demande toocontrol, qui peut se connecter toohello application. Hello valeurs autorisées sont `common`, `organizations`, `consumers`et les identificateurs de client. Pour plus d’informations, consultez les [principes de base du protocole](active-directory-v2-protocols.md#endpoints). |
| client_id |Requis |Hello Application ID que hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) affecté tooyour application. |
| response_type |Requis |Doit inclure `id_token` pour la connexion à OpenID Connect. Il peut également inclure d’autres valeurs `response_types`, par exemple `code`. |
| redirect_uri |Recommandé |Hello URI de redirection de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application. Il doit correspondre exactement à celle de redirection hello URI inscrit dans le portail hello, sauf qu’il doit être URL encodée. |
| scope |Requis |Une liste d’étendues séparées par des espaces. Pour OpenID Connect, elle doit inclure l’étendue de hello `openid`, ce qui se traduit par toohello les autorisations « Connexion vous » dans l’interface utilisateur de consentement hello. Vous pouvez inclure d’autres étendues dans cette requête pour solliciter le consentement. |
| nonce |Requis |Une valeur incluse dans la demande hello, généré par l’application hello, qui est incluse dans la valeur id_token résultante de hello en tant que revendication. application Hello peut vérifier des attaques par relecture jeton toomitigate valeur. valeur de Hello est généralement une chaîne aléatoire unique qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| response_mode |Recommandé |Spécifie la méthode hello qui doit être différé tooyour code d’autorisation résultant toosend utilisé hello application. Peut être `query`, `form_post` ou `fragment`. Pour les applications web, nous vous recommandons d’utiliser `response_mode=form_post`, tooensure hello plus sécuriser le transfert de l’application tooyour de jetons. |
| state |Recommandé |Une valeur incluse dans la demande hello qui sera également renvoyé dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. Une valeur unique générée de manière aléatoire est principalement trop[empêcher les attaques par falsification de requête](http://tools.ietf.org/html/rfc6749#section-10.12). état de Hello est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, telles que les utilisateurs de hello de page ou un affichage hello a eu lieu. |
| prompt |Facultatif |Indique le type hello d’intervention de l’utilisateur qui est requise. Hello uniquement les valeurs valides pour l’instant sont `login`, `none`, et `consent`. Hello `prompt=login` revendication force hello utilisateur tooenter leurs informations d’identification sur cette demande, ce qui rend l’authentification unique. Hello `prompt=none` revendication est hello opposé. Cette revendication garantit que hello ne s’affiche avec une invite interactive que ce soit. Si la demande de hello ne peut pas être effectuée en mode silencieux via l’authentification unique, le point de terminaison hello v2.0 renvoie une erreur. Hello `prompt=consent` revendication déclencheurs hello boîte de dialogue de consentement OAuth après hello utilisateur se connecte. boîte de dialogue de Hello demande hello utilisateur toogrant autorisations toohello application. |
| login_hint |Facultatif |Vous pouvez utiliser ce paramètre toopre remplissage hello nom d’utilisateur et par courrier électronique adresse champ de hello-page de connexion pour l’utilisateur de hello, si vous connaissez le nom d’utilisateur hello avance. Souvent, les applications utilisent ce paramètre au cours de la réauthentification, après avoir déjà extrait les nom d’utilisateur hello à partir d’une connexion à antérieure à l’aide de hello `preferred_username` de revendication. |
| domain_hint |Facultatif |Cette valeur peut être `consumers` ou `organizations`. Si inclus, il ignore le processus de détection d’un e-mail hello cet utilisateur hello traverse sur hello v2.0-page de connexion, pour une expérience utilisateur légèrement plus rapide. Souvent, les applications utilisent ce paramètre au cours de la réauthentification en extrayant hello `tid` de revendications de jeton d’ID hello. Si hello `tid` est de valeur de revendication `9188040d-6c67-4c5b-b112-36a304b66dad`, utilisez `domain_hint=consumers`. Sinon, utilisez `domain_hint=organizations`. |

À ce stade, les utilisateurs hello est invité à tooenter leurs informations d’identification et l’authentification de hello terminée. Hello v2.0 le point de terminaison vérifie que l’utilisateur hello a consenti autorisations toohello indiquées Bonjour `scope` paramètre de requête. Si l’utilisateur de hello a consenti pas tooany de ces autorisations, point de terminaison hello v2.0 invite hello utilisateur tooconsent toohello requis des autorisations. Vous pouvez en savoir plus sur les [autorisations consentements et applications mutualisées](active-directory-v2-scopes.md).

Une fois que l’utilisateur de hello s’authentifie et donne son consentement, hello v2.0 point de terminaison retourne une application tooyour de réponse à hello indiquée les URI de redirection à l’aide de méthode hello spécifié dans hello `response_mode` paramètre.

### Réponse correcte
Une réponse correcte lorsque vous utilisez `response_mode=form_post` ressemble à ceci :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Paramètre | Description |
| --- | --- |
| id_token |Bonjour le jeton d’ID qui hello application demandée. Vous pouvez utiliser hello `id_token` paramètre tooverify hello l’identité de l’utilisateur et démarrer une session avec l’utilisateur de hello. Pour plus d’informations sur les jetons d’ID et leur contenu, consultez hello [référence les jetons de point de terminaison v2.0](active-directory-v2-tokens.md). |
| state |Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |

### Réponse d’erreur
Réponses d’erreur peuvent également être envoyés l’URI de redirection toohello afin que hello application puisse les gérer. Une réponse d’erreur ressemble à ceci :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser tooclassify les types d’erreurs qui se produisent et tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |

### Codes d’erreur pour les erreurs de point de terminaison d’autorisation
Hello tableau suivant décrit les codes d’erreur qui peuvent être retournées dans hello `error` paramètre de réponse d’erreur hello :

| Code d'erreur | Description | Action du client |
| --- | --- | --- |
| invalid_request |Erreur de protocole, tel qu’un paramètre obligatoire manquant. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| unauthorized_client |application cliente de Hello Impossible de demander un code d’autorisation. |Cela se produit généralement lorsque l’application cliente de hello n’est pas inscrit dans Azure AD ou locataire Azure AD de l’utilisateur toohello n’est pas ajoutée. application Hello pouvez hello utilisateur application hello de tooinstall instructions et l’ajouter tooAzure AD. |
| access_denied |propriétaire de la ressource de Hello a refusé son consentement. |application cliente de Hello peut avertir l’utilisateur de hello il ne peut pas continuer à moins que hello utilisateur y consent. |
| unsupported_response_type |serveur d’autorisation de Hello ne prend pas en charge le type de réponse hello dans la demande de hello. |Corrigez et soumettez à nouveau la demande de hello. Il s’agit d’une erreur de développement généralement détectée lors des tests initiaux. |
| server_error |serveur de Hello a rencontré une erreur inattendue. |Réessayez la demande de hello. Ces erreurs peuvent résulter de conditions temporaires. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de l’erreur temporaire de tooa. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de la condition temporaire de tooa. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique que les ressources hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut invite utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |

## Valider le jeton d’ID hello
Réception d’un jeton d’ID n’est pas suffisant utilisateur de hello tooauthenticate. Vous devez également valider la signature du jeton d’ID hello et vérifier les revendications hello dans le jeton hello selon les besoins de votre application. point de terminaison Hello v2.0 utilise [des jetons Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) et public jetons toosign de chiffrement de clé et vérifiez qu’ils sont valides.

Vous pouvez choisir le jeton d’ID toovalidate hello dans le code client, mais une pratique courante est le serveur principal tooa jeton toosend hello ID et effectuer une validation hello il. Une fois que vous avez validé la signature de hello du jeton d’ID hello, vous devez tooverify quelques revendications. Pour plus d’informations, y compris les plus d’informations sur les [valider des jetons](active-directory-v2-tokens.md#validating-tokens) et [des informations importantes sur la substitution de la clé de signature](active-directory-v2-tokens.md#validating-tokens), consultez hello [v2.0 jetons référence](active-directory-v2-tokens.md). Nous vous recommandons d’utiliser une bibliothèque tooparse et valider les jetons. Il existe au moins une de ces bibliothèques pour la plupart des langages et plateformes.
<!--TODO: Improve hello information on this-->

Vous pouvez également toovalidate des revendications supplémentaires, en fonction de votre scénario. Voici quelques validations courantes :

* Vérifiez que hello ou l’organisation utilisateur a inscrit pour l’application hello.
* Assurez-vous que l’utilisateur hello exige des privilèges ou autorisation.
* S’assurer de l’utilisation d’une force certaine d’authentification, comme une authentification multifacteur.

Pour plus d’informations sur les revendications hello dans un jeton d’ID, consultez hello [référence les jetons de point de terminaison v2.0](active-directory-v2-tokens.md).

Après avoir validé le jeton d’ID hello complètement, vous pouvez commencer une session avec l’utilisateur de hello. Utiliser les revendications hello hello ID jeton tooget informations utilisateur hello dans votre application. Vous pouvez utiliser ces informations pour l’affichage, les enregistrements, les autorisations, etc.

## Envoi d’une demande de déconnexion
Lorsque vous souhaitez toosign utilisateur de hello à partir de votre application, il n’est pas suffisant tooclear les cookies de votre application, ou sinon terminer hello session utilisateur. Vous devez également rediriger toosign de point de terminaison hello utilisateur toohello v2.0 out. Si vous ne le faites pas, les utilisateurs hello ré-authentifie tooyour application sans entrer leurs informations d’identification, car ils auront une valide unique de session avec le point de terminaison hello v2.0.

Vous pouvez rediriger hello utilisateur toohello `end_session_endpoint` répertoriées dans le document de métadonnées hello OpenID Connect :

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Paramètre | Condition | Description |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Recommandé | URL Hello hello utilisateur est redirigé tooafter correctement la déconnexion. Si le paramètre hello n’est pas inclus, hello sont affichées un message générique qui est généré par le point de terminaison hello v2.0. Cette URL doit correspondre à un des URI inscrits pour votre application dans le portail de l’enregistrement d’application hello de redirection hello.  |

## Authentification unique
Lorsque vous redirigez hello utilisateur toohello `end_session_endpoint`, point de terminaison hello v2.0 efface hello session utilisateur à partir du navigateur de hello. Toutefois, hello utilisateur peut toujours être connecté tooother les applications qui utilisent des comptes Microsoft pour l’authentification. tooenable ces utilisateurs de hello toosign applications out simultanément, les point de terminaison de v2.0 hello envoie un toohello demande HTTP GET est inscrit `LogoutUrl` de toutes les applications hello cet utilisateur hello est actuellement connecté à. Les applications doivent répondre toothis demande en désactivant toute session qui identifie l’utilisateur de hello et en retournant un `200` réponse.  Si vous souhaitez utiliser l’authentification unique toosupport expire dans votre application, vous devez implémenter ces un `LogoutUrl` dans le code de votre application.  Vous pouvez définir hello `LogoutUrl` à partir du portail de l’enregistrement d’application hello.

## Schéma de protocole : Acquisition de jeton
De nombreuses applications web doivent toonot seul utilisateur signe hello dans, mais également tooaccess un service web pour le compte d’utilisateur de hello en utilisant OAuth. Ce scénario combine OpenID Connect pour l’authentification utilisateur lors de l’obtention de simultanément une autorisation de code que vous pouvez utiliser l’accès tooget jetons si vous utilisez le flux d’un code d’autorisation OAuth hello.

Hello complète OpenID Connect connectez-vous et flux de l’acquisition de jeton est similaire diagramme suivant de toohello. Nous décrivent chaque étape en détail dans les sections suivants hello d’article de hello.

![Protocole OpenID Connect : Acquisition de jeton](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Obtenir des jetons d’accès
jetons d’accès tooacquire, modifiez la demande de connexion hello :

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Cliquez sur hello suivant tooexecute de lien de cette demande. Une fois que vous vous connectez, votre navigateur est redirigé toohttps://localhost/myapp/, avec un jeton d’ID et un code dans la barre d’adresses hello. Notez que cette requête utilise `response_mode=query` (pour les besoins du didacticiel uniquement). Nous vous recommandons d'utiliser `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

En incluant des étendues d’autorisation dans la demande hello et à l’aide de `response_type=id_token code`, point de terminaison hello v2.0 garantit que l’utilisateur hello a consenti autorisations toohello indiquées Bonjour `scope` paramètre de requête. Elle retourne un tooexchange d’application de tooyour de code d’autorisation pour un jeton d’accès.

### Réponse correcte
Une réponse correcte utilisant `response_mode=form_post` se présente ainsi :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Paramètre | Description |
| --- | --- |
| id_token |Bonjour le jeton d’ID qui hello application demandée. Vous pouvez utiliser l’identité de l’utilisateur hello hello ID tooverify jeton et démarrer une session avec l’utilisateur de hello. Vous trouverez plus d’informations sur les jetons d’ID et leur contenu Bonjour [référence les jetons de point de terminaison v2.0](active-directory-v2-tokens.md). |
| code |code d’autorisation Hello hello application demandée. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour la ressource cible de hello. La durée de vie d'un code d’autorisation est très courte. En règle générale, un code d’autorisation expire au bout de 10 minutes environ. |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |

### Réponse d’erreur
Réponses d’erreur peuvent également être envoyés l’URI de redirection toohello afin que hello application peut gérer de façon appropriée. Une réponse d’erreur ressemble à ceci :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur que vous pouvez utiliser tooclassify les types d’erreurs qui se produisent et tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |

Pour obtenir une description des codes d’erreur éventuels et connaître les réponses client recommandées associées, consultez [Codes d’erreur pour les erreurs de point de terminaison d’autorisation](#error-codes-for-authorization-endpoint-errors).

Lorsque vous avez un code d’autorisation et un jeton d’ID, vous pouvez connecter hello utilisateur et obtenir des jetons d’accès de leur part. toosign hello utilisateur, vous devez valider le jeton d’ID hello [exactement comme](#validate-the-id-token). jetons d’accès tooget, suivez les étapes de hello décrites dans nos [documentation du protocole OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
