---
title: Connexion web avec OpenID Connect - Azure AD B2C | Microsoft Docs
description: "Génération d’applications web à l’aide d’implémentation d’Azure Active Directory hello hello OpenID Connect du protocole d’authentification"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C : connexion web avec OpenID Connect
OpenID Connect est un protocole d’authentification, reposant sur OAuth 2.0, qui peuvent être utilisés toosecurely connecter les utilisateurs dans les applications tooweb. En utilisant la mise en œuvre de hello Azure Active Directory B2C (Azure AD B2C) de OpenID Connect, vous pouvez sous-traiter l’inscription, connectez-vous et expériences de gestion d’identité dans votre tooAzure d’applications web Active Directory (Azure AD). Ce guide vous montre comment toodo ce de manière indépendante du langage. Il décrit comment toosend et recevoir des messages HTTP sans utiliser l’un de nos bibliothèques open source.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) étend hello OAuth 2.0 *autorisation* protocole à utiliser comme un *authentification* protocole. Ainsi, vous tooperform l’authentification unique à l’aide d’OAuth. Elle introduit le concept de hello d’un *le jeton d’ID*, qui est un jeton de sécurité qui permet de hello client tooverify hello identité d’utilisateur de hello et obtenir des informations de profil de base sur l’utilisateur de hello.

