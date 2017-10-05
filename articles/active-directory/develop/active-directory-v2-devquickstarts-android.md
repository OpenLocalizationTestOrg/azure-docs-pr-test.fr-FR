---
title: "Application Android Azure Active Directory v2.0 | Microsoft Docs"
description: "Génération d’une application Android qui connecte les utilisateurs à l’aide de leur compte Microsoft personnel et de leurs comptes professionnel ou scolaire et appelle l’API Graph à l’aide de bibliothèques tierces."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="8e421-103">Ajouter l’authentification dans une application Android à l’aide d’une bibliothèque tierce avec l’API Graph à l’aide du point de terminaison v2.0</span><span class="sxs-lookup"><span data-stu-id="8e421-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="8e421-104">La plateforme d’identité Microsoft utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8e421-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="8e421-105">Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent intégrer à nos services.</span><span class="sxs-lookup"><span data-stu-id="8e421-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="8e421-106">Pour aider les développeurs à utiliser notre plateforme avec d’autres bibliothèques, nous avons rédigé quelques procédures pas à pas comme celle-ci pour présenter la configuration des bibliothèques tierces pour se connecter à la plateforme d’identité de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e421-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="8e421-107">La plupart des bibliothèques qui implémentent [la spécification RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peuvent se connecter à la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="8e421-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="8e421-108">Avec l’application créée par cette procédure pas à pas, les utilisateurs peuvent se connecter à leur organisation, puis rechercher eux-mêmes dans leur entreprise à l’aide de l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="8e421-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="8e421-109">Si vous découvrez OAuth2 ou OpenID Connect, cet exemple de configuration n’est peut-être pas très parlant pour vous.</span><span class="sxs-lookup"><span data-stu-id="8e421-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="8e421-110">Nous vous recommandons de lire [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8e421-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="8e421-111">Certaines fonctionnalités de notre plateforme qui ont une expression dans les normes OAuth2 ou OpenID Connect, comme la gestion de la stratégie d’accès conditionnel et d’Intune, requièrent l’utilisation de nos bibliothèques d’identité Microsoft Azure open source.</span><span class="sxs-lookup"><span data-stu-id="8e421-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="8e421-112">Le point de terminaison v2.0 ne prend pas en charge l’intégralité des scénarios et fonctionnalités d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e421-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="8e421-113">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8e421-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="8e421-114">Téléchargez le code à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="8e421-114">Download the code from GitHub</span></span>
<span data-ttu-id="8e421-115">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="8e421-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="8e421-116">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="8e421-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="8e421-117">Vous pouvez aussi simplement télécharger l’exemple et commencer immédiatement :</span><span class="sxs-lookup"><span data-stu-id="8e421-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="8e421-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="8e421-118">Register an app</span></span>
<span data-ttu-id="8e421-119">Créez une nouvelle application dans le [Portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez les étapes détaillées dans [Inscription d’une application avec le point de terminaison v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8e421-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="8e421-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="8e421-120">Make sure to:</span></span>

* <span data-ttu-id="8e421-121">Copiez **l’ID d’application** affecté à votre application, vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="8e421-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="8e421-122">ajouter la plateforme **Mobile** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="8e421-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="8e421-123">Remarque : Le portail d’inscription des applications fournit une valeur **URI de redirection** .</span><span class="sxs-lookup"><span data-stu-id="8e421-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="8e421-124">Toutefois, dans cet exemple, vous devez utiliser la valeur par défaut `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="8e421-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="8e421-125">Téléchargez la bibliothèque tierce NXOAuth2 et créez un espace de travail</span><span class="sxs-lookup"><span data-stu-id="8e421-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="8e421-126">Pour cette procédure pas à pas, vous allez utiliser OIDCAndroidLib de GitHub, une bibliothèque OAuth2 basée sur le code OpenID Connect de Google.</span><span class="sxs-lookup"><span data-stu-id="8e421-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="8e421-127">Elle implémente le profil de l’application native et prend en charge le point de terminaison de l’autorisation de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="8e421-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="8e421-128">Voici tout ce dont vous aurez besoin pour l’intégration avec la plateforme d’identité Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e421-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="8e421-129">Clonez le référentiel OIDCAndroidLib sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8e421-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="8e421-131">Configurer votre environnement Android Studio</span><span class="sxs-lookup"><span data-stu-id="8e421-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="8e421-132">Créez un nouveau projet Android Studio et acceptez les valeurs par défaut dans l’assistant.</span><span class="sxs-lookup"><span data-stu-id="8e421-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Créer un nouveau projet dans Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Cibler des appareils Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Ajouter une activité à un mobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="8e421-136">Pour configurer les modules de votre projet, déplacez le référentiel cloné à l’emplacement du projet.</span><span class="sxs-lookup"><span data-stu-id="8e421-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="8e421-137">Vous pouvez également créer le projet puis le cloner directement dans l’emplacement du projet.</span><span class="sxs-lookup"><span data-stu-id="8e421-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="8e421-139">Ouvrez les paramètres de modules du projet à l’aide du menu contextuel ou en utilisant le raccourci Ctrl + Alt + Maj + S.</span><span class="sxs-lookup"><span data-stu-id="8e421-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Paramètres de modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="8e421-141">Supprimez le module d’application par défaut pour conserver uniquement les paramètres de conteneur du projet.</span><span class="sxs-lookup"><span data-stu-id="8e421-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![Le module d’application par défaut](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="8e421-143">Importez des modules à partir du référentiel cloné dans le projet actuel.</span><span class="sxs-lookup"><span data-stu-id="8e421-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="8e421-144">![Importer un projet gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![créer une nouvelle page de module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="8e421-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="8e421-145">Répétez ces étapes pour le module `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="8e421-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="8e421-146">Vérifiez les dépendances oidclib sur le module `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="8e421-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![Dépendances oidclib sur le module oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="8e421-148">Cliquez sur **OK** et attendez l’activité de synchronisation Gradle.</span><span class="sxs-lookup"><span data-stu-id="8e421-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="8e421-149">Votre fichier settings.gradle doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="8e421-149">Your settings.gradle should look like:</span></span>
   
    ![Capture d’écran de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="8e421-151">Générez l’exemple d’application pour vérifier qu’il s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="8e421-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="8e421-152">Vous ne pourrez pas encore l’utiliser avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e421-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="8e421-153">Vous devez d’abord configurer certains points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8e421-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="8e421-154">Cela permet de vérifier l’absence de problèmes au niveau d’Android Studio avant de commencer à personnaliser l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="8e421-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="8e421-155">Générez et exécutez `oidlib-sample` comme cible dans Android Studio.</span><span class="sxs-lookup"><span data-stu-id="8e421-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Progression de la création d’oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="8e421-157">Supprimez le répertoire `app ` conservé après la suppression du module du projet car Android Studio ne le supprime pas par sécurité.</span><span class="sxs-lookup"><span data-stu-id="8e421-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Structure de fichier qui contient le répertoire d’application](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="8e421-159">Ouvrez le menu **Modifier les configurations** pour supprimer la configuration d’exécution également conservée lors de la suppression du module du projet.</span><span class="sxs-lookup"><span data-stu-id="8e421-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="8e421-160">![Menu Modifier les configurations](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Exécuter la configuration de l’application](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="8e421-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="8e421-161">Configurer les points de terminaison de l’exemple</span><span class="sxs-lookup"><span data-stu-id="8e421-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="8e421-162">Maintenant que `oidlib-sample` s’exécute correctement, vous allez modifier quelques points de terminaison pour qu’il fonctionne avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e421-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="8e421-163">Configurez votre client en modifiant le fichier oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="8e421-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="8e421-164">Dans la mesure où nous utilisons seulement les flux OAuth2 pour obtenir un jeton et appeler l’API Graph, nous allons définir le client pour OAuth2 seulement.</span><span class="sxs-lookup"><span data-stu-id="8e421-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="8e421-165">Nous verrons OIDC dans un autre exemple.</span><span class="sxs-lookup"><span data-stu-id="8e421-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="8e421-166">Configurez l’ID client que vous avez reçu à partir du portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="8e421-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="8e421-167">Configurez votre URI de redirection avec celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8e421-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="8e421-168">Configurez les étendues dont vous avez besoin pour accéder à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="8e421-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="8e421-169">La valeur `User.Read` dans `oidc_scopes` vous permet de lire le profil de base de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="8e421-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="8e421-170">Plus d’informations sur toutes les étendues disponibles, consultez [Étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="8e421-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="8e421-171">Si vous souhaitez des explications sur `openid` ou `offline_access` en tant qu’étendues dans OpenID Connect, consultez [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8e421-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="8e421-172">Configurez vos points de terminaison clients en modifiant le fichier oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="8e421-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="8e421-173">Ouvrez le fichier `oidc_endpoints.xml` et effectuez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e421-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="8e421-174">Ces points de terminaison ne doivent jamais changer si vous utilisez OAuth2 comme protocole.</span><span class="sxs-lookup"><span data-stu-id="8e421-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="8e421-175">Les points de terminaison pour `userInfoEndpoint` et `revocationEndpoint` ne sont actuellement pas pris en charge par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e421-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="8e421-176">Si vous laissez la valeur par défaut exemple.com, vous recevrez un rappel qu’ils ne sont pas disponibles dans l’exemple :-)</span><span class="sxs-lookup"><span data-stu-id="8e421-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="8e421-177">Configurer un appel d’API Graph</span><span class="sxs-lookup"><span data-stu-id="8e421-177">Configure a Graph API call</span></span>
* <span data-ttu-id="8e421-178">Ouvrez le fichier `HomeActivity.java` et effectuez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e421-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="8e421-179">Ici, un simple appel à l’API Graph renvoie nos informations.</span><span class="sxs-lookup"><span data-stu-id="8e421-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="8e421-180">Ce sont toutes les modifications que vous devez faire.</span><span class="sxs-lookup"><span data-stu-id="8e421-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="8e421-181">Exécutez l’application `oidlib-sample` , puis cliquez sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="8e421-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="8e421-182">Une fois que vous avez été authentifié, sélectionnez le bouton **Request Protected Resource** (Demander une ressource protégée) pour tester votre appel à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="8e421-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="8e421-183">Obtenir des mises à jour de sécurité pour notre produit</span><span class="sxs-lookup"><span data-stu-id="8e421-183">Get security updates for our product</span></span>
<span data-ttu-id="8e421-184">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [Security TechCenter](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8e421-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

