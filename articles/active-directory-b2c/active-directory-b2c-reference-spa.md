---
title: "Azure Active Directory B2C : applications à page unique créée avec un flux implicite | Microsoft Docs"
description: "Découvrez comment toobuild seule page applications directement à l’aide d’OAuth 2.0 implicite flux avec Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C : Connexion à une application à page unique en utilisant un flux implicite OAuth 2.0

> [!NOTE]
> Cette fonctionnalité est en préversion.
> 

De nombreuses applications modernes disposent d’un frontend d’application à page unique écrit principalement en JavaScript. Souvent, l’application hello est écrit à l’aide d’une infrastructure telle que AngularJS, Ember.js ou Durandal. Les applications à page unique et d’autres applications JavaScript qui s’exécutent principalement dans un navigateur présentent certaines problématiques supplémentaires pour l’authentification :

* caractéristiques de sécurité Hello de ces applications sont considérablement différentes des applications web traditionnelles de basé sur le serveur.
* Beaucoup de serveurs d’autorisation et de fournisseurs d’identité ne prennent pas en charge les demandes de partage des ressources cross-origin (CORS).
* Redirections du navigateur pleine page en dehors de l’application hello peuvent être toohello INVASIF considérablement l’expérience utilisateur.

toosupport ces applications, Azure Active Directory B2C (B2C Active Directory de Azure) utilise les flux implicites hello OAuth 2.0. flux d’octroi implicite d’autorisation Hello OAuth 2.0 est décrit dans [section 4.2 de spécification de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). Dans le flux implicite, application hello reçoit les jetons directement à partir de hello Azure Active Directory (Azure AD) autoriser le point de terminaison, sans les échanges de serveur à serveur. Tous les logique d’authentification et de gestion prend de session placent entièrement hello JavaScript client, sans les redirections de pages supplémentaires.

Azure AD B2C étend hello toomore flux implicites OAuth 2.0 standard à l’authentification simple et l’autorisation. Azure AD B2C introduit hello [paramètre de stratégie](active-directory-b2c-reference-policies.md). Avec le paramètre de stratégie de hello, vous pouvez utiliser OAuth 2.0 tooadd utilisateur rencontre tooyour application, telles que d’abonnement, connectez-vous et gestion des profils. Dans cet article, nous vous indiquons comment toouse hello flux implicites et Azure AD tooimplement chaque ces expériences dans vos applications à page unique. toohelp commencer, examinons notre [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) et [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) exemples.

