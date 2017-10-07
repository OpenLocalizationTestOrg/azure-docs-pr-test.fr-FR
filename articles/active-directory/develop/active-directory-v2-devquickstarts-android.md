---
title: "application Android d’aaaAzure Active Directory v2.0 | Documents Microsoft"
description: "Comment une application Android qui se connecte à la fois personnelles compte Microsoft et comptes d’établissement scolaire et passe les appels aux utilisateurs de toobuild hello API Graph en utilisant des bibliothèques tierces."
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
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="4a126-103">Ajouter une application Android de tooan connectez-vous à l’aide d’une bibliothèque tierce avec l’API Graph à l’aide du point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="4a126-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="4a126-104">plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4a126-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="4a126-105">Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services.</span><span class="sxs-lookup"><span data-stu-id="4a126-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="4a126-106">les développeurs de toohelp utilisent notre plateforme avec d’autres bibliothèques, nous avons comment écrit quelques procédures pas à pas, comme cette une toodemonstrate plateforme d’identité tooconnect toohello Microsoft tooconfigure des bibliothèques tierces.</span><span class="sxs-lookup"><span data-stu-id="4a126-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="4a126-107">La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peut se connecter de plateforme d’identité Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="4a126-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="4a126-108">Avec l’application hello qui crée de cette procédure pas à pas, les utilisateurs peuvent se connecter tootheir organisation et puis rechercher eux-mêmes dans leur organisation à l’aide de l’API Graph de hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="4a126-109">Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer tooyou de sens.</span><span class="sxs-lookup"><span data-stu-id="4a126-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="4a126-110">Nous vous recommandons de lire [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4a126-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="4a126-111">Certaines fonctionnalités de notre plateforme qui n’ont pas une expression dans hello OAuth2 ou OpenID Connect des normes, telles que l’accès conditionnel et de gestion des stratégies Intune, requièrent vous toouse open source bibliothèques d’identité Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4a126-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="4a126-112">point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a126-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="4a126-113">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4a126-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="4a126-114">Télécharger le code de hello à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4a126-114">Download hello code from GitHub</span></span>
<span data-ttu-id="4a126-115">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="4a126-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="4a126-116">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="4a126-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="4a126-117">Vous pouvez également simplement télécharger l’exemple hello et démarrer immédiatement :</span><span class="sxs-lookup"><span data-stu-id="4a126-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="4a126-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="4a126-118">Register an app</span></span>
<span data-ttu-id="4a126-119">Créer une application à hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez hello étapes détaillées à [comment tooregister une application avec un point de terminaison hello v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4a126-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="4a126-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="4a126-120">Make sure to:</span></span>

* <span data-ttu-id="4a126-121">Hello de copie **Id d’Application** qui est attribué tooyour application, car vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="4a126-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="4a126-122">Ajouter hello **Mobile** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4a126-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="4a126-123">Remarque : portail de l’enregistrement d’Application hello fournit un **URI de redirection** valeur.</span><span class="sxs-lookup"><span data-stu-id="4a126-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="4a126-124">Toutefois, dans cet exemple, vous devez utiliser valeur par défaut hello `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="4a126-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="4a126-125">Télécharger des bibliothèques tierces de NXOAuth2 hello et créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="4a126-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="4a126-126">Pour cette procédure pas à pas, vous allez utiliser hello OIDCAndroidLib à partir de GitHub, qui est une bibliothèque OAuth2 selon hello code d’OpenID Connect de Google.</span><span class="sxs-lookup"><span data-stu-id="4a126-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="4a126-127">Il implémente le profil d’application native hello et prend en charge le point de terminaison hello d’autorisation d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="4a126-128">Il s’agit de tous les éléments hello que vous devez toointegrate avec la plateforme d’identité Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="4a126-129">Cloner l’ordinateur de tooyour hello OIDCAndroidLib référentiel.</span><span class="sxs-lookup"><span data-stu-id="4a126-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="4a126-131">Configurer votre environnement Android Studio</span><span class="sxs-lookup"><span data-stu-id="4a126-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="4a126-132">Créer un projet Android Studio et acceptez les valeurs par défaut hello dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Créer un nouveau projet dans Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Cibler des appareils Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Ajouter une activité toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="4a126-136">tooset des modules de votre projet, déplacez hello cloné dépôt toohello l’emplacement du projet.</span><span class="sxs-lookup"><span data-stu-id="4a126-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="4a126-137">Vous pouvez également créer des projets de hello et puis clonez-le directement toohello l’emplacement du projet.</span><span class="sxs-lookup"><span data-stu-id="4a126-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="4a126-139">Ouvrez les paramètres de modules de projet hello à l’aide du menu contextuel de hello ou à l’aide du raccourci Ctrl + Alt + Maj + S de hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Paramètres de modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="4a126-141">Supprimer le module d’application hello par défaut parce que vous souhaitez uniquement les paramètres de conteneur de projet hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![module d’application Hello par défaut](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="4a126-143">Importer des modules à partir de projet actuel du toohello hello référentiel cloné.</span><span class="sxs-lookup"><span data-stu-id="4a126-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="4a126-144">![Importer un projet gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![créer une nouvelle page de module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="4a126-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="4a126-145">Répétez ces étapes pour hello `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="4a126-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="4a126-146">Vérification des dépendances d’oidclib hello sur hello `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="4a126-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![oidclib des dépendances sur le module d’oidlib-exemple hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="4a126-148">Cliquez sur **OK** et attendez l’activité de synchronisation Gradle.</span><span class="sxs-lookup"><span data-stu-id="4a126-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="4a126-149">Votre fichier settings.gradle doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4a126-149">Your settings.gradle should look like:</span></span>
   
    ![Capture d’écran de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="4a126-151">Build hello exemple application toomake que cet exemple hello fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="4a126-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="4a126-152">Vous ne pourra plus être en mesure de toouse cela avec Azure Active Directory encore.</span><span class="sxs-lookup"><span data-stu-id="4a126-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="4a126-153">Nous devrons tooconfigure certains points de terminaison tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="4a126-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="4a126-154">Il s’agit de tooensure vous n’avez pas un problème dans Android Studio avant de commencer la personnalisation de hello, exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="4a126-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="4a126-155">Générez et exécutez `oidlib-sample` comme cible de hello dans Android Studio.</span><span class="sxs-lookup"><span data-stu-id="4a126-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Progression de la création d’oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="4a126-157">Supprimer hello `app ` active a été laissée lorsque vous retiré module de hello hello projet car Android Studio ne le supprime pas de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4a126-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Structure de fichier qui inclut le répertoire de l’application hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="4a126-159">Ouvrez hello **modifier les Configurations** menu tooremove hello exécuter configuration qui a été laissée également lorsque vous avez supprimé le module de hello à partir du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="4a126-160">![Menu Modifier les configurations](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Exécuter la configuration de l’application](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="4a126-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="4a126-161">Configurer des points de terminaison hello de l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="4a126-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="4a126-162">Maintenant que vous avez hello `oidlib-sample` en cours d’exécution avec succès, permet de modifier certains points de terminaison tooget ce travail avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a126-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="4a126-163">Configurer votre client en modifiant le fichier de oidc_clientconf.xml hello</span><span class="sxs-lookup"><span data-stu-id="4a126-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="4a126-164">Étant donné que vous utilisez OAuth2 flux tooget uniquement un jeton et appelez hello API Graph, définissez hello client toodo OAuth2 uniquement.</span><span class="sxs-lookup"><span data-stu-id="4a126-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="4a126-165">Nous verrons OIDC dans un autre exemple.</span><span class="sxs-lookup"><span data-stu-id="4a126-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="4a126-166">Configurez votre ID client que vous avez reçu à partir du portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="4a126-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="4a126-167">Configurez votre URI de redirection par hello un ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4a126-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="4a126-168">Configurez vos étendues que vous avez besoin dans l’ordre tooaccess hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="4a126-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="4a126-169">Hello `User.Read` valeur `oidc_scopes` permet de vous tooread hello profil de base hello utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="4a126-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="4a126-170">Plus d’informations sur toutes les étendues disponibles hello à [étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="4a126-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="4a126-171">Si vous souhaitez des explications sur `openid` ou `offline_access` en tant qu’étendues dans OpenID Connect, consultez [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="4a126-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="4a126-172">Configurer vos points de terminaison client en modifiant le fichier de oidc_endpoints.xml hello</span><span class="sxs-lookup"><span data-stu-id="4a126-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="4a126-173">Ouvrez hello `oidc_endpoints.xml` et apportez hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a126-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="4a126-174">Ces points de terminaison ne doivent jamais changer si vous utilisez OAuth2 comme protocole.</span><span class="sxs-lookup"><span data-stu-id="4a126-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="4a126-175">Hello des points de terminaison pour `userInfoEndpoint` et `revocationEndpoint` ne sont actuellement pas pris en charge par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a126-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="4a126-176">Si vous laissez ces hello valeur par défaut exemple.com, rappel qu’ils ne sont pas disponibles dans l’exemple hello  :-)</span><span class="sxs-lookup"><span data-stu-id="4a126-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="4a126-177">Configurer un appel d’API Graph</span><span class="sxs-lookup"><span data-stu-id="4a126-177">Configure a Graph API call</span></span>
* <span data-ttu-id="4a126-178">Ouvrez hello `HomeActivity.java` et apportez hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a126-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="4a126-179">Ici, un simple appel à l’API Graph renvoie nos informations.</span><span class="sxs-lookup"><span data-stu-id="4a126-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="4a126-180">Ce sont toutes les modifications de hello que vous avez besoin de toodo.</span><span class="sxs-lookup"><span data-stu-id="4a126-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="4a126-181">Exécutez hello `oidlib-sample` application, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="4a126-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="4a126-182">Une fois que vous avez été authentifié avec succès, sélectionnez hello **demander la ressource protégée** bouton tootest votre toohello appel API Graph.</span><span class="sxs-lookup"><span data-stu-id="4a126-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="4a126-183">Obtenir des mises à jour de sécurité pour notre produit</span><span class="sxs-lookup"><span data-stu-id="4a126-183">Get security updates for our product</span></span>
<span data-ttu-id="4a126-184">Nous vous encourageons tooget des notifications sur les incidents de sécurité en visitant hello [TechCenter sur la sécurité](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="4a126-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

