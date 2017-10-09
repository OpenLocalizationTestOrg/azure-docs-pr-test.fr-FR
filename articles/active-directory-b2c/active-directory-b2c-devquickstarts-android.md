---
title: "Azure Active Directory B2C : Obtenir un jeton à l’aide d’une application Android | Microsoft Docs"
description: "Cet article vous indiquent comment toocreate une application Android qui utilise AppAuth avec des identités d’utilisateur Azure Active Directory B2C toomanage et authentifie les utilisateurs."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="04686-103">Azure Active Directory B2C : Se connecter à l’aide d’une application Android</span><span class="sxs-lookup"><span data-stu-id="04686-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="04686-104">plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="04686-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="04686-105">Cela permet aux développeurs tooleverage n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services.</span><span class="sxs-lookup"><span data-stu-id="04686-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="04686-106">les développeurs tooaid à l’aide de notre plateforme avec d’autres bibliothèques, nous avons écrit quelques procédures pas à pas, comme ce un toodemonstrate comment tooconfigure 3e partie bibliothèques tooconnect toohello plateforme d’identité Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04686-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="04686-107">La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sera platform de Microsoft Identity toohello tooconnect en mesure de.</span><span class="sxs-lookup"><span data-stu-id="04686-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="04686-108">Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="04686-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="04686-109">Cet exemple utilise une bibliothèque tiers 3e appelée AppAuth qui a été testé pour la compatibilité dans les scénarios de base avec hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="04686-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="04686-110">Problèmes et des demandes de fonctionnalités doivent être projet open source de la bibliothèque toohello dirigée.</span><span class="sxs-lookup"><span data-stu-id="04686-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="04686-111">Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="04686-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="04686-112">Si vous êtes tooOAuth2 nouveau ou OpenID Connect une grande partie de cet exemple de configuration peut ne pas effectuer de tooyou sens.</span><span class="sxs-lookup"><span data-stu-id="04686-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="04686-113">Nous vous recommandons de consulter un résumé [vue d’ensemble du protocole hello que nous avons présentés ici](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="04686-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="04686-114">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="04686-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="04686-115">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="04686-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="04686-116">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="04686-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="04686-117">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="04686-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="04686-118">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="04686-118">Create an application</span></span>

<span data-ttu-id="04686-119">Ensuite, vous devez toocreate une application dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="04686-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="04686-120">Cela fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application.</span><span class="sxs-lookup"><span data-stu-id="04686-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="04686-121">toocreate une application mobile, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="04686-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="04686-122">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="04686-122">Be sure to:</span></span>

* <span data-ttu-id="04686-123">Inclure un **Native Client** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="04686-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="04686-124">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="04686-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="04686-125">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="04686-125">You will need this later.</span></span>
* <span data-ttu-id="04686-126">Configurez un **URI de redirection** de client natif (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="04686-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="04686-127">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="04686-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="04686-128">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="04686-128">Create your policies</span></span>

<span data-ttu-id="04686-129">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="04686-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="04686-130">Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées.</span><span class="sxs-lookup"><span data-stu-id="04686-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="04686-131">Vous devez toocreate cette stratégie, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="04686-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="04686-132">Lorsque vous créez la stratégie de hello, veillez à :</span><span class="sxs-lookup"><span data-stu-id="04686-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="04686-133">Choisissez hello **nom d’affichage** comme un attribut d’inscription de votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="04686-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="04686-134">Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="04686-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="04686-135">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="04686-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="04686-136">Hello de copie **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="04686-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="04686-137">Il doit avoir le préfixe de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="04686-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="04686-138">Vous aurez besoin nom de la stratégie hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="04686-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="04686-139">Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="04686-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="04686-140">Télécharger l’exemple de code hello</span><span class="sxs-lookup"><span data-stu-id="04686-140">Download hello sample code</span></span>

<span data-ttu-id="04686-141">Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="04686-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="04686-142">Vous pouvez télécharger le code de hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="04686-142">You can download hello code and run it.</span></span> <span data-ttu-id="04686-143">Vous pouvez rapidement commencer à utiliser votre propre application à l’aide de votre propre configuration Azure AD B2C en suivant les instructions de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="04686-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="04686-144">exemple Hello est une modification de l’exemple hello fournie par [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="04686-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="04686-145">Visitez leur toolearn page plus d’informations sur les AppAuth et de ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="04686-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="04686-146">Modification de votre toouse application Azure AD B2C avec AppAuth</span><span class="sxs-lookup"><span data-stu-id="04686-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="04686-147">AppAuth prend en charge Android API 16 (Jellybean) et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="04686-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="04686-148">Nous recommandons d’utiliser API 23 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="04686-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="04686-149">Configuration</span><span class="sxs-lookup"><span data-stu-id="04686-149">Configuration</span></span>

<span data-ttu-id="04686-150">Vous pouvez configurer la communication avec Azure AD B2C par soit découverte hello en spécifiant des URI ou en spécifiant le point de terminaison d’autorisation hello et URI de point de terminaison token.</span><span class="sxs-lookup"><span data-stu-id="04686-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="04686-151">Dans les deux cas, vous devez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="04686-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="04686-152">ID client (par ex., contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="04686-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="04686-153">Nom de la stratégie (par ex., B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="04686-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="04686-154">Si vous choisissez tooautomatically découverte hello d’autorisation et le jeton de point de terminaison URI, vous aurez besoin des informations de toofetch de la découverte de hello URI.</span><span class="sxs-lookup"><span data-stu-id="04686-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="04686-155">détection de Hello URI peut être généré en remplaçant hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="04686-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="04686-156">Vous pouvez acquérir l’autorisation de hello et URI de point de terminaison token et créer un objet AuthorizationServiceConfiguration en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="04686-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="04686-157">Au lieu d’utiliser l’autorisation de découverte tooobtain hello et URI de point de terminaison token, vous pouvez également spécifier les explicitement en remplaçant hello client\_ID et hello stratégie\_nom dans l’URL de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="04686-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="04686-158">Exécutez hello suivant toocreate de code de votre objet AuthorizationServiceConfiguration :</span><span class="sxs-lookup"><span data-stu-id="04686-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="04686-159">Autorisation</span><span class="sxs-lookup"><span data-stu-id="04686-159">Authorizing</span></span>

<span data-ttu-id="04686-160">Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée.</span><span class="sxs-lookup"><span data-stu-id="04686-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="04686-161">toocreate hello demande, vous devez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="04686-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="04686-162">ID client (par ex. 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="04686-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="04686-163">URI de redirection avec un schéma personnalisé (par ex., com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="04686-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="04686-164">Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="04686-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="04686-165">Reportez-vous toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) sur la façon dont toocomplete hello reste du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="04686-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="04686-166">Si vous avez besoin de tooquickly commencer avec une application, l’extraction [notre exemple](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="04686-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="04686-167">Suivez les étapes de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter votre propre configuration Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="04686-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="04686-168">Nous sommes toujours ouvrir toofeedback ainsi que des suggestions !</span><span class="sxs-lookup"><span data-stu-id="04686-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="04686-169">Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="04686-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="04686-170">Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="04686-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