Dans les requêtes d’exemple HTTP hello dans cet article, nous utilisons notre répertoire Azure AD B2C d’exemple, **fabrikamb2c.onmicrosoft.com**. Nous utilisons également nos propres exemples d’application et de stratégies. Vous pouvez essayer de demandes de hello vous-même à l’aide de ces valeurs, ou vous pouvez les remplacer par vos propres valeurs.
Découvrez comment trop[obtenir votre propre annuaire Azure AD B2C, application et des stratégies](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Schéma de protocole

flux de connexion implicite Hello ressemble hello figure suivante. Chaque étape est décrite en détail plus loin dans l’article de hello.

![Couloirs OpenId Connect](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Envoi de demandes d’authentification
Lorsque votre application web a besoin d’utilisateur de hello tooauthenticate et exécuter une stratégie, il dirige hello utilisateur toohello `/authorize` point de terminaison. Il s’agit d’hello de partie interactive du flux de hello, où hello utilisateur agit, en fonction de la stratégie de hello. utilisateur de Hello Obtient un ID de jeton à partir du point de terminaison Azure AD hello.

Dans cette demande, les clients hello indique Bonjour `scope` autorisations hello de paramètre qu’il nécessite de tooacquire à partir de l’utilisateur de hello. Bonjour `p` paramètre, il indique hello stratégie tooexecute. Hello trois chacun des exemples suivants (avec les sauts de ligne pour une meilleure lisibilité) utilisent une stratégie différente. tooget une idée de fonctionne de chaque demande, essayez de demande hello de collage dans un navigateur et de son exécution.

### <a name="use-a-sign-in-policy"></a>Utilisation d’une stratégie de connexion
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Utilisation d’une stratégie d’inscription
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Utilisation d’une stratégie de modification de profil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| client_id |Requis |ID de l’application Hello affecté application tooyour Bonjour [portail Azure](https://portal.azure.com). |
| response_type |Requis |Doit inclure `id_token` pour la connexion à OpenID Connect. Il peut également inclure les type de réponse hello `token`. Si vous utilisez `token`, votre application peut recevoir immédiatement d’un jeton d’accès à hello autoriser un point de terminaison, sans apporter une deuxième toohello de demande de point de terminaison authorize.  Si vous utilisez hello `token` type de réponse, hello `scope` paramètre doit contenir une étendue qui indique quel jeton de hello ressource tooissue pour. |
| redirect_uri |Recommandé |Hello URI de redirection de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application. Il doit correspondre exactement à celle de redirection de hello URI que vous avez enregistré dans le portail hello, sauf qu’il doit être encodé en URL. |
| response_mode |Recommandé |Spécifie les hello méthode toouse toosend hello résultant tooyour précédent jeton application.  Pour les flux implicites, utilisez `fragment`. |
| scope |Requis |Une liste d’étendues séparées par des espaces. Une valeur d’étendue unique indique tooAzure AD à la fois des autorisations de hello sont demandés. Hello `openid` étendue indique une autorisation toosign dans hello utilisateur et obtenir des données sur utilisateur hello sous forme de hello de jetons de code. (Nous parlerons de cette suite dans l’article de hello.) Hello `offline_access` étendue est facultative pour les applications web. Il indique que votre application a besoin d’un jeton d’actualisation pour l’accès à long terme tooresources. |
| state |Recommandé |Une valeur incluse dans la demande hello également retournée dans la réponse du jeton hello. Il peut être une chaîne de contenu que vous souhaitez toouse. En règle générale, une valeur unique générée de manière aléatoire est utilisée, les attaques par falsification de tooprevent demande entre sites. Hello état est également utilisé tooencode plus d’informations sur l’état de l’utilisateur hello dans application hello avant de la demande d’authentification hello s’est produite, comme page de hello qu’ils étaient sur. |
| nonce |Requis |Une valeur incluse dans la demande hello (généré par l’application hello) qui est inclus dans le jeton d’ID hello résultant comme une revendication. application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur. En règle générale, la valeur de hello est une chaîne aléatoire unique qui peut être l’origine de hello tooidentify utilisés de demande de hello. |
| p |Requis |Hello tooexecute de stratégie. Son hello nom d’une stratégie qui est créée dans votre locataire Azure AD B2C. valeur de nom de stratégie Hello doit commencer par **b2c\_1\_**. Pour plus d’informations, consultez [Stratégies prédéfinies d’Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Facultatif |type de Hello d’intervention de l’utilisateur qui est requis. Actuellement, hello seule valeur valide est `login`. Cela force le hello utilisateur tooenter leurs informations d’identification sur cette demande. L’authentification unique ne prendra pas effet. |

À ce stade, les flux de travail de la stratégie toocomplete hello est demandé à utilisateur de hello. Cela peut également impliquer l’utilisateur de hello entrer leur nom d’utilisateur et un mot de passe, vous connecter avec une identité sociale, souscrire hello répertoire ou tout autre nombre d’étapes. Actions de l’utilisateur dépendent de la stratégie de hello est définie.

Utilisateur de hello après la stratégie de hello, Azure AD renvoie une application tooyour de réponse à la valeur hello vous avez utilisé pour `redirect_uri`. Il utilise la méthode hello spécifié dans hello `response_mode` paramètre. réponse de Hello est exactement hello même pour chacun des hello action scénarios utilisateur, indépendamment de la stratégie de hello qui a été exécutée.

### <a name="successful-response"></a>Réponse correcte
Une réponse correcte qui utilise `response_mode=fragment` et `response_type=id_token+token` ressemble à hello suivants, avec des sauts de ligne pour une meilleure lisibilité :

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Paramètre | Description |
| --- | --- |
| access_token |jeton d’accès Hello hello application demandée.  jeton d’accès Hello ne doit pas être décodé ou inspecté. Il peut être traité comme une chaîne opaque. |
| token_type |valeur de type de jeton Hello. Hello tapez uniquement que prend en charge d’Azure AD est porteur. |
| expires_in |Durée Hello de hello du jeton d’accès est valide (en secondes). |
| scope |étendues de Hello hello jeton est valide pour. Vous pouvez également utiliser des jetons de toocache étendues pour une utilisation ultérieure. |
| id_token |Bonjour le jeton d’ID qui hello application demandée. Vous pouvez utiliser l’identité de l’utilisateur hello hello ID tooverify jeton et démarrer une session avec l’utilisateur de hello. Pour plus d’informations sur les jetons d’ID et leur contenu, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| state |Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |

### <a name="error-response"></a>Réponse d’erreur
Réponses d’erreur peuvent également être envoyés l’URI de redirection toohello afin que hello application peut gérer de façon appropriée :

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur utilisé tooclassify les types d’erreurs qui se produisent. Vous pouvez également utiliser le code d’erreur hello pour la gestion des erreurs. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |
| state |Consultez la description complète de hello Bonjour tableau précédent. Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques.|

## <a name="validate-hello-id-token"></a>Valider le jeton d’ID hello
Réception d’un jeton d’ID n’est pas suffisamment utilisateur de hello tooauthenticate. Vous devez valider la signature du jeton d’ID hello et vérifier les revendications hello dans le jeton hello selon les besoins de votre application. Azure AD B2C utilise [des jetons Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) et public jetons toosign de chiffrement de clé et vérifiez qu’ils sont valides.

De nombreuses bibliothèques open source sont disponibles pour la validation de jetons Web JSON, en fonction du langage de hello vous préférez toouse. Nous vous recommandons d’explorer ces bibliothèques open source plutôt que d’implémenter votre propre logique de validation. Vous pouvez utiliser les informations de hello dans toohelp de cet article, vous apprenez tooproperly utiliser ces bibliothèques.

Azure AD B2C a un point de terminaison des métadonnées OpenID Connect. Une application peut utiliser hello point de terminaison toofetch plus d’informations sur Azure AD B2C lors de l’exécution. Ces informations incluent les points de terminaison, le contenu des jetons et les clés de signature de jetons. Il existe un document de métadonnées JSON pour chaque stratégie dans votre locataire Azure AD B2C. Par exemple, le document de métadonnées hello pour la stratégie de b2c_1_sign_in hello dans le locataire de fabrikamb2c.onmicrosoft.com hello est situé :

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Une des propriétés de hello de ce document de configuration est hello `jwks_uri`. valeur Hello pour hello même stratégie serait :

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine stratégie qui a été toosign utilisé un jeton d’ID (et où toofetch hello des métadonnées à partir de), vous avez deux options. Tout d’abord, le nom de la stratégie hello est inclus dans hello `acr` de revendication dans `id_token`. Pour plus d’informations sur la façon dont les revendications à partir d’un jeton d’ID tooparse hello, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md). L’autre option consiste à stratégie de hello tooencode valeur hello Hello `state` paramètre lors de l’exécution de la demande de hello. Ensuite, décoder hello `state` toodetermine paramètre stratégie qui a été utilisée. Les 2 méthodes sont valides.

Une fois que vous avez acquis le document de métadonnées hello à partir du point de terminaison des métadonnées de OpenID Connect hello, vous pouvez utiliser hello RSA-256 (situés dans ce point de terminaison) de clés publiques toovalidate hello signature de jeton d’ID hello. Il peut y avoir plusieurs clés répertoriées sur ce point de terminaison, chacune étant identifiée par un `kid`. en-tête Hello de `id_token` contient également un `kid` de revendication. Il indique laquelle de ces clés a été toosign utilisé le jeton d’ID hello. Pour plus d’informations, y compris les découvrir [valider des jetons](active-directory-b2c-reference-tokens.md#token-validation), consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Après avoir validé la signature de hello du jeton d’ID hello, plusieurs revendications exigent la vérification. Par exemple :

* Valider hello `nonce` tooprevent les attaques de relecture de jetons de revendications. Sa valeur doit être spécifiée dans la demande de connexion hello.
* Valider hello `aud` revendication tooensure qui hello le jeton d’ID a été émis pour votre application. Sa valeur doit être l’ID de l’application hello de votre application.
* Valider hello `iat` et `exp` revendications tooensure qui hello le jeton d’ID n’a pas expiré.

Vous devez effectuer plusieurs validations plus sont décrites en détail dans hello [OpenID connecter Core Spec](http://openid.net/specs/openid-connect-core-1_0.html). Vous pouvez également vous toovalidate des revendications supplémentaires, en fonction de votre scénario. Voici quelques validations courantes :

* Vérification de l’utilisateur de hello ou organisation a souscrit application hello.
* S’assurer que l’utilisateur hello bénéficie des privilèges et l’autorisation appropriée.
* Vérifier qu’une certaine force d’authentification a été appliquée, comme Azure Multi-Factor Authentication.

Pour plus d’informations sur les revendications hello dans un jeton d’ID, consultez hello [référence de jeton Azure AD B2C](active-directory-b2c-reference-tokens.md).

Après avoir validé le jeton d’ID hello complètement, vous pouvez commencer une session avec l’utilisateur de hello. Dans votre application, utilisez les revendications hello dans hello ID jeton tooobtain informations hello utilisateur. Ces informations peuvent être utilisées pour l’affichage, les enregistrements, les autorisations, etc.

## <a name="get-access-tokens"></a>Obtenir des jetons d’accès
Si votre toodo de besoins d’applications web est seul hello exécution des stratégies, vous pouvez ignorer hello les sections suivantes. informations Hello Bonjour les sections suivantes sont applicables uniquement tooweb et des applications qui ont besoin de toomake authentifié appels tooa web API, qui sont protégés par Azure AD B2C.

Maintenant que vous avez signé utilisateur hello dans application tooyour une seule page, vous pouvez obtenir des jetons d’accès pour le web appelant les API qui sont sécurisés par Azure AD. Même si vous avez déjà reçu un jeton à l’aide de hello `token` type de réponse, vous pouvez utiliser les jetons de tooacquire de cette méthode pour des ressources supplémentaires sans redirection toosign d’utilisateur hello dans à nouveau.

Dans un flux d’applications web classiques, vous faites cela en effectuant une demande toohello `/token` point de terminaison.  Toutefois, point de terminaison hello n’est pas prise en charge CORS demandes, AJAX appels tooget et jetons d’actualisation n’est pas une option. Au lieu de cela, vous pouvez utiliser les flux implicites hello dans un masqué HTML iframe élément tooget nouveaux jetons pour les autres API web. Voici un exemple, avec des sauts de ligne pour une meilleure lisibilité :

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| client_id |Requis |ID de l’application Hello affecté application tooyour Bonjour [portail Azure](https://portal.azure.com). |
| response_type |Requis |Doit inclure `id_token` pour la connexion à OpenID Connect.  Il peut également inclure le type de réponse hello `token`. Si vous utilisez `token` ici, votre application peut immédiatement recevoir un jeton d’accès à hello autoriser un point de terminaison, sans apporter une deuxième toohello de demande de point de terminaison authorize. Si vous utilisez hello `token` type de réponse, hello `scope` paramètre doit contenir une étendue qui indique quel jeton de hello ressource tooissue pour. |
| redirect_uri |Recommandé |Hello URI de redirection de votre application, où les réponses d’authentification peuvent être envoyés et reçus par votre application. Il doit correspondre exactement à celle de la redirection de hello URI que vous avez enregistré dans le portail de hello, sauf qu’il doit être encodé en URL. |
| scope |Requis |Une liste d’étendues séparées par des espaces.  Pour obtenir des jetons, inclure toutes les étendues que vous avez besoin pour la ressource de hello destiné. |
| response_mode |Recommandé |Spécifie la méthode hello application tooyour précédent jeton résultant de toosend utilisé hello.  Peut être `query`, `form_post` ou `fragment`. |
| state |Recommandé |Une valeur incluse dans la demande hello qui est retourné dans la réponse du jeton hello.  Il peut être une chaîne de contenu que vous souhaitez toouse.  En règle générale, une valeur unique générée de manière aléatoire est utilisée, les attaques par falsification de tooprevent demande entre sites.  état de Hello est également utilisé tooencode informations hello l’état utilisateur dans une application hello avant de la demande d’authentification hello s’est produite. Par exemple, hello page ou un affichage hello utilisateurs a eu lieu. |
| nonce |Requis |Une valeur incluse dans la demande hello, généré par l’application hello, qui est incluse dans le jeton d’ID hello résultant comme une revendication.  application Hello peut ensuite vérifier des attaques par relecture jeton toomitigate valeur. En règle générale, la valeur de hello est une chaîne aléatoire unique qui identifie l’origine hello de demande de hello. |
| prompt |Requis |toorefresh et obtenir des jetons dans un iframe masqué, utilisez `prompt=none` tooensure qui hello iframe ne pas être bloqué sur la page de connexion hello et retourne immédiatement. |
| login_hint |Requis |toorefresh et obtenir des jetons dans un iframe masqué, incluez hello les nom d’utilisateur de l’utilisateur de hello dans cette toodistinguish indicateur entre plusieurs sessions hello utilisateur devra peut-être à un moment donné. Vous pouvez extraire le nom d’utilisateur hello à partir d’une connexion à antérieure à l’aide de hello `preferred_username` de revendication. |
| domain_hint |Requis |Peut être `consumers` ou `organizations`.  Pour l’actualisation et l’obtention de jetons dans un iframe masqué, vous devez inclure hello `domain_hint` valeur dans la requête de hello.  Extraire hello `tid` de revendication à partir du jeton d’ID hello d’une version antérieure connectez-vous toodetermine le toouse de valeur.  Si hello `tid` est de valeur de revendication `9188040d-6c67-4c5b-b112-36a304b66dad`, utilisez `domain_hint=consumers`.  Sinon, utilisez `domain_hint=organizations`. |

En définissant un hello `prompt=none` paramètre, cette demande soit réussit ou échoue immédiatement et renvoie tooyour application.  Une réponse correcte est envoyée tooyour application à hello indiqué rediriger URI, en utilisant la méthode hello spécifié dans hello `response_mode` paramètre.

### <a name="successful-response"></a>Réponse correcte
Une réponse de réussite utilisant `response_mode=fragment` se présente ainsi :

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Paramètre | Description |
| --- | --- |
| access_token |jeton Hello hello application demandée. |
| token_type |le type de jeton Hello sera toujours porteur. |
| state |Si un `state` paramètre est inclus dans la demande hello, même valeur hello doit apparaître dans la réponse de hello. Hello application doit vérifier que hello `state` valeurs hello demande et de réponse sont identiques. |
| expires_in |La durée pendant laquelle le jeton d’accès hello est valide (en secondes). |
| scope |étendues de Hello hello du jeton d’accès est valide pour. |

### <a name="error-response"></a>Réponse d’erreur
Réponses d’erreur également peuvent être envoyés l’URI de redirection toohello afin que hello application peut gérer de façon appropriée.  Pour `prompt=none`, une erreur attendue se présente ainsi :

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Paramètre | Description |
| --- | --- |
| error |Une chaîne de code d’erreur qui peut être utilisés tooclassify des types d’erreurs qui se produisent. Vous pouvez également utiliser hello chaîne tooreact tooerrors. |
| error_description |Un message d’erreur spécifique qui peut vous aider à identifier hello origine d’une erreur d’authentification. |

Si vous recevez cette erreur dans la demande iframe hello, hello utilisateur doit interactivement se connecter à nouveau tooretrieve un nouveau jeton. Vous pouvez gérer ceci de manière appropriée pour votre application.

## <a name="refresh-tokens"></a>Jetons d’actualisation
Les jetons d’ID et les jetons d’accès expirent après une courte période de temps. Votre application doit être préparée toorefresh ces jetons régulièrement.  effectuer de chaque type de jeton, toorefresh hello même iframe masqué demande, nous avons utilisé dans l’exemple précédent, à l’aide de hello `prompt=none` étapes toocontrol Azure AD de paramètre.  tooreceive un nouveau `id_token` valeur, être vraiment toouse `response_type=id_token` et `scope=openid`et un `nonce` paramètre.

## <a name="send-a-sign-out-request"></a>Envoi d’une demande de déconnexion
Toosign hello utilisation de l’application hello, vous pouvez rediriger hello utilisateur tooAzure AD toosign out. Si vous ne le faites pas, hello utilisateur devra peut-être application tooyour de tooreauthenticate en mesure de sans entrer de nouveau leurs informations d’identification. En effet, il dispose d’une session d’authentification unique valide avec Azure AD.

Vous pouvez rediriger simplement hello utilisateur toohello `end_session_endpoint` qui est mentionné dans hello OpenID Connect même document des métadonnées décrites dans [valider le jeton d’ID hello](#validate-the-id-token). Par exemple :

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| p |Requis |Hello stratégie toouse toosign hello utilisateur hors de votre application. |
| post_logout_redirect_uri |Recommandé |Hello URL cet utilisateur hello doit être redirigé tooafter réussie déconnexion. Si elle n’est pas inclus, Azure AD B2C affiche un utilisateur de toohello message générique. |

> [!NOTE]
> Direction de hello utilisateur toohello `end_session_endpoint` efface certains hello l’état d’utilisateur unique authentification avec Azure Active Directory B2C. Toutefois, il ne signe pas utilisateur hello en dehors de la session du fournisseur d’identité sociaux de l’utilisateur hello. Si l’utilisateur de hello sélectionne hello même identifier le fournisseur pendant un signe suivantes, utilisateur de hello est authentifié, sans entrer leurs informations d’identification. Si un utilisateur souhaite toosign hors de votre application Azure AD B2C, il ne signifie pas nécessairement qu’ils souhaitent toocompletely Déconnectez-vous de leur compte Facebook, par exemple. Toutefois, pour les comptes locaux, hello session utilisateur sera terminée correctement.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Utiliser votre propre locataire Azure AD B2C
tootry ces demandes vous-même, terminer hello suivant trois étapes. Remplacez les valeurs de l’exemple hello que nous utilisons dans cet article avec vos propres valeurs :

1. [Créez un locataire Azure AD B2C](active-directory-b2c-get-started.md). Utiliser le nom hello de votre client dans les demandes de hello.
2. [Créer une application](active-directory-b2c-app-registration.md) tooobtain un ID d’application et un `redirect_uri` valeur. Incluez une application web ou une API web dans votre application. Si vous le souhaitez, vous pouvez créer un secret d’application.
3. [Créer vos stratégies](active-directory-b2c-reference-policies.md) tooobtain vos noms de stratégie.

## <a name="samples"></a>Exemples

* [Créer une application à page unique en utilisant Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Créer une application à page unique en utilisant .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

