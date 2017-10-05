---
title: "Ajoutez la connexion à une application iOS à l’aide du point de terminaison Azure AD v2.0 | Microsoft Docs"
description: "Génération d’une application iOS qui connecte les utilisateurs à l’aide de leur compte Microsoft personnel et de leurs comptes professionnel ou scolaire à l’aide de bibliothèques tierces."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="48339-103">Ajouter la connexion à une application iOS à l’aide d’une bibliothèque tierce avec l’API Graph utilisant le point de terminaison v2.0</span><span class="sxs-lookup"><span data-stu-id="48339-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="48339-104">La plateforme d’identité Microsoft utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="48339-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="48339-105">Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent intégrer à nos services.</span><span class="sxs-lookup"><span data-stu-id="48339-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="48339-106">Pour aider les développeurs à utiliser notre plateforme avec d’autres bibliothèques, nous avons rédigé quelques procédures pas à pas comme celle-ci pour présenter la configuration des bibliothèques tierces pour se connecter à la plateforme d’identité de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48339-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="48339-107">La plupart des bibliothèques qui implémentent [la spécification RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peuvent se connecter à la plateforme Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="48339-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="48339-108">Avec l’application créée par cette procédure pas à pas, les utilisateurs peuvent se connecter à leur organisation, puis rechercher pour d’autres dans leur entreprise à l’aide de l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="48339-109">Si vous découvrez OAuth2 ou OpenID Connect, cet exemple de configuration n’est peut-être pas très parlant pour vous.</span><span class="sxs-lookup"><span data-stu-id="48339-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="48339-110">Nous vous recommandons de lire [Protocoles v2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour l’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="48339-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="48339-111">Certaines fonctionnalités de notre plateforme qui ont une expression dans les normes OAuth2 ou OpenID Connect, comme la gestion de la stratégie d’accès conditionnel et d’Intune, requièrent l’utilisation de nos bibliothèques d’identité Microsoft Azure open source.</span><span class="sxs-lookup"><span data-stu-id="48339-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="48339-112">Le point de terminaison v2.0 ne prend pas en charge l’intégralité des scénarios et fonctionnalités d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48339-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="48339-113">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="48339-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="48339-114">Télécharger le code à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="48339-114">Download code from GitHub</span></span>
<span data-ttu-id="48339-115">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="48339-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="48339-116">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="48339-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="48339-117">Vous pouvez aussi simplement télécharger l’exemple et commencer immédiatement :</span><span class="sxs-lookup"><span data-stu-id="48339-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="48339-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="48339-118">Register an app</span></span>
<span data-ttu-id="48339-119">Créez une nouvelle application dans le [Portail d’inscription des applications](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez les étapes détaillées dans [Inscription d’une application avec le point de terminaison v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="48339-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="48339-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="48339-120">Make sure to:</span></span>

* <span data-ttu-id="48339-121">Copiez **l’ID d’application** affecté à votre application, vous en aurez besoin rapidement.</span><span class="sxs-lookup"><span data-stu-id="48339-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="48339-122">ajouter la plateforme **Mobile** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="48339-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="48339-123">Copiez **l’URI de redirection** provenant du portail.</span><span class="sxs-lookup"><span data-stu-id="48339-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="48339-124">Vous devez utiliser la valeur par défaut de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="48339-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="48339-125">Télécharger la bibliothèque tierce NXOAuth2 et créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="48339-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="48339-126">Pour cette procédure pas à pas, vous utiliserez OAuth2Client à partir de GitHub, une bibliothèque OAuth2 pour Mac OS X et iOS (Cocoa et Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="48339-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="48339-127">Cette bibliothèque est basée sur le brouillon 10 de la spécification OAuth2.</span><span class="sxs-lookup"><span data-stu-id="48339-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="48339-128">Elle implémente le profil de l’application native et prend en charge le point de terminaison de l’autorisation de l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="48339-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="48339-129">Voici tout ce dont vous aurez besoin pour l’intégration avec la plateforme d’identité Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48339-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="48339-130">Ajout de la bibliothèque à votre projet à l’aide de CocoaPods</span><span class="sxs-lookup"><span data-stu-id="48339-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="48339-131">CocoaPods est un gestionnaire de dépendances pour les projets Xcode.</span><span class="sxs-lookup"><span data-stu-id="48339-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="48339-132">Il gère automatiquement les étapes d’installation précédentes.</span><span class="sxs-lookup"><span data-stu-id="48339-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="48339-133">Ajoutez le code suivant à ce podfile :</span><span class="sxs-lookup"><span data-stu-id="48339-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="48339-134">Chargez le podfile à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="48339-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="48339-135">Cette opération crée un nouvel espace de travail Xcode que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="48339-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="48339-136">Explorer la structure du projet</span><span class="sxs-lookup"><span data-stu-id="48339-136">Explore the structure of the project</span></span>
<span data-ttu-id="48339-137">La structure suivante est définie pour notre projet dans le squelette :</span><span class="sxs-lookup"><span data-stu-id="48339-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="48339-138">Une vue principale avec une recherche de noms UPN</span><span class="sxs-lookup"><span data-stu-id="48339-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="48339-139">Une vue détaillée pour les données concernant l’utilisateur sélectionné</span><span class="sxs-lookup"><span data-stu-id="48339-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="48339-140">Une vue de connexion permettant à un utilisateur de se connecter à l’application pour interroger le graphique</span><span class="sxs-lookup"><span data-stu-id="48339-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="48339-141">Nous accéderons à différents fichiers dans le squelette pour ajouter l’authentification.</span><span class="sxs-lookup"><span data-stu-id="48339-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="48339-142">D’autres parties du code, comme le code de l’élément visuel, ne sont pas associées à l’identité mais sont fournies pour vous.</span><span class="sxs-lookup"><span data-stu-id="48339-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="48339-143">Configurer le fichier settings.plst dans la bibliothèque</span><span class="sxs-lookup"><span data-stu-id="48339-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="48339-144">Dans le projet de démarrage rapide, ouvrez le fichier `settings.plist` .</span><span class="sxs-lookup"><span data-stu-id="48339-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="48339-145">Remplacez les valeurs des éléments de la section afin qu’elles reflètent les valeurs que vous avez utilisées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48339-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="48339-146">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque d’authentification Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48339-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="48339-147">`clientId` est l’ID client de votre application, copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="48339-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="48339-148">`redirectUri` est l’URL de redirection fournie par le portail.</span><span class="sxs-lookup"><span data-stu-id="48339-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="48339-149">Configurer la bibliothèque NXOAuth2Client dans votre LoginViewController</span><span class="sxs-lookup"><span data-stu-id="48339-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="48339-150">La bibliothèque NXOAuth2Client requiert des valeurs pour sa configuration.</span><span class="sxs-lookup"><span data-stu-id="48339-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="48339-151">Après avoir effectué cette tâche, vous pouvez utiliser le jeton acquis pour appeler l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="48339-152">Étant donné que `LoginView` est appelé chaque fois que nous avons besoin de nous authentifier, il est judicieux de placer les valeurs de configuration dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="48339-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="48339-153">Ajoutons quelques valeurs au fichier `LoginViewController.m` pour définir le contexte pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="48339-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="48339-154">Des détails sur les valeurs sont inclus après le code.</span><span class="sxs-lookup"><span data-stu-id="48339-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="48339-155">Observons les détails du code.</span><span class="sxs-lookup"><span data-stu-id="48339-155">Let's look at details about the code.</span></span>

<span data-ttu-id="48339-156">La première chaîne est pour `scopes`.</span><span class="sxs-lookup"><span data-stu-id="48339-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="48339-157">La valeur `User.Read` vous permet de lire le profil de base de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="48339-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="48339-158">Plus d’informations sur toutes les étendues disponibles, consultez [Étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="48339-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="48339-159">Pour `authURL`, `loginURL`, `bhh` et `tokenURL`, utilisez les valeurs indiquées précédemment.</span><span class="sxs-lookup"><span data-stu-id="48339-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="48339-160">Si vous utilisez les bibliothèques d’identité Microsoft Azure open source, nous extrairons ces données pour vous à l’aide de notre point de terminaison des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="48339-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="48339-161">Nous avons effectué le travail d’extraction de ces valeurs pour vous.</span><span class="sxs-lookup"><span data-stu-id="48339-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="48339-162">La valeur `keychain` est le conteneur qu’utilisera la bibliothèque NXOAuth2Client pour créer un porte-clés pour stocker vos jetons.</span><span class="sxs-lookup"><span data-stu-id="48339-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="48339-163">Si vous souhaitez obtenir l’authentification unique (SSO) entre de nombreuses applications, vous pouvez spécifier le même porte-clés dans chacune de vos applications, ainsi que demander l’utilisation de ce porte-clés dans vos droits Xcode.</span><span class="sxs-lookup"><span data-stu-id="48339-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="48339-164">Cela est expliqué dans la documentation Apple.</span><span class="sxs-lookup"><span data-stu-id="48339-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="48339-165">Le reste de ces valeurs est requis pour utiliser la bibliothèque et créer des emplacements pour que vous puissiez traiter des valeurs dans le contexte.</span><span class="sxs-lookup"><span data-stu-id="48339-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="48339-166">Créer un cache d’URL</span><span class="sxs-lookup"><span data-stu-id="48339-166">Create a URL cache</span></span>
<span data-ttu-id="48339-167">À l’intérieur de `(void)viewDidLoad()`, qui est toujours appelé une fois que la vue est chargée, le code suivant prépare un cache pour notre utilisation.</span><span class="sxs-lookup"><span data-stu-id="48339-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="48339-168">Ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="48339-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="48339-169">Créer une WebView pour la connexion</span><span class="sxs-lookup"><span data-stu-id="48339-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="48339-170">Une WebView peut inviter l’utilisateur à utiliser des facteurs supplémentaires comme les SMS (s’ils sont configurés) ou de renvoyer les messages d’erreur à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48339-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="48339-171">Ici, vous allez définir l’affichage web, puis écrire ultérieurement le code pour gérer les rappels qui surviendront dans l’affichage web à partir du service d’identité.</span><span class="sxs-lookup"><span data-stu-id="48339-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="48339-172">Substituer les méthodes d’affichage web pour gérer l’authentification</span><span class="sxs-lookup"><span data-stu-id="48339-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="48339-173">Pour indiquer la WebView qui s’affiche lorsqu’un utilisateur doit se connecter comme indiqué précédemment, vous pouvez coller le code suivant.</span><span class="sxs-lookup"><span data-stu-id="48339-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="48339-174">Écrire du code pour gérer le résultat de la demande OAuth2</span><span class="sxs-lookup"><span data-stu-id="48339-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="48339-175">Le code suivant gère la valeur redirectURL qui est renvoyée par la WebView.</span><span class="sxs-lookup"><span data-stu-id="48339-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="48339-176">Si l’authentification a échoué, le code va à nouveau être exécuté.</span><span class="sxs-lookup"><span data-stu-id="48339-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="48339-177">En attendant, la bibliothèque indique l’erreur que vous pouvez voir dans la console ou gérer de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="48339-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="48339-178">Définir le contexte OAuth (appelé magasin de comptes)</span><span class="sxs-lookup"><span data-stu-id="48339-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="48339-179">Ici, vous pouvez appeler `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` sur le magasin de comptes partagé pour chaque service auquel vous souhaitez rendre accessible pour votre application.</span><span class="sxs-lookup"><span data-stu-id="48339-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="48339-180">Le type de compte est une chaîne qui est utilisée comme identificateur pour un certain service.</span><span class="sxs-lookup"><span data-stu-id="48339-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="48339-181">Étant donné que vous accédez à l’API Graph, le code y fait référence en tant que `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="48339-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="48339-182">Ensuite, vous allez configurer un observateur qui vous indique les modifications avec le jeton.</span><span class="sxs-lookup"><span data-stu-id="48339-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="48339-183">Une fois que vous obtenez le jeton, vous renvoyez l’utilisateur vers `masterView`.</span><span class="sxs-lookup"><span data-stu-id="48339-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="48339-184">Configurer la vue principale pour rechercher et afficher les utilisateurs de l’API Graph</span><span class="sxs-lookup"><span data-stu-id="48339-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="48339-185">Une application à contrôleur de vue principale (MVC) qui affiche les données retournées dans la grille dépasse le cadre de cette procédure pas à pas ; il existe de nombreux didacticiels en ligne pour expliquer comment en créer une.</span><span class="sxs-lookup"><span data-stu-id="48339-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="48339-186">Tout ce code se trouve dans le fichier squelette.</span><span class="sxs-lookup"><span data-stu-id="48339-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="48339-187">Toutefois, vous devez traiter quelques éléments dans cette application MVC :</span><span class="sxs-lookup"><span data-stu-id="48339-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="48339-188">Intercepter lorsqu’un utilisateur saisit des données dans le champ de recherche</span><span class="sxs-lookup"><span data-stu-id="48339-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="48339-189">Fournir un objet de données vers la vue principale afin d’afficher les résultats dans la grille</span><span class="sxs-lookup"><span data-stu-id="48339-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="48339-190">Nous effectuerons ces actions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="48339-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="48339-191">Ajouter une vérification pour voir si vous êtes connecté</span><span class="sxs-lookup"><span data-stu-id="48339-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="48339-192">L’application ne fait pas grand-chose si l’utilisateur n’est pas connecté ; par conséquent, il est judicieux de vérifier s’il existe déjà un jeton dans le cache.</span><span class="sxs-lookup"><span data-stu-id="48339-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="48339-193">Si ce n’est pas le cas, vous redirigez vers la vue de connexion pour que l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="48339-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="48339-194">Rappelez-vous : la meilleure façon d’effectuer des actions lorsqu’une vue se charge consiste à utiliser la méthode `viewDidLoad()` fournie par Apple.</span><span class="sxs-lookup"><span data-stu-id="48339-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="48339-195">Mettre à jour la vue de table lors de la réception de données</span><span class="sxs-lookup"><span data-stu-id="48339-195">Update the Table View when data is received</span></span>
<span data-ttu-id="48339-196">Lorsque l’API Graph renvoie les données, vous devez afficher ces dernières.</span><span class="sxs-lookup"><span data-stu-id="48339-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="48339-197">Pour plus de simplicité, voici l’ensemble du code permettant de mettre à jour la table.</span><span class="sxs-lookup"><span data-stu-id="48339-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="48339-198">Vous pouvez simplement coller les valeurs appropriées dans votre code réutilisable MVC.</span><span class="sxs-lookup"><span data-stu-id="48339-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="48339-199">Fournir un moyen d’appeler l’API Graph lorsqu’un utilisateur tape dans le champ de recherche</span><span class="sxs-lookup"><span data-stu-id="48339-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="48339-200">Lorsqu’un utilisateur tape une recherche dans la zone, vous devez l’indiquer à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="48339-201">La classe `GraphAPICaller` , que vous allez créer dans le code suivant, sépare la fonctionnalité de recherche de la présentation.</span><span class="sxs-lookup"><span data-stu-id="48339-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="48339-202">Pour l’instant, nous allons écrire le code qui envoie tous les caractères de recherche à l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="48339-203">Pour ce faire, nous allons fournir une méthode appelée `lookupInGraph`, qui accepte la chaîne que nous souhaitons rechercher.</span><span class="sxs-lookup"><span data-stu-id="48339-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="48339-204">Écrire une classe d’assistance pour accéder à l’API Graph</span><span class="sxs-lookup"><span data-stu-id="48339-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="48339-205">Il s’agit de l’essentiel de l’application.</span><span class="sxs-lookup"><span data-stu-id="48339-205">This is the core of our application.</span></span> <span data-ttu-id="48339-206">Le reste consistait à insérer du code dans le modèle MVC par défaut d’Apple, mais ici vous écrivez du code pour interroger le graphique pendant la saisie de l’utilisateur, puis renvoyez ces données.</span><span class="sxs-lookup"><span data-stu-id="48339-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="48339-207">Voici le code, avec une explication détaillée ensuite.</span><span class="sxs-lookup"><span data-stu-id="48339-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="48339-208">Créer un nouveau fichier d’en-tête Objective C</span><span class="sxs-lookup"><span data-stu-id="48339-208">Create a new Objective C header file</span></span>
<span data-ttu-id="48339-209">Nommez le fichier `GraphAPICaller.h`, puis ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="48339-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="48339-210">Vous voyez ici qu’une méthode prend une chaîne et retourne un completionBlock.</span><span class="sxs-lookup"><span data-stu-id="48339-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="48339-211">Ce completionBlock, comme vous l’avez peut-être deviné, va mettre à jour la table en fournissant un objet avec des données renseignées en temps réel pendant la recherche de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48339-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="48339-212">Créer un nouveau fichier Objective C</span><span class="sxs-lookup"><span data-stu-id="48339-212">Create a new Objective C file</span></span>
<span data-ttu-id="48339-213">Nommez le fichier `GraphAPICaller.m`, puis ajoutez la méthode suivante.</span><span class="sxs-lookup"><span data-stu-id="48339-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="48339-214">Examinons cette méthode en détail.</span><span class="sxs-lookup"><span data-stu-id="48339-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="48339-215">L’essentiel de ce code se trouve dans la méthode `NXOAuth2Request`qui prend les paramètres que vous avez définis à l’intérieur du fichier settings.plist.</span><span class="sxs-lookup"><span data-stu-id="48339-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="48339-216">La première étape consiste à construire l’appel approprié de l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="48339-217">Étant donné que nous appelons `/users`, vous l’indiquez en l’ajoutant (ainsi que sa version) à la ressource API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="48339-218">Il est judicieux de placer ces éléments dans un fichier de paramètres externe, car ceux-ci peuvent changer à mesure que l’API évolue.</span><span class="sxs-lookup"><span data-stu-id="48339-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="48339-219">Ensuite, vous devez spécifier les paramètres que vous allez également fournir à l’appel de l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="48339-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="48339-220">Il est *très important* que vous ne placiez pas les paramètres dans le point de terminaison de ressource, car il est modifié pour tous les caractères non URI lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="48339-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="48339-221">Tout code de requête doit être fourni dans les paramètres.</span><span class="sxs-lookup"><span data-stu-id="48339-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="48339-222">Vous remarquerez peut-être que cela appelle une méthode `convertParamsToDictionary` que vous n’avez pas encore écrite.</span><span class="sxs-lookup"><span data-stu-id="48339-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="48339-223">Faisons-le maintenant à la fin du fichier :</span><span class="sxs-lookup"><span data-stu-id="48339-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="48339-224">Ensuite, nous utiliserons la méthode `NXOAuth2Request` pour obtenir des données de l’API au format JSON.</span><span class="sxs-lookup"><span data-stu-id="48339-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="48339-225">Enfin, nous verrons comment vous retournez les données vers MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="48339-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="48339-226">Les données nous reviennent sérialisées et doivent être désérialisées et chargées dans un objet que MainViewController peut consommer.</span><span class="sxs-lookup"><span data-stu-id="48339-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="48339-227">A cet effet, le squelette dispose d’un fichier `User.m/h` qui crée un objet Utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48339-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="48339-228">Vos remplissez cet objet utilisateur avec les informations du graphique.</span><span class="sxs-lookup"><span data-stu-id="48339-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="48339-229">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="48339-229">Run the sample</span></span>
<span data-ttu-id="48339-230">Si vous avez utilisé le squelette ou suivi la procédure pas à pas, votre application doit maintenant s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="48339-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="48339-231">Lancez le simulateur et cliquez sur **Connexion** pour utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="48339-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="48339-232">Obtenir des mises à jour de sécurité pour notre produit</span><span class="sxs-lookup"><span data-stu-id="48339-232">Get security updates for our product</span></span>
<span data-ttu-id="48339-233">Nous vous encourageons à activer les notifications lorsque des incidents de sécurité surviennent en vous rendant sur [Security TechCenter](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="48339-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

