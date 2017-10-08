---
title: point de terminaison v2.0 aaaChanges toohello AD Azure | Documents Microsoft
description: "Une description des modifications sont apportées protocoles de version préliminaire publique toohello application modèle v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>V2.0 de toohello mises à jour importantes des protocoles d’authentification
À l’intention des développeurs ! Sur hello deux prochaines semaines, nous allons quelques mises à jour les protocoles d’authentification tooour v2.0 qui peuvent signifier que les dernières modifications de toutes les applications que vous avez écrit pendant votre période d’évaluation.  

## <a name="who-does-this-affect"></a>Quelles sont les applications concernées ?
Toutes les applications qui ont été écrits toouse hello v2.0 convergent de point de terminaison d’authentification

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Plus d’informations sur le point de terminaison hello v2.0 trouverez [ici](active-directory-appmodel-v2-overview.md).

Si vous avez créé une application à l’aide du point de terminaison v2.0 hello en codant directement toohello v2.0 protocole, à l’aide de notre middlewares web OpenID Connect ou OAuth, ou l’autre authentification de tooperform 3e partie bibliothèques, vous devez être préparé tootest vos projets et la marque modifications si nécessaire.

## <a name="who-doesnt-this-affect"></a>Quelles sont les applications non concernées ?
Toutes les applications qui ont été écrits sur le point de terminaison d’authentification de production Azure AD hello,

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Ce protocole n’est pas susceptible de subir des modifications.

En outre, si votre application **uniquement** utilise notre bibliothèque ADAL tooperform l’authentification, vous n’aurez toochange quoi que ce soit.  La bibliothèque ADAL a protégé à votre application des modifications de hello.  

## <a name="what-are-hello-changes"></a>Quelles sont les modifications hello ?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Valeur de x5t hello suppression des en-têtes de JSON
point de terminaison Hello v2.0 utilise des jetons JWT largement, qui contient une section d’en-tête paramètres avec les métadonnées pertinentes sur le jeton de hello.  Si vous décodez en-tête hello de l’un de nos jetons Web JSON en cours, vous trouveriez quelque chose comme :

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Les deux propriétés de « x5t » et « enfant » hello identifient où la clé publique de hello qui doit être signature du jeton utilisé toovalidate hello récupérées à partir du point de terminaison des métadonnées de OpenID Connect hello.

modification Hello que nous faisons ici est la propriété de hello « x5t » de tooremove.  Vous pouvez continuer toouse hello même toovalidate de mécanismes de jetons, mais doit dépendre uniquement hello « enfant » propriété tooretrieve hello clé publique appropriée, comme spécifié dans hello protocole OpenID Connect. 

> [!IMPORTANT]
> **Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello de valeur de x5t hello.**
> 
> 

### <a name="removing-profileinfo"></a>Suppression de profile_info
Auparavant, point de terminaison hello v2.0 a été retournant un objet JSON encodé en base 64 dans les réponses jeton appelés `profile_info`.  Lors de la demande un jeton d’accès à partir du point de terminaison v2.0 hello en envoyant une demande pour :

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

réponse de Hello ressemblerait à hello suivant l’objet JSON :

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `profile_info` valeur contenue plus d’informations sur utilisateur hello connecté à l’application hello - leur nom complet, prénom, nom, adresse de messagerie, identificateur et ainsi de suite.  Principalement, hello `profile_info` a été utilisé pour le cache de jetons et d’affichage.

Nous sommes en train de supprimer hello `profile_info` valeur – mais ne vous inquiétez pas, nous fournissons toujours cette toodevelopers informations dans un emplacement légèrement différent.  Au lieu de `profile_info`, point de terminaison hello v2.0 retournent désormais une `id_token` dans chaque réponse de jeton :

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Vous pouvez décoder et analyser hello id_token tooretrieve hello les mêmes informations que vous avez reçu de profile_info.  Hello id_token est un JSON Web Token (JWT), avec le contenu, tel que spécifié par OpenID Connect.  Hello code pour ce faire, doit être très semblable, vous devez simplement intermédiaire de hello tooextract tooaccess hello JSON objet décodera segment (corps hello) de hello id_token et base64.

Sur hello deux prochaines semaines, vous devez coder vos informations d’utilisateur application tooretrieve hello à partir de deux hello `id_token` ou `profile_info`; selon ce qui est présent.  De cette façon lorsque hello est modifié, votre application peut gérer en toute transparence de transition hello de `profile_info` trop`id_token` sans interruption.

> [!IMPORTANT]
> **Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello Hello `profile_info` valeur.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Suppression de id_token_expires_in
Similaire trop`profile_info`, nous allons supprimer également hello `id_token_expires_in` paramètre des réponses.  Auparavant, point de terminaison hello v2.0 retourne une valeur pour `id_token_expires_in` avec chaque réponse id_token, par exemple dans une réponse autoriser :

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Ou dans une réponse de jeton :

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `id_token_expires_in` valeur indiquerait nombre hello de secondes hello id_token reste valide pour.  Maintenant, nous allons supprimer hello `id_token_expires_in` valeur complètement.  Au lieu de cela, vous pouvez utiliser la norme d’OpenID Connect hello `nbf` et `exp` validité de hello tooexamine d’un id_token de revendications.  Consultez hello [référence de jeton v2.0](active-directory-v2-tokens.md) pour plus d’informations sur ces revendications.

> [!IMPORTANT]
> **Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello Hello `id_token_expires_in` valeur.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Modification revendications hello renvoyées par scope = openid
Cette modification sera hello plus significatif – en fait, cela affectera presque chaque application qui utilise le point de terminaison hello v2.0.  Plusieurs applications envoi demandes toohello v2.0 point de terminaison à l’aide de hello `openid` étendue, comme :

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Aujourd'hui, lorsque les utilisateur hello consentement pour hello `openid` étendue, votre application reçoit une mine d’informations sur l’utilisateur de hello en hello résultant id_token.  Ces revendications peuvent inclure son nom, son nom d’utilisateur par défaut, son adresse de messagerie, son ID objet, etc.