Car elle étend OAuth 2.0, il permet également d’applications toosecurely acquérir *jetons d’accès*. Vous pouvez utiliser les ressources de tooaccess access_tokens qui sont sécurisés par une [serveur d’autorisation](active-directory-b2c-reference-protocols.md#the-basics). Nous recommandons OpenID Connect si vous concevez une application web hébergée sur un serveur et accessible par le biais d’un navigateur. Si vous souhaitez tooadd identité tooyour mobile ou de bureau des applications de gestion à l’aide d’Azure AD B2C, vous devez utiliser [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) plutôt que OpenID Connect.

Azure AD B2C étend hello standard toodo protocole OpenID Connect plus simple d’authentification et d’autorisation. Il introduit hello [paramètre de stratégie](active-directory-b2c-reference-policies.md), qui vous permet de toouse OpenID Connect tooadd des expériences utilisateur, tel que d’abonnement, connectez-vous et gestion des profils--tooyour application. Ici, nous vous indiquons comment toouse tooimplement OpenID Connect et les stratégies de chacun de ces expériences dans vos applications web. Nous allons également vous montrer comment tooget les jetons d’accès pour l’accès aux API web.

demandes d’exemple HTTP Hello dans la section suivante de hello utilisent notre répertoire B2C d’exemple, fabrikamb2c.onmicrosoft.com, ainsi que notre exemple d’application, https://aadb2cplayground.azurewebsites.net et stratégies. Vous êtes libre tootry out hello vous-même des demandes à l’aide de ces valeurs, ou vous pouvez les remplacer par les vôtres.
Découvrez comment trop[obtenir votre propre B2C locataire, application et des stratégies](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Envoi de demandes d’authentification
Lorsque votre application web a besoin d’utilisateur de hello tooauthenticate et exécuter une stratégie, il peut diriger hello utilisateur toohello `/authorize` point de terminaison. Il s’agit d’hello de partie interactive du flux de hello, où hello utilisateur agit, en fonction de la stratégie de hello.

Dans cette demande, client de hello indique les autorisations hello qu’il nécessite de tooacquire à partir de l’utilisateur hello Bonjour `scope` tooexecute de stratégie de paramètre et hello Bonjour `p` paramètre. Trois exemples sont fournis Bonjour suivant sections (avec les sauts de ligne pour une meilleure lisibilité), chacun à l’aide d’une autre stratégie. tooget une idée de fonctionne de chaque demande, essayez de demande hello de collage dans un navigateur et de son exécution.

#### <a name="use-a-sign-in-policy"></a>Utilisation d’une stratégie de connexion
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Utilisation d’une stratégie d’inscription
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Utilisation d’une stratégie de modification de profil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| client_id |Requis |application Hello ID que hello [portail Azure](https://portal.azure.com/) affecté tooyour application. |
| response_type |Requis |type de réponse Hello, qui doit inclure un jeton d’ID de connexion OpenID. Si votre application web a également besoin de jetons pour appeler une API web, vous pouvez utiliser `code+id_token`, comme nous l’avons fait ici. |
| redirect_uri |Recommandé |Hello `redirect_uri` paramètre de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application. Il doit correspondre exactement à celle de hello `redirect_uri` les paramètres que vous avez enregistré dans le portail hello, sauf qu’elle doit être codée URL. |
| scope |Requis |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD les autorisations qui sont demandées. Hello `openid` étendue indique une autorisation toosign dans hello utilisateur et obtenir des données sur l’utilisateur hello sous forme de hello de jetons d’ID (toocome plus sur ce plus loin dans l’article de hello). Hello `offline_access` étendue est facultative pour les applications web. Il indique que nécessaires à votre application un *jeton d’actualisation* pour tooresources de longue durée d’accès. |
| response_mode |Recommandé |méthode Hello qui doit être différé tooyour code d’autorisation résultant toosend utilisé hello application. Il peut s’agir de `query`, `form_post` ou `fragment`.  Hello `form_post` mode de réponse est recommandé pour une sécurité optimale. |
| state |Recommandé |Une valeur incluse dans la demande de hello est également renvoyé dans la réponse du jeton hello. Il peut s’agir d’une chaîne du contenu de votre choix. Une valeur unique générée de manière aléatoire est généralement utilisée pour empêcher les falsifications de requête intersite. Hello état est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite, page hello qu’ils étaient sur. |
| nonce |Requis |Une valeur incluse dans la demande hello (généré par l’application hello) qui est inclus dans le jeton d’ID hello résultant comme une revendication. application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur. Hello valeur est généralement une chaîne aléatoire unique qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| p |Requis |stratégie Hello qui sera exécutée. Il désigne hello une stratégie qui est créée dans votre client B2C. valeur de nom de stratégie Hello doit commencer par `b2c\_1\_`. En savoir plus sur les stratégies et hello [infrastructure de stratégie extensible](active-directory-b2c-reference-policies.md). |
| prompt |Facultatif |type de Hello d’intervention de l’utilisateur qui est requise. Hello seule valeur valide pour l’instant est `login`, qui force hello utilisateur tooenter leurs informations d’identification pour cette demande. L’authentification unique ne prendra pas effet. |

À ce stade, les flux de travail de la stratégie toocomplete hello est demandé à utilisateur de hello. Cela peut également impliquer l’utilisateur de hello entrer leur nom d’utilisateur et un mot de passe, vous connecter avec une identité sociale, souscrire hello répertoire ou tout autre nombre d’étapes, selon la façon dont la stratégie de hello est définie.

Utilisateur de hello après la stratégie de hello, Azure AD renvoie une application tooyour de réponse à hello indiqué `redirect_uri` paramètre, en utilisant la méthode hello qui est spécifié dans hello `response_mode` paramètre. réponse de Hello est hello même pour chacun des hello précédant le cas, indépendamment de la stratégie de hello est exécutée.

Une réponse réussie utilisant `response_mode=fragment` se présenterait ainsi :

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Paramètre | Description |
| --- | --- |
| id_token |Bonjour le jeton d’ID qui hello application demandée. Vous pouvez utiliser l’identité de l’utilisateur hello hello ID tooverify jeton et démarrer une session avec l’utilisateur de hello. Plus d’informations sur les jetons d’ID et leur contenu sont inclus dans hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| code |Hello code d’autorisation cette application hello demandée, si vous avez utilisé `response_type=code+id_token`. application Hello peut utiliser toorequest de code d’autorisation hello un jeton d’accès pour une ressource cible. Les codes d’autorisation ont des durées de vie très courtes. Généralement, ils expirent au bout de 10 minutes. |
| state |Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |

Réponses d’erreur peuvent également être envoyés à toohello `redirect_uri` paramètre pour que cette application hello puisse les gérer en conséquence :

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être des types d’erreurs qui se produisent et qui peut être utilisé tooreact tooerrors tooclassify utilisé. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |
| state |Consultez la description complète de hello hello premier tableau dans cette section. Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |

## <a name="validate-hello-id-token"></a>Valider le jeton d’ID hello
Simplement reçoit un jeton d’ID n’est pas suffisamment utilisateur de hello tooauthenticate. Vous devez valider la signature du jeton d’ID hello et vérifier les revendications hello dans le jeton hello selon les besoins de votre application. Azure AD B2C utilise [des jetons Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) et public jetons toosign de chiffrement de clé et vérifiez qu’ils sont valides.

Il existe de nombreuses bibliothèques open source pour valider les jetons JWT en fonction de votre langage préféré. Nous vous recommandons d’explorer ces options plutôt que d’implémenter votre propre logique de validation. informations Hello ici sera utiles précieuse pour déterminer comment tooproperly utiliser ces bibliothèques.

Azure AD B2C a OpenID Connect métadonnées point de terminaison, ce qui permet à une application toofetch d’informations sur Azure AD B2C lors de l’exécution. Ces informations incluent les points de terminaison, le contenu des jetons et les clés de signature de jetons. Il existe un document de métadonnées JSON pour chaque stratégie dans votre client B2C. Par exemple, les documents de métadonnées hello pour hello `b2c_1_sign_in` stratégie dans `fabrikamb2c.onmicrosoft.com` se trouve dans :

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Une des propriétés hello de ce document de configuration est `jwks_uri`, dont la valeur de hello même stratégie serait :

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine stratégie qui a été utilisée dans un jeton d’ID de signature (et à partir d’où toofetch hello métadonnées), vous avez deux options. Tout d’abord, le nom de la stratégie hello est inclus dans hello `acr` de revendication dans le jeton d’ID hello. Pour plus d’informations sur la façon dont les revendications à partir d’un jeton d’ID tooparse hello, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). L’autre option consiste à stratégie de hello tooencode valeur hello Hello `state` paramètre lorsque vous émettez la demande de hello et décoder toodetermine stratégie qui a été utilisée. Les 2 méthodes sont valides.

Une fois que vous avez acquis le document de métadonnées hello à partir du point de terminaison des métadonnées de OpenID Connect hello, vous pouvez utiliser les clés publiques RSA 256 de hello (qui sont trouvent dans ce point de terminaison) signature de hello toovalidate de jeton d’ID hello. Ce point de terminaison peut comporter plusieurs clés à tout moment, chacune étant identifiée par une revendication `kid`. Hello en-tête de jeton d’ID hello contient également un `kid` de revendication, qui indique à lequel de ces clés a été toosign utilisé le jeton d’ID hello. Pour plus d’informations, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md) (hello section sur [valider des jetons](active-directory-b2c-reference-tokens.md#token-validation), en particulier).
<!--TODO: Improve hello information on this-->

Une fois que vous avez validé la signature de hello du jeton d’ID hello, il existe plusieurs revendications que vous avez besoin de tooverify. Exemple :

* Vous devez valider hello `nonce` tooprevent les attaques de relecture de jetons de revendications. Sa valeur doit être spécifiée dans la demande de connexion hello.
* Vous devez valider hello `aud` revendication tooensure qui hello le jeton d’ID a été émis pour votre application. Sa valeur doit être l’ID de l’application hello de votre application.
* Vous devez valider hello `iat` et `exp` revendications tooensure qui hello le jeton d’ID n’a pas expiré.

Vous devez également effectuer plusieurs autres validations. Ceux-ci sont décrits en détail dans hello [OpenID connecter Core Spec](http://openid.net/specs/openid-connect-core-1_0.html).  Vous pouvez également vous toovalidate des revendications supplémentaires, en fonction de votre scénario. Voici quelques validations courantes :

* S’assurer que hello / l’organisation de l’utilisateur a inscrit pour l’application hello.
* En vous assurant que l’utilisateur hello a des privilèges / d’autorisation.
* S’assurer de l’utilisation d’une force certaine d’authentification, comme Azure Multi-Factor Authentication.

Pour plus d’informations sur les revendications hello dans un jeton d’ID, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md).

Après avoir validé le jeton d’ID hello, vous pouvez commencer une session avec l’utilisateur de hello. Vous pouvez utiliser les revendications hello dans hello ID jeton tooobtain informations hello utilisateur dans votre application. Les utilisations de ces informations sont notamment l’affichage, les enregistrements et les autorisations.

## <a name="get-a-token"></a>Obtention d’un jeton
Si vous avez besoin de votre tooonly d’application web exécution des stratégies, vous pouvez ignorer hello les sections suivantes. Ces sections sont des applications tooweb uniquement applicable qui doivent toomake authentifié appels tooa web API et sont également protégées par Azure AD B2C.

Vous pouvez utiliser le code d’autorisation hello que vous avez obtenue (à l’aide de `response_type=code+id_token`) pour un jeton toohello souhaité ressource en envoyant un `POST` demande toohello `/token` point de terminaison. Actuellement, hello uniquement les ressources que vous pouvez demander un jeton sont votre site web principal de l’application API. convention de Hello pour demander un jeton tooyourself est toouse l’ID de client de votre application en tant qu’étendue de hello :

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| p |Requis |Hello stratégie qui a été utilisé tooacquire hello autorisation code. Vous ne pouvez pas utiliser une autre stratégie dans cette demande. Notez que vous ajoutez cette chaîne de requête de paramètre toohello, le toohello pas `POST` corps. |
| client_id |Requis |application Hello ID que hello [portail Azure](https://portal.azure.com/) affecté tooyour application. |
| grant_type |Requis |Hello type d’octroi, qui doit être `authorization_code` pour les flux de code d’autorisation hello. |
| scope |Recommandé |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD les autorisations qui sont demandées. Hello `openid` étendue indique une autorisation toosign dans hello utilisateur et obtenir des données sur utilisateur de hello sous forme hello id_token paramètres. Il peut être utilisé tooget jetons tooyour l’application back-end API web, qui est représentée par hello même ID d’application en tant que client de hello. Hello `offline_access` étendue indique que nécessaires à votre application un jeton d’actualisation pour l’accès à long terme tooresources. |
| code |Requis |code d’autorisation Hello que vous avez obtenue dans la première branche de hello du flux de hello. |
| redirect_uri |Requis |Hello `redirect_uri` paramètre d’application hello où vous avez reçu le code d’autorisation de hello. |
| client_secret |Requis |secret d’application Hello que vous avez généré dans hello [portail Azure](https://portal.azure.com/). Ce secret d’application est un artefact de sécurité important. Vous devez le stocker sur votre serveur de manière sécurisée. Vous devez également veiller à renouveler ce secret du client régulièrement. |

Un jeton de réponse de réussite se présente ainsi :

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
| token_type |valeur de type de jeton Hello. Hello uniquement le type qui prend en charge d’Azure AD est `Bearer`. |
| access_token |Hello signé le jeton Web JSON que vous avez demandé. |
| scope |étendues Hello pour le hello jeton est valide. Elles peuvent être utilisées pour mettre en cache des jetons pour une utilisation ultérieure. |
| expires_in |Durée Hello de hello du jeton d’accès est valide (en secondes). |
| refresh_token |Un jeton d’actualisation OAuth 2.0. application Hello peut utiliser ce jeton tooacquire des jetons supplémentaires après l’expiration du jeton actuel de hello. Actualiser les jetons sont de longue durées et peut être utilisé tooretain accès tooresources pendant de longues périodes de temps. Pour plus d’informations, consultez toohello [référence de jeton B2C](active-directory-b2c-reference-tokens.md). Notez que vous devez avoir utilisé étendue de hello `offline_access` d’autorisation de hello et jeton de demande dans l’ordre tooreceive un jeton d’actualisation. |

Les réponses d’erreur se présentent comme ceci :

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être des types d’erreurs qui se produisent et qui peut être utilisé tooreact tooerrors tooclassify utilisé. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

## <a name="use-hello-token"></a>Utilisation du jeton hello
Maintenant que vous avez acquis avec succès d’un jeton d’accès, vous pouvez utiliser le jeton de hello dans l’API web principale tooyour de demandes en l’incluant dans hello `Authorization` en-tête :

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Actualiser le jeton de hello
Les jetons d’ID ont une durée de vie courte. Vous devez actualiser les qui arrivent à expiration toocontinue en cours tooaccess en mesure de ressources. Vous pouvez le faire en envoyant un autre `POST` demande toohello `/token` point de terminaison. Cette fois-ci, fournir hello `refresh_token` paramètre au lieu de hello `code` paramètre :

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Paramètre | Requis | Description |
| --- | --- | --- |
| p |Requis |stratégie Hello qui était le jeton d’actualisation d’origine utilisé tooacquire hello. Vous ne pouvez pas utiliser une autre stratégie dans cette demande. Notez que vous ajoutez cette chaîne de requête de paramètre toohello, le toohello pas les corps de publication. |
| client_id |Requis |application Hello ID que hello [portail Azure](https://portal.azure.com/) affecté tooyour application. |
| grant_type |Requis |type de Hello d’octroi, qui doit être un jeton d’actualisation de cette section de flux de code d’autorisation hello. |
| scope |Recommandé |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD les autorisations qui sont demandées. Hello `openid` étendue indique une autorisation toosign dans hello utilisateur et obtenir des données sur utilisateur hello sous forme de hello de jetons de code. Il peut être utilisé tooget jetons tooyour l’application back-end API web, qui est représentée par hello même ID d’application en tant que client de hello. Hello `offline_access` étendue indique que nécessaires à votre application un jeton d’actualisation pour l’accès à long terme tooresources. |
| redirect_uri |Recommandé |Hello `redirect_uri` paramètre d’application hello où vous avez reçu le code d’autorisation de hello. |
| refresh_token |Requis |Hello d’origine jeton d’actualisation que vous avez obtenue dans la branche de deuxième hello du flux de hello. Notez que vous devez avoir utilisé étendue de hello `offline_access` d’autorisation de hello et jeton de demande dans l’ordre tooreceive un jeton d’actualisation. |
| client_secret |Requis |secret d’application Hello que vous avez généré dans hello [portail Azure](https://portal.azure.com/). Ce secret d’application est un artefact de sécurité important. Vous devez le stocker sur votre serveur de manière sécurisée. Vous devez également veiller à renouveler ce secret du client régulièrement. |

Un jeton de réponse de réussite se présente ainsi :

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
| token_type |valeur de type de jeton Hello. Hello uniquement le type qui prend en charge d’Azure AD est `Bearer`. |
| access_token |Hello signé le jeton Web JSON que vous avez demandé. |
| scope |étendue de Hello hello jeton est valide, qui peut être utilisé pour mettre en cache des jetons pour une utilisation ultérieure. |
| expires_in |Durée Hello de hello du jeton d’accès est valide (en secondes). |
| refresh_token |Un jeton d’actualisation OAuth 2.0. application Hello peut utiliser ce jeton tooacquire des jetons supplémentaires après l’expiration du jeton actuel de hello.  Actualiser les jetons sont de longue durées et peut être utilisé tooretain accès tooresources pendant de longues périodes de temps. Pour plus d’informations, consultez toohello [référence de jeton B2C](active-directory-b2c-reference-tokens.md). |

Les réponses d’erreur se présentent comme ceci :

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être des types d’erreurs qui se produisent et qui peut être utilisé tooreact tooerrors tooclassify utilisé. |
| error_description |Un message d’erreur spécifique qui permettre aider un développeur à identifier la cause de hello d’une erreur d’authentification. |

## <a name="send-a-sign-out-request"></a>Envoi d’une demande de déconnexion
Lorsque vous souhaitez toosign hello utilisation de l’application hello, il n’est pas suffisant tooclear les cookies de votre application ou sinon final session hello avec l’utilisateur de hello. Vous devez également rediriger hello utilisateur tooAzure AD toosign out. Si vous ne toodo donc, hello utilisateur devra peut-être application tooyour de tooreauthenticate en mesure de sans entrer de nouveau leurs informations d’identification. En effet, il dispose d’une session d’authentification unique valide avec Azure AD.

Vous pouvez rediriger simplement hello utilisateur toohello `end_session` point de terminaison qui est répertorié dans le document de métadonnées OpenID Connect hello décrit précédemment dans les hello « Valider le jeton d’ID hello » la section :

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| p |Requis |stratégie Hello que vous souhaitez que toouse toosign hello utilisateur hors de votre application. |
| post_logout_redirect_uri |Recommandé |Hello URL cet utilisateur hello doit être redirigé tooafter réussie déconnexion. Si elle n’est pas incluse, Azure AD B2C affiche hello un message générique. |

> [!NOTE]
> Bien que la direction de hello utilisateur toohello `end_session` point de terminaison supprime certaines des hello l’état d’utilisateur unique authentification avec Azure AD B2C, il ne signe pas utilisateur hello hors de leur session du fournisseur (IDP) identité sociaux. Si l’utilisateur de hello sélectionne hello IDP même pendant un signe suivantes, elles seront authentifiés, sans entrer leurs informations d’identification. Si un utilisateur souhaite toosign hors de votre application B2C, il ne signifie pas nécessairement qu’ils souhaitent toosign hors de leur compte Facebook. Toutefois, dans les cas de hello de comptes locaux, hello session utilisateur sera terminée correctement.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Utilisation de votre propre client B2C
Si vous souhaitez tootry de ces requêtes pour vous-même, vous devez d’abord effectuer ces trois étapes et puis remplacez décrits précédemment avec vos propres valeurs de l’exemple hello :

1. [Créer un client B2C](active-directory-b2c-get-started.md)et utiliser le nom hello de votre client dans les demandes de hello.
2. [Créer une application](active-directory-b2c-app-registration.md) tooobtain un ID d’application. Incluez une application web/API web dans votre application. Si vous le souhaitez, créez un secret d’application.
3. [Créer vos stratégies](active-directory-b2c-reference-policies.md) tooobtain vos noms de stratégie.

