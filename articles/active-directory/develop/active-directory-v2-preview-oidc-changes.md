---
title: "Modifications apportées au point de terminaison Azure AD v2.0 | Microsoft Docs"
description: "Description des modifications apportées aux protocoles de version préliminaire publique v2.0 du modèle d’application."
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="a173b-103">Mises à jour importantes des protocoles d’authentification v2.0</span><span class="sxs-lookup"><span data-stu-id="a173b-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="a173b-104">À l’intention des développeurs !</span><span class="sxs-lookup"><span data-stu-id="a173b-104">Attention developers!</span></span> <span data-ttu-id="a173b-105">Au cours des deux prochaines semaines, nous allons apporter quelques mises à jour à nos protocoles d’authentification v2.0, qui peuvent impliquer des modifications de dernière minute pour les applications que vous avez écrites pendant la période de la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a173b-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="a173b-106">Quelles sont les applications concernées ?</span><span class="sxs-lookup"><span data-stu-id="a173b-106">Who does this affect?</span></span>
<span data-ttu-id="a173b-107">Les applications qui ont été écrites pour utiliser le point de terminaison d’authentification convergé v2.0 :</span><span class="sxs-lookup"><span data-stu-id="a173b-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="a173b-108">Pour plus d’informations sur le point de terminaison v2.0, cliquez [ici](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a173b-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="a173b-109">Si vous avez développé une application utilisant le point de terminaison v2.0 en la codant directement dans le protocole v2.0, à l’aide de nos intergiciels web OpenID Connect ou OAuth ou à l’aide d’autres bibliothèques tierces pour effectuer l’authentification, vous devez vous préparer à tester vos projets et à leur apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a173b-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="a173b-110">Quelles sont les applications non concernées ?</span><span class="sxs-lookup"><span data-stu-id="a173b-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="a173b-111">Les applications qui ont été écrites par rapport au point de terminaison d’authentification Azure AD de production :</span><span class="sxs-lookup"><span data-stu-id="a173b-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="a173b-112">Ce protocole n’est pas susceptible de subir des modifications.</span><span class="sxs-lookup"><span data-stu-id="a173b-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="a173b-113">En outre, si votre application utilise **uniquement** notre bibliothèque ADAL pour effectuer l’authentification, vous n’avez pas à modifier quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="a173b-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="a173b-114">ADAL protège votre application des modifications.</span><span class="sxs-lookup"><span data-stu-id="a173b-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="a173b-115">Quelles sont les modifications ?</span><span class="sxs-lookup"><span data-stu-id="a173b-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="a173b-116">Suppression de la valeur x5t des en-têtes JWT</span><span class="sxs-lookup"><span data-stu-id="a173b-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="a173b-117">Le point de terminaison v2.0 utilise largement les jetons JWT, qui contiennent une section de paramètres d’en-tête avec des métadonnées pertinentes sur le jeton.</span><span class="sxs-lookup"><span data-stu-id="a173b-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="a173b-118">Si vous décodez l’en-tête de l’un de nos jetons JWT actuels, le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a173b-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="a173b-119">Où les propriétés « x5t » et « kid » identifient la clé publique à utiliser pour valider la signature du jeton, récupérée à partir du point de terminaison des métadonnées OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="a173b-120">La modification que nous effectuons ici consiste à supprimer la propriété « x5t ».</span><span class="sxs-lookup"><span data-stu-id="a173b-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="a173b-121">Vous pouvez continuer à utiliser les mêmes mécanismes pour valider les jetons, mais vous devez utiliser uniquement la propriété « kid » pour récupérer la clé publique appropriée, comme spécifié dans le protocole OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a173b-122">**Votre tâche : vous assurer que votre application ne dépend pas de l’existence de la valeur x5t.**</span><span class="sxs-lookup"><span data-stu-id="a173b-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="a173b-123">Suppression de profile_info</span><span class="sxs-lookup"><span data-stu-id="a173b-123">Removing profile_info</span></span>
<span data-ttu-id="a173b-124">Auparavant, le point de terminaison v2.0 retournait un objet JSON encodé en Base64 dans les réponses de jeton `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="a173b-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="a173b-125">Lorsque vous demandiez un jeton d’accès à partir du point de terminaison v2.0 en envoyant une requête à :</span><span class="sxs-lookup"><span data-stu-id="a173b-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="a173b-126">La réponse ressemblait à l’objet JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="a173b-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="a173b-127">La valeur `profile_info` contenait des informations sur l’utilisateur connecté à l’application : son nom d’affichage, son prénom, son nom, son adresse de messagerie, son identificateur, etc.</span><span class="sxs-lookup"><span data-stu-id="a173b-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="a173b-128">Le paramètre `profile_info` était essentiellement utilisé pour la mise en cache des jetons et l’affichage.</span><span class="sxs-lookup"><span data-stu-id="a173b-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="a173b-129">Nous procédons actuellement à la suppression de la valeur `profile_info` , mais ne vous inquiétez pas, nous fournirons toujours ces informations aux développeurs à un endroit légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="a173b-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="a173b-130">À la place du paramètre `profile_info`, le point de terminaison v2.0 retourne désormais un paramètre `id_token` dans chaque réponse de jeton :</span><span class="sxs-lookup"><span data-stu-id="a173b-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="a173b-131">Vous pouvez décoder et analyser le paramètre id_token pour récupérer les informations que vous receviez de profile_info.</span><span class="sxs-lookup"><span data-stu-id="a173b-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="a173b-132">Le paramètre id_token est un jeton JWT (JSON Web Token) comportant du contenu, comme spécifié par OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="a173b-133">Le code permettant d’effectuer cette opération est très semblable : il vous suffit d’extraire le segment de milieu (le corps) du paramètre id_token et de le décoder en Base64 pour accéder à l’objet JSON qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="a173b-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="a173b-134">Au cours des deux prochaines semaines, vous devrez coder votre application pour récupérer les informations utilisateur des paramètres `id_token` ou `profile_info` selon celui qui sera présent.</span><span class="sxs-lookup"><span data-stu-id="a173b-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="a173b-135">Ce faisant, lorsque la modification sera effectuée, votre application pourra gérer en toute transparence la transition de `profile_info` à `id_token` sans interruption.</span><span class="sxs-lookup"><span data-stu-id="a173b-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a173b-136">**Votre tâche : vérifier que votre application ne dépend pas de l’existence de la valeur `profile_info`.**</span><span class="sxs-lookup"><span data-stu-id="a173b-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="a173b-137">Suppression de id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="a173b-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="a173b-138">Comme pour le paramètre `profile_info`, nous allons également supprimer le paramètre `id_token_expires_in` dans les réponses.</span><span class="sxs-lookup"><span data-stu-id="a173b-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="a173b-139">Auparavant, le point de terminaison v2.0 retournait une valeur pour le paramètre `id_token_expires_in` avec chaque réponse id_token, par exemple dans une réponse d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="a173b-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="a173b-140">Ou dans une réponse de jeton :</span><span class="sxs-lookup"><span data-stu-id="a173b-140">Or in a token response:</span></span>

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

<span data-ttu-id="a173b-141">La valeur `id_token_expires_in` indiquait le nombre de secondes pendant lesquelles le paramètre id_token restait valide.</span><span class="sxs-lookup"><span data-stu-id="a173b-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="a173b-142">À présent, nous allons supprimer complètement la valeur `id_token_expires_in` .</span><span class="sxs-lookup"><span data-stu-id="a173b-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="a173b-143">À la place, vous pourrez utiliser les revendications OpenID Connect `nbf` et `exp` standard pour examiner la validité d’un paramètre id_token.</span><span class="sxs-lookup"><span data-stu-id="a173b-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="a173b-144">Pour plus d’informations sur ces revendications, consultez les [Informations de référence sur les jetons v2.0](active-directory-v2-tokens.md)</span><span class="sxs-lookup"><span data-stu-id="a173b-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a173b-145">**Votre tâche : vérifier que votre application ne dépend pas de l’existence de la valeur `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="a173b-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="a173b-146">Modification des revendications retournées par scope=openid</span><span class="sxs-lookup"><span data-stu-id="a173b-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="a173b-147">Cette modification sera la plus importante : de fait, elle concerne pratiquement toutes les applications qui utilisent le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="a173b-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="a173b-148">De nombreuses applications envoient des requêtes vers le point de terminaison v2.0 en utilisant l’étendue `openid`, comme :</span><span class="sxs-lookup"><span data-stu-id="a173b-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="a173b-149">Aujourd’hui, lorsque l’utilisateur autorise l’étendue `openid`, votre application reçoit une mine d’informations sur l’utilisateur dans le paramètre id_token résultant.</span><span class="sxs-lookup"><span data-stu-id="a173b-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="a173b-150">Ces revendications peuvent inclure son nom, son nom d’utilisateur par défaut, son adresse de messagerie, son ID objet, etc.</span><span class="sxs-lookup"><span data-stu-id="a173b-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="a173b-151">Au cours de cette mise à jour, nous allons modifier les informations auxquelles l’étendue `openid` permet à votre application d’accéder afin d’assurer une meilleure conformité avec la spécification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="a173b-152">L’étendue `openid` permettra uniquement à votre application de connecter l’utilisateur et de recevoir un identificateur propre à l’application pour l’utilisateur dans la revendication `sub` du paramètre id_token.</span><span class="sxs-lookup"><span data-stu-id="a173b-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="a173b-153">Les revendications contenues dans un paramètre id_token avec uniquement l’étendue `openid` accordée seront dépourvues des informations d’identification personnelle.</span><span class="sxs-lookup"><span data-stu-id="a173b-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="a173b-154">Exemples de revendication contenus dans le paramètre id_token :</span><span class="sxs-lookup"><span data-stu-id="a173b-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="a173b-155">Si vous souhaitez obtenir des informations d’identification personnelle (PII) sur l’utilisateur dans votre application, votre application devra lui demander des autorisations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a173b-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="a173b-156">Nous introduisons la prise en charge de deux nouvelles étendues de la spécification OpenID Connect, les étendues `email` et `profile`, qui vous permettront d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="a173b-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="a173b-157">L’étendue `email` est très directe : elle permet à votre application d’accéder à l’adresse de messagerie principale de l’utilisateur via la revendication `email` contenue dans le paramètre id_token.</span><span class="sxs-lookup"><span data-stu-id="a173b-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="a173b-158">Notez que la revendication `email` n’est pas toujours présente dans le paramètre id_token : elle n’est incluse que si elle est disponible dans le profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a173b-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="a173b-159">L’étendue `profile` permet à votre application d’accéder à toutes les autres informations de base sur l’utilisateur (nom, nom d’utilisateur par défaut, ID objet, etc.).</span><span class="sxs-lookup"><span data-stu-id="a173b-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="a173b-160">Vous pouvez ainsi coder votre application en en divulguant le moins possible : vous pouvez vous contenter de demander à l’utilisateur les informations nécessaires à l’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="a173b-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="a173b-161">Si vous souhaitez continuer à obtenir les informations utilisateur complètes reçues actuellement par votre application, vous devez inclure les trois étendues dans vos demandes d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="a173b-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="a173b-162">Votre application peut commencer à envoyer immédiatement les étendues `email` et `profile`, et le point de terminaison v2.0 acceptera ces deux étendues et commencera à demander des autorisations aux utilisateurs, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a173b-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="a173b-163">Toutefois, la modification de l’interprétation de l’étendue `openid` ne prendra pas effet avant quelques semaines.</span><span class="sxs-lookup"><span data-stu-id="a173b-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a173b-164">**Votre tâche : ajouter les étendues `profile` et `email` si votre application a besoin d’informations sur l’utilisateur.**</span><span class="sxs-lookup"><span data-stu-id="a173b-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="a173b-165">Notez que la bibliothèque ADAL inclut ces deux autorisations dans les requêtes par défaut.</span><span class="sxs-lookup"><span data-stu-id="a173b-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="a173b-166">Suppression de la barre oblique finale dans la valeur issuer</span><span class="sxs-lookup"><span data-stu-id="a173b-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="a173b-167">Auparavant, la valeur issuer qui apparaissait dans les jetons du point de terminaison v2.0 prenait la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="a173b-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="a173b-168">Où le GUID était l’ID du locataire Azure AD qui a émis le jeton.</span><span class="sxs-lookup"><span data-stu-id="a173b-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="a173b-169">Avec ces modifications, la valeur issuer devient :</span><span class="sxs-lookup"><span data-stu-id="a173b-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="a173b-170">dans les deux jetons et dans le document de découverte OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a173b-171">**Votre travail : vous assurer que votre application accepte la valeur issuer avec et sans barre oblique finale lors de la validation de l’émetteur.**</span><span class="sxs-lookup"><span data-stu-id="a173b-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="a173b-172">Pourquoi introduire des modifications ?</span><span class="sxs-lookup"><span data-stu-id="a173b-172">Why change?</span></span>
<span data-ttu-id="a173b-173">La principale motivation ayant amené à introduire ces modifications est la conformité à la spécification standard OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a173b-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="a173b-174">Avec cette conformité, nous espérons réduire les différences entre l’intégration aux services d’identité de Microsoft et l’intégration aux autres services d’identité du secteur d’activité.</span><span class="sxs-lookup"><span data-stu-id="a173b-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="a173b-175">Nous souhaitons permettre aux développeurs d’utiliser leurs bibliothèques d’authentification open source favorites sans avoir à les modifier pour prendre en compte les différences de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a173b-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="a173b-176">Que pouvez-vous faire ?</span><span class="sxs-lookup"><span data-stu-id="a173b-176">What can you do?</span></span>
<span data-ttu-id="a173b-177">Dès aujourd’hui, vous pouvez commencer à effectuer toutes les modifications décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a173b-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="a173b-178">Vous devez immédiatement :</span><span class="sxs-lookup"><span data-stu-id="a173b-178">You should immediately:</span></span>

