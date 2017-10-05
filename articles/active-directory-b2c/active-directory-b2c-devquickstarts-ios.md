---
title: "Obtention d’un jeton à l’aide d’une application iOS - Azure AD B2C | Microsoft Docs"
description: "Cet article vous montre comment créer une application iOS qui utilise AppAuth avec Azure Active Directory B2C pour gérer les identités utilisateur et authentifier les utilisateurs."
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
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="f7663-103">Azure Active Directory B2C : Se connecter à l’aide d’une application iOS</span><span class="sxs-lookup"><span data-stu-id="f7663-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="f7663-104">La plateforme d’identité Microsoft utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f7663-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f7663-105">L’utilisation d’un protocole standard ouvert offre plusieurs options de développeur lors de la sélection d’une bibliothèque à intégrer à nos services.</span><span class="sxs-lookup"><span data-stu-id="f7663-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="f7663-106">Nous proposons cette procédure pas à pas et d’autres similaires pour aider les développeurs à écrire des applications qui se connectent à la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="f7663-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="f7663-107">La plupart des bibliothèques qui implémentent [la spécification RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sont en mesure de se connecter à la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="f7663-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="f7663-108">Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="f7663-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="f7663-109">Cet exemple utilise une bibliothèque tierce appelée AppAuth dont la compatibilité a été testée dans des scénarios de base avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f7663-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="f7663-110">Les problèmes et les demandes de fonctionnalités doivent être soumis au projet open source de la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="f7663-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="f7663-111">Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="f7663-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="f7663-112">Si vous découvrez OAuth2 ou OpenID Connect, cet exemple de configuration n’est peut-être pas très parlant pour vous.</span><span class="sxs-lookup"><span data-stu-id="f7663-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="f7663-113">Nous vous recommandons de consulter une brève [vue d’ensemble du protocole que nous avons décrit ici](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f7663-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f7663-114">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f7663-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="f7663-115">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="f7663-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f7663-116">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes et autres.</span><span class="sxs-lookup"><span data-stu-id="f7663-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="f7663-117">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f7663-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f7663-118">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="f7663-118">Create an application</span></span>
<span data-ttu-id="f7663-119">Vous devez maintenant créer dans votre répertoire B2C une application</span><span class="sxs-lookup"><span data-stu-id="f7663-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="f7663-120">L’inscription des applications fournit à Azure AD les informations nécessaires pour communiquer avec votre application en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="f7663-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="f7663-121">Pour créer une application mobile, suivez [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f7663-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f7663-122">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7663-122">Be sure to:</span></span>

* <span data-ttu-id="f7663-123">Incluez un **Client natif** dans l’application.</span><span class="sxs-lookup"><span data-stu-id="f7663-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="f7663-124">Copiez l’ **ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="f7663-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="f7663-125">Vous aurez besoin de ce GUID ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f7663-125">You need this GUID later.</span></span>
* <span data-ttu-id="f7663-126">Configurez un **URI de redirection** avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="f7663-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="f7663-127">Vous aurez besoin de cet URI ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f7663-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f7663-128">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="f7663-128">Create your policies</span></span>
<span data-ttu-id="f7663-129">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f7663-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f7663-130">Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées.</span><span class="sxs-lookup"><span data-stu-id="f7663-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="f7663-131">Créez cette stratégie, comme décrit dans l’[article de référence sur les stratégies](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="f7663-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f7663-132">Lorsque vous créez la stratégie, prenez soin de :</span><span class="sxs-lookup"><span data-stu-id="f7663-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="f7663-133">Sous **Sign-up attributes** (Attributs d’abonnement), sélectionnez l’attribut **Nom complet**.</span><span class="sxs-lookup"><span data-stu-id="f7663-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="f7663-134">Vous pouvez sélectionner d’autres attributs également.</span><span class="sxs-lookup"><span data-stu-id="f7663-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="f7663-135">Sous **Revendications d’applications**, sélectionnez le **Nom d’affichage** et l’**ID d’objet de l’utilisateur** des revendications.</span><span class="sxs-lookup"><span data-stu-id="f7663-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="f7663-136">Vous pouvez aussi sélectionner d’autres revendications.</span><span class="sxs-lookup"><span data-stu-id="f7663-136">You can select other claims as well.</span></span>
* <span data-ttu-id="f7663-137">Copiez le **nom** de chaque stratégie après sa création.</span><span class="sxs-lookup"><span data-stu-id="f7663-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="f7663-138">Lorsque vous enregistrez la stratégie, son nom a le préfixe `b2c_1_` .</span><span class="sxs-lookup"><span data-stu-id="f7663-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="f7663-139">Le nom de stratégie vous est demandé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f7663-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f7663-140">Une fois vos stratégies créées, vous pouvez générer votre application.</span><span class="sxs-lookup"><span data-stu-id="f7663-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="f7663-141">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="f7663-141">Download the sample code</span></span>
<span data-ttu-id="f7663-142">Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="f7663-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f7663-143">Vous pouvez télécharger le code et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f7663-143">You can download the code and run it.</span></span> <span data-ttu-id="f7663-144">Pour utiliser votre propre client Azure AD B2C, suivez les instructions du fichier [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f7663-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="f7663-145">Cet exemple a été créé en suivant les instructions du fichier README par le [projet iOS AppAuth sur GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="f7663-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="f7663-146">Pour plus d’informations sur le fonctionnement de l’exemple et la bibliothèque, consultez le fichier README AppAuth sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f7663-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="f7663-147">Modification de votre application pour utiliser Azure AD B2C avec AppAuth</span><span class="sxs-lookup"><span data-stu-id="f7663-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="f7663-148">AppAuth prend en charge iOS 7 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f7663-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="f7663-149">Cependant, pour prendre en charge les connexions sociales sur Google, SFSafariViewController qui requiert iOS 9 ou version ultérieure est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f7663-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="f7663-150">Configuration</span><span class="sxs-lookup"><span data-stu-id="f7663-150">Configuration</span></span>

<span data-ttu-id="f7663-151">Vous pouvez configurer la communication avec Azure AD B2C en spécifiant les URI du point de terminaison d’autorisation et du point de terminaison de jeton.</span><span class="sxs-lookup"><span data-stu-id="f7663-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="f7663-152">Pour générer ces URI, vous avez besoin des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7663-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="f7663-153">ID client (par exemple, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f7663-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="f7663-154">Nom de la stratégie (par exemple, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="f7663-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="f7663-155">L’URI du point de terminaison de jeton peut être généré en remplaçant l’\_ID client et le nom de la stratégie\_ dans l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="f7663-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="f7663-156">L’URI du point de terminaison d’autorisation peut être généré en remplaçant l’\_ID client et le nom de la stratégie\_ dans l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="f7663-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="f7663-157">Exécutez le code suivant pour créer votre objet AuthorizationServiceConfiguration :</span><span class="sxs-lookup"><span data-stu-id="f7663-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="f7663-158">Autorisation</span><span class="sxs-lookup"><span data-stu-id="f7663-158">Authorizing</span></span>

<span data-ttu-id="f7663-159">Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée.</span><span class="sxs-lookup"><span data-stu-id="f7663-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="f7663-160">Pour créer la demande, vous avez besoin des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7663-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="f7663-161">ID client (par exemple, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="f7663-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="f7663-162">URI de redirection avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="f7663-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="f7663-163">Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="f7663-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="f7663-164">Pour configurer votre application pour gérer la redirection vers l’URI avec le schéma personnalisé, vous devez mettre à jour la liste de « schémas d’URL » dans votre Info.pList :</span><span class="sxs-lookup"><span data-stu-id="f7663-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="f7663-165">Ouvrez Info.pList.</span><span class="sxs-lookup"><span data-stu-id="f7663-165">Open Info.pList.</span></span>
* <span data-ttu-id="f7663-166">Survolez une ligne comme « Bundle OS Type Code », puis cliquez sur le symbole \+.</span><span class="sxs-lookup"><span data-stu-id="f7663-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="f7663-167">Renommez la nouvelle ligne « Types d’URL ».</span><span class="sxs-lookup"><span data-stu-id="f7663-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="f7663-168">Cliquez sur la flèche à gauche de « Types d’URL » pour ouvrir l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="f7663-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="f7663-169">Cliquez sur la flèche à gauche de « Élément 0 » pour ouvrir l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="f7663-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="f7663-170">Renommez le premier élément sous l’élément 0 « Modèles d’URL ».</span><span class="sxs-lookup"><span data-stu-id="f7663-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="f7663-171">Cliquez sur la flèche à gauche de « Modèles d’URL » pour ouvrir l’arborescence.</span><span class="sxs-lookup"><span data-stu-id="f7663-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="f7663-172">Dans la colonne « Valeur », il y a un champ vide à gauche de « Élément 0 » sous « Modèles d’URL ».</span><span class="sxs-lookup"><span data-stu-id="f7663-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="f7663-173">Définissez la valeur sur le modèle unique de votre application.</span><span class="sxs-lookup"><span data-stu-id="f7663-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="f7663-174">La valeur doit correspondre au modèle utilisé dans redirectURL lors de la création de l’objet OIDAuthorizationRequest.</span><span class="sxs-lookup"><span data-stu-id="f7663-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="f7663-175">Dans notre exemple, nous avons utilisé le schéma « com.onmicrosoft.fabrikamb2c.exampleapp ».</span><span class="sxs-lookup"><span data-stu-id="f7663-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="f7663-176">Reportez-vous au [guide d’AppAuth](https://openid.github.io/AppAuth-iOS/) pour le reste du processus.</span><span class="sxs-lookup"><span data-stu-id="f7663-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="f7663-177">Si vous avez besoin de prendre rapidement en main une application, consultez [notre exemple](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="f7663-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f7663-178">Suivez les étapes du fichier [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) pour entrer votre propre configuration Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f7663-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="f7663-179">Nous sommes ouverts aux commentaires et suggestions !</span><span class="sxs-lookup"><span data-stu-id="f7663-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="f7663-180">Si vous avez des difficultés avec cette rubrique, ou si vous avez des conseils pour améliorer ce contenu, faites-nous part de vos commentaires en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="f7663-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="f7663-181">En cas de demandes liées aux fonctionnalités, utilisez [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="f7663-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
