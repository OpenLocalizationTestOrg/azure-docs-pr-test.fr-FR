---
title: "aaaUnderstand hello OpenID Connect des flux de code d’authentification dans Azure AD | Documents Microsoft"
description: "Cet article décrit comment accéder à toouse HTTP messages tooauthorize tooweb applications et API web dans votre client à l’aide d’Azure Active Directory et OpenID Connect."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Autoriser les applications tooweb à l’aide de OpenID Connect et Azure Active Directory
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) est une couche d’identité simple reposant sur le protocole de hello OAuth 2.0. OAuth 2.0 définit les mécanismes tooobtain et l’utilisation **jetons d’accès** tooaccess des ressources protégées, mais ils ne définissent pas les informations d’identité tooprovide méthodes standard. OpenID Connect d’implémente l’authentification en tant qu’une extension de toohello processus d’autorisation OAuth 2.0. Il fournit des informations sur l’utilisateur final de hello sous forme de hello d’un `id_token` qui vérifie l’identité de hello d’utilisateur de hello et fournit des informations de profil de base sur l’utilisateur de hello.

Nous recommandons OpenID Connect si vous concevez une application web hébergée sur un serveur et accessible par le biais d’un navigateur.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Flux d’authentification à l’aide d’OpenID Connect
flux de connexion plus basique Hello contient hello comme suit : chacun d’eux est décrit en détail ci-dessous.

