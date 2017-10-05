---
title: "Azure Active Directory B2C : Obtenir un jeton à l’aide d’une application Android | Microsoft Docs"
description: "Cet article vous montre comment créer une application Android qui utilise AppAuth avec Azure Active Directory B2C pour gérer les identités utilisateur et authentifier les utilisateurs."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="360bb-103">Azure Active Directory B2C : Se connecter à l’aide d’une application Android</span><span class="sxs-lookup"><span data-stu-id="360bb-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="360bb-104">La plateforme d’identité Microsoft utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="360bb-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="360bb-105">Cela permet aux développeurs de tirer parti de toute bibliothèque qu’ils souhaitent intégrer à nos services.</span><span class="sxs-lookup"><span data-stu-id="360bb-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="360bb-106">Pour aider les développeurs à utiliser notre plateforme avec d’autres bibliothèques, nous avons rédigé quelques procédures pas à pas comme celle-ci, afin d’expliquer la configuration des bibliothèques tierces pour se connecter à la plateforme d’identité Microsoft.</span><span class="sxs-lookup"><span data-stu-id="360bb-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="360bb-107">La plupart des bibliothèques qui implémentent [la spécification RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) seront en mesure de se connecter à la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="360bb-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="360bb-108">Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="360bb-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="360bb-109">Cet exemple utilise une bibliothèque tierce appelée AppAuth dont la compatibilité a été testée dans des scénarios de base avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="360bb-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="360bb-110">Les problèmes et les demandes de fonctionnalités doivent être soumis au projet open source de la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="360bb-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="360bb-111">Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="360bb-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="360bb-112">Si vous découvrez OAuth2 ou OpenID Connect, cet exemple de configuration n’est peut-être pas très parlant pour vous.</span><span class="sxs-lookup"><span data-stu-id="360bb-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="360bb-113">Nous vous recommandons de consulter une brève [vue d’ensemble du protocole que nous avons décrit ici](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="360bb-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="360bb-114">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="360bb-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="360bb-115">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="360bb-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="360bb-116">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="360bb-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="360bb-117">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="360bb-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="360bb-118">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="360bb-118">Create an application</span></span>

<span data-ttu-id="360bb-119">Vous devez maintenant créer dans votre répertoire B2C une application</span><span class="sxs-lookup"><span data-stu-id="360bb-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="360bb-120">fournissant à Azure AD les informations nécessaires pour communiquer avec votre application en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="360bb-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="360bb-121">Pour créer une application mobile, suivez [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="360bb-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="360bb-122">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="360bb-122">Be sure to:</span></span>

* <span data-ttu-id="360bb-123">Incluez un **client natif** dans l’application.</span><span class="sxs-lookup"><span data-stu-id="360bb-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="360bb-124">Copiez l’ **ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="360bb-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="360bb-125">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="360bb-125">You will need this later.</span></span>
* <span data-ttu-id="360bb-126">Configurez un **URI de redirection** de client natif (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="360bb-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="360bb-127">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="360bb-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="360bb-128">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="360bb-128">Create your policies</span></span>

<span data-ttu-id="360bb-129">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="360bb-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="360bb-130">Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées.</span><span class="sxs-lookup"><span data-stu-id="360bb-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="360bb-131">Vous devez créer cette stratégie, comme décrit dans l’[article de référence sur les stratégies](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="360bb-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="360bb-132">Lorsque vous créez la stratégie, prenez soin de :</span><span class="sxs-lookup"><span data-stu-id="360bb-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="360bb-133">Choisir le **nom d’affichage** et un attribut d’inscription dans votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="360bb-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="360bb-134">Choisissez le **nom d’affichage** et **l’ID objet** comme revendications d’application pour chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="360bb-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="360bb-135">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="360bb-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="360bb-136">Copiez le **nom** de chaque stratégie après sa création.</span><span class="sxs-lookup"><span data-stu-id="360bb-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="360bb-137">Il doit porter le préfixe `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="360bb-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="360bb-138">Le nom de stratégie vous sera demandé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="360bb-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="360bb-139">Une fois vos stratégies créées, vous pouvez générer votre application.</span><span class="sxs-lookup"><span data-stu-id="360bb-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="360bb-140">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="360bb-140">Download the sample code</span></span>

<span data-ttu-id="360bb-141">Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="360bb-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="360bb-142">Vous pouvez télécharger le code et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="360bb-142">You can download the code and run it.</span></span> <span data-ttu-id="360bb-143">Vous pouvez prendre rapidement en main votre application à l’aide de votre propre configuration Azure AD B2C en suivant les instructions du fichier [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="360bb-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="360bb-144">L’exemple est une modification de l’exemple fourni par [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="360bb-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="360bb-145">Consultez la page correspondante pour en savoir plus sur AppAuth et ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="360bb-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="360bb-146">Modification de votre application pour utiliser Azure AD B2C avec AppAuth</span><span class="sxs-lookup"><span data-stu-id="360bb-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="360bb-147">AppAuth prend en charge Android API 16 (Jellybean) et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="360bb-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="360bb-148">Nous recommandons d’utiliser API 23 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="360bb-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="360bb-149">Configuration</span><span class="sxs-lookup"><span data-stu-id="360bb-149">Configuration</span></span>

<span data-ttu-id="360bb-150">Vous pouvez configurer la communication avec Azure AD B2C en spécifiant l’URI de détection ou en spécifiant les URI du point de terminaison d’autorisation et du point de terminaison de jeton.</span><span class="sxs-lookup"><span data-stu-id="360bb-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="360bb-151">Dans les deux cas, vous aurez besoin des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="360bb-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="360bb-152">ID client (par ex., contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="360bb-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="360bb-153">Nom de la stratégie (par ex., B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="360bb-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="360bb-154">Si vous choisissez de détecter automatiquement les URI du point de terminaison d’autorisation et de jeton URI, vous devrez extraire des informations de l’URI de détection.</span><span class="sxs-lookup"><span data-stu-id="360bb-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="360bb-155">L’URI de détection peut être généré en remplaçant l’\_ID client et le nom de la stratégie\_ dans l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="360bb-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="360bb-156">Vous pouvez alors obtenir les URI des points de terminaison d’autorisation et de jeton et créer un objet AuthorizationServiceConfiguration en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="360bb-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="360bb-157">Plutôt que d’utiliser la détection pour obtenir les URI des points de terminaison d’autorisation et de jeton, vous pouvez également les spécifier explicitement en remplaçant l’\_ID client et le nom de la\_stratégie dans l’URL ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="360bb-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="360bb-158">Exécutez le code suivant pour créer votre objet AuthorizationServiceConfiguration :</span><span class="sxs-lookup"><span data-stu-id="360bb-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="360bb-159">Autorisation</span><span class="sxs-lookup"><span data-stu-id="360bb-159">Authorizing</span></span>

<span data-ttu-id="360bb-160">Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée.</span><span class="sxs-lookup"><span data-stu-id="360bb-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="360bb-161">Pour créer la demande, vous aurez besoin des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="360bb-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="360bb-162">ID client (par ex. 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="360bb-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="360bb-163">URI de redirection avec un schéma personnalisé (par ex., com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="360bb-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="360bb-164">Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="360bb-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="360bb-165">Veuillez vous reporter au [guide d’AppAuth](https://openid.github.io/AppAuth-Android/) pour le reste du processus.</span><span class="sxs-lookup"><span data-stu-id="360bb-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="360bb-166">Si vous avez besoin de prendre rapidement en main une application, consultez [notre exemple](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="360bb-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="360bb-167">Suivez les étapes du fichier [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) pour entrer votre propre configuration Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="360bb-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="360bb-168">Nous sommes ouverts aux commentaires et suggestions !</span><span class="sxs-lookup"><span data-stu-id="360bb-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="360bb-169">Si vous avez des difficultés avec cette rubrique, ou si vous avez des conseils pour améliorer ce contenu, faites-nous part de vos commentaires en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="360bb-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="360bb-170">En cas de demandes liées aux fonctionnalités, utilisez [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="360bb-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

