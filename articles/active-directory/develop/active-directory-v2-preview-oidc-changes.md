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
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="c233b-103">V2.0 de toohello mises à jour importantes des protocoles d’authentification</span><span class="sxs-lookup"><span data-stu-id="c233b-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="c233b-104">À l’intention des développeurs !</span><span class="sxs-lookup"><span data-stu-id="c233b-104">Attention developers!</span></span> <span data-ttu-id="c233b-105">Sur hello deux prochaines semaines, nous allons quelques mises à jour les protocoles d’authentification tooour v2.0 qui peuvent signifier que les dernières modifications de toutes les applications que vous avez écrit pendant votre période d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="c233b-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="c233b-106">Quelles sont les applications concernées ?</span><span class="sxs-lookup"><span data-stu-id="c233b-106">Who does this affect?</span></span>
<span data-ttu-id="c233b-107">Toutes les applications qui ont été écrits toouse hello v2.0 convergent de point de terminaison d’authentification</span><span class="sxs-lookup"><span data-stu-id="c233b-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="c233b-108">Plus d’informations sur le point de terminaison hello v2.0 trouverez [ici](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c233b-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="c233b-109">Si vous avez créé une application à l’aide du point de terminaison v2.0 hello en codant directement toohello v2.0 protocole, à l’aide de notre middlewares web OpenID Connect ou OAuth, ou l’autre authentification de tooperform 3e partie bibliothèques, vous devez être préparé tootest vos projets et la marque modifications si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c233b-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="c233b-110">Quelles sont les applications non concernées ?</span><span class="sxs-lookup"><span data-stu-id="c233b-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="c233b-111">Toutes les applications qui ont été écrits sur le point de terminaison d’authentification de production Azure AD hello,</span><span class="sxs-lookup"><span data-stu-id="c233b-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="c233b-112">Ce protocole n’est pas susceptible de subir des modifications.</span><span class="sxs-lookup"><span data-stu-id="c233b-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="c233b-113">En outre, si votre application **uniquement** utilise notre bibliothèque ADAL tooperform l’authentification, vous n’aurez toochange quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="c233b-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="c233b-114">La bibliothèque ADAL a protégé à votre application des modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="c233b-115">Quelles sont les modifications hello ?</span><span class="sxs-lookup"><span data-stu-id="c233b-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="c233b-116">Valeur de x5t hello suppression des en-têtes de JSON</span><span class="sxs-lookup"><span data-stu-id="c233b-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="c233b-117">point de terminaison Hello v2.0 utilise des jetons JWT largement, qui contient une section d’en-tête paramètres avec les métadonnées pertinentes sur le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="c233b-118">Si vous décodez en-tête hello de l’un de nos jetons Web JSON en cours, vous trouveriez quelque chose comme :</span><span class="sxs-lookup"><span data-stu-id="c233b-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="c233b-119">Les deux propriétés de « x5t » et « enfant » hello identifient où la clé publique de hello qui doit être signature du jeton utilisé toovalidate hello récupérées à partir du point de terminaison des métadonnées de OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="c233b-120">modification Hello que nous faisons ici est la propriété de hello « x5t » de tooremove.</span><span class="sxs-lookup"><span data-stu-id="c233b-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="c233b-121">Vous pouvez continuer toouse hello même toovalidate de mécanismes de jetons, mais doit dépendre uniquement hello « enfant » propriété tooretrieve hello clé publique appropriée, comme spécifié dans hello protocole OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c233b-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c233b-122">**Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello de valeur de x5t hello.**</span><span class="sxs-lookup"><span data-stu-id="c233b-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="c233b-123">Suppression de profile_info</span><span class="sxs-lookup"><span data-stu-id="c233b-123">Removing profile_info</span></span>
<span data-ttu-id="c233b-124">Auparavant, point de terminaison hello v2.0 a été retournant un objet JSON encodé en base 64 dans les réponses jeton appelés `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="c233b-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="c233b-125">Lors de la demande un jeton d’accès à partir du point de terminaison v2.0 hello en envoyant une demande pour :</span><span class="sxs-lookup"><span data-stu-id="c233b-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="c233b-126">réponse de Hello ressemblerait à hello suivant l’objet JSON :</span><span class="sxs-lookup"><span data-stu-id="c233b-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="c233b-127">Hello `profile_info` valeur contenue plus d’informations sur utilisateur hello connecté à l’application hello - leur nom complet, prénom, nom, adresse de messagerie, identificateur et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="c233b-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="c233b-128">Principalement, hello `profile_info` a été utilisé pour le cache de jetons et d’affichage.</span><span class="sxs-lookup"><span data-stu-id="c233b-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="c233b-129">Nous sommes en train de supprimer hello `profile_info` valeur – mais ne vous inquiétez pas, nous fournissons toujours cette toodevelopers informations dans un emplacement légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="c233b-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="c233b-130">Au lieu de `profile_info`, point de terminaison hello v2.0 retournent désormais une `id_token` dans chaque réponse de jeton :</span><span class="sxs-lookup"><span data-stu-id="c233b-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="c233b-131">Vous pouvez décoder et analyser hello id_token tooretrieve hello les mêmes informations que vous avez reçu de profile_info.</span><span class="sxs-lookup"><span data-stu-id="c233b-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="c233b-132">Hello id_token est un JSON Web Token (JWT), avec le contenu, tel que spécifié par OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c233b-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="c233b-133">Hello code pour ce faire, doit être très semblable, vous devez simplement intermédiaire de hello tooextract tooaccess hello JSON objet décodera segment (corps hello) de hello id_token et base64.</span><span class="sxs-lookup"><span data-stu-id="c233b-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="c233b-134">Sur hello deux prochaines semaines, vous devez coder vos informations d’utilisateur application tooretrieve hello à partir de deux hello `id_token` ou `profile_info`; selon ce qui est présent.</span><span class="sxs-lookup"><span data-stu-id="c233b-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="c233b-135">De cette façon lorsque hello est modifié, votre application peut gérer en toute transparence de transition hello de `profile_info` trop`id_token` sans interruption.</span><span class="sxs-lookup"><span data-stu-id="c233b-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c233b-136">**Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello Hello `profile_info` valeur.**</span><span class="sxs-lookup"><span data-stu-id="c233b-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="c233b-137">Suppression de id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="c233b-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="c233b-138">Similaire trop`profile_info`, nous allons supprimer également hello `id_token_expires_in` paramètre des réponses.</span><span class="sxs-lookup"><span data-stu-id="c233b-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="c233b-139">Auparavant, point de terminaison hello v2.0 retourne une valeur pour `id_token_expires_in` avec chaque réponse id_token, par exemple dans une réponse autoriser :</span><span class="sxs-lookup"><span data-stu-id="c233b-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="c233b-140">Ou dans une réponse de jeton :</span><span class="sxs-lookup"><span data-stu-id="c233b-140">Or in a token response:</span></span>

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

<span data-ttu-id="c233b-141">Hello `id_token_expires_in` valeur indiquerait nombre hello de secondes hello id_token reste valide pour.</span><span class="sxs-lookup"><span data-stu-id="c233b-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="c233b-142">Maintenant, nous allons supprimer hello `id_token_expires_in` valeur complètement.</span><span class="sxs-lookup"><span data-stu-id="c233b-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="c233b-143">Au lieu de cela, vous pouvez utiliser la norme d’OpenID Connect hello `nbf` et `exp` validité de hello tooexamine d’un id_token de revendications.</span><span class="sxs-lookup"><span data-stu-id="c233b-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="c233b-144">Consultez hello [référence de jeton v2.0](active-directory-v2-tokens.md) pour plus d’informations sur ces revendications.</span><span class="sxs-lookup"><span data-stu-id="c233b-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c233b-145">**Votre travail : Assurez-vous que votre application ne dépend pas d’existence hello Hello `id_token_expires_in` valeur.**</span><span class="sxs-lookup"><span data-stu-id="c233b-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="c233b-146">Modification revendications hello renvoyées par scope = openid</span><span class="sxs-lookup"><span data-stu-id="c233b-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="c233b-147">Cette modification sera hello plus significatif – en fait, cela affectera presque chaque application qui utilise le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="c233b-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="c233b-148">Plusieurs applications envoi demandes toohello v2.0 point de terminaison à l’aide de hello `openid` étendue, comme :</span><span class="sxs-lookup"><span data-stu-id="c233b-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="c233b-149">Aujourd'hui, lorsque les utilisateur hello consentement pour hello `openid` étendue, votre application reçoit une mine d’informations sur l’utilisateur de hello en hello résultant id_token.</span><span class="sxs-lookup"><span data-stu-id="c233b-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="c233b-150">Ces revendications peuvent inclure son nom, son nom d’utilisateur par défaut, son adresse de messagerie, son ID objet, etc.</span><span class="sxs-lookup"><span data-stu-id="c233b-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="c233b-151">Cette mise à jour, nous modifions les informations hello que hello `openid` étendue permet à votre application l’accès à comform toobetter avec hello OpenID Connect de spécification.</span><span class="sxs-lookup"><span data-stu-id="c233b-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="c233b-152">Hello `openid` étendue uniquement votre application toosign hello utilisateur et de recevoir un identificateur spécifique à l’application pour l’utilisateur de hello Bonjour `sub` de hello id_token de revendication.</span><span class="sxs-lookup"><span data-stu-id="c233b-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="c233b-153">Hello des revendications dans une id_token avec uniquement hello `openid` étendue accordée sera inclut pas les informations d’identification personnelle.</span><span class="sxs-lookup"><span data-stu-id="c233b-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="c233b-154">Exemples de revendication contenus dans le paramètre id_token :</span><span class="sxs-lookup"><span data-stu-id="c233b-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="c233b-155">Si vous souhaitez tooobtain informations d’identification personnelle (PII) sur l’utilisateur de hello dans votre application, toorequest des autorisations supplémentaires à partir de l’utilisateur de hello est nécessaire à votre application.</span><span class="sxs-lookup"><span data-stu-id="c233b-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="c233b-156">Nous vous présentons prise en charge de deux étendues à partir de la spécification OpenID Connect de hello : hello `email` et `profile` étendues – qui vous toodo donc.</span><span class="sxs-lookup"><span data-stu-id="c233b-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="c233b-157">Hello `email` étendue est très simple : il permet d’adresse de messagerie principale de votre application l’accès toohello l’utilisateur via hello `email` hello id_token de revendication.</span><span class="sxs-lookup"><span data-stu-id="c233b-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="c233b-158">Notez que hello `email` revendication pas sera toujours présente dans id_tokens : elle sera inclus si elle est disponible dans le profil de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="c233b-159">Hello `profile` étendue permet à votre tooall d’accès application autres informations de base utilisateur hello-le nom, le nom d’utilisateur par défaut, ID d’objet et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="c233b-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="c233b-160">Cela vous permet de toocode votre application de façon minimale divulgation – vous pouvez demander à utilisateur de hello pour simplement hello information que votre application requiert toodo son travail.</span><span class="sxs-lookup"><span data-stu-id="c233b-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="c233b-161">Si vous souhaitez toocontinue mise en route du jeu complet de hello des informations utilisateur qui reçoit actuellement votre application, vous devez inclure toutes les étendues de trois dans vos demandes d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="c233b-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="c233b-162">Votre application peut commencer à envoyer hello `email` et `profile` étendues immédiatement et point de terminaison hello v2.0 acceptera ces deux étendues et commencer à demander des autorisations aux utilisateurs selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="c233b-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="c233b-163">Toutefois, hello modifier dans interprétation hello Hello `openid` étendue ne prendront effet que de quelques semaines.</span><span class="sxs-lookup"><span data-stu-id="c233b-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c233b-164">**Votre travail : ajouter hello `profile` et `email` étendues si votre application nécessite des informations sur l’utilisateur de hello.**</span><span class="sxs-lookup"><span data-stu-id="c233b-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="c233b-165">Notez que la bibliothèque ADAL inclut ces deux autorisations dans les requêtes par défaut.</span><span class="sxs-lookup"><span data-stu-id="c233b-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="c233b-166">Suppression hello émetteur barre oblique de fin.</span><span class="sxs-lookup"><span data-stu-id="c233b-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="c233b-167">Auparavant, valeur d’émetteur hello qui apparaît dans les jetons à partir du point de terminaison hello v2.0 a duré formulaire de hello</span><span class="sxs-lookup"><span data-stu-id="c233b-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="c233b-168">Où le guid de hello a été tenantId hello du client hello Azure AD qui a émis le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="c233b-169">Avec ces modifications, valeur d’émetteur hello devient</span><span class="sxs-lookup"><span data-stu-id="c233b-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="c233b-170">dans les deux jetons et dans le document de découverte hello OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c233b-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c233b-171">**Votre travail : Assurez-vous que votre application accepte une valeur d’émetteur hello avec et sans barre oblique de fin lors de la validation de l’émetteur.**</span><span class="sxs-lookup"><span data-stu-id="c233b-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="c233b-172">Pourquoi introduire des modifications ?</span><span class="sxs-lookup"><span data-stu-id="c233b-172">Why change?</span></span>
<span data-ttu-id="c233b-173">la motivation principale Hello pour l’introduction de ces modifications est toobe conforme à hello OpenID Connect la spécification standard.</span><span class="sxs-lookup"><span data-stu-id="c233b-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="c233b-174">En étant OpenID Connect conforme, nous espérons que toominimize les différences entre l’intégration avec les services d’identité de Microsoft et à d’autres services d’identité dans l’industrie de hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="c233b-175">Il convient de leurs bibliothèques d’authentification open source favorite tooenable développeurs toouse sans avoir des différences de Microsoft tooaccommodate tooalter hello bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="c233b-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="c233b-176">Que pouvez-vous faire ?</span><span class="sxs-lookup"><span data-stu-id="c233b-176">What can you do?</span></span>
<span data-ttu-id="c233b-177">À compter d’aujourd'hui, vous pouvez commencer à effectuer toutes les modifications de hello décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c233b-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="c233b-178">Vous devez immédiatement :</span><span class="sxs-lookup"><span data-stu-id="c233b-178">You should immediately:</span></span>

1. <span data-ttu-id="c233b-179">**Supprimez toutes les dépendances hello `x5t` paramètre d’en-tête.**</span><span class="sxs-lookup"><span data-stu-id="c233b-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="c233b-180">**Transition hello de façon à gérer `profile_info` trop`id_token` dans les réponses de jeton.**</span><span class="sxs-lookup"><span data-stu-id="c233b-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="c233b-181">**Supprimez toutes les dépendances hello `id_token_expires_in` paramètre de la réponse.**</span><span class="sxs-lookup"><span data-stu-id="c233b-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="c233b-182">**Ajouter hello `profile` et `email` étendues tooyour application si votre application a besoin des informations utilisateur de base.**</span><span class="sxs-lookup"><span data-stu-id="c233b-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="c233b-183">**Accepter les valeurs issuer dans les jetons avec et sans barre oblique finale.**</span><span class="sxs-lookup"><span data-stu-id="c233b-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="c233b-184">Notre [documentation du protocole v2.0](active-directory-v2-protocols.md) a déjà été mis à jour tooreflect ces modifications, donc vous pouvez l’utiliser comme référence pour aider aux mettre à jour votre code.</span><span class="sxs-lookup"><span data-stu-id="c233b-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="c233b-185">Si vous avez d’autres questions sur l’étendue de hello des modifications de hello, vous pouvez tooreach libre hors toous sur Twitter à @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="c233b-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="c233b-186">Quelle sera la fréquence des modifications du protocole ?</span><span class="sxs-lookup"><span data-stu-id="c233b-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="c233b-187">Nous ne prévoient pas les dernières modifications toohello protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="c233b-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="c233b-188">Nous sommes intentionnellement regroupement de ces modifications dans une version afin que vous n’avez pas à nouveau tôt toogo via ce type de processus de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c233b-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="c233b-189">Bien entendu, nous continuerons tooadd fonctionnalités toohello convergé service d’authentification v2.0 dont vous pouvez tirer parti de, mais ces modifications doivent être additif et saut pas de code existant.</span><span class="sxs-lookup"><span data-stu-id="c233b-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="c233b-190">Enfin, nous aimerions toosay Merci d’essayer les choses pendant la période d’évaluation hello.</span><span class="sxs-lookup"><span data-stu-id="c233b-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="c233b-191">analyses de Hello et l’expérience de nos premiers ont été inestimable jusqu’ici, et nous espérons que vous allez continuer tooshare votre avis et des idées.</span><span class="sxs-lookup"><span data-stu-id="c233b-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="c233b-192">Codez bien !</span><span class="sxs-lookup"><span data-stu-id="c233b-192">Happy coding!</span></span>

<span data-ttu-id="c233b-193">Hello Division d’identité Microsoft</span><span class="sxs-lookup"><span data-stu-id="c233b-193">hello Microsoft Identity Division</span></span>

