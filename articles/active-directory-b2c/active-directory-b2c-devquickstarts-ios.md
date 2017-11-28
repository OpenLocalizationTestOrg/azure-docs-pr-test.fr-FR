---
title: "Obtention d’un jeton à l’aide d’une application iOS - Azure AD B2C | Microsoft Docs"
description: "Cet article vous indiquent comment toocreate une application iOS qui utilise AppAuth avec des identités d’utilisateur Azure Active Directory B2C toomanage et authentifie les utilisateurs."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="5c859-103">Azure Active Directory B2C : Se connecter à l’aide d’une application iOS</span><span class="sxs-lookup"><span data-stu-id="5c859-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="5c859-104">plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5c859-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="5c859-105">À l’aide d’un protocole standard ouvert propose plusieurs développeurs lors de la sélection d’un toointegrate de bibliothèque avec nos services.</span><span class="sxs-lookup"><span data-stu-id="5c859-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="5c859-106">Nous vous avons fourni cette procédure pas à pas et autres similaires aux développeurs de tooaid avec l’écriture d’applications qui se connectent de plateforme de Microsoft Identity toohello.</span><span class="sxs-lookup"><span data-stu-id="5c859-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="5c859-107">La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sont en mesure de tooconnect toohello Microsoft Identity plateforme.</span><span class="sxs-lookup"><span data-stu-id="5c859-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="5c859-108">Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="5c859-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="5c859-109">Cet exemple utilise une bibliothèque tierce appelée AppAuth qui a été testé pour la compatibilité dans les scénarios de base avec hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5c859-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="5c859-110">Problèmes et des demandes de fonctionnalités doivent être projet open source de la bibliothèque toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="5c859-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="5c859-111">Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="5c859-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="5c859-112">Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer de tooyou sens.</span><span class="sxs-lookup"><span data-stu-id="5c859-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="5c859-113">Nous vous recommandons de consulter un résumé [vue d’ensemble du protocole hello que nous avons présentés ici](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="5c859-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="5c859-114">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5c859-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="5c859-115">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="5c859-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="5c859-116">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes et autres.</span><span class="sxs-lookup"><span data-stu-id="5c859-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="5c859-117">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="5c859-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="5c859-118">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="5c859-118">Create an application</span></span>
<span data-ttu-id="5c859-119">Ensuite, vous devez toocreate une application dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="5c859-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="5c859-120">inscription d’une application Hello fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application.</span><span class="sxs-lookup"><span data-stu-id="5c859-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="5c859-121">toocreate une application mobile, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5c859-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="5c859-122">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c859-122">Be sure to:</span></span>

* <span data-ttu-id="5c859-123">Inclure un **Native client** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="5c859-124">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="5c859-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="5c859-125">Vous aurez besoin de ce GUID ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="5c859-125">You need this GUID later.</span></span>
* <span data-ttu-id="5c859-126">Configurez un **URI de redirection** avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="5c859-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="5c859-127">Vous aurez besoin de cet URI ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="5c859-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="5c859-128">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="5c859-128">Create your policies</span></span>
<span data-ttu-id="5c859-129">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5c859-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5c859-130">Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées.</span><span class="sxs-lookup"><span data-stu-id="5c859-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="5c859-131">Créez cette stratégie, comme décrit dans l’[article de référence sur les stratégies](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="5c859-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="5c859-132">Lorsque vous créez la stratégie de hello, veillez à :</span><span class="sxs-lookup"><span data-stu-id="5c859-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="5c859-133">Sous **des attributs d’abonnement**, sélectionnez les attributs hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="5c859-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="5c859-134">Vous pouvez sélectionner d’autres attributs également.</span><span class="sxs-lookup"><span data-stu-id="5c859-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="5c859-135">Sous **revendications Application**, sélectionnez les revendications hello **nom d’affichage** et **ID d’objet de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5c859-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="5c859-136">Vous pouvez aussi sélectionner d’autres revendications.</span><span class="sxs-lookup"><span data-stu-id="5c859-136">You can select other claims as well.</span></span>
* <span data-ttu-id="5c859-137">Hello de copie **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="5c859-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="5c859-138">Votre nom de la stratégie est préfixé avec `b2c_1_` lorsque vous enregistrez la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="5c859-139">Vous devez nom de la stratégie hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="5c859-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="5c859-140">Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="5c859-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="5c859-141">Télécharger l’exemple de code hello</span><span class="sxs-lookup"><span data-stu-id="5c859-141">Download hello sample code</span></span>
<span data-ttu-id="5c859-142">Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="5c859-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="5c859-143">Vous pouvez télécharger le code de hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="5c859-143">You can download hello code and run it.</span></span> <span data-ttu-id="5c859-144">toouse votre propre B2C de AD Azure locataire, suivez les instructions de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5c859-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="5c859-145">Cet exemple a été créé en suivant les instructions du fichier Lisezmoi hello en hello [iOS AppAuth projet sur GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="5c859-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="5c859-146">Pour plus d’informations sur le fonctionnement des exemple hello et bibliothèque de hello, référence hello README AppAuth sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c859-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="5c859-147">Modification de votre toouse application Azure AD B2C avec AppAuth</span><span class="sxs-lookup"><span data-stu-id="5c859-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="5c859-148">AppAuth prend en charge iOS 7 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="5c859-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="5c859-149">Toutefois, toosupport des connexions social de Google, SFSafariViewController qui nécessite d’iOS 9 ou version ultérieure est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5c859-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="5c859-150">Configuration</span><span class="sxs-lookup"><span data-stu-id="5c859-150">Configuration</span></span>

<span data-ttu-id="5c859-151">Vous pouvez configurer la communication avec Azure AD B2C en spécifiant le point de terminaison d’autorisation hello et URI de point de terminaison token.</span><span class="sxs-lookup"><span data-stu-id="5c859-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="5c859-152">toogenerate ces URI, vous devez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c859-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="5c859-153">ID client (par exemple, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="5c859-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="5c859-154">Nom de la stratégie (par exemple, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="5c859-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="5c859-155">point de terminaison token URI peut être généré en remplaçant Hello hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="5c859-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="5c859-156">point de terminaison d’URI peut être généré en remplaçant Hello hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="5c859-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="5c859-157">Exécutez hello suivant toocreate de code de votre objet AuthorizationServiceConfiguration :</span><span class="sxs-lookup"><span data-stu-id="5c859-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="5c859-158">Autorisation</span><span class="sxs-lookup"><span data-stu-id="5c859-158">Authorizing</span></span>

<span data-ttu-id="5c859-159">Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée.</span><span class="sxs-lookup"><span data-stu-id="5c859-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="5c859-160">toocreate hello demande, vous devez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c859-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="5c859-161">ID client (par exemple, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="5c859-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="5c859-162">URI de redirection avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="5c859-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="5c859-163">Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="5c859-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="5c859-164">tooset de votre toohello de redirection des hello de toohandle application URI avec un jeu personnalisé de hello, vous avez besoin tooupdate hello liste de « Modèles d’URL » dans votre fichier Info.pList :</span><span class="sxs-lookup"><span data-stu-id="5c859-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="5c859-165">Ouvrez Info.pList.</span><span class="sxs-lookup"><span data-stu-id="5c859-165">Open Info.pList.</span></span>
* <span data-ttu-id="5c859-166">Placez le curseur sur une ligne, comme « Code de Type du système d’exploitation offre groupée » et cliquez sur hello \+ symbole.</span><span class="sxs-lookup"><span data-stu-id="5c859-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="5c859-167">Renommez hello nouvelle ligne 'URL types'.</span><span class="sxs-lookup"><span data-stu-id="5c859-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="5c859-168">Cliquez sur hello flèche toohello gauche d’arborescence de « Types d’URL » tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="5c859-169">Cliquez sur hello flèche toohello gauche d’arborescence de hello tooopen 'Élément 0'.</span><span class="sxs-lookup"><span data-stu-id="5c859-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="5c859-170">Renommez le premier élément sous l’élément 0 too'URL schémas.</span><span class="sxs-lookup"><span data-stu-id="5c859-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="5c859-171">Cliquez sur hello flèche toohello gauche d’arborescence de 'schémas d’URL ' tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="5c859-172">Dans la colonne hello 'Value' ne dispose plus un champ vide toohello de 'Élément 0 », sous « Schémas d’URL ».</span><span class="sxs-lookup"><span data-stu-id="5c859-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="5c859-173">Définissez un jeu unique de l’application hello valeur tooyour.</span><span class="sxs-lookup"><span data-stu-id="5c859-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="5c859-174">valeur de Hello doit correspondre au schéma de hello utilisé dans redirectURL lors de la création d’objet de OIDAuthorizationRequest hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="5c859-175">Dans notre exemple, nous avons utilisé schéma hello 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="5c859-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="5c859-176">Consultez toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) sur la façon dont toocomplete hello reste du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="5c859-177">Si vous avez besoin de tooquickly commencer avec une application, l’extraction [notre exemple](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="5c859-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="5c859-178">Suivez les étapes de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter votre propre configuration Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5c859-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="5c859-179">Nous sommes toujours ouvrir toofeedback ainsi que des suggestions !</span><span class="sxs-lookup"><span data-stu-id="5c859-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="5c859-180">Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="5c859-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="5c859-181">Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="5c859-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