1. <span data-ttu-id="a173b-179">**Supprimer toutes les dépendances dans le paramètre d’en-tête `x5t`.**</span><span class="sxs-lookup"><span data-stu-id="a173b-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="a173b-180">**Gérer en douceur la transition entre les paramètres `profile_info` et `id_token` dans les réponses de jeton.**</span><span class="sxs-lookup"><span data-stu-id="a173b-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="a173b-181">**Supprimer toutes les dépendances dans le paramètre de réponse `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="a173b-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="a173b-182">**Ajouter les étendues `profile` et `email` à votre application, si celle-ci a besoin d’informations utilisateur de base.**</span><span class="sxs-lookup"><span data-stu-id="a173b-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="a173b-183">**Accepter les valeurs issuer dans les jetons avec et sans barre oblique finale.**</span><span class="sxs-lookup"><span data-stu-id="a173b-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="a173b-184">Notre [documentation relative au protocole v2.0](active-directory-v2-protocols.md) a déjà été mise à jour pour refléter ces modifications. Vous pouvez donc l’utiliser à titre de référence pour vous aider à mettre à jour votre code.</span><span class="sxs-lookup"><span data-stu-id="a173b-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="a173b-185">Si vous avez d’autres questions sur l’étendue de ces modifications, n’hésitez pas à nous contacter sur Twitter à @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="a173b-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="a173b-186">Quelle sera la fréquence des modifications du protocole ?</span><span class="sxs-lookup"><span data-stu-id="a173b-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="a173b-187">Nous ne prévoyons pas d’apporter d’autres modifications de ce type aux protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a173b-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="a173b-188">Nous regroupons intentionnellement ces modifications dans une seule version afin que vous n’ayez pas à effectuer de nouveau ce type de mise à jour dans un temps rapproché.</span><span class="sxs-lookup"><span data-stu-id="a173b-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="a173b-189">Bien entendu, nous continuerons d’ajouter des fonctionnalités au service d’authentification v2.0 convergé dont vous pourrez bénéficier. Néanmoins, ces modifications devraient constituer des ajouts et pas une rupture du code existant.</span><span class="sxs-lookup"><span data-stu-id="a173b-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="a173b-190">Pour finir, nous souhaitons vous remercier d’avoir procédé à des essais pendant cette version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a173b-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="a173b-191">Les informations et les expériences de nos utilisateurs précoces nous ont été très utiles jusqu’à présent, et nous espérons que vous continuerez de partager vos opinions et vos idées.</span><span class="sxs-lookup"><span data-stu-id="a173b-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="a173b-192">Codez bien !</span><span class="sxs-lookup"><span data-stu-id="a173b-192">Happy coding!</span></span>

<span data-ttu-id="a173b-193">La Division d’identité de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a173b-193">The Microsoft Identity Division</span></span>