Cette mise à jour, nous modifions les informations hello que hello `openid` étendue permet à votre application l’accès à comform toobetter avec hello OpenID Connect de spécification.  Hello `openid` étendue uniquement votre application toosign hello utilisateur et de recevoir un identificateur spécifique à l’application pour l’utilisateur de hello Bonjour `sub` de hello id_token de revendication.  Hello des revendications dans une id_token avec uniquement hello `openid` étendue accordée sera inclut pas les informations d’identification personnelle.  Exemples de revendication contenus dans le paramètre id_token :

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Si vous souhaitez tooobtain informations d’identification personnelle (PII) sur l’utilisateur de hello dans votre application, toorequest des autorisations supplémentaires à partir de l’utilisateur de hello est nécessaire à votre application.  Nous vous présentons prise en charge de deux étendues à partir de la spécification OpenID Connect de hello : hello `email` et `profile` étendues – qui vous toodo donc.

* Hello `email` étendue est très simple : il permet d’adresse de messagerie principale de votre application l’accès toohello l’utilisateur via hello `email` hello id_token de revendication.  Notez que hello `email` revendication pas sera toujours présente dans id_tokens : elle sera inclus si elle est disponible dans le profil de l’utilisateur hello.
* Hello `profile` étendue permet à votre tooall d’accès application autres informations de base utilisateur hello-le nom, le nom d’utilisateur par défaut, ID d’objet et ainsi de suite.

Cela vous permet de toocode votre application de façon minimale divulgation – vous pouvez demander à utilisateur de hello pour simplement hello information que votre application requiert toodo son travail.  Si vous souhaitez toocontinue mise en route du jeu complet de hello des informations utilisateur qui reçoit actuellement votre application, vous devez inclure toutes les étendues de trois dans vos demandes d’autorisation :

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Votre application peut commencer à envoyer hello `email` et `profile` étendues immédiatement et point de terminaison hello v2.0 acceptera ces deux étendues et commencer à demander des autorisations aux utilisateurs selon les besoins.  Toutefois, hello modifier dans interprétation hello Hello `openid` étendue ne prendront effet que de quelques semaines.

> [!IMPORTANT]
> **Votre travail : ajouter hello `profile` et `email` étendues si votre application nécessite des informations sur l’utilisateur de hello.**  Notez que la bibliothèque ADAL inclut ces deux autorisations dans les requêtes par défaut. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Suppression hello émetteur barre oblique de fin.
Auparavant, valeur d’émetteur hello qui apparaît dans les jetons à partir du point de terminaison hello v2.0 a duré formulaire de hello

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Où le guid de hello a été tenantId hello du client hello Azure AD qui a émis le jeton de hello.  Avec ces modifications, valeur d’émetteur hello devient

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

dans les deux jetons et dans le document de découverte hello OpenID Connect.

> [!IMPORTANT]
> **Votre travail : Assurez-vous que votre application accepte une valeur d’émetteur hello avec et sans barre oblique de fin lors de la validation de l’émetteur.**
> 
> 

## <a name="why-change"></a>Pourquoi introduire des modifications ?
la motivation principale Hello pour l’introduction de ces modifications est toobe conforme à hello OpenID Connect la spécification standard.  En étant OpenID Connect conforme, nous espérons que toominimize les différences entre l’intégration avec les services d’identité de Microsoft et à d’autres services d’identité dans l’industrie de hello.  Il convient de leurs bibliothèques d’authentification open source favorite tooenable développeurs toouse sans avoir des différences de Microsoft tooaccommodate tooalter hello bibliothèques.

## <a name="what-can-you-do"></a>Que pouvez-vous faire ?
À compter d’aujourd'hui, vous pouvez commencer à effectuer toutes les modifications de hello décrites ci-dessus.  Vous devez immédiatement :

1. **Supprimez toutes les dépendances hello `x5t` paramètre d’en-tête.**
2. **Transition hello de façon à gérer `profile_info` trop`id_token` dans les réponses de jeton.**
3. **Supprimez toutes les dépendances hello `id_token_expires_in` paramètre de la réponse.**
4. **Ajouter hello `profile` et `email` étendues tooyour application si votre application a besoin des informations utilisateur de base.**
5. **Accepter les valeurs issuer dans les jetons avec et sans barre oblique finale.**

Notre [documentation du protocole v2.0](active-directory-v2-protocols.md) a déjà été mis à jour tooreflect ces modifications, donc vous pouvez l’utiliser comme référence pour aider aux mettre à jour votre code.

Si vous avez d’autres questions sur l’étendue de hello des modifications de hello, vous pouvez tooreach libre hors toous sur Twitter à @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Quelle sera la fréquence des modifications du protocole ?
Nous ne prévoient pas les dernières modifications toohello protocoles d’authentification.  Nous sommes intentionnellement regroupement de ces modifications dans une version afin que vous n’avez pas à nouveau tôt toogo via ce type de processus de mise à jour.  Bien entendu, nous continuerons tooadd fonctionnalités toohello convergé service d’authentification v2.0 dont vous pouvez tirer parti de, mais ces modifications doivent être additif et saut pas de code existant.

Enfin, nous aimerions toosay Merci d’essayer les choses pendant la période d’évaluation hello.  analyses de Hello et l’expérience de nos premiers ont été inestimable jusqu’ici, et nous espérons que vous allez continuer tooshare votre avis et des idées.

Codez bien !

Hello Division d’identité Microsoft