![Flux d’authentification OpenID Connect](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Document de métadonnées OpenID Connect

OpenID Connect décrit un document de métadonnées qui contient la plupart des informations hello requises pour une application tooperform connexion. Ces informations indiquent notamment hello URL toouse et l’emplacement de hello publique de du service hello clés de signature. document de métadonnées Hello OpenID Connect peut se trouve à :

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
les métadonnées Hello sont un document JavaScript Objet Notation (JSON) simple. Consultez hello suivant extrait de code pour obtenir un exemple. Hello contenu de l’extrait de code est décrites en détail dans hello [OpenID Connect de spécification](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Envoyer la demande de connexion hello
Lorsque l’utilisateur de hello tooauthenticate a besoin de votre application web, il doit diriger hello utilisateur toohello `/authorize` point de terminaison. Cette demande est similaire toohello première branche de hello [flux du Code d’autorisation OAuth 2.0](active-directory-protocols-oauth-code.md), avec quelques différences importantes :

* demande de Hello doit inclure l’étendue de hello `openid` Bonjour `scope` paramètre.
* Hello `response_type` paramètre doit inclure `id_token`.
* demande de Hello doit inclure hello `nonce` paramètre.

Voici donc un exemple de requête :

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Paramètre |  | Description |
| --- | --- | --- |
| locataire |required |Hello `{tenant}` valeur de chemin d’accès de hello de demande de hello peut être utilisé toocontrol qui peut se connecter à l’application hello.  Hello valeurs autorisées sont des identificateurs de client, par exemple, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` ou `common` pour les jetons d’indépendant du locataire |
| client_id |required |Hello Id d’Application attribué tooyour application lorsque vous avez l’inscrit auprès d’Azure AD. Vous pouvez le trouver dans hello portail Azure. Cliquez sur **Azure Active Directory**, cliquez sur **inscriptions d’application**, choisissez l’application hello et localiser hello Id d’Application sur la page de l’application hello. |
| response_type |required |Doit inclure `id_token` pour la connexion à OpenID Connect.  Il peut inclure d’autres types de réponses, comme `code`. |
| scope |required |Une liste d’étendues séparées par des espaces.  Pour OpenID Connect, elle doit inclure l’étendue de hello `openid`, ce qui se traduit par toohello les autorisations « Connexion vous » dans l’interface utilisateur de consentement hello.  Vous pouvez inclure d’autres étendues dans cette requête pour solliciter le consentement. |
| nonce |required |Une valeur incluse dans la demande de hello, généré par l’application hello, qui est incluse dans hello résultant `id_token` comme une revendication.  application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur.  valeur de Hello est généralement une chaîne aléatoire et unique ou un GUID qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| redirect_uri |recommandé |Bonjour redirect_uri de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application.  Il doit correspondre exactement à celle de redirect_uris hello que vous inscrit dans le portail hello, à ceci près qu’il doit être codée url. |
| response_mode |recommandé |Spécifie la méthode hello qui doit être utilisés toosend hello résultant authorization_code tooyour arrière application.  Les valeurs prises en charge sont `form_post` pour une *requête HTTP POST de type formulaire* ou `fragment` pour un *fragment d’URL*.  Pour les applications web, nous vous recommandons d’utiliser `response_mode=form_post` tooensure hello plus sécuriser le transfert de l’application tooyour de jetons. |
| state |recommandé |Une valeur incluse dans la demande hello qui est retourné dans la réponse du jeton hello.  Il peut s’agir d’une chaîne du contenu de votre choix.  Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |
| prompt |facultatif |Indique le type hello d’intervention de l’utilisateur qui est requise.  Hello actuellement, les seules valeurs valides sont « login », « none » et ''.  `prompt=login`force hello utilisateur tooenter leurs informations d’identification sur cette demande, une inversion d’authentification unique.  `prompt=none`hello opposé - il garantit que cet utilisateur hello n’est pas présenté avec n’importe quel interactif invite quelque.  Si la demande de hello ne peut pas être effectuée en mode silencieux via l’authentification unique, le point de terminaison hello renvoie une erreur.  `prompt=consent`déclenche hello OAuth consentement boîte de dialogue après le signe d’utilisateur hello, demandant hello utilisateur toogrant autorisations toohello application. |
| login_hint |facultatif |Possible champ d’adresse utilisé toopre-remplissage hello nom d’utilisateur et de la messagerie de hello-page de connexion pour l’utilisateur de hello, si vous connaissez le nom d’utilisateur à l’avance.  Applications souvent utilisent ce paramètre lors de la réauthentification, ayant déjà extrait le nom d’utilisateur hello à partir d’une connexion précédente sign-in à l’aide de hello `preferred_username` de revendication. |

À ce stade, les utilisateurs hello sont demandé tooenter leurs informations d’identification et l’authentification de hello terminée.

### Exemple de réponse
Un exemple de réponse, une fois que l’utilisateur de hello a authentifié, pourrait ressembler à ceci :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Paramètre | Description |
| --- | --- |
| id_token |Hello `id_token` cette application hello demandée. Vous pouvez utiliser hello `id_token` tooverify hello l’identité de l’utilisateur et démarrer une session avec l’utilisateur de hello. |
| state |Une valeur incluse dans la demande de hello est également renvoyé dans la réponse du jeton hello. Une valeur unique générée de manière aléatoire est généralement utilisée pour [empêcher les falsifications de requête intersite](http://tools.ietf.org/html/rfc6749#section-10.12).  Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page de hello ou un affichage qu’ils étaient sur. |

### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin de l’application hello peut gérer de façon appropriée :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
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
| server_error |serveur de Hello a rencontré une erreur inattendue. |Réessayez la demande de hello. Ces erreurs peuvent résulter de conditions temporaires. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de l’erreur temporaire de tooa. |
| temporarily_unavailable |serveur de Hello est temporairement trop occupé toohandle hello demande. |Réessayez la demande de hello. application cliente de Hello peut expliquer toohello utilisateur que sa réponse est retardée en raison de la condition temporaire de tooa. |
| invalid_resource |ressource de Hello cible n’est pas valide, car il n’existe pas, Azure AD ne peut pas trouver ou il n’est pas configuré correctement. |Cela indique la ressource de hello, s’il en existe n'a pas été configurée dans hello client. application Hello peut inviter l’utilisateur hello avec des instructions pour installer l’application hello et en l’ajoutant tooAzure AD. |

## Valider hello id_token
Recevoir uniquement un `id_token` n’est pas suffisant tooauthenticate hello ; vous devez valider la signature de hello et vérifier les revendications hello Bonjour `id_token` selon les besoins de votre application. point de terminaison Hello Azure AD utilise des jetons Web JSON (Jwt) et les jetons de toosign de chiffrement à clé publique et vérifiez qu’ils sont valides.

Vous pouvez choisir toovalidate hello `id_token` dans le code client, mais une pratique courante consiste à toosend hello `id_token` tooa du serveur principal et effectuer une validation hello il. Une fois que vous avez validé la signature hello Hello `id_token`, il existe quelques revendications que vous êtes tooverify requis.

Vous pouvez également y toovalidate des revendications supplémentaires en fonction de votre scénario. Voici quelques validations courantes :

* Assurer hello / l’organisation de l’utilisateur a inscrit pour l’application hello.
* Garantie qu’utilisateur de hello dispose des privilèges / d’autorisation
* S’assurer de l’utilisation d’une force certaine d’authentification, comme une authentification multifacteur.

Une fois que vous avez validé hello `id_token`, vous pouvez démarrer une session avec l’utilisateur de hello et utiliser les revendications hello Bonjour `id_token` tooobtain informations utilisateur hello dans votre application. Ces informations peuvent être utilisées pour l’affichage, les enregistrements, les autorisations, etc. Pour plus d’informations sur les types de jetons hello et revendications, consultez [prise en charge du jeton et Types de revendications](active-directory-token-and-claims.md).

## Envoi d’une demande de déconnexion
Lorsque vous souhaitez toosign hello utilisation de l’application hello, il n’est pas suffisant tooclear les cookies de votre application ou sinon final session hello avec l’utilisateur de hello.  Vous devez également rediriger hello utilisateur toohello `end_session_endpoint` de déconnexion.  Si vous ne toodo donc, utilisateur de hello sera application tooyour de tooreauthenticate en mesure de sans entrer leurs informations d’identification, car ils auront une unique session session valide avec le point de terminaison Azure AD hello.

Vous pouvez rediriger simplement hello utilisateur toohello `end_session_endpoint` répertoriées dans le document de métadonnées hello OpenID Connect :

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Paramètre |  | Description |
| --- | --- | --- |
| post_logout_redirect_uri |recommandé |URL Hello hello utilisateur doit être redirigé tooafter les déconnexion réussie.  Si ne pas inclus, hello sont affichées un message générique. |

## Authentification unique
Lorsque vous redirigez hello utilisateur toohello `end_session_endpoint`, Azure AD efface hello session utilisateur à partir du navigateur de hello. Toutefois, hello utilisateur peut toujours être connecté tooother les applications qui utilisent Azure AD pour l’authentification. tooenable toosign de ces applications hello utilisateur out simultanément, Azure AD envoie une toohello de demande HTTP GET inscrit `LogoutUrl` de toutes les applications hello cet utilisateur hello est actuellement connecté à. Les applications doivent répondre toothis demande en désactivant toute session qui identifie l’utilisateur de hello et en retournant un `200` réponse.  Si vous souhaitez utiliser l’authentification unique toosupport expire dans votre application, vous devez implémenter ces un `LogoutUrl` dans le code de votre application.  Vous pouvez définir hello `LogoutUrl` de hello portail Azure :

1. Accédez toohello [Azure Portal](https://portal.azure.com).
2. Choisissez votre annuaire Active Directory en cliquant sur votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation de gauche hello, choisissez **Azure Active Directory**, puis choisissez **inscriptions d’application** et sélectionnez votre application.
4. Cliquez sur **propriétés** et recherche hello **URL de déconnexion** zone de texte. 

## Acquisition de jeton
De nombreuses applications web ont besoin de toonot utilisateur hello signe uniquement dans, mais également accéder à un service web pour le compte d’utilisateur à l’aide d’OAuth. Ce scénario combine OpenID Connect pour l’authentification utilisateur lors de l’acquisition simultanément un `authorization_code` qui peut être utilisé tooget `access_tokens` à l’aide de hello flux de Code d’autorisation OAuth.

## Obtenir des jetons d’accès
jetons d’accès tooacquire, vous devez toomodify hello demande de connexion à partir du haut :

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

En incluant des étendues d’autorisation dans la demande hello et à l’aide de `response_type=code+id_token`, hello `authorize` point de terminaison permet de s’assurer que l’utilisateur hello a consenti autorisations toohello indiquées Bonjour `scope` paramètre de requête et un code d’autorisation de retour de votre application tooexchange pour un jeton d’accès.

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
| id_token |Hello `id_token` cette application hello demandée. Vous pouvez utiliser hello `id_token` tooverify hello l’identité de l’utilisateur et démarrer une session avec l’utilisateur de hello. |
| code |Bonjour authorization_code qui hello application demandée. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour la ressource cible de hello. Les codes d’autorisation présentent une durée de vie courte. Généralement, ils expirent au bout de 10 minutes. |
| state |Si un paramètre d’état est inclus dans la demande de hello, hello même valeur doit figurer dans la réponse de hello. application Hello doit vérifier que les valeurs d’état hello dans hello demande et de réponse sont identiques. |

### Réponse d’erreur
Réponses d’erreur peuvent aussi être envoyés à toohello `redirect_uri` afin de l’application hello peut gérer de façon appropriée :

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent et peut être utilisé tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

Pour obtenir une description des codes d’erreur possibles hello et leur action recommandée de client, consultez [codes d’erreur pour les erreurs de point de terminaison d’autorisation](#error-codes-for-authorization-endpoint-errors).

Une fois que vous avez obtenu une autorisation `code` et une `id_token`, vous pouvez connecter hello utilisateur et obtenir des jetons d’accès de leur part.  toosign hello utilisateur, vous devez valider hello `id_token` exactement comme décrit ci-dessus. jetons d’accès tooget, vous pouvez suivre les étapes de hello décrites dans hello « toorequest de code d’autorisation hello un jeton d’accès « section utiliser notre [documentation du protocole OAuth](active-directory-protocols-oauth-code.md).
